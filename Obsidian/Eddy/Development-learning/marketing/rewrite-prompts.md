# Rewrite prompt sample

- Before
    
    I want to create a plan to check every screen in the system. The system is based on SAP ECC. Create a new file in @check folder in @d:\projects\harmony-erp/docs-journal/  named `screen-core-function.md` in markdown format.
    
    First:
    
    - Scan for every modules in the system
    - List out every screens in each module with thymeleaf .html file
    - create first section named `screen list` in `screen-core-function.md` file
    - add the list of module and screen into `screen-core-function.md` with format:
    
    ```markdown
    ## Module
    - screen thymeleaf name
    
    ```
    
    Second:
    
    - for each module, add a task to task management, each task wil have a sub task group that each sub task is a screen
    - for each sub task, the core content of the subtask will be find out what's main function of the screen ( that is it do)
    
    Third:
    
    - Add new section in `screen-core-function.md` file named `# result`
    - After find out the main function of each screen, update the result into result section with format
    
    ```markdown
    ## Module
    ### screen
    - core function:
    `
    ```
    

- After
    
    I want to create a comprehensive plan to analyze every screen in the Harmony ERP system (which is based on SAP ECC integration). This will be a multi-phase task that involves discovery, task planning, and documentation.
    
    **File Creation:**
    Create a new markdown file at the following exact path: `d:\\projects\\harmony-erp/docs-journal/check/screen-core-function.md`
    
    **Phase 1 - Discovery and Initial Documentation:**
    
    1. Scan the entire codebase to identify all modules in the system
    2. For each module, identify all screens by finding their Thymeleaf `.html` template files (typically located in `src/main/resources/templates/` or similar directories)
    3. Create the first section in `screen-core-function.md` named `# Screen List`
    4. Document all discovered modules and their screens in the following markdown format:
    
    ```markdown
    # Screen List
    
    ## [Module Name 1]
    - [screen-id-001.html] - [Screen ID or Title if available]
    - [screen-id-002.html] - [Screen ID or Title if available]
    
    ## [Module Name 2]
    - [screen-id-003.html] - [Screen ID or Title if available]
    
    ```
    
    **Phase 2 - Task Management Setup:**
    
    1. Create a parent task for each module using the task management tools
    2. Under each module parent task, create subtasks where each subtask represents one screen
    3. Each subtask should be named clearly (e.g., "Analyze [Screen ID/Name] - [filename.html]")
    4. The description of each subtask should state: "Identify the core/main business function of this screen by analyzing its controller, service layer, and database interactions"
    
    **Phase 3 - Analysis and Results Documentation:**
    
    1. Add a new section in `screen-core-function.md` named `# Result`
    2. As you complete the analysis for each screen (following the task list), update the Result section with findings in this format:
    
    ```markdown
    # Result
    
    ## [Module Name 1]
    
    ### [Screen ID/Name] - [filename.html]
    - **Core Function:** [Brief description of the main business purpose - what the screen does, what business process it supports, key operations it performs]
    - **Related Backend:** [Controller and Service class names if relevant]
    - **Database Operations:** [Key tables or procedures involved, if applicable]
    
    ### [Screen ID/Name] - [filename.html]
    - **Core Function:** [Description]
    - **Related Backend:** [Details]
    - **Database Operations:** [Details]
    
    ## [Module Name 2]
    ...
    
    ```
    
    **Important Notes:**
    
    - Module names should follow the existing naming conventions in the codebase (e.g., FIFS, FIGL, FIAR, etc.)
    - Screen IDs typically follow patterns like `FIGL_XXX`, `FIAR_XXX`, etc.
    - When analyzing core functions, consider: what business process does this screen support? (e.g., "Journal Entry Creation", "AR Invoice Management", "GL Account Inquiry", etc.)
    - Use the task management system to track progress through all screens systematically
    - Refer to existing documentation in `docs-journal/` folders (ar/, gl/, etc.) for context on known screens
    
    **Execution Approach:**
    
    1. Start with Phase 1 to get a complete inventory
    2. Set up Phase 2 task structure for systematic tracking
    3. Work through Phase 3 screen-by-screen, updating tasks and documentation as you progress