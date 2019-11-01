# 一份前端开发工程的装机清单 - Mac

## 科学上网

### 代理

> 你需要拥有自己的 shadowsocks 账号。

安装 [ShadowsocksX-NG]。

### 终端过墙

ShadowsocksX-NG 打开 PAC 或者全局模式。

右击程序，Copy HTTP Proxy Shell Export Line。

或者复制：

```shell
export http_proxy=http://127.0.0.1:1087;
export https_proxy=http://127.0.0.1:1087;
```

编辑 .zshrc 文件粘贴剪切板。

```shell
vim ~/.zshrc

source ~/.zshrc

curl ip.gs
```

### DNS

> 如果不使用代理，你还可以使用 DNS 方案来访问墙外的一些域名。注意以下 host 可能失效。

#### 命令行

```shell
cd /etc && sudo chmod 777 hosts && vim hosts
```

添加

```shell
192.30.253.118  gist.github.com
192.30.253.119  gist.github.com
151.101.228.133 avatars0.githubusercontent.com
151.101.76.133  avatars1.githubusercontent.com
```

刷新 DNS

```shell
sudo dscacheutil -flushcache; sudo killall -HUP mDNSResponder;
```

查询

```shell
nslookup gist.github.com
```

恢复

```shell
sudo chmod 444 hosts
```

#### 交互式界面

安装软件 switchhosts 以切换 host。

## 终端设置

### power-shell 切换

```shell
# zsh
chsh -s /bin/zsh

#bash
chsh -s /bin/bash
```

### 文件列表颜色

```shell
vim ~/.bash_profile
```

```shell
# set color
export CLICOLOR=1
export LSCOLORS=Exfxaxdxcxegedabagacad
```

```shell
source ~/.bash_profile
```

## 安装 Homebrew

> 你可能需要先安装 Xcode。

```shell
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

### 使用 brew

```shell
brew install nginx mysql yarn gnupg gnupg2
```

> 如果你是 macOS High Sierra 用户，通过 brew 安装应用前你可能需要以下操作。

```shell
sudo mkdir /usr/local/Cellar && sudo mkdir /usr/local/opt && sudo mkdir /usr/local/include && sudo mkdir /usr/local/Frameworks && sudo mkdir /usr/local/lib
```

```shell
sudo chown -R $(whoami) $(brew --prefix)/*
```

更新

```shell
brew upgrade
```

### 使用 brew cask

```shell
brew tap phinze/homebrew-cask && brew install brew-cask
```

> 安装过程可能会中止，app 从 Homebrew 下架。

```shell
brew cask install alfred appcleanerc baidunetdisk charles cheatsheet dingtalk evernote foxmail google-chrome iterm2 neteasemusic postman qiyimedia qq qqlive snipaste sublime-text switchhosts teamviewer typora visual-studio-code wechat wechatwebdevtools wechatwork youdaodict youku
```

> 你可以通过 homebrew-cask-upgrade 以获取交互式界面更新。

安装

```shell
brew tap buo/cask-upgrade
```

更新

```shell
brew cu -a

y
```

## App Store

```text
Keynote、Numbers、Pages、RAR Extractor Lite、GIF Brewery 3、Sakura、Core Shell、iTunes、OhMyStar2、Xcode、Yummy FTP Pro、iCopy
```

## 其他

> 多数需要付费使用。（非 brew cask 平台）

```text
Cornerstone、Micrisift、Office、Zoom It、Final Cut Pro、Adobe Photoshop CC、Navicat、Premium、FileZilla、Sketch
```

## 允许从任何来源下载的应用

> 在使用一些其他来源的应用程序时，你可能需要以下操作以启动软件时允许任何来源。

显示

```shell
sudo spctl --master-disable
```

隐藏

```shell
sudo spctl --master-enable
```

## Finder 文件夹的显示与隐藏

显示

```shell
defaults write com.apple.finder AppleShowAllFiles -bool true; killall Finder
```

隐藏

```shell
defaults write com.apple.finder AppleShowAllFiles -bool false; killall Finder
```

## svn

### svn 命令行

```shell
mkdir /Users/vin/Public/svn && cd /Users/vin/Public/svn

svnadmin create code

cd code/conf && vim svnserve.conf
```

取消下列配置项注释

```text
anon-access = read
auth-access = write
password-db = passwd
authz-db = authz
```

添加账户与密码

```shell
vim passwd
```

```text
[users]
account=password
```

设置权限

```shell
vim authz
```

```text
[groups]
groups = account
@group = rw
```

启动 svn

```shell
svnserve -d -r /Users/vin/Public/svn
```

checkout

> 将服务器中 code 仓库的代码 checkout 到本地当前目录下。

```shell
svn checkout svn://localhost/code
```

全局忽略文件

```shell
vim ~/.subversion/config
```

取消 global-ignores 行注释并追加以下可选项

```text
.DS_Store
node_modules
dist
npm-debug.log*
yarn-debug.log*
yarn-error.log*

# Editor directories and files
.idea
.vscode
*.suo
*.ntvs*
*.njsproj
*.sln
```

## git

### ssh

> 你可能需要执行 `xcode-select --install`。

新建密钥并添加到 github 与 gitlab

```shell
ssh-keygen -t rsa -C 'zhangyu.vin@gmail.com'

cat ~/.ssh/id_rsa.pub
```

```shell
ssh-keygen -t rsa -C 'enterprise-mailbox@*'

id_rsa_*

cat ~/.ssh/id_rsa_*.pub
```

```shell
vim ~/.ssh/config
```

```text
# github
  Host github.com
    HostName github.com
    PreferredAuthentications publickey
    IdentityFile ~/.ssh/id_rsa

# gitlab
  Host gitlab.*.com
    HostName gitlab.*.com
    PreferredAuthentications publickey
    IdentityFile ~/.ssh/id_rsa_*
```

```shell
ssh -T git@github.com

yes
```

```shell
ssh -T git@gitlab.*.com

yes
```

### Access token

> 如果不通过 ssh 连接，这是一个可选方案。

```shell
git clone https://<username>:<private-token>@myrepo.git
```

### 默认设置

github 项目

```shell
git config --global user.name 'Zhang Yu'

git config --global user.email 'zhangyu.vin@gmail.com'
```

gitlab 项目

```shell
git config user.name 'Zhang Yu'

git config user.email 'enterprise-mailbox@*'
```

## 编辑器

### Visual Studio Code

> 插件列表。

```text
Atom One Dark Theme、Auto Import、Bracket Pair Colorizer、Chinese (Simplified) Language、Code Runner、Color Highlight、Color Info、CSS Peek、Debugger for Chrome、File Utils、Git History、Git History Diff、Git Project Manager、GitLens — Git supercharged、HTML CSS Support、indent-rainbow、IntelliSense for CSS class names in HTML、lit-html、Live Server、markdownlint、minapp、npm、npm Intellisense、open-in-browser、Prettier - Code formatter、Quokka.js、React Native Tools、shell-format、Snippetica for Markdown、SVG Viewer、TODO Highlight、Trailing Spaces、TSLint、TypeScript Hero、Vetur、Vetur-wepy、vscode-faker、vscode-pdf、vue-beautify、XML Tools
```

### Atom

> 同步 Atom 的设置。

安装

```shell
apm install sync-settings
```

设置

Personal Access Token 与 Gist Id

命令选项板

shift + command + p

备份

sync-settings:backup

恢复

sync-settings:restore

> 你可能初次使用 Atom，可运行脚本文件快速安装相应插件与主题。

下载 [apm.sh]。

```shell
chmod 777 apm.sh

./apm.sh
```

## nvm 与 node 安装

### nvm

```shell
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.11/install.sh | bash
```

```shell
# 根据不同的 shell 更改配置文件 .zshrc | .bash_profile | .profile
vim ~/.zshrc
```

```text
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm
```

```shell
source ~/.zshrc

command -v nvm
```

### node

```shell
nvm ls-remote

nvm install x.x.x

```

### npm

npm 登录

```shell
npm login

vincheung

******

zhangyu.vin@gmail.com

npm whoami
```

npm 配置

```shell
npm set init-author-name 'Zhang Yu'

npm set init-author-email 'zhangyu.vin@gmail.com'

npm set init-license 'MIT'

npm config list
```

使用 nrm 管理源

```shell
npm install -g nrm

nrm ls
```

使用 cnpm 与 tyarn

```shell
npm install -g cnpm

yarn global add tyarn
```

## rvm、ruby 与 jekyll 安装

### rvm

> 你可能需要先安装 GnuPG。`$ brew install gnupg gnupg2`。

```shell
gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 7D2BAF1CF37B13E2069D6956105BD0E739499BDB

\curl -sSL https://get.rvm.io | bash -s stable

source /Users/vin/.rvm/scripts/rvm
```

### ruby

```shell
rvm list known

rvm install x.x.x
```

### jekyll 安装

```shell
gem install jekyll
```

## pyenv 与 python 安装

### pyenv

```shell
brew install pyenv

echo -e 'if command -v pyenv 1>/dev/null 2>&1; then\n  eval "$(pyenv init -)"\nfi' >> ~/.bash_profile

source ~/.bash_profile
```

### python

```shell
pyenv install --list

pyenv install x.x.x

pyenv global x.x.x

pyenv local x.x.x
```

## [Redis Desktop Manager 安装]

## License

The [MIT License].

[shadowsocksx-ng]: ./public/ShadowsocksX-NG.1.6.1.zip
[apm.sh]: ./public/apm.sh
[qt 5.9]: http://download.qt.io/official_releases/qt/5.9/5.9.6/qt-opensource-mac-x64-5.9.6.dmg
[redis desktop manager 安装]: ./doc/RedisDesktopManager.md
[mit license]: ./LICENSE
