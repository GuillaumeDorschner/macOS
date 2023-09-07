# Setup Mac 🖥

I wrote this git for the configuration of my Mac

## Install brew

```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
brew update
```

## Oh-my-zsh

```
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
brew install neofetch
cat <<EOF >> ~/.zshrc
export ZSH="$HOME/.oh-my-zsh"

ZSH_THEME="robbyrussell"

plugins=(
	git
	sudo
	)

source $ZSH/oh-my-zsh.sh

neofetch --ascii ~/.config/neofetch/ascii-art.txt
EOF
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


## Alias

```
cat << EOF >> ~/.zshrc
alias dcr='docker compose down && docker compose up -d --build'
alias dkc='docker rm -f $(docker ps -a -q)'
alias dki='docker rmi -f $(docker images -q)'

alias finder='open -a Finder .'
alias python='python3'

mcd() {
  mkdir -p "$1" && cd "$1"
}
EOF
```

## Autocomplete

```
brew install bash-completion
source <(kubectl completion zsh)
echo "source <(kubectl completion zsh)" >> ~/.zshrc
```

## Bases
```
brew install git
brew install node
brew install python
brew install rustup-init
# npm package for reload js files on change
npm install -g nodemon
# npm package makes copies of git repositories
npm install -g degit
# nvm installation
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
brew cask install dashlane
brew cask install visual-studio-code
brew cask install gitkraken
brew cask install figma
brew cask install notion
brew cask install telegram
```
- Docker (You can't download via brew)  
https://docs.docker.com/docker-for-mac/install/

## Add Working directory To Program

mkdir /Users/guillaumedorschner/Git

## 𝗗𝗶𝘀𝗮𝗯𝗹𝗲 𝗔𝗻𝗻𝗼𝘆𝗶𝗻𝗴 𝗗𝗶𝘀𝗸 𝗪𝗮𝗿𝗻𝗶𝗻𝗴 and capture to jpg

```
sudo defaults write /Library/Preferences/SystemConfiguration/com.apple.DiskArbitration.diskarbitrationd.plist DADisableEjectNotification -bool YES && sudo pkill diskarbitrationd
# defaults write com.apple.screencapture type jpg
```

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
