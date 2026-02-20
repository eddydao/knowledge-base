# Install jenkins

# Install docker

Add jenkins user to docker group (for linux - not MacOS)
`sudo usermod -aG docker jenkins`

# Maven installed

# Create Jenkins pipeline

## Install plugins
- Docker pipeline
- pipeline maven integration

## Steps
1. Create `dockerfile` in project
2. Config maven in jenkins - optional but recommended
-  add Maven in **Manage Jenkins -> Tool configuration -> Maven**
- Config JDK home in Jenkins configuration
1. Create new Jenkins pipeline job


node {
    def mvnHome = tool 'maven'
    def appName = 'springboottest' // Change this to your application's name
    def dockerImageName = "${appName}" // Or your private registry path
    def dockerImageTag = "latest" // Or use build numbers: "${env.BUILD_NUMBER}"
    def springBootPort = 8080 // The port your Spring Boot app runs on
    def hostPort = 8082
    
    stage('Checkout') {
        git url: 'https://github.com/HaTruong311/demo-jenkins-java-freestyle.git', branch: 'main'
    }
    stage('build maven') {
        echo 'build maven'
        
        def javaHome = tool 'JDK17'
        env.JAVA_HOME = javaHome
        env.PATH = "${env.JAVA_HOME}/bin:${env.PATH}"

        sh "${mvnHome}/bin/mvn clean package -DskipTests"
    }
    stage('build docker'){
            //  sh 'docker build . -t hatruong/testspringboot'
            env.PATH = "/usr/local/bin:/opt/homebrew/bin:${env.PATH}"
             sh 'echo "--- DEBUG INFO ---"'
    sh 'echo "User: $(whoami)"'
    sh 'echo "Effective PATH in Jenkins: $PATH"'
    sh 'which docker' // This should now find docker
    sh 'docker --version' // This should also work
    sh 'echo "--- END DEBUG INFO ---"'
             
            echo "Building Docker image: ${dockerImageName}:${dockerImageTag}"
            
            // The Dockerfile should be in the root of your project
            docker.build("${dockerImageName}:${dockerImageTag}", "--build-arg JAR_FILE=target/*.jar .") // Pass JAR_FILE build-arg [12]
            echo 'Docker image built.'
    }
    stage('deploy'){
        // echo 'deploying..'
        // sh 'docker rm -f hatruongtrong || true'
        // sh 'docker run -d --name hatruongtrong -p 333:8080 hatruong/testspringboot'
        
        
        echo "Deploying Docker container..."

        // Stop and remove any existing container with the same name (optional, for idempotency)
        sh "docker stop ${appName} || true"
        sh "docker rm ${appName} || true"

        // Run the new Docker container
        // The -d flag runs the container in detached mode (in the background)
        // The -p flag maps the host port to the container port
        sh "docker run -d --name ${appName} -p ${hostPort}:${springBootPort} ${dockerImageName}:${dockerImageTag}"
        echo "Docker container ${appName} deployed and running on port ${hostPort}."
    }
}




