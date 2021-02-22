# My VM Linux Setup *Notes*


### WIP setup vm: Deian 10

### update and install

```bash
sudo apt update -y && sudo apt upgrade -y
sudo apt install python3-pip
python3 -V # check default version (time of these notes 3.7)
# sudo apt install python3.x
sudo apt install virtualenv
sudo pip3 install virtualenvwrapper
sudo apt install python3-tk
sudo apt install xauth
sudo apt install git
sudo apt install wget
```


### Install terminator, sublime, zsh and configure with Oh My ZSH
```bash
sudo apt install zsh
sh -c "$(wget https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)"
```

### remember (if needed)
- .gitconfig
- ./ssh

### add to .zshrc (zsh customization)
```bash
ZSH_THEME="bureau"

plugins=(
git
zsh-autosuggestions
zsh-syntax-highlighting
)
```

### check
```bash
sudo find / -name virtualenvwrapper.sh
```

### add to .bashrc or / .zshrc
```bash
export WORKON_HOME=$HOME/.virtualenvs
export VIRTUALENVWRAPPER_PYTHON=/usr/bin/python3
source /usr/local/bin/virtualenvwrapper.sh
```

### Get started
```bash
source ~/.bashrc
source ~/.zshrc
```

<!-- ## Install from deadsnakes (Ubuntu)

```bash
sudo apt install software-properties-common
sudo add-apt-repository ppa:fkrull/deadsnakes
sudo apt install python3.7
``` -->

### fix /etc/ssh/sshd_config (uncomment)
# X11Forwarding yes
# X11DisplayOffset 10
# X11UseLocalhost yes

### docker
https://docs.docker.com/engine/install/debian/

### Google Cloud SDK
- install
- init
- add to docker authentification

### Add to .ssh
- add config; user
- add ssh-keys (in GCP, use default ssh-key naming for repo-connect)
- set rw permission for ssh-keys