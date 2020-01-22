# Debugger for Chrome setup

## Launch ASP.NET Core + SPA

`launch.json` should look like this:

```json
"compounds": [
		{
			"name": ".Net+Browser",
			"configurations": [".NET Core Launch (console)", "Launch Chrome"]
		}
	],
  //...
  "configurations": [
		{
			"type": "chrome",
			"request": "launch",
			"name": "Launch Chrome",
			"url": "http://localhost:5000",
			"webRoot": "${workspaceRoot}/ClientApp",
			"userDataDir": "${workspaceRoot}/.vscode/chrome"
		},
    {
			"name": ".NET Core Launch (console)",
			"type": "coreclr",
			"request": "launch",
			"preLaunchTask": "build",
			"program": "${workspaceFolder}/bin/Debug/netcoreapp3.1/path.to.project.dll",
			"args": [],
			"cwd": "${workspaceRoot}",
			"stopAtEntry": false,
			"console": "internalConsole"
	  }

```

## Extensions

Add this line to the configuration that you use to be able to download and use extensions that saves between sessions.

```json
"userDataDir": "${workspaceRoot}/.vscode/chrome"
```
