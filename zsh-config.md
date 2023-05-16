# Zsh Config

### Install ZSH shell
```shell
sudo pacman -S zsh
```

### Install oh-my-zsh
```shell
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

### Install `powerlevel10k` theme
```shell
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k
```

### Add theme to `.zshrc`
```shell
# Set name of the theme to load
ZSH_THEME="powerlevel10k/powerlevel10k"
```

### Configure `powerlevel10k` theme
```shell
p10k configure
```

### Install dependencies
```shell
sudo pacman -S exa zoxide lazygit gping
```
```shell
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```
```shell
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```

### Update `.zshrc` file

```vim
# Enable Powerlevel10k instant prompt. Should stay close to the top of ~/.zshrc.
# Initialization code that may require console input (password prompts, [y/n]
# confirmations, etc.) must go above this block; everything else may go below.
if [[ -r "${XDG_CACHE_HOME:-$HOME/.cache}/p10k-instant-prompt-${(%):-%n}.zsh" ]]; then
  source "${XDG_CACHE_HOME:-$HOME/.cache}/p10k-instant-prompt-${(%):-%n}.zsh"
fi

# GPG Signing
export GPG_TTY=`tty`

# Path to your oh-my-zsh installation.
export ZSH="$HOME/.oh-my-zsh"

# Set name of the theme to load
ZSH_THEME="powerlevel10k/powerlevel10k"

# Which plugins would you like to load?
# Standard plugins can be found in $ZSH/plugins/
plugins=(git yarn sudo zoxide zsh-autosuggestions zsh-syntax-highlighting)

source $ZSH/oh-my-zsh.sh

# Preferred editor for local and remote sessions
# if [[ -n $SSH_CONNECTION ]]; then
#   export EDITOR='vim'
# else
#   export EDITOR='mvim'
# fi

# Compilation flags
# export ARCHFLAGS="-arch x86_64"

# To customize prompt, run `p10k configure` or edit ~/.p10k.zsh.
[[ ! -f ~/.p10k.zsh ]] || source ~/.p10k.zsh

# Blur
if [[ $(ps --no-header -p $PPID -o comm) =~ '^yakuake|kitty$' ]]; then
        for wid in $(xdotool search --pid $PPID); do
            xprop -f _KDE_NET_WM_BLUR_BEHIND_REGION 32c -set _KDE_NET_WM_BLUR_BEHIND_REGION 0 -id $wid; done
fi

# Custom functions
function compile-cpp() {
    cpp_file=$1
    output_file=(${(s/./)cpp_file})
    g++ -o $output_file[1] $cpp_file
    echo Compilation completed
    ./$output_file[1]
}

function update-discord() {
    ds_folder=$1
    sudo rm -r /usr/share/discord/Discord/
    sudo mv $ds_folder /usr/share/discord/Discord/
}

# Configure default editor
export EDITOR="nvim"

# Aliases
alias ls="exa -l"
alias cd="z"
alias lz="lazygit"
alias gz="lazygit"
alias ping="gping"
alias :q="exit"
alias vim="nvim"
alias vi="vim"
alias v="vim"
alias v.="vim ."
alias vconfig="vim ~/.config/nvim/"
alias zconfig="vim ~/.zshrc"
alias kconfig="vim ~/.config/kitty/kitty.conf"
alias grb="git remote update origin --prune"
alias gc="compile-cpp"
alias fbd="flutter pub run build_runner build"

# Configure NVM 
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh"  # This loads nvm
[ -s "$NVM_DIR/bash_completion" ] && . "$NVM_DIR/bash_completion"  # This loads nvm bash_completion

# Deno Version Manager
export DVM_DIR="$HOME/.dvm"
[ -f "$DVM_DIR/dvm.sh" ] && . "$DVM_DIR/dvm.sh"
[ -f "$DVM_DIR/bash_completion" ] && . "$DVM_DIR/bash_completion"

# Configure zoxide
eval "$(zoxide init zsh)"

# Configue Flutter
export JAVA_HOME="/usr/lib/jvm/java-17-openjdk"
export PATH=$JAVA_HOME/bin:$PATH
export PATH=/opt/flutter/bin:$PATH
export CHROME_EXECUTABLE="/usr/bin/google-chrome-stable"
export PATH="$PATH:$HOME/.pub-cache/bin"
```