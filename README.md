# A-Linux-Machine-for-Programming-on-Terminal

# Ubuntu

## Essential
```shell
sudo apt-get update
sudo apt dist-upgrade
sudo apt install -y make build-essential libssl-dev zlib1g-dev libbz2-dev libreadline-dev libsqlite3-dev wget llvm libncurses5-dev libncursesw5-dev xz-utils tk-dev tk8.6 git git-doc tmux htop openssh-server curl graphviz
```
Essentials for programming and general propose:
* git git-doc: version control
* tmux: multiple terminal pane in same screen
* htop: task monitor
* openssh-server: remote access
* curl: download from web
* wget: get new repositories
Remove the superfluous

```shell
sudo apt remove --purge thunderbird libreoffice-\* gmusicbrowser parole simple-scan orage gnome-mines gnome-sudoku pidgin xfburn
sudo apt-get clean
sudo apt-get autoremove
```

## Vim
Installation
```shell
sudo apt install vim vim-doc
```
Plugging system
```shell
curl -fLo ~/.vim/autoload/plug.vim --create-dirs https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
```
Recommended configuration
```shell
wget https://raw.githubusercontent.com/wesleywilly/myvimrc/master/.vimrc -O ~/.vimrc
```

## ZSH and Oh-my-zsh
For more details, go to:
https://www.howtoforge.com/tutorial/how-to-setup-zsh-and-oh-my-zsh-on-linux/
Installing ZSH

```shell
sudo -s
apt install zsh -y
```

after install, don't touch anything, just continue..
```shell
which zsh
chsh -s /usr/bin/zsh root
exit
chsh -s /usr/bin/zsh 
which zsh
sudo su
reboot
```

When Xubuntu reload, open the terminal. If Zsh was successful installed, you will see a message with a question that you need to choose one option. Is recommended press  2 .
Confirm if installation done well with:
```shell
echo $SHELL
```

Download and install Oh-my-zsh
```shell
wget https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh -O - | zsh
cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc
source ~/.zshrc
```

Changing Theme
Go to themes directory and list the options available.
```shell
cd ~/.oh-my-zsh/themes/
ls -a
```

To view example of these themes go to:
https://github.com/robbyrussell/oh-my-zsh/wiki/Themes.
        
Pick one and open the Zsh configuration file:
```shell
vim ~/.zshrc
```

Find the line where are ZSH\_THEME= and insert the name of picked theme.
        
Remember to change vim to Insert mode pressing  i .
        
After changing, change Vim to Command mode pressing  esc , save and close file inserting the command  :wq and pressing  enter , see example below:
```text
ZSH_THEME="candy"
```

Now, reload the configuration file:
```shell
source ~/.zshrc
```

Setting up Plug-ins on Zsh
Go to plug-ins directory and list the options available.
```shell
cd ~/.oh-my-zsh/plugins/
ls -a
```

See more details about these plug-ins on: https://github.com/robbyrussell/oh-my-zsh/wiki/Plugins
        
Choose one or more plug-ins and open the Zsh configuration file to install.
```shell
vim ~/.zshrc +61
```

Toggle to Insert mode pressing  i  and add your plug-ins between bracket separated by space. See example of recommended plugins below.
```shell
plugins=(git extract web-search git-extras vagrant tmux jsontools lwd)
```

Back to Command mode pressing  esc  and insert the command  :wq  to save and exit. Don’t forget to press  enter .


Activating configurations
Back to Zsh configuration file:
```shell
vim ~/.zshrc
```

Toggle to Insert mode pressing  i  and remove the comment symbol # from follow lines:
```text
ENABLE_CORRECTION='true'
```

Back to Command mode pressing   esc , save and close file inserting the command  :wq and pressing  enter .


## Python
Install Python and essentials
```shell
sudo apt-get dist-upgrade
sudo apt-get install build-essential python-dev python-setuptools python-pip python-smbus
sudo apt-get install libncursesw5-dev libgdbm-dev libc6-dev
sudo apt-get install zlib1g-dev libsqlite3-dev tk-dev
sudo apt-get install libssl-dev openssl
sudo apt-get install libffi-dev
sudo apt install -y python3-tk python3-pip python3-dev python3-setuptools python3-bs4
pip install --upgrade pip
```

### Brew
Download and install.
```shell
sh -c "$(curl -fsSL https://raw.githubusercontent.com/Linuxbrew/install/master/install.sh)"
```

Execute the commands required after installation, include the gcc installation
        
Add Linuxbrew to PATH and to Zsh bash shell profile script
```shell
test -d ~/.linuxbrew && PATH="$HOME/.linuxbrew/bin:$HOME/.linuxbrew/sbin:$PATH"
test -d /home/linuxbrew/.linuxbrew && PATH="/home/linuxbrew/.linuxbrew/bin:/home/linuxbrew/.linuxbrew/sbin:$PATH"
test -r ~/.zshrc && echo "export PATH='$(brew --prefix)/bin:$(brew --prefix)/sbin'":'"$PATH"' >> ~/.profile
```
### Pyenv
Download and install.
```shell
curl -L https://raw.githubusercontent.com/yyuu/pyenv-installer/master/bin/pyenv-installer | zsh
```

Setup on Zsh configuration file.
```shell
vim ~/.zshrc +6
```

Create a white line pressing  o  and add these lines:
```text
export ZSH=$HOME/.oh-my-zsh
export PATH=$HOME/.pyenv/bin:$PATH
export WORKON_HOME=~/.ve
export PROJECT_HOME=~/workspace
eval "$(pyenv init -)"
#eval "(pyenv virtualenv-init -)"
#pyenv virtualenvwrapper_lazy
```

Back to Command mode pressing   esc , save and close file inserting the command  :wq and pressing  enter .
        
Reload the configuration file:
```shell
source ~/.zshrc
```
Update pyenv.
```shell
pyenv global 3.7.0
pyenv update
```

Install the last version using the command pyenv install. See example:
```shell
pyenv install 3.7.0
pyenv install 2.7.15
```

#### pyenv-virtualenvwrapper
Install both tools.
```shell
pip3 install virtualenvwrapper
brew install pyenv-virtualenvwrapper
```
Creating 4 specials virtualenvs
```shell
pyenv virtualenv 3.7.0 jupyter3
pyenv virtualenv 3.7.0 tools3
pyenv virtualenv 2.7.15 ipython2
pyenv virtualenv 2.7.15 tools2
```

Configuring the virtualenvs for work with python 3
```shell
pyenv activate jupyter3
pip3 install jupyter jupyterlab
python3 -m ipykernel install --user
pyenv deactivate
```

Configuring the virtualenvs for work with python 2
```shell
pyenv activate ipython2
pip install ipykernel
python -m ipykernel install --user
pyenv deactivate
```

Now install the modules that you will use in your project, see example below
```shell
pyenv activate tools3
pip3 install numpy matplotlib pandas scikit-learn nltk scrapy scipy graphviz pydotplus beautifulsoup4 requests
pyenv deactivate
pyenv activate tools2
pip install numpy matplotlib pandas scikit-learn nltk scrapy scipy graphviz pydotplus
pyenv deactivate
```

#### Global configuration

```shell
pyenv global 3.6.4 2.7.14 jupyter3 ipython2 tools3 tools2
```
The order of the environments is very important because it establish the PATH priority for the order of access of scripts.

Now back to zshrc file to uncomment the line “#pyenv virtualenvwrapper_lazy” removing the ‘#’
```shell
vim ~/.zshrc +6
```

put the cursor over the ‘#’ and press  d  and  [right] .
the line need to appear like that line:
```text
pyenv virtualenvwrapper_lazy
```
Save and close file inserting the command  :wq and pressing  enter .
Reload the configuration file:
```shell
source ~/.zshrc
```
#### Local configuration
Configuring a new project
```shell
mkproject project_example
```

opening  an existing project
```shell
workon project_example
```

changing virtual environment (from python3 to python 2, for example)
```shell
cd ~/workspace/project_example_copy
mkvirtualenv -a ~/workspace/project_example_copy -p python2 project_example_copy
```

#### Configuring The jupyter and iPython
```shell
ipython profile create
curl -L http://hbn.link/hb-ipython-startup-script > ~/.ipython/profile_default/startup/00-venv-sitepackages.py
```

## NLP with NLTK

```shell
python3
```
In python console
```python
import nltk
nltk.download()
```

Once you've installed NLTK, start up the Python interpreter as before, and install the data required for the book by typing the following two commands at the Python prompt, then selecting the book collection

Once the data is downloaded to your machine, you can load some of it using the Python interpreter.

The first step is to type a special command at the Python prompt which tells the interpreter to load some texts for us to explore: 
```python
from nltk.book import *
```
## Java
JDK from Oracle
```shell
sudo add-apt-repository ppa:webupd8team/java
sudo apt update
sudo apt install default-jdk
java -version
```

### Netbeans
```shell
cd ~/Downloads
chmod +x netbeans-8.1-linux.sh
./netbeans-8.1-linux.sh
```
