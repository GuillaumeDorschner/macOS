# Setup Mac 🖥

I wrote this git for the configuration of my Mac

## Install brew

```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
brew update
```

## Alias

```
alias finder='open -a Finder .'
alias python='python3'

mcd() {
  mkdir -p "$1" && cd "$1"
}
```

## Autocomplete

```source <(kubectl completion zsh)```

## Bases
```
brew install git
brew install node
brew install python
brew install rustup-init
```
npm package for reload js files on change
```
npm install -g nodemon
```
npm package makes copies of git repositories
```
npm install -g degit
````
nvm installation
```
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash
```
then restart the terminal and create a file nano ~/.zshrc and paste it the code below
```
export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm
```


## Install the softwares 

- Iterm2 (update iterm2 settings -> colors)
```
brew cask install iterm2
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
- Docker (You can't download via brew)  
https://docs.docker.com/docker-for-mac/install/

## Add Working directory To Program

mkdir /Users/guillaumedorschner/Git

## The extras for a Mac

- Magnet (it's in the app store)
- Mos
```
brew cask install mos
```

## Setting de VSCode

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

## Extention de VSCode

- Community Material Theme
- Material Theme Icons
- Python
- Svelte 3 Snippets
- Svelte for VS Code
