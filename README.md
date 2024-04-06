# Setup Mac 🖥
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


## Install the softwares 
- Iterm2 (update iterm2 settings -> colors)
```bash
brew install --cask iterm2
brew install --cask visual-studio-code
brew install --cask gitkraken
brew install --cask figma
brew install --cask notion
brew install --cask telegram
```
- Docker (You can't download via brew)  
https://docs.docker.com/docker-for-mac/install/

## Add Working directory To Program
```bash
mkdir /Users/guillaumedorschner/Git
mkdir /Users/guillaumedorschner/Dev
```

## 𝗗𝗶𝘀𝗮𝗯𝗹𝗲 𝗔𝗻𝗻𝗼𝘆𝗶𝗻𝗴 𝗗𝗶𝘀𝗸 𝗪𝗮𝗿𝗻𝗶𝗻𝗴 and capture to jpg
```bash
sudo defaults write /Library/Preferences/SystemConfiguration/com.apple.DiskArbitration.diskarbitrationd.plist DADisableEjectNotification -bool YES && sudo pkill diskarbitrationd
# defaults write com.apple.screencapture type jpg
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

## Setting de VSCode
With `Commande`+`Shift`+`P` go to `Preferences > settings (JSON)` paste the following:
```json
{
  // Python
  "[python]": {
    "editor.formatOnSave": true,
    "editor.tabSize": 4,
    // "editor.defaultFormatter": "ms-python.black-formatter",
    "editor.defaultFormatter": "charliermarsh.ruff",
    "editor.codeActionsOnSave": {
      "source.organizeImports": "explicit",
      "source.fixAll": "explicit"
    }
  },
  // "python.analysis.typeCheckingMode": "strict",
  "ruff.path": ["/Library/Frameworks/Python.framework/Versions/3.11/bin/ruff"],
  "black-formatter.path": [
    "/Library/Frameworks/Python.framework/Versions/3.11/bin/black"
  ],
  "black-formatter.args": [
    "--line-length",
    "130",
    "--experimental-string-processing"
  ],

  // Github copilot
  "github.copilot.enable": {
    "*": true
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

  // Prettier
  "[yaml]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[yml]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[jsonc]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[javascript]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[json]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[html]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[css]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },

  // General
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
  "terminal.integrated.showExitAlert": false, // termianl: exit ot ctrl + d --> error 127 so disable showExitAlert

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
