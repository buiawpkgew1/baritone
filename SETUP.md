# 安装

安装Baritone最简单的方法是安装[Impact](https://impactclient.net/)，它是Baritone自带的。

You can also use a custom version json for Minecraft, with the [1.14.4](https://www.dropbox.com/s/rkml3hjokd3qv0m/1.14.4-Baritone.zip?dl=1) version or the [1.15.2](https://www.dropbox.com/s/8rx6f0kts9hvd4f/1.15.2-Baritone.zip?dl=1) version or the [1.16.5](https://www.dropbox.com/s/i6f292o2i7o9acp/1.16.5-Baritone.zip?dl=1) version.

一旦Baritone被安装，请看[这里](USAGE.md)关于如何使用它的说明。

## 预建的官方版本
这些版本并不总是完全符合最新的功能，而且只从`master`发布。(所以如果你想要`backfill-2`分支，你必须自己构建它)

链接到发布页面。[发布](https://github.com/cabaletta/baritone/releases)

v1.2.* is for 1.12.2, v1.3.* is for 1.13.2, v1.4.* is for 1.14.4, v1.5.* is for 1.15.2, v1.6.* is for 1.16.2 or 1.16.4 or 1.16.5 (LOL)

Any official release will be GPG signed by leijurv (44A3EA646EADAC6A). Please verify that the hash of the file you download is in `checksums.txt` and that `checksums_signed.asc` is a valid signature by that public keys of `checksums.txt`. 

构建是完全确定的，可重复的，你可以通过运行`docker build --no-cache -t cabaletta/baritone .`自己并比较shasum来验证Travis是否正确。这在Travis、Mac和Linux上都是一样的（如果你在Windows上有docker，如果你能让我知道它是否也能工作，我会很感激）。


## Artifacts

构建Baritone将导致在``dist``目录下创建5个工件。这些与在[release](https://github.com/cabaletta/baritone/releases)中创建的工件相同。

**Forge版本可以简单地作为Forge mod.**添加。

如果你的另一个Forge mods有一个Baritone集成，你需要`baritone-api-forge-VERSION.jar`。否则，你需要`baritone-standalon-forge-VERSION.jar`。

- **API**。只有非api包被混淆了。这应该用在其他mods想使用Baritone的功能的环境中。
- **Forge API**: 与API相同，但为Forge打包。这应该用在其他mod有Baritone集成的地方。
- **Standalone**: 一切都被混淆了。这应该用在没有其他想使用Baritone功能的mods的环境中。
- **Forge Standalone**: 与Standalone相同，但为Forge打包。当Baritone是你唯一的Forge修改器，或者你的其他Forge修改器都没有与Baritone集成时，应该使用它。
- 未经优化的**。没有任何东西是被混淆的。这不应该在生产中使用。

## Build it yourself
- Clone or download Baritone

  ![图片](https://i.imgur.com/kbqBtoN.png)
  - 如果你选择下载，请确保你解压缩ZIP档案。
- 根据你的喜好，按照下面的指令集之一进行操作

## 命令行
在Mac OSX和Linux上，使用`./gradlew`而不是`gradlew`。

如果你遇到软件包丢失的错误，请确认你已经设置了你的环境，并且使用了Oracle JDK 8。

要检查你使用的是哪种java，请执行 
`java -version`在命令提示符或终端中。
如果你使用的是OpenJDK 8以上的版本，可能无法工作，因为JDK 8以上的Java发行版可能没有所需的javax类。

Open JDK 8下载：https://openjdk.java.net/install/
#### macOS 指南
为了获得 JDK 8，请尝试运行以下命令。
`% /usr/libexec/java_home -V`。
如果不成功，请尝试以下指南： https://stackoverflow.com/questions/46513639/how-to-downgrade-java-from-9-to-8-on-a-macos-eclipse-is-not-running-with-java-9

如果你看到类似以下内容

`% 1.8.0_VERSION, x86_64: "Java SE 8" /Library/Java/JavaVirtualMachines/jdk1.8.0_VERSION.jdk/Contents/Home`。

列表中，那么你已经安装了JDK 8。
为了让 JDK 8 在 ** 当前的终端窗口中运行，你必须运行以下命令。

`% export JAVA_HOME=$（/usr/libexec/java_home -v 1.8）`。

要将OpenJDK 8添加到你的PATH中，如果你希望它适用于每一个新的终端，请在你的".zshrc / .bashrc "的末尾添加export这一行。如果你使用的是bash，请修改.bachrc，如果你使用的是zsh，请修改.zshrc。

设置环境。

```
$ gradlew setupDecompWorkspace
``$ gradlew --refresh-dependencies
```

构建Baritone。

```
$ gradlew build
```

对于minecraft 1.15.2以上版本，运行以下程序以包含Forge的jars。

```
$ gradlew build -Pbaritone.forge_build
```

运行Baritone。

```
$ gradlew runClient
```

关于如何构建baritone的信息，见[Building Baritone](#building-baritone)

## IntelliJ
- 在IntelliJ中以Gradle项目的形式打开该项目
  
  ![Image](https://i.imgur.com/jw7Q6vY.png)

- 运行Gradle任务`setupDecompWorkspace`和`genIntellijRuns`。
  
  ![Image](https://i.imgur.com/QEfVvWP.png)

- 刷新Gradle项目（或者，安全起见，直接重启IntelliJ）。
  
  ![Image](https://i.imgur.com/3V7EdWr.png)

- 选择 "Minecraft客户端 "的启动配置
  
  ![Image](https://i.imgur.com/1qz2QGV.png)

- 在同一下拉菜单中点击``编辑配置...``，并选择 "Minecraft客户端 "配置
  
  ![Image](https://i.imgur.com/s4ly0ZF.png)

- 在`编辑配置...`中，你需要选择`baritone_launch`作为`使用模块的classpath：`。
  
  ![Image](https://i.imgur.com/hrLhG9u.png)

## IntelliJ

- 在右边的标签上导航到gradle任务，如下所示

  ![Image](https://i.imgur.com/PE6r9iN.png)

- 双击**build**来运行它
