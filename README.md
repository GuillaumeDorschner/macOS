# macOS setup 🖥
I wrote this git for the configuration of my Mac

## Install brew
```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
brew update
```

## Oh-my-zsh
```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
brew install neofetch

echo -e "install neofetch / oh my zsh"
cat <<EOF >> ~/.zshrc
export ZSH="$HOME/.oh-my-zsh"

ZSH_THEME="robbyrussell"

plugins=(git sudo kubectl docker docker-compose doctl)

source $ZSH/oh-my-zsh.sh
neofetch --ascii ~/.config/neofetch/ascii-art.txt
source <(kubectl completion zsh)
source <(helm completion zsh)

alias finder='open -a Finder .'
alias python='python3'

mcd() {
  mkdir -p "$1" && cd "$1"
}

source $(brew --prefix)/share/zsh-autosuggestions/zsh-autosuggestions.zsh
export PATH="/usr/local/opt/ruby/bin:$PATH"
EOF

echo -e "oh-my-zsh set"
cat <<EOF >> ~/.config/neofetch/ascii-art.txt
      %%% %%%%%%%            |#|
    %%%% %%%%%%%%%%%        |#|####
  %%%%% %         %%%       |#|=#####
 %%%%% %   @    @   %%      | | ==####
%%%%%% % (_  ()  )  %%     | |    ===##
%%  %%% %  \_    | %%      | |       =##
%    %%%% %  u^uuu %%     | |         ==#
      %%%% %%%%%%%%%      | |           V
EOF

echo -e "Neofetch set"
cat <<EOF >> ~/.config/neofetch/config.conf
# Source: https://github.com/Chick2D/neofetch-themes/ 
# Do consider checking out the repository, it has a ton of great configs like this.

# Made by Chick (BlockFetch)

# Customization Wiki https://github.com/dylanaraps/neofetch/wiki/Customizing-Info

print_info() {
    
    info " ​ ​ ${cl5}██ CPU" cpu
    info " ​ ​ ${cl2}██ GPU" gpu
    info " ​ ​ ${cl6}██ Distro" distro
    info " ​ ​ ${cl4}██ Kernel" kernel
    info " ​ ​ ${cl1}██ WM" wm
    info " ​ ​ ${cl7}██ Shell" shell
    info " ​ ​ ${cl3}██ Packages" packages 
    info " ​ ​ ${cl6}██ MEM" memory
    info cols
}

kernel_shorthand="on"
distro_shorthand="off"
os_arch="off"
uptime_shorthand="on"
memory_percent="on"
package_managers="on"
shell_path="off"
shell_version="on"
speed_type="bios_limit"
speed_shorthand="on"
cpu_brand="off"
cpu_speed="off"
cpu_cores="logical"
cpu_temp="off"
gpu_brand="off"
gpu_type="all"
refresh_rate="on"
gtk_shorthand="on"
gtk2="on"
gtk3="on"
public_ip_host="http://ident.me"
public_ip_timeout=2
disk_show=('/')
music_player="vlc"
song_format="%artist% - %title%"
song_shorthand="off"
colors=(distro)
bold="on"
underline_enabled="on"
underline_char="-"
separator=""
color_blocks="off"
block_range=(0 15) # Colorblocks

# Colors for custom colorblocks
magenta="\033[1;35m"
green="\033[1;32m"
white="\033[1;37m"
blue="\033[1;34m"
red="\033[1;31m"
black="\033[1;40;30m"
yellow="\033[1;33m"
cyan="\033[1;36m"
reset="\033[0m"
bgyellow="\033[1;43;33m"
bgwhite="\033[1;47;37m"
cl0="${reset}"
cl1="${magenta}"
cl2="${green}"
cl3="${white}"
cl4="${blue}"
cl5="${red}"
cl6="${yellow}"
cl7="${cyan}"
cl8="${black}"
cl9="${bgyellow}"
cl10="${bgwhite}"

block_width=4
block_height=1

bar_char_elapsed="-"
bar_char_total="="
bar_border="on"
bar_length=15
bar_color_elapsed="distro"
bar_color_total="distro"

cpu_display="on"
memory_display="on"
battery_display="on"
disk_display="on"

image_backend="ascii"
#image_source="$HOME/"
image_size="auto"
image_loop="off"

ascii_distro="arch_small"
ascii_colors=(distro)
ascii_bold="on"

thumbnail_dir="${XDG_CACHE_HOME:-${HOME}/.cache}/thumbnails/neofetch"
crop_mode="normal"
crop_offset="center"

gap=2

yoffset=0
xoffset=0

stdout="off"
```

## Tmux
```bash
git clone https://github.com/tmux-plugins/tpm ~/.tmux/plugins/tpm
cat <<EOF >> $HOME/.tmux.conf
set-option -sa terminal-overrides ",xterm*:Tc"
set -g mouse on

unbind C-b
set -g prefix C-Space
bind C-Space send-prefix

# Vim style pane selection
bind h select-pane -L
bind j select-pane -D 
bind k select-pane -U
bind l select-pane -R

# Start windows and panes at 1, not 0
set -g base-index 1
set -g pane-base-index 1
set-window-option -g pane-base-index 1
set-option -g renumber-windows on

# Use Alt-arrow keys without prefix key to switch panes
bind -n M-Left select-pane -L
bind -n M-Right select-pane -R
bind -n M-Up select-pane -U
bind -n M-Down select-pane -D

# Shift arrow to switch windows
bind -n S-Left  previous-window
bind -n S-Right next-window

# Shift Alt vim keys to switch windows
bind -n M-H previous-window
bind -n M-L next-window

set -g @catppuccin_flavour 'mocha'

set -g @plugin 'tmux-plugins/tpm'
set -g @plugin 'tmux-plugins/tmux-sensible'
set -g @plugin 'christoomey/vim-tmux-navigator'
set -g @plugin 'dreamsofcode-io/catppuccin-tmux'
set -g @plugin 'tmux-plugins/tmux-yank'

run '~/.tmux/plugins/tpm/tpm'

# set vi-mode
set-window-option -g mode-keys vi
# keybindings
bind-key -T copy-mode-vi v send-keys -X begin-selection
bind-key -T copy-mode-vi C-v send-keys -X rectangle-toggle
bind-key -T copy-mode-vi y send-keys -X copy-selection-and-cancel

bind '"' split-window -v -c "#{pane_current_path}"
bind % split-window -h -c "#{pane_current_path}"
EOF
```

## Vim
```bash
cat <<EOF >> ~/.vimrc
syntax on
set number
EOF
```


## Bases
```bash
brew install git
brew install node
brew install python
brew install rustup-init
brew install --cask mactex
# npm package for reload js files on change
npm install -g nodemon
npm install -g pnpm
# npm package makes copies of git repositories
npm install -g degit
# nvm installation
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash
```
then restart the terminal and create a file nano ~/.zshrc and paste it the code below
```bash
export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm
```

## Brew dev
```bash
brew install ansible
brew instal k9s
brew insatll nmap
```

## Security
> [!CAUTION]
> 1. Create a backup!
> ```sudo cp /etc/pam.d/sudo_local /etc/pam.d/sudo_local.bak```
> 2. Open another sudo terminal.
> 3. Git clone & make project for Apple Watch. See instructions [here](https://github.com/biscuitehh/pam-watchid) and [this blog](https://heywoodlh.io/macos-sudo-watch-touch-id#the-pam_tid-module-does-not-work-with-a-macbooks-lid-closed) gave me the hint.
> 4. Modify to authorize biometrics in the terminal. Add the following text at the beginning of the `sudo nano /etc/pam.d/sudo_local` file.
```
# sudo_local: local config file which survives system update and is included for sudo
auth       sufficient     pam_tid.so
auth sufficient pam_watchid.so "reason=execute a command as root"
```

## Install the softwares 
- terminal --> `Setting > Profile > Shell` When the shell exit to close if the shell exit cleanly
```bash
brew install --cask visual-studio-code
brew install --cask libreoffice
brew install --cask gitkraken
brew install --cask figma
brew install --cask notion

```
- Docker (You can't download via brew)  
https://docs.docker.com/docker-for-mac/install/

- Libre Office
https://youtu.be/x44bda1dz84

## Add Working directory To Program
```bash
mkdir /Users/guillaumedorschner/Git
mkdir /Users/guillaumedorschner/Dev
```

## Macos config
```bash
###############################################################################
# My config                                                                   #
###############################################################################

# 𝗗𝗶𝘀𝗮𝗯𝗹𝗲 𝗔𝗻𝗻𝗼𝘆𝗶𝗻𝗴 𝗗𝗶𝘀𝗸 𝗪𝗮𝗿𝗻𝗶𝗻𝗴
sudo defaults write /Library/Preferences/SystemConfiguration/com.apple.DiskArbitration.diskarbitrationd.plist DADisableEjectNotification -bool YES && sudo pkill diskarbitrationd

# # capture to jpg
# defaults write com.apple.screencapture type jpg

# Automatically quit printer app once the print jobs complete
defaults write com.apple.print.PrintingPrefs "Quit When Finished" -bool true


###############################################################################
# Screen                                                                      #
###############################################################################

# Require password immediately after sleep or screen saver begins
defaults write com.apple.screensaver askForPassword -int 1
defaults write com.apple.screensaver askForPasswordDelay -int 0

# Save screenshots to the desktop
defaults write com.apple.screencapture location -string "${HOME}/Desktop"


###############################################################################
# Finder                                                                      #
###############################################################################

# Finder: show all filename extensions
defaults write NSGlobalDomain AppleShowAllExtensions -bool true

# When performing a search, search the current folder by default
defaults write com.apple.finder FXDefaultSearchScope -string "SCcf"

# Avoid creating .DS_Store files on network or USB volumes
defaults write com.apple.desktopservices DSDontWriteNetworkStores -bool true
# defaults write com.apple.desktopservices DSDontWriteUSBStores -bool true

# Automatically open a new Finder window when a volume is mounted
defaults write com.apple.frameworks.diskimages auto-open-ro-root -bool true
defaults write com.apple.frameworks.diskimages auto-open-rw-root -bool true
defaults write com.apple.finder OpenWindowForNewRemovableDisk -bool true

# Disable snap-to-grid for icons on the desktop and in other icon views
/usr/libexec/PlistBuddy -c "Set :DesktopViewSettings:IconViewSettings:arrangeBy arranged" ~/Library/Preferences/com.apple.finder.plist
/usr/libexec/PlistBuddy -c "Set :FK_StandardViewSettings:IconViewSettings:arrangeBy arranged" ~/Library/Preferences/com.apple.finder.plist
/usr/libexec/PlistBuddy -c "Set :StandardViewSettings:IconViewSettings:arrangeBy arranged" ~/Library/Preferences/com.apple.finder.plist

# Revert grid spacing for icons on the desktop and in other icon views
/usr/libexec/PlistBuddy -c "Set :DesktopViewSettings:IconViewSettings:gridSpacing 54" ~/Library/Preferences/com.apple.finder.plist
/usr/libexec/PlistBuddy -c "Set :FK_StandardViewSettings:IconViewSettings:gridSpacing 54" ~/Library/Preferences/com.apple.finder.plist
/usr/libexec/PlistBuddy -c "Set :StandardViewSettings:IconViewSettings:gridSpacing 54" ~/Library/Preferences/com.apple.finder.plist

# Revert the size of icons on the desktop and in other icon views
/usr/libexec/PlistBuddy -c "Set :DesktopViewSettings:IconViewSettings:iconSize 64" ~/Library/Preferences/com.apple.finder.plist
/usr/libexec/PlistBuddy -c "Set :FK_StandardViewSettings:IconViewSettings:iconSize 64" ~/Library/Preferences/com.apple.finder.plist
/usr/libexec/PlistBuddy -c "Set :StandardViewSettings:IconViewSettings:iconSize 64" ~/Library/Preferences/com.apple.finder.plist

# Enable AirDrop over Ethernet and on unsupported Macs running Lion
defaults write com.apple.NetworkBrowser BrowseAllInterfaces -bool true

# Disable the warning before emptying the Trash
defaults write com.apple.finder WarnOnEmptyTrash -bool false


###############################################################################
# Dock, Dashboard, and hot corners                                            #
###############################################################################

# Don’t show recent applications in Dock
defaults write com.apple.dock show-recents -bool false

# Hot corners
# Possible values:
#  0: no-op
#  2: Mission Control
#  3: Show application windows
#  4: Desktop
#  5: Start screen saver
#  6: Disable screen saver
#  7: Dashboard
# 10: Put display to sleep
# 11: Launchpad
# 12: Notification Center
# 13: Lock Screen
# 14: Quick Note
# Bottom right screen corner → Quick note
defaults write com.apple.dock wvous-br-corner -int 14
defaults write com.apple.dock wvous-br-modifier -int 0
# Bottom left screen corner → Desktop
defaults write com.apple.dock wvous-bl-corner -int 4
defaults write com.apple.dock wvous-bl-modifier -int 0


###############################################################################
# Safari & WebKit                                                             #
###############################################################################

# Privacy: don’t send search queries to Apple
defaults write com.apple.Safari UniversalSearchEnabled -bool false
defaults write com.apple.Safari SuppressSearchSuggestions -bool true

# Enable Safari’s debug menu
defaults write com.apple.Safari IncludeInternalDebugMenu -bool true

# Enable the Develop menu and the Web Inspector in Safari
defaults write com.apple.Safari IncludeDevelopMenu -bool true
defaults write com.apple.Safari WebKitDeveloperExtrasEnabledPreferenceKey -bool true
defaults write com.apple.Safari com.apple.Safari.ContentPageGroupIdentifier.WebKit2DeveloperExtrasEnabled -bool true

# Add a context menu item for showing the Web Inspector in web views
defaults write NSGlobalDomain WebKitDeveloperExtras -bool true

# Enable “Do Not Track”
defaults write com.apple.Safari SendDoNotTrackHTTPHeader -bool true


###############################################################################
# Terminal & iTerm 2                                                          #
###############################################################################

# Don’t display the annoying prompt when quitting iTerm
defaults write com.googlecode.iterm2 PromptOnQuit -bool false


###############################################################################
# Time Machine                                                                #
###############################################################################

# Prevent Time Machine from prompting to use new hard drives as backup volume
defaults write com.apple.TimeMachine DoNotOfferNewDisksForBackup -bool true

# Disable local Time Machine backups
hash tmutil &>/dev/null && sudo tmutil disablelocal


###############################################################################
# Mac App Store                                                               #
###############################################################################

# Enable the automatic update check
defaults write com.apple.SoftwareUpdate AutomaticCheckEnabled -bool true

# Download newly available updates in background
defaults write com.apple.SoftwareUpdate AutomaticDownload -int 1

# Turn on app auto-update
defaults write com.apple.commerce AutoUpdate -bool true


###############################################################################
# Messages                                                                    #
###############################################################################

# Disable smart quotes as it’s annoying for messages that contain code
defaults write com.apple.messageshelper.MessageController SOInputLineSettings -dict-add "automaticQuoteSubstitutionEnabled" -bool false


###############################################################################
# Kill affected applications                                                  #
###############################################################################

for app in "Activity Monitor" \
	"Address Book" \
	"Calendar" \
	"cfprefsd" \
	"Contacts" \
	"Dock" \
	"Finder" \
	"Mail" \
	"Messages" \
	"Photos" \
	"Safari" \
	"SizeUp" \
	"SystemUIServer" \
	"Terminal" \
	"iCal"; do
	killall "${app}" &>/dev/null
done
echo "Done. Note that some of these changes require a logout/restart to take effect."
```

## Dot files
```bash
defaults write com.apple.finder AppleShowAllFiles YES
```

## The extras for a Mac
- Magnet (it's in the app store)
- Mos
```bash
brew cask install mos
```

## Finder Shortcut
Go to settings `Keyboard > Keyboard Shortcuts... > Services > Files and Folders` and check the following:
![image](https://github.com/GuillaumeDorschner/Setup-Mac/assets/44686652/b4b46d93-ae25-4372-a098-9a06ec860c7d)


## Setting de VSCode
With `Commande`+`Shift`+`P` go to `Preferences > settings (JSON)` paste the following:
```json
{
  // --- Language ---
  // all
  "editor.formatOnSave": true,
  "editor.defaultFormatter": "esbenp.prettier-vscode",

  // Python
  "[python]": {
    "editor.formatOnSave": true,
    "editor.tabSize": 4,
    // "editor.defaultFormatter": "ms-python.black-formatter",
    "editor.defaultFormatter": "charliermarsh.ruff"
    // "editor.codeActionsOnSave": {
    //   "source.organizeImports": "explicit",
    //   "source.fixAll": "explicit"
    // }
  },
  // "python.analysis.typeCheckingMode": "strict",
  "ruff.path": ["/Library/Frameworks/Python.framework/Versions/3.11/bin/ruff"],

  // typescript
  "[typescriptreact]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode",
    "typescript.validate.enable": false
  },

  // Github copilot
  "github.copilot.enable": {
    "*": true,
    "plaintext": false,
    "markdown": false,
    "scminput": false
  },

  // Notebook
  "notebook.formatOnCellExecution": true,
  "notebook.formatOnSave.enabled": true,
  "notebook.codeActionsOnSave": {
    "source.organizeImports": true
  },

  // Latex
  "latex-workshop.view.pdf.viewer": "tab",
  "latex-workshop.latex.autoBuild.run": "onSave",
  "latex-workshop.latex.recipe.default": "lastUsed",
  "latex-workshop.synctex.afterBuild.enabled": true,
  "latex-workshop.latex.autoClean.run": "onBuilt",
  "latex-workshop.view.outline.sync.viewer": true,
  "latex-workshop.latex.tools": [
    {
      "name": "latexmk",
      "command": "xelatex",
      "args": [
        "-xelatex",
        "-interaction=nonstopmode",
        "-outdir=%OUTDIR%",
        "%DOCFILE%"
      ]
    }
  ],

  // --- General VSC ---
  "editor.snippetSuggestions": "top",
  "editor.inlineSuggest.enabled": true,
  "editor.cursorSmoothCaretAnimation": "on",
  "editor.minimap.enabled": false,
  "editor.linkedEditing": true,
  "workbench.startupEditor": "none",
  "workbench.sideBar.location": "right",
  "workbench.iconTheme": "material-icon-theme",
  "workbench.editorAssociations": {
    "*.pdf": "latex-workshop-pdf-hook"
  },
  "explorer.confirmDragAndDrop": false,
  "explorer.confirmPasteNative": false,
  "explorer.confirmDelete": false,
  "security.workspace.trust.enabled": false,
  "security.workspace.trust.untrustedFiles": "newWindow",
  "python.defaultInterpreterPath": "/usr/local/bin/python3",
  "redhat.telemetry.enabled": true,
  "liveServer.settings.donotShowInfoMsg": true,
  "application.shellEnvironmentResolutionTimeout": 30,
  "git.autofetch": true,
  "python.createEnvironment.trigger": "off",
  "git.confirmSync": false,
  "window.confirmSaveUntitledWorkspace": false,
  "terminal.integrated.enableMultiLinePasteWarning": "never",
  "terminal.integrated.showExitAlert": false, // termianl: exit ctrl + d --> error 127 so disable showExitAlert

  // --- Extensions ---
  // Code snap
  "codesnap.backgroundColor": "",
  "codesnap.showWindowTitle": true,
  "codesnap.shutterAction": "copy",
  "codesnap.transparentBackground": true,
  "codesnap.boxShadow": "rgba(0, 0, 0, 0.45) 0px 8px 28px",
  "vs-kubernetes": {
    "vscode-kubernetes.minikube-path.mac": "/Users/guillaumedorschner/.vs-kubernetes/tools/minikube/darwin-amd64/minikube",
    "vs-kubernetes.minikube-show-information-expiration": "2024-06-08T09:06:34.356Z"
  },

  // Flutter
  "dart.previewFlutterUiGuides": true,
  "dart.previewFlutterUiGuidesCustomTracking": true,
  "dart.showInspectorNotificationsForWidgetErrors": false,
  "dart.debugExternalPackageLibraries": true,
  "dart.debugSdkLibraries": false,

  // Svelte
  "svelte.enable-ts-plugin": true,
  "workbench.editor.labelFormat": "short",
  "explorer.compactFolders": false,
  "workbench.colorTheme": "Material Theme Ocean High Contrast",
  "markdown.marp.chromePath": "/Applications/Brave Browser.app",
  "markdown.marp.enableHtml": true,
  "jupyter.askForKernelRestart": false,
  "git.openRepositoryInParentFolders": "never"
}
```

## Extention de VSCode
- C++
- C#
- CodeSnap
- CQL
- Dart
- Dev Container
- Docker
- Error Lens
- Flutter
- Jupyter
- Koltin
- Kubernetes
- LateX Works
- Live Server
- Live Share
- Manim SideView
- Markdown All in one
- Markdown Preview Enhanced
- Markdown Preview Mermaid Support
- Marp
- Community Material Theme
- Material Theme Icons
- Mermaid Markdown
- Prettier
- Prisma
- Python
- R
- Reload
- Remote SSH
- Ruff
- Rust Analyser
- Svelte 3 Snippets
- Svelte for VS Code
- YAML
- VIM
