# Setup Mac

Les logiciel a installer sont:

- chrome
- visual studio code
- Gitkraken
- Iterm
- Figma
- Dashlane
- Notion
- Telegram
- Spotify


Homebrew/terminal/bash
OSX Productivity - Window Management/Quick Launcher/Hyperswitch
OSX Settings - Dock/Finder
Web Browser - Extensions - AdBlock, Privacy Badger, OneTab, JSONViewer, Stylus, Vue Devtools, React Devtools
Node.js - nvm
Code Editor - vs code
Code Editor Extensions
Break timer and Flux

ligicel brew:

````
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
brew update
brew cask install iterm2
# update iterm2 settings -> colors, keep directory open new shell, keyboard shortcuts
brew install git
brew install node
brew cask install postman
brew cask install visual-studio-code
# update vscode settings
# install vscode extensions 
````


while read line; do code --install-extension "$line";done < vscode-extensions.txt
