# Setup Mac 🖥

I wrote this git for the configuration of my Mac

# Install brew

```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
brew update
```

# Bases
```
brew install git
brew install node
````

# Install the softwares 

- Iterm2 (update iterm2 settings -> colors)
```
brew cask install iterm2
```
- Chrome
```
brew cask install google-chrome
```
- Dashlane
```
brew cask install dashlane
```
- Visual Studio Code
```
brew cask install visual-studio-code
```
- Gitkraken
```
brew cask install gitkraken
```
- Figma
```
brew cask install figma
```
- Notion
```
brew cask install notion
```
- Telegram
```
brew cask install telegram
```
- Spotify
```
brew cask install spotify
```
- PostMan
```
brew cask install postman
```
- Docker (You can't download via brew)
https://docs.docker.com/docker-for-mac/install/

# Add Working directory For Prgrammation

mkdir /Users/guillaumedorschner/Git

# The extras for a Mac

- Magnet (it's in the app store)
- Mos
```
brew cask install mos
```

# Setting de VSCode

> Preferences > settings (JSON)

```
{
    "workbench.startupEditor": "newUntitledFile",
    "python.showStartPage": false,
    "python.pythonPath": "/usr/local/bin/python3",
    "editor.cursorSmoothCaretAnimation": true,
    "workbench.iconTheme": "material-icon-theme",
    "workbench.colorTheme": "Material Theme Ocean High Contrast",
    "terminal.integrated.shell.osx": "/bin/bash",
    "explorer.confirmDelete": false,
    "breadcrumbs.enabled": true,
    "editor.renderWhitespace": "none",
    "editor.formatOnSave": true,
    "explorer.confirmDragAndDrop": false
}
```

# Extention de VSCode

- Community Material Theme
- Material Theme Icons
- Python
- Svelte 3 Snippets
- Svelte for VS Code
