# Oh My Posh

[Official Docs](https://docs.microsoft.com/en-us/windows/terminal/tutorials/custom-prompt-setup)

1. Download Windows Terminal
1. Download Windows Powershell (new goodness)
1. Download [Caskaydia Cove Nerd Font](https://github.com/ryanoasis/nerd-fonts/releases/download/v2.1.0/CascadiaCode.zip?WT.mc_id=-blog-scottha)
   - Optional
1. Install Oh My Posh for PS
   ```ps1
   Install-Module oh-my-posh -Scope CurrentUser
   ```
1. Find a theme you like
   ```ps1
   Get-PoshThemes
   ```
1. Either create or update your powershell profile
   ```ps1
   notepad $PROFILE
   ```
1. Add the following lines to the profile
   ```ps1
   Import-Module oh-my-posh
   Set-PoshPrompt -Theme paradox
   ```
1. Terminal Icons
   ```ps1
   Install-Module -Name Terminal-Icons -Repository PSGallery
   ```
   - Add to profile
   ```ps1
   Import-Module -Name Terminal-Icons
   ```
3. json for the theme I'm using:

   ```json
   {
   	"final_space": true,
   	"console_title": true,
   	"console_title_style": "folder",
   	"blocks": [
   		{
   			"type": "prompt",
   			"alignment": "left",
   			"horizontal_offset": 0,
   			"vertical_offset": 0,
   			"segments": [
   				{
   					"type": "path",
   					"style": "diamond",
   					"powerline_symbol": "",
   					"invert_powerline": false,
   					"foreground": "#ffffff",
   					"background": "#ff479c",
   					"leading_diamond": "",
   					"trailing_diamond": "",
   					"properties": {
   						"prefix": "  ",
   						"style": "folder"
   					}
   				},
   				{
   					"type": "git",
   					"style": "powerline",
   					"powerline_symbol": "",
   					"invert_powerline": false,
   					"foreground": "#193549",
   					"background": "#fffb38",
   					"leading_diamond": "",
   					"trailing_diamond": "",
   					"properties": {
   						"display_status": true,
   						"display_stash_count": true,
   						"display_upstream_icon": true
   					}
   				},
   				{
   					"type": "dotnet",
   					"style": "powerline",
   					"powerline_symbol": "",
   					"invert_powerline": false,
   					"foreground": "#ffffff",
   					"background": "#6CA35E",
   					"leading_diamond": "",
   					"trailing_diamond": "",
   					"properties": {
   						"display_version": true,
   						"prefix": "  "
   					}
   				},
   				{
   					"type": "root",
   					"style": "powerline",
   					"powerline_symbol": "",
   					"invert_powerline": false,
   					"foreground": "#ffffff",
   					"background": "#ffff66",
   					"leading_diamond": "",
   					"trailing_diamond": "",
   					"properties": null
   				},
   				{
   					"type": "exit",
   					"style": "powerline",
   					"powerline_symbol": "",
   					"invert_powerline": false,
   					"foreground": "#ffffff",
   					"background": "#2e9599",
   					"leading_diamond": "",
   					"trailing_diamond": "",
   					"properties": {
   						"always_enabled": true,
   						"color_background": true,
   						"display_exit_code": false,
   						"error_color": "#f1184c",
   						"prefix": " "
   					}
   				}
   			]
   		}
   	]
   }
   ```
