# C++ Development Setup with VSCode

## Requirements

1. **Create a `.vscode/` folder** inside your project directory.
2. **Use the `g++` compiler** (and change before push to c++).
3. **Install the C/C++ extension**:

   * **Extension ID**: `ms-vscode.cpptools`
   * [Install from the VS Marketplace](https://marketplace.visualstudio.com/items?itemName=ms-vscode.cpptools)

---

## Debug Configuration

Create a `launch.json` file inside the `.vscode/` folder with the following configuration:

### `.vscode/launch.json`

```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Déboguer C++",                // Name shown in the Run panel
            "type": "cppdbg",                      // Use C++ debugger
            "request": "launch",                   // Launch mode (as opposed to attach)
            "program": "${workspaceFolder}/btc",   // Path to compiled binary
            "args": [
                "${workspaceFolder}/input.txt"     // Arguments passed to your program
            ],
            "stopAtEntry": false,                  // Do not pause at main()
            "cwd": "${workspaceFolder}",           // Set working directory to the project root
            "environment": [],                     // No special environment variables
            "externalConsole": false,              // Run in integrated terminal
            "MIMode": "gdb",                       // Use GDB for debugging (for g++)
            "setupCommands": [
                {
                    "description": "Activer l'impression des types",
                    "text": "-enable-pretty-printing", // Improves readability of complex types
                    "ignoreFailures": true
                }
            ],
            "preLaunchTask": "build"               // Task to run before debugging (compile)
        }
    ]
}
```

* **Note**: Modify the `"program"` field to match the compiled binary output (e.g., `btc`).
* **Note**: The `"args"` field specifies arguments passed to your program; you can remove `"${workspaceFolder}/input.txt"` if not needed.

---

## Build Task Configuration

Create a `tasks.json` file inside the `.vscode/` folder with the following configuration:

### `.vscode/tasks.json`

```json
{
    "version": "2.0.0",
    "tasks": [
        {
            "label": "build",                      // Task name used in launch.json
            "type": "shell",                       // Use shell to execute the command
            "command": "make",                     // Run `make` command
            "args": [
                "re"                               // Argument to rebuild everything (make re)
            ],
            "group": {
                "kind": "build",                   // Marks it as a build task
                "isDefault": true                  // Sets this task as the default build action
            },
            "problemMatcher": [],                  // Can be extended to parse compiler errors
            "detail": "Compile le projet avec 'make re'" // Description shown in the UI
        }
    ]
}
```

* **Note**: Ensure your `Makefile` has a `re` target to rebuild everything.

---

## C/C++ Extension Details

* **Name**: C/C++
* **ID**: `ms-vscode.cpptools`
* **Description**: Adds IntelliSense, debugging, and code navigation for C/C++ in Visual Studio Code.
* **Link**: [Install on VSCode Marketplace](https://marketplace.visualstudio.com/items?itemName=ms-vscode.cpptools)

