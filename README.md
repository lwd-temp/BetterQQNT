# LiteLoaderQQNT

LiteLoaderQQNT 是 QQNT 的插件加载器，  
一般在 QQNT 的环境内简称为 LiteLoader。  
它可以让你自由地为 QQNT 添加各种插件，  
并实现例如美化主题、增加功能等各种功能。

Telegram 闲聊群：https://t.me/LiteLoaderQQNT


## 注意事项

> 本项目仅为个人兴趣而制作，开发目的在于学习和探索，一切开发皆在学习，请勿用于非法用途。  
> 因使用本项目产生的一切问题与后果由使用者自行承担，项目开发者不承担任何责任。

- 目前仍在开发当中，可能会存在一些问题和不足。
- 仅为个人兴趣而制作，开发目的在于学习和探索。
- 能力有限，随缘更新。不过也欢迎各位来提交PR。
- 由于项目特殊性，必要时会停止开发或删除仓库。


## 插件开发

如需上架插件市场，请参考最新的插件模板，也建议参考其他插件。  
需要打包的插件请在仓库发布 Release，文件尽量使用 Github Actions 打包。  
插件模板：[LiteLoaderQQNT-Plugin-Template](https://github.com/mo-jinran/LiteLoaderQQNT-Plugin-Template)  
插件仓库：[LiteLoaderQQNT-Plugin-List](https://github.com/mo-jinran/LiteLoaderQQNT-Plugin-List)

> Windows QQNT 9.8.5 版本及以上暂时无法打开自身的 DevTools，请安装 Chii Devtools 插件（推荐）或 QQNT vConsole 插件进行调试。


## 安装方法

由于 `package.json` 在 Windows 版 QQNT 9.9.1 还有 Mac 版 QQNT 6.9.18 被添加了完整性校验，除去 Windows 版 9.9.1-15717 外，下方对于不含完整性验证的 QQNT 版本的安装方法可能不适用，提示文件损坏。对于新版 Windows QQNT 安装 LiteLoader 可按照最下方的[针对 Windows 版 QQNT 9.9.1 及以上版本的安装方法](#针对-windows-版-qqnt-991-及以上版本的安装方法)。MacOS 目前只能通过安装老版本 QQNT 来解决，不过目前 [App Store 版 QQ](itms-apps://itunes.apple.com/app/id451108668) 仍然不含完整性校验。  
安装时请**不要修改** LiteLoader 文件夹内的 `package.json`。可能需要修改的 `package.json` 仅为 LiteLoader 上一级目录处的（即 `QQNT安装目录/resources/app/package.json`）。  
安装 LiteLoaderQQNT 之前，确保你安装好了基于 QQNT 架构的 QQ。安装分为从 Releases 中下载稳定版（推荐）和通过 git clone 安装。


### 安装位置

正常情况下，需要将含有 LiteLoaderQQNT 本体的文件夹放到 `QQNT安装目录/resources/app` 下。  
对于不同系统，默认情况下此位置位置可能为：

- Windows: `C:\Program Files\Tencent\QQNT\resources\app`
- Linux: `/opt/QQ/resources/app`
- MacOS: `/Applications/QQ.app/Contents/Resources/app`

安装完成后的目录结构应类似于这样：

```
├─app_launcher
├─LiteLoader    <- 含有 LiteLoader 本体的文件夹
│  ├─builtins
│  ├─src
│  ├─package.json
│  └─...
├─package.json  <- 需要修改的 package.json
└─...
```

需要修改的 `package.json` 的示例：

```
{
    ...
    "homepage": "https://im.qq.com",
    "sideEffects": true,
    "main": "LiteLoader",   <- 修改这里（只需要指向文件夹即可）
    ...
}
```


### 从 Releases 中下载稳定版的方式进行安装（对于不含完整性验证的 QQNT）（推荐）

1. 从 Releases 中下载最新的 `LiteLoaderQQNT.zip`。
2. 解压 `LiteLoaderQQNT.zip` 的 `LiteLoader` 文件夹到上方提到的安装位置。
3. 修改 `LiteLoader` 文件夹上一级处的 `package.json`，将其中的 `"main": "/app_launcher/index.js"` 那一行改为 `"main": "LiteLoader"`，这里的 `"LiteLoader"` 即为解压出来的文件夹的名字。
4. 至此，安装完成。


### 使用 git clone 的方式安装（对于不含完整性验证的 QQNT）（不推荐，适合高阶用户）

1. 确保你的系统装有 [Git](https://git-scm.com/downloads)。
2. 在终端中打开上文提到的 LiteLoaderQQNT 需要安装到的位置。
3. 终端中用 `git clone https://github.com/mo-jinran/LiteLoaderQQNT.git` 拉取仓库到 `LiteLoaderQQNT` 文件夹下，读写时可能需要 root 权限或管理员权限运行。
4. 用 `cd LiteLoaderQQNT && git submodule update --init --recursive` 拉取子模块。读写时可能需要 root 权限或管理员权限运行。
5. 将 `LiteLoaderQQNT` 文件夹上一级处的 `package.json` 中 `"main"` 键对应的值修改到 `"LiteLoaderQQNT"`，这里的键值即为解压出来的文件夹名称。
6. 至此，安装完成。


### 针对 Windows 版 QQNT 9.9.1 及以上版本的安装方法

在新版 QQNT 中，对于 `package.json` 的完整性验证被加上了。因此对于新版 QQNT，只能通过其他方案加载 LiteLoaderQQNT。  
下面的安装方法为使用 Release 下载 `LiteLoaderQQNT.zip` 的方式安装，如需使用 git clone 方式安装可能需要额外重命名 clone 下来的文件夹到 `LiteLoader`。  
如果 Launcher 或 Patch 运行失败无反应请尝试使用管理员权限运行重试

#### 使用 Launcher （推荐，闭源）：

1. 前往 releases 中下载最新的 `LiteLoaderQQNT.zip` 以及额外的 Launcher（`LiteLoaderQQNT-Launcher_x64.exe` 或 `LiteLoaderQQNT-Launcher_x86.exe`），Launcher 可以只用x86版本。
2. 将额外下载的 Launcher 移动到 QQNT 安装目录下 QQ.exe 同级目录（未修改安装位置情况下默认在 `C:\Program Files\Tencent\QQNT`）。
3. 解压 `LiteLoaderQQNT.zip` 的 `LiteLoader` 文件夹到上方提到的安装位置，并且此文件夹只能够名为 `LiteLoader`。
4. 至此，安装完成。但是为了加载 LiteLoaderQQNT，运行 QQ 的时候需要运行 QQ 对应目录下的 Launcher。为了方便使用，可以修改快捷方式指向或者修改注册表配置映像劫持。


#### 使用 Patch （不推荐，开源）：

1. 前往 releases 中下载最新的 `LiteLoaderQQNT.zip`。
2. 解压 `LiteLoaderQQNT.zip` 的 `LiteLoader` 文件夹到上方提到的安装位置。
3. 使用管理员权限运行解压出来的 LiteLoader 目录下 patch 目录内的脚本，并等待修补完成。一些用户运行 ps1 脚本可能会出现报错，可以根据 patch 目录内的脚本手动修改。
4. 修改 `LiteLoader` 文件夹上一级处的`package.json`，将其中的 `"main": "/app_launcher/index.js"` 那一行改为`"main": "LiteLoader"`，这里的 `"LiteLoader"` 即为解压出来的文件夹的名字。
5. 至此，安装完成，并且去除完整性验证的 Patch 将永久生效。


## 数据目录

LiteLoaderQQNT 的默认数据文件夹在 `用户目录/Documents/LiteLoaderQQNT`，修改环境变量 `LITELOADERQQNT_PROFILE` 可指定目录位置。

数据目录结构：

```
LiteLoaderQQNT
    ├─plugins           <- 插件本体目录
    │   ├─my-plugin     <- 插件本体
    │   └─...
    ├─plugins_cache     <- 插件缓存目录
    │   ├─my-plugin
    │   └─...
    ├─plugins_data      <- 插件数据目录
    │   ├─my-plugin
    │   └─...
    └─config.json       <- LiteLoader配置文件
```


## 开源协议

```
MIT License

Copyright (c) 2023 沫烬染

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```
