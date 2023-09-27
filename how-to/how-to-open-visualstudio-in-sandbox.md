---
tags: Visual-Studio
---

# How to open Visual Studio in a Sandbox on Windows

To run Visual Studio without all the configurations, themes, and references to user settings, you need to run an instance in a **sandbox**.

On Windows, open a Powershell or the VS2022 Developer Console:

![VS2022 Developer console](developer-console.png)

and type

```plaintext
devenv /RootSuffix NameYouWantToDisplay
```

_NameYouWantToDisplay_ is the name that will appear on the top-right corner.

![Visual Studio name appears on the top-right corner](visual-studio-name.png)

Then, you can change the theme by navigating Tools>Options>Environment>General.

More info at [Use Visual Studio in Presentation Mode 🔗](https://devblogs.microsoft.com/visualstudio/use-visual-studio-in-presentation-mode)
