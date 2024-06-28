# .NET Logging

In vs code, logs from the [debug provider][dotnet-logging-debug-provider] and the [console provider][dotnet-logging-console-provider] both show up in the [debug console][vscode-debug-console]. This ends up duplicating all the logs, and since they're in different formats, makes it really difficult to read and understand.

To make things worse they're not [in color](#add-some-color). Lame :roll_eyes:.

![debug_console_log](/img/debug_console_log.png)

## Reduce the noise

Since the [console provider][dotnet-logging-console-provider] already logs to the [debug console][vscode-debug-console], I tend to just turn the [debug provider][dotnet-logging-debug-provider] off:

```diff
// appsettings.Development.json
{
  "Logging": {
    ...
    "Debug": {
      "LogLevel": {
+       "LogLevel": "None"
      }
    }
  }
}
```

![console_log](/img/console_log.png)

And we get much less! ...exactly half as much :nerd_face:

## Add some color

So... how bout color? Color would make it a hell of a lot easier to find that error I decided to log earlier (instead of fix), and I recently just so happen to come across [this little gem][dotnet-env-var-enable-color] :heart_eyes:

```json
"DOTNET_SYSTEM_CONSOLE_ALLOW_ANSI_COLOR_REDIRECTION": "true"
```

![console_log_allow_ansi](/img/console_log_allow_ansi.png)

It can be set in your [launchSettings.json][dotnet-lsj] or vscode [launch.json][vscode-launch-json] files.

> [!TIP]
> Add it to your [global launch.json][vscode-global-launch-json] and forget it

## Single line

Finally, if you're the type that selects **_compact_** mode in for your Teams and email threads, we've got something for you too:

```diff
// appsettings.Development.json
{
  "Logging": {
    "Console": {
      ...
+     "FormatterOptions": {
+       "SingleLine": true
+     }
    }
  }
}
```

![console_log_allow_ansi_single_line](/img/console_log_allow_ansi_single_line.png)

## Other settings

I've found that a couple more settings will reduce the noise in your logs when developing locally:

```json
//.vscode/settings.json
{
  "csharp.debug.logging.moduleLoad": false,
  "csharp.debug.logging.exceptions": false
}
```

[dotnet-logging-console-provider]: https://learn.microsoft.com/aspnet/core/fundamentals/logging/#console
[dotnet-logging-debug-provider]: https://learn.microsoft.com/aspnet/core/fundamentals/logging/#debug
[dotnet-env-var-enable-color]: https://github.com/dotnet/runtime/blob/d88e6680e1f9e2cb4f5ee428aa169ab715158eab/src/libraries/Common/src/System/Console/ConsoleUtils.cs#L38-L40
[dotnet-lsj]: https://learn.microsoft.com/aspnet/core/fundamentals/environments#lsj
[vscode-debug-console]: https://code.visualstudio.com/docs/editor/debugging
[vscode-launch-json]: https://code.visualstudio.com/docs/editor/debugging#_launchjson-attributes
[vscode-global-launch-json]: https://code.visualstudio.com/docs/editor/debugging#_global-launch-configuration
