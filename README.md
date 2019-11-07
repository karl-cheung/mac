# 一份前端开发工程的装机清单 - Mac

## 目录

- [科学上网](#科学上网)

- [应用程序](#应用程序)

- [编辑器](#编辑器)

- [git](#git)

- [svn](#svn)

- [nvm node npm](#nvm-node-npm)

- [rvm ruby jekyll](#rvm-ruby-jekyll)

- [pyenv python](#pyenv-python)

- [设备的一些预备操作](#设备的一些预备操作)

- [Redis Desktop Manager]

## 科学上网

### SS 代理

> 你需要拥有自己的 shadowsocks 账号。

安装 [ShadowsocksX-NG]。

### 终端过墙

- ShadowsocksX-NG 打开 PAC 或者全局模式

- 右击程序，Copy HTTP Proxy Shell Export Line

- 编辑 .bash_profile 文件粘贴剪切板

```shell
vim ~/.bash_profile

source ~/.bash_profile

curl ip.gs
```

### DNS

> 如果不使用 SS 代理，你还可以使用 DNS 方案来访问墙外一些域名。注意以下 hosts 可能失效。

#### 命令行

```shell
cd /etc && sudo chmod 777 hosts && vim hosts
```

```shell
# 添加

192.30.253.118  gist.github.com
192.30.253.119  gist.github.com
151.101.228.133 avatars0.githubusercontent.com
151.101.76.133  avatars1.githubusercontent.com
```

```shell
# 刷新 DNS

sudo dscacheutil -flushcache; sudo killall -HUP mDNSResponder;
```

```shell
# 查询

nslookup gist.github.com
```

```shell
# 恢复文件权限

sudo chmod 444 hosts
```

#### 交互式界面

安装软件 switchhosts 以切换 hosts。

## shell

### zsh 与 bash 切换

```shell
# zsh

chsh -s /bin/zsh

# bash

chsh -s /bin/bash
```

### 文件列表颜色

> 写入文件取决于使用哪种 shell

```shell
vim ~/.zshrc
```

```shell
# set color

export CLICOLOR=1
export LSCOLORS=Exfxaxdxcxegedabagacad
```

```shell
source ~/.zshrc
```

## 应用程序

### Homebrew

> 你可能需要先安装 Xcode。

```shell
# 安装
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

```shell
# 使用
brew install nginx mysql yarn gnupg gnupg2
```

> 如果你是 macOS High Sierra 用户，通过 brew 安装应用前你可能需要以下操作。

```shell
sudo mkdir /usr/local/Cellar && sudo mkdir /usr/local/opt && sudo mkdir /usr/local/include && sudo mkdir /usr/local/Frameworks && sudo mkdir /usr/local/lib
sudo chown -R $(whoami) $(brew --prefix)/*
```

```shell
# 更新

brew upgrade
```

### 使用 brew cask

```shell
brew tap phinze/homebrew-cask && brew install brew-cask
```

> 安装过程可能会中止，app 从 Homebrew 下架。

```shell
brew cask install alfred baidunetdisk charles cheatsheet dingtalk foxmail google-chrome iterm2 neteasemusic postman qq snipaste sublime-text switchhosts teamviewer typora visual-studio-code wechat wechatwebdevtools wechatwork youdaonote
```

> 你可以通过 homebrew-cask-upgrade 以获取交互式界面更新。

```shell
# 安装

brew tap buo/cask-upgrade
```

```shell
# 更新

brew cu -a
y
```

### App Store

```text
Keynote、Numbers、Pages、RAR Extractor Lite、GIF Brewery 3、OhMyStar2、Yummy FTP Pro、iCopy、Xcode
```

### 其他

> 多数需要付费使用。（非 brew cask 平台）

```text
Cornerstone、Micrisift、Office、Zoom It、Final Cut Pro、Adobe Photoshop CC、Navicat、Premium、FileZilla、Sketch
```

## 允许从任何来源下载的应用

> 在使用一些其他来源的应用程序时，你可能需要以下操作显示任何来源以启动软件。

```shell
# 显示

sudo spctl --master-disable
```

```shell
# 隐藏

sudo spctl --master-enable
```

## 编辑器

### Visual Studio Code

#### 插件列表

```text
Atom One Dark Theme、Auto Import、Bracket Pair Colorizer、Chinese (Simplified) Language、Code Runner、Color Highlight、Color Info、CSS Peek、Debugger for Chrome、File Utils、Git History、Git History Diff、Git Project Manager、GitLens — Git supercharged、HTML CSS Support、indent-rainbow、IntelliSense for CSS class names in HTML、lit-html、Live Server、markdownlint、minapp、npm、npm Intellisense、open-in-browser、Prettier - Code formatter、Quokka.js、React Native Tools、shell-format、Snippetica for Markdown、SVG Viewer、TODO Highlight、Trailing Spaces、TSLint、TypeScript Hero、Vetur、Vetur-wepy、vscode-faker、vscode-pdf、vue-beautify、XML Tools
```

#### 配置

```json
# settings.json

{
  "files.associations": {
    "*.wpy": "vue",
    "*.wxml": "html",
    "*.wxs": "javascript",
    "*.vue": "vue",
    "*.wxss": "css",
    "*.cjson": "jsonc"
  },
  "emmet.includeLanguages": {
    "wxml": "html"
  },
  "minapp-vscode.disableAutoConfig": true,
  "workbench.startupEditor": "newUntitledFile",
  "editor.formatOnSave": true,
  "vetur.format.defaultFormatter.html": "js-beautify-html",
}
```

### Atom

#### 配置同步

- 安装

```shell
apm install sync-settings
```

- 设置

Personal Access Token 与 Gist Id

- 命令选项板

shift + command + p

- 备份

sync-settings:backup

- 恢复

sync-settings:restore

> 你可能初次使用 Atom，可运行脚本文件快速安装相应插件与主题。

下载 [apm.sh]。

```shell
chmod 777 apm.sh

./apm.sh
```

## git

### ssh

> 你可能需要执行 `xcode-select --install`。

#### github 与 gitlab 共同生效

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

```shell
# 全局配置

git config --global user.name 'Zhang Yu'

git config --global user.email 'zhangyu.vin@gmail.com'
```

```shell
# 局部配置

git config user.name 'Zhang Yu'

git config user.email 'enterprise-mailbox@*'
```

## svn

### svn 命令行

```shell
mkdir /Users/vin/Public/svn && cd /Users/vin/Public/svn

svnadmin create code

cd code/conf && vim svnserve.conf
```

- 取消下列配置项注释

```text
anon-access = read
auth-access = write
password-db = passwd
authz-db = authz
```

- 添加账户与密码

```shell
vim passwd
```

```text
[users]
account=password
```

- 设置权限

```shell
vim authz
```

```text
[groups]
groups = account
@group = rw
```

- 启动

```shell
svnserve -d -r /Users/vin/Public/svn
```

- checkout

> 将服务器中 code 仓库的代码 checkout 到本地当前目录下。

```shell
svn checkout svn://localhost/code
```

- 全局忽略文件

```shell
vim ~/.subversion/config
```

- 取消 global-ignores 行注释并追加以下可选项

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

## nvm node npm

### nvm

```shell
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.11/install.sh | bash
```

```shell
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

```shell
# 设置默认版本

nvm alias default x.x.x
```

### npm

```shell
# npm 登录

npm login

vincheung

******

zhangyu.vin@gmail.com

npm whoami
```

```shell
# npm 配置

npm set init-author-name 'Zhang Yu'

npm set init-author-email 'zhangyu.vin@gmail.com'

npm set init-license 'MIT'

npm config list
```

```shell
# 使用 nrm 管理源
npm install -g nrm

nrm ls
```

```shell
# 使用 cnpm 与 tyarn

npm install -g cnpm

yarn global add tyarn
```

```shell
# 一些全局模块

npm install -g @vue/cli rollup
```

```shell
# @vue/cli

vue create my-app
```

```shell
# create-react-app

npx create-react-app my-app
```

```shell
# ant-design-pro

yarn create umi  # or npm create um

# Choose ant-design-pro

npm install

npm start
```

## rvm ruby jekyll

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

> 使用 jekyll 来生成你的静态博客。

```shell
gem install jekyll
```

## pyenv python

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

## 设备的一些预备操作

### Finder 隐藏属性的文件夹的显示与隐藏

```shell
# 显示

defaults write com.apple.finder AppleShowAllFiles -bool true; killall Finder
```

```shell
# 隐藏

defaults write com.apple.finder AppleShowAllFiles -bool false; killall Finder
```

### Charles 激活

Registered Name: `https://zhile.io`

License Key: `48891cf209c6d32bf4`

## [Redis Desktop Manager]

## License

The [MIT License].

[shadowsocksx-ng]: ./public/ShadowsocksX-NG.1.6.1.zip
[apm.sh]: ./public/apm.sh
[qt 5.9]: http://download.qt.io/official_releases/qt/5.9/5.9.6/qt-opensource-mac-x64-5.9.6.dmg
[redis desktop manager]: ./doc/RedisDesktopManager.md
[mit license]: ./LICENSE
