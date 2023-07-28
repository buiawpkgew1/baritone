# 安装

安装Baritone最简单的方法是安装[Impact](https://impactclient.net/)，它是Baritone自带的。

You can also use a custom version json for Minecraft, with the [1.14.4](https://www.dropbox.com/s/rkml3hjokd3qv0m/1.14.4-Baritone.zip?dl=1) version or the [1.15.2](https://www.dropbox.com/s/8rx6f0kts9hvd4f/1.15.2-Baritone.zip?dl=1) version or the [1.16.5](https://www.dropbox.com/s/i6f292o2i7o9acp/1.16.5-Baritone.zip?dl=1) version.

一旦Baritone被安装，请看[这里](USAGE.md)关于如何使用它的说明。

## 预建的官方版本
这些版本并不总是完全符合最新的功能，而且只从`master`发布。(所以如果你想要`backfill-2`分支，你必须自己构建它)

链接到发布页面。[发布](https://github.com/cabaletta/baritone/releases)

v1.2.* is for 1.12.2, v1.3.* is for 1.13.2, v1.4.* is for 1.14.4, v1.5.* is for 1.15.2, v1.6.* is for 1.16.5, v1.7.* is for 1.17.1, v1.8.* is for 1.18.1

Any official release will be GPG signed by leijurv (44A3EA646EADAC6A). Please verify that the hash of the file you download is in `checksums.txt` and that `checksums_signed.asc` is a valid signature by that public keys of `checksums.txt`. 

构建是完全确定的，可重复的，你可以通过运行`docker build --no-cache -t cabaletta/baritone .`自己并比较shasum来验证Travis是否正确。这在Travis、Mac和Linux上都是一样的（如果你在Windows上有docker，如果你能让我知道它是否也能工作，我会很感激）。


## Artifacts

构建Baritone将导致在``dist``目录下创建5个工件。这些与在[release](https://github.com/cabaletta/baritone/releases)中创建的工件相同。

**The Forge and Fabric releases can simply be added as a Forge/Fabric mods.**

如果你的另一个Forge mods有一个Baritone集成，你需要`baritone-api-forge-VERSION.jar`。否则，你需要`baritone-standalon-forge-VERSION.jar`。

- **API**: Only the non-api packages are obfuscated. This should be used in environments where other mods would like to use Baritone's features.
- **Forge/Fabric API**: Same as API, but packaged for Forge/Fabric. This should be used where another mod has a Baritone integration.
- **Standalone**: Everything is obfuscated. This should be used in environments where there are no other mods present that would like to use Baritone's features.
- **Forge/Fabric Standalone**: Same as Standalone, but packaged for Forge/Fabric. This should be used when Baritone is your only Forge/Fabric mod, or none of your other Forge/Fabric mods integrate with Baritone.
- **Unoptimized**: Nothing is obfuscated. This shouldn't be used ever in production.
- **Forge/Fabric Unoptimized**: Same as Unoptimized, but packaged for Forge/Fabric.

## Build it yourself
- Clone or download Baritone

  ![图片](https://i.imgur.com/kbqBtoN.png)
  - 如果你选择下载，请确保你解压缩ZIP档案。
- 根据你的喜好，按照下面的指令集之一进行操作

## 命令行
在Mac OSX和Linux上，使用`./gradlew`而不是`gradlew`。

If you have errors with a package missing please make sure you have setup your environment, and are using Oracle JDK 8 for 1.12.2-1.16.5, JDK 16+ for 1.17.1, and JDK 17+ for 1.18.1.

To check which java you are using do 
`java -version` in a command prompt or terminal.
If you are using anything above OpenJDK 8 for 1.12.2-1.16.5, it might not work because the Java distributions above JDK 8 using may not have the needed javax classes.

Download java: https://adoptium.net/
#### macOS guide
In order to get JDK 8, Try running the following command:
`% /usr/libexec/java_home -V`
If it doesn't work try this guide: https://stackoverflow.com/questions/46513639/how-to-downgrade-java-from-9-to-8-on-a-macos-eclipse-is-not-running-with-java-9

如果你看到类似以下内容

`% 1.8.0_VERSION, x86_64:	"Java SE 8"	/Library/Java/JavaVirtualMachines/jdk1.8.0_VERSION.jdk/Contents/Home`

列表中，那么你已经安装了JDK 8。
为了让 JDK 8 在 ** 当前的终端窗口中运行，你必须运行以下命令。

`% export JAVA_HOME=$（/usr/libexec/java_home -v 1.8）`。

要将OpenJDK 8添加到你的PATH中，如果你希望它适用于每一个新的终端，请在你的".zshrc / .bashrc "的末尾添加export这一行。如果你使用的是bash，请修改.bachrc，如果你使用的是zsh，请修改.zshrc。

### Building Baritone

These tasks depend on the minecraft version, but are (for the most part) standard for building mods.

for more details, see [the build ci action](/.github/workflows/gradle_build.yml)

## IntelliJ
- Open the project in IntelliJ as a Gradle project
- Refresh the Gradle project (or, to be safe, just restart IntelliJ)
- depending on the minecraft version, you may need to run `setupDecompWorkspace` or `genIntellijRuns` in order to get everything working