# Redis Desktop Manager 安装

```shell
git clone --recursive https://github.com/uglide/RedisDesktopManager.git -b 0.9 rdm && cd ./rdm
```

1. Install XCode with Xcode build tools.

2. Install Homebrew.

3. Copy `cd ./src && cp ./resources/Info.plist.sample ./resources/Info.plist`.

4. Building RDM dependencies require i.a. openssl and cmake.Install them: `brew install openssl cmake`.

5. Build RDM dependencies `./configure`.

6. Install Qt 5.9. Add Qt Creator and under Qt 5.9.x add Qt Charts module.

7. Open ./src/rdm.pro in Qt Creator.

8. Run build.

## 补充与拓展

在 Run build 前你可能需要:

1. rdm 目录下新建 build 目录 build-rdm-redis-desktop-manager-Debug.

2. `brew install qt5`.

3. 项目 -> Manage Kits -> Qt Versions -> 添加 -> Qt 5.11.1(5.11.1) /usr/local/Cellar/qt/5.11.1/bin/qmake -> 构建套件(Kit) -> rdm -> 编译器：C: Apple Clang(x86_64) C++: Apple Clang(x86_64) -> Qt 版本: Qt 5.11.1(5.11.1)

## 安装 Qt

下载 [Qt 5.9]。

## 生成应用程序版本

1. 下载 [crashreporter]。文件放置 rdm/bin/osx/debug 目录下。

2. 编辑 rdm/src/rdm.pro 注释 `debug: CONFIG-=app_bundle`。

3. Run build 会在 rdm/bin/osx/debug 目录下得到应用程序版本 rdm 将其拖拽至 Applications。

[crashreporter]: ../public/crashreporter
