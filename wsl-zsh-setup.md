# wsl-terminal-setup

## WSL + zsh <3

- Installation: https://docs.microsoft.com/en-us/windows/wsl/install-win10
- Update and upgrade:  
```
sudo apt update && sudo apt upgrade
sudo apt dist-upgrade
sudo apt autoremove
```
- In Ubuntu terminal, install Zsh (and curl and git):  
```
sudo apt install zsh curl git
```
- Install Oh-My-Zsh:   
```
sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```
- Change the default terminal to zsh:
```
sudo chsh -s $(which zsh)
```
- Change the Theme to agnoster:  
```
sed -i 's/ZSH_THEME="robbyrussell"/ZSH_THEME="agnoster"/g' ~/.zshrc
```
- To have a correctly working agnoster theme, it’s needed to download and install the needed fonts, in Powershell:  
``` 
git clone https://github.com/powerline/fonts.git --depth=1
cd fonts
.\install.ps1

#clean up
cd ..
rd /S /Q fonts
```
- Make the directory more readable by changing the back color to a bit lighter blue:  
```
sed -i '0,/blue/{s/blue/39d/}' ~/.oh-my-zsh/themes/agnoster.zsh-theme
```
- Enable autocorrection:  
```
sed -i 's/# ENABLE_CORRECTION="true"/ENABLE_CORRECTION="true"/g' ~/.zshrc
```
- Enable autosuggestions:  
```
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```
- Enable syntax highlighting:     
```
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```
- Change zshrc-file: ```nano ~/.zshrc``` AND change the file:   
```
plugins=(
    git
    zsh-autosuggestions
    zsh-syntax-highlighting
)
```
- Add the following line right under the plugins part to prevent error message: “Insecure completion-dependent directories detected”:  
```
ZSH_DISABLE_COMPFIX=true
```
- Put this in ~/.zshrc to make commandline more colorful (read <a href="https://stackoverflow.com/a/2534676">this</a> for details):
```
autoload -U colors && colors
PS1="%{$fg[red]%}%n%{$reset_color%}@%{$fg[blue]%}%m %{$fg[yellow]%}%~ %{$reset_color%}%% "
```
- Do not show the username in the prompt:  
```
prompt_context() {
    DEFAULT_USER="($whoami)"
    if [[ "$USER" != "$DEFAULT_USER" || -n "$SSH_CLIENT" ]]; then
        prompt_segment black default "%(!.%{%F{yellow}%}.)$USER"
    fi
}
```
- Have the cursor on the next line by default, change .zshrc following:  
```
prompt_end() {
    if [[ -n $CURRENT_BG ]]; then
        echo -n " %{%k%F{$CURRENT_BG}%}$SEGMENT_SEPARATOR\n"
    else
        echo -n "%{%k%}"
    fi
    echo -n "%{%f%}"
    CURRENT_BG=''
}
```
- in VSCode:
```
"terminal.integrated.fontFamily": "DejaVu Sans Mono for Powerline",
"terminal.integrated.shell.windows": "C:\\Windows\\System32\\wsl.exe"
```
- Windows binaries can now be invoked directly from the WSL command line (<a href="https://docs.microsoft.com/en-us/windows/wsl/release-notes?redirectedfrom=MSDN&f=255&MSPPError=-2147217396#build-14951">details</a>), add to .zshrc:  
```
export PATH=$PATH:/mnt/c/Windows/System32
```
<hr>  

- Worth checking: https://github.com/sorin-ionescu/prezto

- Python  
```
sudo apt -y update
sudo apt -y install python3-pip  
pip3 --version
pip3 install jupyter
```
Add to the end of the file and save/exit: ```alias jupyter-notebook="~/.local/bin/jupyter-notebook --no-browser"```  
Update your bash profile: ```source ~/.bashrc```
