# Setting Up GCC on Mac M1 with Homebrew

## Install Homebrew & Setup GCC

### Install GCC via Homebrew
```sh
brew install gcc
```

### Verify Installation Path
```sh
cd /opt/homebrew/bin
```

### Check GCC Version
```sh
g++ --version
```

### Remove Existing g++ Symlink
```sh
sudo rm g++
```

### Create New Symlink
```sh
ln -s g++-14 g++
```

### Restart Terminal and Verify Setup
```sh
g++ --version
g++-14 --version
ls -ltrh
which g++-14
which g++
```

### Create a Symlink for System-wide Usage
```sh
sudo ln -s /opt/homebrew/opt/gcc/bin/g++-14 /usr/local/bin/g++
```

## Configure C++ Compilation

### Modify C++ Single File Build System using PackageResourceViewer
1. Install `PackageResourceViewer` in Sublime Text.
2. Open Sublime Text and open the command palette (`Cmd + Shift + P`).
3. Select `PackageResourceViewer: Open Resource`.
4. Choose `C++` and then `C++ Single File.sublime-build`.
5. Modify the file with the following content:
```
{
	"shell_cmd": "/opt/homebrew/bin/g++-14 -std=c++17 \"${file}\" -o \"${file_path}/${file_base_name}\"",
	"file_regex": "^(..[^:]*):([0-9]+):?([0-9]+)?:? (.*)$",
	"working_dir": "${file_path}",
	"selector": "source.c++",

	"variants": [
		{
			"name": "Run",
			"shell_cmd": "/opt/homebrew/bin/g++-14 -std=c++17 \"${file}\" -o \"${file_path}/${file_base_name}\" && \"${file_path}/${file_base_name}\""
		}
	]
}
```
6. Save and close the file.

## Configure .zshrc

### Add Environment Variables
Append the following lines to `~/.zshrc`:
```
export CPATH=/opt/homebrew/include
export LIBRARY_PATH=/opt/homebrew/lib
```

### Apply Changes and Restart Sublime Text
```sh
source ~/.zshrc
```

## Updating GCC

### Install Latest GCC via Homebrew
```sh
brew install gcc
```

### Verify Installation Path
```sh
ls /opt/homebrew/bin
```

### Check GCC Version
```sh
gcc --version
```

### Remove Existing gcc Symlink (if any)
```sh
sudo rm /usr/local/bin/gcc
```

### Create New Symlink
```sh
sudo ln -s /opt/homebrew/opt/gcc/bin/gcc-14 /usr/local/bin/gcc
```

### Restart Terminal and Verify Setup
```sh
gcc --version
gcc-14 --version
ls -ltrh /usr/local/bin
which gcc-14
which gcc
```

## Tweaking Sublime Text Preferences

### Disable Font Smoothing for Better Rendering (to be run from terminal)
```sh
defaults write com.sublimetext.4 AppleFontSmoothing -int 0
```

### Update Preferences in `Preferences.sublime-settings`
```
{
    "ignored_packages": [
        "Vintage"
    ],
    "color_scheme": "Packages/Material Theme/schemes/Material-Theme-Darker.tmTheme",
    "theme": "Material-Theme-Darker.sublime-theme",
    "always_show_minimap_viewport": true,
    "bold_folder_labels": true,
    "font_options": ["gray_antialias", "subpixel_antialias", "no_italic", "no_bold"],
    "indent_guide_options": ["draw_normal", "draw_active"],
    "line_padding_bottom": 3,
    "line_padding_top": 3,
    "overlay_scroll_bars": "enabled",
    "index_files": true,
    "font_face": "JetBrains Mono",
    "font_size": 16,
    "gutter": true,
    "highlight_line": false,
    "scroll_past_end": true,
    "word_wrap": false,
    "wide_caret": true,
    "material_theme_accent_blue": true
}
```

## Install Sublime Text Packages

To enhance development experience, install the following packages in Sublime Text:

- **A File Icon** - Adds file icons to the sidebar.
- **AdvancedNewFile** - Quickly create new files from the command palette.
- **auto-save** - Automatically saves files when switching tabs or after inactivity.
- **C++ Completions** - Provides C++ autocompletion and snippets.
- **FileIcons** - Displays better file icons.
- **Formatter** - Format C++ and other language files.
- **HighlightWords** - Highlights selected words in the editor.
- **Material Theme** - A clean and modern theme.
- **Package Control** - The essential package manager for Sublime Text.
- **PackageResourceViewer** - Allows editing of built-in Sublime Text files.
- **SideBarEnhancements** - Adds extra functionality to the sidebar.
- **SublimeAStyleFormatter** - Auto format C++ code.
- **SublimeCodeIntel** - Provides intelligent code completion.
- **SublimeLinter** - Linting framework for various languages.
- **SublimeLinter-gcc** - Linter for C++ using `gcc`.
- **Terminal** - Open terminal inside Sublime.

To install all packages, follow these steps:

1. Open **Sublime Text**.
2. Press `Cmd + Shift + P` and type `"Package Control: Install Package"`.
3. Install each package one by one.


## Add Key Mapping in Sublime Text

Modify the **`Default (OSX).sublime-keymap`** file to add a new key binding for opening the terminal in the project folder:

1. Open Sublime Text and go to **Preferences > Key Bindings**.
2. Add the following entry inside the array:
```
[
	{ "keys": ["super+shift+t"], "command": "open_terminal_project_folder" }
]
```
3. Save and close the file.

