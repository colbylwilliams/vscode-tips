# vscode-tips

Useful tips & tricks for Visual Studio Code. Mostly for me, but public so others might enjoy.

> [!Important]
> I'm on a mac, results may vary

## .NET Logging

> Full set of tips at [`/dotnet/logging.md`](/dotnet/logging.md)

In vs code, [debug provider][dotnet-logging-debug-provider] and the [console provider][dotnet-logging-console-provider] both log to the [debug console][vscode-debug-console]. This ends up duplicating all the logs, in different formats, which makes it difficult to read and understand. To make things worse they're not [in color](/dotnet/logging.md#add-some-color) :roll_eyes:.

I've spent way too much time figuring out how to go from this:

![debug_console_log](./img/debug_console_log.png)

To this:

![console_log_allow_ansi_single_line](./img/console_log_allow_ansi_single_line.png)

If you're interested in doing the same (or something in between), check out [`/dotnet/logging.md`](/dotnet/logging.md)

### Other settings

I've found that a couple more settings will reduce the noise in your logs when developing locally:

```jsonc
//settings.json
{
  "csharp.debug.logging.moduleLoad": false,
  "csharp.debug.logging.exceptions": false
}
```

## Settings

I'm not trying to tell you how to live your life. But here are some settings that I've found make life more delightful _(and more importantly, get the stuff that I don't care about, out of my way)_.

### :mag: Explorer settings

Here are some **Explorer** settings that I find useful for .NET:

```jsonc
// settings.json
{
  "explorer.fileNesting.enabled": true,
  "explorer.fileNesting.expand": false,
  "explorer.fileNesting.patterns": {
    // global
    "README.md": ".gitignore, .gitattributes, LICENSE, SECURITY.md, SUPPORT.md, CODE_OF_CONDUCT.md",
    "dockerfile": ".dockerignore",
    // ts, js
    ".env": ".env.development, .env.production",
    "*.tsx": "${capture}.ts, ${capture}.test.tsx, ${capture}.css",
    ".*rc.yml": ".${capture}ignore",
    ".*rc.js": ".${capture}ignore",
    // .net
    "*.cs": "I${capture}.cs,",
    "*.csproj": "appsettings.json, dockerfile, host.json, local.settings.json, .gitignore",
    "appsettings.json": "appsettings.development.json, appsettings.production.json"
  }
}
```

_The new C# DevKit has a pretty nice Explorer, but since I bounce around to different programming languages (and I've taken the time to set up vscode's Explorer just the way I like it), I tend to use vscode's Explorer._

### :file_cabinet: Files settings

```jsonc
// settings.json
{
  // see-ya squigglies
  "files.associations": {
    "appsettings.*.json": "jsonc",
    "local.settings.json": "jsonc",
    "launchSettings.json": "jsonc"
  },
  "files.exclude": {
    "**/.vs": true,
    "**/bin": true,
    "**/obj": true,
    "**/.git": true,
    "**/.DS_Store": true,
    "**/__pycache__": true,
    "**/**.dist-info": true,
    "**/node_modules": true
  }
}
```

### :pencil2: Editor settings

I've found that all of the tool trying to help me type my next line of code, end up competing and creating a poor experience. The editor settings below are just a subset of my editor settings, but these are the settings that I've found make my active coding experience most efficient (i.e. I can intuitively accept suggestions from intellicode or copilot):

```jsonc
{
  "editor.emptySelectionClipboard": false, // why the hell is this even a thing
  "editor.acceptSuggestionOnCommitCharacter": false,
  "editor.inlineSuggest.enabled": true,
  "editor.parameterHints.cycle": true,
  "editor.suggest.localityBonus": true,
  "editor.suggest.preview": true,
  "editor.suggest.matchOnWordStartOnly": false,
  "editor.suggest.showStatusBar": true,
  "editor.suggestSelection": "first",
  "editor.snippetSuggestions": "bottom",
  "editor.tabCompletion": "on",

  "github.copilot.editor.enableAutoCompletions": true,

  "editor.minimap.autohide": true,
  "editor.minimap.enabled": false, // I tend to toggle this
  "editor.minimap.showSlider": "always"
}
```

#### :straight_ruler: Rulers

I write a lot of code that ends up on GitHub; prototypes, samples, customer development, etc.<br/>
On github.com depending on settings this sentence should be just about full-with across the readme without wrapping.

```yaml
# and the first line just fits in a code block
I write a lot of code that ends up on GitHub; prototypes, samples, customer development, etc.
```

This is what these rulers are for. They represent (approx) widths of different renderings on github.com (gists, readme, classic code view, etc.). You'll may need to change the color.

```jsonc
// settings.json
{
  "editor.rulers": [
    { "column": 99, "color": "#2e2e2e" },
    { "column": 112, "color": "#2e2e2e" },
    { "column": 117, "color": "#2e2e2e" },
    { "column": 139, "color": "#2e2e2e" },
    { "column": 177, "color": "#2e2e2e" },
    { "column": 250, "color": "#2e2e2e" }
  ]
}
```

[dotnet-logging-console-provider]: https://learn.microsoft.com/aspnet/core/fundamentals/logging/#console
[dotnet-logging-debug-provider]: https://learn.microsoft.com/aspnet/core/fundamentals/logging/#debug
[vscode-debug-console]: https://code.visualstudio.com/docs/editor/debugging
