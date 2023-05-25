# macOS使用VSCode插件CodeRunner运行MATLAB脚本

Referring to the official documentation of "Start MATLAB program from macOS Terminal" <https://ww2.mathworks.cn/help/matlab/ref/matlabmacos.html?lang=en>

```shell
mkdir newFolder && cd newFolder
code . # open in VS Code
mkdir .vscode && cd .vscode
touch settings.json && vim settings.json # write in the following text, save and quit.
```

```json
{
    "code-runner.executorMap": {
        // run matlab .m script with Code Runner in VS Code
        // Change pathToMATLAB before using it.
        // Put all functions to call in the same folder as the script itself.
        "matlab": "/Applications/MATLAB_R2020b.app/bin/matlab -sd $dir -batch $fileNameWithoutExt",
        // Supported customized parameters:
        //   $workspaceRoot: The path of the folder opened in VS Code
        //   $dir: The directory of the code file being run
        //   $fullFileName: The full name of the code file being run
        //   $fileName: The base name of the code file being run, that is the file without the directory
        //   $fileNameWithoutExt: The base name of the code file being run without its extension
    },
    // Whether to clear previous output before each run (default is false):
    "code-runner.clearPreviousOutput": true,
    // Whether to save all files before running (default is false):
    "code-runner.saveAllFilesBeforeRun": true,
    // Whether to save the current file before running (default is false):
    "code-runner.saveFileBeforeRun": true,
    // Whether to show extra execution message like [Running] ... and [Done] ... (default is true):
    "code-runner.showExecutionMessage": true, // cannot see that message is you set "code-runner.runInTerminal" to true
    // Whether to run code in Integrated Terminal (only support to run whole file in Integrated Terminal, neither untitled file nor code snippet) (default is false):
    "code-runner.runInTerminal": true, // cannot input data when setting to false
    // Whether to preserve focus on code editor after code run is triggered (default is true, the code editor will keep focus; when it is false, Terminal or Output Channel will take focus):
    "code-runner.preserveFocus": true,
    // Whether to ignore selection to always run entire file. (Default is false)
    "code-runner.ignoreSelection": true,
}
```

Then use the extension `Code Runner` to run MATLAB script in `VS Code`.
