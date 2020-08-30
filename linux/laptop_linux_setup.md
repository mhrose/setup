# My Linux Setup *Notes*

### Manjaro Linux (Arch) e.g. in virtualbox
- install Manjaro latest from iso-file
- add network
- start installer
- choose free drivers
- choose encryption

### Get Toolbox (GitHub)
- mkdir mygit
- clone toolbox

### Browser
- sync Firefox account
- Set proxy under settings manually if needed

### Install Sublime
- https://www.sublimetext.com/docs/3/linux_repositories.html#pacman
- setup sublime according to toolbox files and registration


### Install terminator, zsh and configure with Oh My ZSH
```bash
pacman -S zsh
echo $SHELL
chsh -s $(which zsh)
restart shell
```

### get Oh My ZSH:
```bash
sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```

### Install virtualenvwrapper
```bash
sudo pip install virtualenv
sudo pip install virtualenvwrapper
mkdir ~/projects
```

###### add the following to .bashrc / .zshrc
```bash
export WORKON_HOME=$HOME/.virtualenvs
export PROJECT_HOME=$HOME/projects
export VIRTUALENVWRAPPER_PYTHON=/usr/bin/python
source /usr/bin/virtualenvwrapper.sh
```

###### make alias's in .zshrc e.g
```bash
boxcon="~/.dropbox-dist/dropboxd"
alias fixdisp="xrandr --output Virtual1 --mode 1920x1440"
alias xfixdisp="xrandr --output Virtual1 --mode 2560x1600"
```

### Add to .ssh
- add config; user and alias for cloud vm's
- add ssh-keys
- set rw permission for ssh-keys

### Git
- add .gitconfig (with token and proxy etc)

### Setup docker
```bash
sudo pacman -S docker
```

### add docker to systemctl
```bash
sudo systemctl start docker.service
sudo systemctl enable docker.service
```

##### add curret user to docker user group
```bash
sudo groupadd docker
sudo gpasswd -a mhrose docker
```

### install R
```bash
sudo pacman -S r
```

### Graphviz
```bash
sudo pacman -Syu graphviz
```

### Pandoc
```bash
sudo pacman -S pandoc
sudo pacman -S texlive-most
```

### Add Oracle Repository *for odbc drivers*
add to /etc/pacman.conf
```bash
[oracle]
SigLevel=Optional TrustAll
Server=http://linux.shikadi.net/arch/$repo/$arch/
```
and run

```bash
sudo pacman -Ss odbc
sudo pacman -S oracle-instantclient-odbc
```