# Modify Application Dock Items

Problem: I want to start Chromium with a command line flag.

Solution:

[Use the MacOS inbuilt application "Automator" to create a new application as a drop-in-replacement.](https://superuser.com/questions/271678/how-do-i-pass-command-line-arguments-to-dock-items)

* Start Automator
* create "Application"
* choose "Run Shell Script" from the options
* enter `open -a "Chromium.app" --args --silent-debugger-extension-api` (replace with correct application name and command line flags)
* save in `/Applications` folder on your Mac with a suitable name
* replace icon: go to the original application with the MacOS Finder, right click to "Get Info", copy the icon on the top left (`Command + C`), then open the new application and replace the icon with `Command + V`
