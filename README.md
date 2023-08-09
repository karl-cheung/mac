# 一份前端开发工程的装机清单 - Mac

## 目录

- [shell](#shell)
&emsp;
- [应用程序](#应用程序)
&emsp;
- [编辑器](#编辑器)
&emsp;
- [git](#git)
&emsp;
- [svn](#svn)
&emsp;
- [nvm node npm](#nvm-node-npm)
&emsp;
- [rvm ruby jekyll](#rvm-ruby-jekyll)
&emsp;
- [pyenv python](#pyenv-python)
&emsp;
- [Redis Desktop Manager]

### shell

#### zsh 与 bash 切换

##### zsh

```shell
chsh -s /bin/zsh
```

##### bash

```shell
chsh -s /bin/bash
```

#### 文件列表颜色

> 写入文件取决于使用哪种 shell

```shell
vim ~/.zshrc
```

```
export CLICOLOR=1
export LSCOLORS=Exfxaxdxcxegedabagacad
```

```shell
source ~/.zshrc
```

#### 允许从任何来源下载的应用

> 在使用一些其他来源的应用程序时，你可能需要以下操作显示任何来源以启动软件。

##### 显示

```shell
sudo spctl --master-disable
```

##### 隐藏

```shell
sudo spctl --master-enable
```

#### Finder 隐藏属性的文件夹的显示与隐藏

##### 显示

```shell
defaults write com.apple.finder AppleShowAllFiles -bool true; killall Finder
```

##### 隐藏

```shell
defaults write com.apple.finder AppleShowAllFiles -bool false; killall Finder
```

#### 修改文件权限

##### 权限 777

```shell
sudo chmod 777 file
```

##### 权限 444

```shell
sudo chmod 444 file
```

#### 查看本机 ip 信息

```shell
curl cip.cc
```

### 应用程序

#### Homebrew

> 你可能需要先安装 Xcode。

```shell
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

```shell
brew install nginx mysql yarn gnupg gnupg2
```

```shell
brew install baidunetdisk charles cheatsheet clash-for-windows cursor dingtalk forklift google-chrome hbuilderx iterm2 maczip microsoft-remote-desktop neteasemusic pdfelement postman qq qqmusic snipaste switchhosts tencent-meeting visual-studio-code wechat wechatwebdevtools wechatwork
```

> 如果你是 macOS High Sierra 用户，通过 brew 安装应用前你可能需要以下操作。

```shell
sudo mkdir /usr/local/Cellar && sudo mkdir /usr/local/opt && sudo mkdir /usr/local/include && sudo mkdir /usr/local/Frameworks && sudo mkdir /usr/local/lib
sudo chown -R $(whoami) $(brew --prefix)/*
```

#### 一些推荐的 App Store

```
# 免费
Xcode、Keynote、Numbers、Pages、GIF Brewery 3、OhMyStar2、Yummy FTP Pro、iCopy

# 付费
Cornerstone、Micrisift、Office、Zoom It、Final Cut Pro、Adobe Photoshop CC、Navicat、Premium、FileZilla、Sketch
```

### 编辑器

#### Visual Studio Code

##### [Settings Sync]

> https://code.visualstudio.com/docs/editor/settings-sync

### git

#### ssh

> 你可能需要执行 `xcode-select --install`。

##### github 与 gitlab 共同生效

```shell
ssh-keygen -t rsa -C 'you@example.com'
```

```shell
cat ~/.ssh/id_rsa.pub
```

```
github/gitlab 添加相应密钥
```

```shell
ssh-keygen -t rsa -C 'you@example.com'
```

```shell
id_rsa_*
```

```shell
cat ~/.ssh/id_rsa_*.pub
```

```shell
vim ~/.ssh/config
```

```
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

##### 连接测试
```shell
ssh -T git@github.com
yes
```

#### Access token

> 如果不通过 ssh 连接，这是一个可选方案。

```shell
git clone https://<username>:<private-token>@myrepo.git
```

#### 默认设置

##### 全局配置

```shell
git config --global user.name 'your name'
```

```shell
git config --global user.email 'you@example.com'
```

##### 局部配置

```shell
git config user.name 'your name'
```

```shell
git config user.email 'you@example.com'
```

### svn

#### svn 命令行

```shell
mkdir /Users/username/Public/svn && cd /Users/username/Public/svn
```

```shell
svnadmin create code
```

```shell
cd code/conf && vim svnserve.conf
```

```
# 取消下列配置项注释
anon-access = read
auth-access = write
password-db = passwd
authz-db = authz
```

#### 添加账户与密码

```shell
vim passwd
```

```
[users]
account=password
```

##### 设置权限

```shell
vim authz
```

```
[groups]
groups = account
@group = rw
```

##### 启动

```shell
svnserve -d -r /Users/username/Public/svn
```

##### checkout

> 将服务器中 code 仓库的代码 checkout 到本地当前目录下。

```shell
svn checkout svn://localhost/code
```

##### 全局忽略文件

```shell
vim ~/.subversion/config
```

##### 取消 global-ignores 行注释并追加以下可选项

```
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

### nvm node npm

#### nvm

```shell
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.11/install.sh | bash
```

#### node

```shell
nvm ls-remote
```

```shell
nvm install x.x.x
```

##### 设置默认版本

```shell
nvm alias default x.x.x
```

#### npm

##### npm 登录

```shell
npm login

username

******

you@example.com

npm whoami
```

##### npm 配置

```shell

npm set init-author-name 'author name'

npm set init-author-email 'you@example.com'

npm set init-license 'MIT'

npm config list
```

###### 使用 nrm 管理源

```shell

npm install -g nrm

nrm ls
```

###### 使用 cnpm 与 tyarn

```shell

npm install -g cnpm

yarn global add tyarn
```

###### 一些全局模块

```
rollup vite vue-cli create-react-app ant-design-pro taro
```

### rvm ruby jekyll

#### rvm

> 你可能需要先安装 GnuPG。`$ brew install gnupg gnupg2`。

```shell
gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 7D2BAF1CF37B13E2069D6956105BD0E739499BDB

\curl -sSL https://get.rvm.io | bash -s stable

source /Users/username/.rvm/scripts/rvm
```

#### ruby

```shell
rvm list known

rvm install x.x.x
```

#### jekyll 安装

> 使用 jekyll 来生成你的静态博客。

```shell
gem install jekyll
```

### pyenv python

#### pyenv

```shell
brew install pyenv

echo -e 'if command -v pyenv 1>/dev/null 2>&1; then\n  eval "$(pyenv init -)"\nfi' >> ~/.bash_profile

source ~/.bash_profile
```

#### python

```shell
pyenv install --list

pyenv install x.x.x

pyenv global x.x.x

pyenv local x.x.x
```

## [Redis Desktop Manager]

## License

The [MIT License].

[redis desktop manager]: ./doc/RedisDesktopManager.md
[mit license]: ./LICENSE
