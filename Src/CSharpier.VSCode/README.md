# CSharpier Formatter for Visual Studio Code

This extension makes use of the dotnet tool [CSharpier](https://github.com/belav/csharpier) to format your code. This extension is versioned independently from CSharpier itself.

CSharpier is an opinionated code formatter for c# and xml. \
It provides very few options and a deterministic way to enforce formatting of your code. \
The printing process was ported from [prettier](https://prettier.io) but has evolved over time.

## Installation

Install through VS Code extensions. Search for `CSharpier`

Can also be installed in VS Code: Launch VS Code Quick Open (Ctrl+P), paste the following command, and press enter.

```
ext install csharpier.csharpier-vscode
```

## CSharpier Version
The extension determines which version of csharpier is needed to format a given file by looking for a dotnet manifest file. If one is not found it looks for a globally installed version of CSharpier.

## XML Formatting
Formatting XML is only available using CSharpier >= 1.0.0

## Dotnet Commands
The extension makes use of `dotnet` commands and uses the following logic to locate `dotnet`.
- If `dotnet.dotnetPath` is set try using that to find `dotnet`
- If `omnisharp.dotNetCliPaths` is set try using that to find `dotnet`
- Try running `dotnet --info` to see if `dotnet` is on the PATH
- For non-windows - Try running `sh -c "dotnet --info"` to see if `dotnet` is on the PATH

## Default Formatter
To ensure that CSharpier is used to format files, be sure to set it as the default formatter.

You can modify your [settings.json](https://code.visualstudio.com/docs/configure/settings#_settings-json-file) file.

```json
  "[csharp]": {
    "editor.defaultFormatter": "csharpier.csharpier-vscode"
  },
  "[xml]": {
    "editor.defaultFormatter": "csharpier.csharpier-vscode"
  },
```

## Troubleshooting

See [this page](https://csharpier.com/docs/EditorsTroubleshooting)

## Usage

### Keyboard Shortcuts

Visual Studio Code provides [default keyboard shortcuts](https://code.visualstudio.com/docs/getstarted/keybindings#_keyboard-shortcuts-reference) for code formatting. You can learn about these for each platform in the [VS Code documentation](https://code.visualstudio.com/docs/getstarted/keybindings#_keyboard-shortcuts-reference).

If you don't like the defaults, you can rebind `editor.action.formatDocument` and `editor.action.formatSelection` in the keyboard shortcuts menu of vscode.

### Format On Save

Respects `editor.formatOnSave` setting.

Found in the settings at Text Editor | Formatting | Format on Save

You can turn on format-on-save on a per-language basis by scoping the setting:

```json
// Set the default
"editor.formatOnSave": false,
// Enable per-language
"[csharp]": {
    "editor.formatOnSave": true
},
"[xml]": {
    "editor.formatOnSave": true
}
```

### Devcontainers

CSharpier supports DevContainers if it is installed as a local dotnet tool.
```bash
# if no .config/dotnet-tools.json file exists
dotnet new tool-manifest

# add csharpier to manifest
dotnet tool install csharpier

# rebuild container image
```
