Okay, let's create a declarative Jenkins pipeline for your Spring Boot application using Maven and deploying it into a Docker container.

**Assumptions:**

1.  You have Jenkins installed and running.
2.  You have the necessary Jenkins plugins installed:
    *   `Pipeline` (usually installed by default)
    *   `Docker Pipeline`
    *   `Docker Commons`
    *   `Credentials Binding`
    *   `Git` (or your SCM plugin)
3.  Your Jenkins agent (where the pipeline runs) has:
    *   Docker installed and running.
    *   The Jenkins user has permission to interact with the Docker daemon.
    *   Maven installed, OR you have configured a Maven installation in Jenkins Global Tool Configuration.
4.  Your Spring Boot project is managed with Maven and has a `pom.xml`.
5.  Your project's source code is in a Git repository (or another SCM Jenkins supports).
6.  You have a Docker registry (like Docker Hub, AWS ECR, Google GCR, Artifactory) where you want to push the image (optional but recommended).
7.  You have credentials configured in Jenkins for your Docker registry (if pushing).

---

**Step 1: Create a `Dockerfile`**

Place this file named `Dockerfile` (no extension) in the root directory of your Spring Boot project. This file tells Docker how to build your image.

```dockerfile
# Use an official OpenJDK runtime as a parent image
FROM openjdk:17-jdk-slim as builder

# Set the working directory
WORKDIR /app

# Copy the Maven wrapper files (if you use it) - Optional
# COPY .mvn/ .mvn
# COPY mvnw pom.xml ./

# Copy the pom.xml file
COPY pom.xml .

# Download dependencies (this layer is cached if pom.xml doesn't change)
# Using skipTests to avoid running tests during dependency resolution
RUN mvn dependency:go-offline -B

# Copy the project source code
COPY src ./src

# Package the application (run tests here if desired, or use -DskipTests)
# Make sure the final JAR name matches what your pom.xml produces
RUN mvn package -DskipTests

# --- Second Stage: Create the final lightweight image ---
FROM openjdk:17-jre-slim

WORKDIR /app

# Define arguments for user/group IDs (optional, good practice for security)
ARG APP_USER_ID=1001
ARG APP_GROUP_ID=1001

# Create a non-root user and group
RUN groupadd --system --gid ${APP_GROUP_ID} appgroup && \
    useradd --system --uid ${APP_USER_ID} --gid ${APP_GROUP_ID} appuser

# Copy the executable JAR file from the builder stage
# Adjust the path if your pom.xml builds the JAR in a different location or with a different name
COPY --from=builder /app/target/*.jar app.jar

# Change ownership to the non-root user
RUN chown ${APP_USER_ID}:${APP_GROUP_ID} app.jar

# Switch to the non-root user
USER appuser

# Expose the port the application runs on (default for Spring Boot is 8080)
EXPOSE 8080

# Command to run the application
ENTRYPOINT ["java", "-jar", "app.jar"]

# Optional: Add healthcheck
# HEALTHCHECK --interval=30s --timeout=5s --start-period=15s --retries=3 \
#   CMD curl -f http://localhost:8080/actuator/health || exit 1
```

**Explanation of `Dockerfile`:**

*   **Multi-stage Build:** Uses a `builder` stage with a full JDK and Maven to build the app, then copies *only* the final JAR into a smaller JRE image. This makes the final image much smaller and more secure.
*   **Dependency Caching:** Downloads dependencies *before* copying source code, so Docker reuses the dependency layer if only the code changes.
*   **Non-Root User:** Creates and runs the application as a non-root user (`appuser`) for better security.
*   **`target/*.jar`:** Assumes your Maven build produces one JAR file in the `target` directory. Adjust the `COPY` command if the name or location is different.
*   **`EXPOSE 8080`:** Informs Docker that the container listens on port 8080.
*   **`ENTRYPOINT`:** Specifies the command to run when the container starts.
*   **Healthcheck (Optional):** If you have Spring Boot Actuator enabled, this provides a basic health check.

---

**Step 2: Create a `.dockerignore` file (Optional but Recommended)**

Place this file named `.dockerignore` in the root directory of your project. It prevents unnecessary files from being copied into the Docker build context, speeding up builds and reducing image size.

```
.git
.gitignore
.idea
target/
*.log
.mvn/
mvnw
mvnw.cmd
```

---

**Step 3: Create the `Jenkinsfile`**

Place this file named `Jenkinsfile` (no extension) in the root directory of your project and commit it to your repository.

```groovy
pipeline {
    agent any // Runs on any available agent with Docker & Maven

    // Environment variables used throughout the pipeline
    environment {
        // --- Configuration ---
        // Replace with your actual app name (used for image naming and container naming)
        APP_NAME = 'my-spring-boot-app'
        // Replace with your Docker Hub username or registry URL/namespace
        // e.g., 'docker.io/yourusername', 'your-registry.com/your-project'
        DOCKER_REGISTRY = 'yourdockerhubusername'
        // Jenkins Credentials ID for your Docker Registry (configured in Jenkins)
        DOCKER_CREDENTIALS_ID = 'dockerhub-credentials' // Or your specific ID
        // --- Dynamic ---
        // Calculated image name
        DOCKER_IMAGE_NAME = "${DOCKER_REGISTRY}/${APP_NAME}"
        // Tag will be the Jenkins build number
        IMAGE_TAG = "${env.BUILD_NUMBER}"
    }

    // Define tools needed (Maven in this case)
    // 'Maven3' should match the name configured in Jenkins Global Tool Configuration
    tools {
        maven 'Maven3'
    }

    stages {
        stage('1. Checkout Code') {
            steps {
                echo "Checking out code from SCM..."
                // This step checks out the code from the SCM configured in the Jenkins job
                checkout scm
            }
        }

        stage('2. Build Application') {
            steps {
                echo "Building Spring Boot application with Maven..."
                // Run Maven clean package. -DskipTests speeds up the build in CI.
                // Ensure your agent has Maven configured or use the 'tools' directive.
                sh "mvn clean package -DskipTests"
            }
            // Store the built JAR file for later stages
            // post {
            //     success {
            //         // Example: Stash the JAR if needed in a different agent context later
            //         // stash includes: 'target/*.jar', name: 'app-jar'
            //     }
            // }
        }

        stage('3. Build Docker Image') {
            steps {
                script {
                    echo "Building Docker image: ${env.DOCKER_IMAGE_NAME}:${env.IMAGE_TAG}"
                    // Build the Docker image using the Dockerfile in the current directory (.)
                    // The -t flag tags the image with name:tag
                    sh "docker build -t ${env.DOCKER_IMAGE_NAME}:${env.IMAGE_TAG} ."
                }
            }
        }

        stage('4. Push Docker Image (Optional)') {
            // Only run this stage if you want to push to a registry
            // when { expression { return env.DOCKER_REGISTRY != '' && env.DOCKER_CREDENTIALS_ID != '' } }
            steps {
                script {
                    echo "Logging into Docker Registry..."
                    // Use Jenkins Credentials Binding to securely access Docker credentials
                    withCredentials([usernamePassword(credentialsId: env.DOCKER_CREDENTIALS_ID, usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                        // Login to Docker registry - use --password-stdin for security
                        sh "echo $DOCKER_PASS | docker login ${env.DOCKER_REGISTRY.split('/')[0]} -u $DOCKER_USER --password-stdin"
                    }
                    echo "Pushing Docker image ${env.DOCKER_IMAGE_NAME}:${env.IMAGE_TAG}..."
                    sh "docker push ${env.DOCKER_IMAGE_NAME}:${env.IMAGE_TAG}"
                }
            }
            post {
                always {
                    // Always logout after trying to push
                    echo "Logging out from Docker Registry..."
                    sh "docker logout ${env.DOCKER_REGISTRY.split('/')[0]}"
                }
            }
        }

        stage('5. Deploy Container (Example)') {
            // --- WARNING: Basic Deployment Example ---
            // This is a VERY simple deployment running the container directly on the Jenkins agent.
            // Replace this with your actual deployment strategy (e.g., ssh, kubectl, ansible).
            steps {
                script {
                    def containerName = "${env.APP_NAME}-${env.IMAGE_TAG}"
                    echo "Deploying container ${containerName}..."

                    // Stop and remove any existing container with the *same exact name* if it exists
                    // Using || true to prevent failure if the container doesn't exist
                    sh "docker stop ${containerName} || true"
                    sh "docker rm ${containerName} || true"

                    // Run the new container
                    // -d: detached mode (run in background)
                    // -p 8080:8080: map host port 8080 to container port 8080
                    // --name: assign a name to the container
                    // --restart unless-stopped: Example restart policy
                    sh "docker run -d -p 8080:8080 --name ${containerName} --restart unless-stopped ${env.DOCKER_IMAGE_NAME}:${env.IMAGE_TAG}"

                    echo "Container ${containerName} deployed."
                    // Add a small sleep to allow the container to potentially start
                    sleep(time: 10, unit: 'SECONDS')
                    // Optional: Check if the container is running
                    sh "docker ps -f name=${containerName}"
                }
            }
        }
    }

    post {
        // Actions to perform after the entire pipeline finishes
        always {
            echo "Pipeline finished."
            // Clean up workspace? Remove old images? Depends on your strategy.
            // Example: Remove the locally built image if space is a concern
            // sh "docker rmi ${env.DOCKER_IMAGE_NAME}:${env.IMAGE_TAG} || true"
        }
        success {
            echo "Pipeline succeeded!"
            // Send notification?
        }
        failure {
            echo "Pipeline failed!"
            // Send notification?
        }
    }
}
```

**Explanation of `Jenkinsfile`:**

1.  **`pipeline { ... }`**: Defines the entire declarative pipeline.
2.  **`agent any`**: Specifies that the pipeline can run on any available Jenkins agent. Ensure this agent has Maven and Docker configured. You could use specific labels (`agent { label 'docker-maven-agent' }`) or even Docker agents (`agent { docker { ... } }`) for more complex setups.
3.  **`environment { ... }`**: Defines environment variables.
    *   `APP_NAME`: Your application's name. **Customize this.**
    *   `DOCKER_REGISTRY`: Your Docker registry URL/username. **Customize this.** For Docker Hub, use your username. For others (ECR, GCR), use the full registry URL. Leave blank or remove the Push stage if not pushing.
    *   `DOCKER_CREDENTIALS_ID`: The ID of the Username/Password credentials you stored in Jenkins for your registry. **Customize this.**
    *   `DOCKER_IMAGE_NAME`: Constructed image name (e.g., `yourusername/my-spring-boot-app`).
    *   `IMAGE_TAG`: Uses the Jenkins build number (`env.BUILD_NUMBER`) as the Docker image tag for versioning.
4.  **`tools { ... }`**: Declares tools needed from Jenkins Global Tool Configuration. Replace `'Maven3'` with the name you gave your Maven installation in Jenkins.
5.  **`stages { ... }`**: Contains the different phases of the pipeline.
    *   **`stage('1. Checkout Code')`**: Uses the `checkout scm` step to get the source code based on the Jenkins job configuration.
    *   **`stage('2. Build Application')`**: Runs `mvn clean package -DskipTests` using the `sh` (shell) step. `-DskipTests` is common in CI pipelines to speed things up, assuming tests are run elsewhere or not needed at this specific stage.
    *   **`stage('3. Build Docker Image')`**: Uses `docker build` command to create the image using the `Dockerfile` in the workspace root (`.`). It tags the image using the environment variables defined earlier.
    *   **`stage('4. Push Docker Image (Optional)')`**:
        *   Uses `withCredentials` to securely inject the Docker registry username and password into environment variables (`DOCKER_USER`, `DOCKER_PASS`).
        *   Logs in using `docker login`. Using `--password-stdin` is more secure than putting the password directly on the command line.
        *   Pushes the image using `docker push`.
        *   The `post { always { ... } }` block ensures `docker logout` is always called.
        *   *(Commented out `when` condition):* You can uncomment the `when` block if you want this stage to be skipped if registry/credentials aren't configured.
    *   **`stage('5. Deploy Container (Example)')`**:
        *   **IMPORTANT:** This is a *basic* example that runs the container directly on the Jenkins agent node using `docker run`. This is suitable only for simple tests or development environments.
        *   It stops and removes any container with the *exact same name* before starting the new one.
        *   It runs the container in detached mode (`-d`), maps the port (`-p`), gives it a name (`--name`), and uses a restart policy.
        *   **For production, replace this stage with your actual deployment mechanism** (e.g., using `ssh` to run commands on a remote server, `kubectl apply` for Kubernetes, Ansible playbooks, Terraform, etc.).
6.  **`post { ... }`**: Defines actions to run after the pipeline completes, regardless of status (`always`), or specifically on `success` or `failure`. Good for cleanup or notifications.

---

**Step 4: Configure Jenkins Job**

1.  Go to your Jenkins dashboard.
2.  Create a new item -> Select "Pipeline" -> Give it a name (e.g., `my-spring-boot-app-pipeline`).
3.  In the configuration page, scroll down to the "Pipeline" section.
4.  Select "Pipeline script from SCM" in the Definition dropdown.
5.  Select "Git" (or your SCM) from the SCM dropdown.
6.  Enter your Repository URL.
7.  Add Credentials if your repository is private.
8.  Specify the Branch to build (e.g., `*/main` or `*/master`).
9.  Make sure the "Script Path" is `Jenkinsfile` (this is the default).
10. **Crucially:** Configure your Docker registry credentials in Jenkins:
    *   Go to Manage Jenkins -> Credentials -> System -> Global credentials (or a specific domain).
    *   Add Credentials -> Kind: "Username with password".
    *   Enter your Docker registry username and password.
    *   Give it an ID (e.g., `dockerhub-credentials`). **This ID must match the `DOCKER_CREDENTIALS_ID` in your `Jenkinsfile`**.
11. **Crucially:** Configure Maven in Jenkins Global Tool Configuration:
    *   Go to Manage Jenkins -> Global Tool Configuration.
    *   Scroll down to "Maven" -> Add Maven.
    *   Give it a Name (e.g., `Maven3`). **This name must match the one used in the `tools` directive in your `Jenkinsfile`**.
    *   Choose an installation method (e.g., "Install from Apache" or provide `MAVEN_HOME`).
12. Save the Jenkins job configuration.

---

**Step 5: Run the Pipeline**

Click "Build Now" on your newly configured Jenkins job. Jenkins will check out the code (including the `Jenkinsfile`), parse it, and execute the defined stages.

You now have a declarative Jenkins pipeline that builds your Spring Boot app, packages it into a Docker container, optionally pushes it to a registry, and runs a basic deployment. Remember to adapt the deployment stage for your specific environment.



# Alternative script 

```groovy
pipeline {
    // Use an agent that has Docker and Maven available.
    // 'any' works if your default agents have these tools.
    // Otherwise, use a specific label: agent { label 'docker-maven-agent' }
    agent any

    // Environment variables used throughout the pipeline
    environment {
        // --- Configuration ---
        APP_NAME              = 'my-spring-boot-app' // CHANGE: Your app's name
        DOCKER_REGISTRY       = 'yourdockerhubusername' // CHANGE: Docker Hub username or registry URL (e.g., 'your-registry.com/your-project')
        DOCKER_CREDENTIALS_ID = 'dockerhub-credentials' // CHANGE: Jenkins Credentials ID for Docker Registry
        // --- Dynamic ---
        DOCKER_IMAGE_NAME     = "${DOCKER_REGISTRY}/${APP_NAME}"
        // Tag will be the Jenkins build number for simplicity
        IMAGE_TAG             = "${env.BUILD_NUMBER}"
        // Calculated full image name with tag
        FULL_IMAGE_NAME       = "${DOCKER_IMAGE_NAME}:${IMAGE_TAG}"
        // Container name based on app and tag
        CONTAINER_NAME        = "${APP_NAME}-${IMAGE_TAG}"
    }

    // Define tools needed (Maven in this case)
    // 'Maven3' should match the name configured in Jenkins Global Tool Configuration
    tools {
        maven 'Maven3'
    }

    stages {
        stage('1. Checkout Code') {
            steps {
                echo "Checking out code from SCM..."
                // Checks out code based on the Jenkins job SCM configuration
                checkout scm
            }
        }

        stage('2. Build Application') {
            steps {
                echo "Building Spring Boot application with Maven..."
                // Using 'sh' step is the standard declarative way to run shell commands
                sh "mvn clean package -DskipTests"
            }
        }

        stage('3. Build Docker Image') {
            steps {
                echo "Building Docker image: ${env.FULL_IMAGE_NAME}"
                // Use the docker.build command provided by the Docker Pipeline plugin.
                // The '.' indicates the build context is the current directory (where Dockerfile is).
                // While often shown in a script block to capture the return value,
                // we can call it directly here if we don't need the 'image' object later.
                // For push, we'll reference it by name.
                 script { // script block is often necessary here to use docker object methods
                    docker.build(env.FULL_IMAGE_NAME, '.')
                 }
            }
        }

        stage('4. Push Docker Image (Optional)') {
            // Define condition declaratively using 'when'
            when {
                // Only run if registry and credentials ID are set
                environment name: 'DOCKER_REGISTRY', value: '' , comparator: 'NOT_EQUALS'
                environment name: 'DOCKER_CREDENTIALS_ID', value: '' , comparator: 'NOT_EQUALS'
            }
            steps {
                echo "Pushing Docker image ${env.FULL_IMAGE_NAME}..."
                // Use the declarative docker.withRegistry block for login/logout handling.
                // Provide the registry URL and the Jenkins credentials ID.
                 script { // script block is often necessary here to use docker object methods
                    docker.withRegistry("https://${env.DOCKER_REGISTRY.split('/')[0]}", env.DOCKER_CREDENTIALS_ID) {
                        // Push the image tagged in the previous stage
                        docker.image(env.FULL_IMAGE_NAME).push()

                        // Optional: Also push a 'latest' tag
                        // docker.image(env.FULL_IMAGE_NAME).push('latest')
                    }
                 }
            }
        }

        stage('5. Deploy Container (Example)') {
            // --- WARNING: Basic Deployment Example ---
            // This uses 'sh' steps, which is the standard declarative way to execute shell commands.
            // Replace with your actual deployment plugin/steps (Kubernetes, ECS, SSH etc.) for real environments.
            steps {
                echo "Deploying container ${env.CONTAINER_NAME}..."

                // Stop and remove existing container with the same name (ignore errors if not found)
                sh "docker stop ${env.CONTAINER_NAME} || true"
                sh "docker rm ${env.CONTAINER_NAME} || true"

                // Run the new container using the image built/pushed earlier
                sh """
                    docker run -d \
                      -p 8080:8080 \
                      --name ${env.CONTAINER_NAME} \
                      --restart unless-stopped \
                      ${env.FULL_IMAGE_NAME}
                """

                echo "Container ${env.CONTAINER_NAME} deployment initiated."
                // Add a small sleep to allow the container to potentially start
                sleep(time: 10, unit: 'SECONDS')
                // Optional: Check if the container is running
                sh "docker ps -f name=${env.CONTAINER_NAME}"
            }
        }
    }

    post {
        // Actions to perform after the entire pipeline finishes
        always {
            echo "Pipeline finished."
            // Example cleanup: Remove the locally built image if desired
            // sh "docker rmi ${env.FULL_IMAGE_NAME} || true"
        }
        success {
            echo "Pipeline succeeded!"
            // Add success notifications if needed
        }
        failure {
            echo "Pipeline failed!"
            // Add failure notifications if needed
        }
    }
}
```
