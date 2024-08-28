# 安装

安装 Baritone 最简单的方法是安装 [Impact](https://impactclient.net/)，Impact 包含了 Baritone。

你也可以使用自定义版本的 Minecraft json，例如 [1.14.4](https://www.dropbox.com/s/rkml3hjokd3qv0m/1.14.4-Baritone.zip?dl=1) 版本、[1.15.2](https://www.dropbox.com/s/8rx6f0kts9hvd4f/1.15.2-Baritone.zip?dl=1) 版本或 [1.16.5](https://www.dropbox.com/s/i6f292o2i7o9acp/1.16.5-Baritone.zip?dl=1) 版本。

一旦安装了 Baritone，请查看 [这里](USAGE.md) 了解如何使用它。

## 预构建的官方版本
这些版本并不总是完全与最新功能同步，并且仅从 `master` 分支发布。（因此，如果你想使用 `backfill-2` 分支，你需要自己构建它）

发布页面链接：[发布](https://github.com/cabaletta/baritone/releases)

v1.2.* 是为 1.12.2 版本设计的，v1.3.* 是为 1.13.2 版本设计的，v1.4.* 是为 1.14.4 版本设计的，v1.5.* 是为 1.15.2 版本设计的，v1.6.* 是为 1.16.5 版本设计的，v1.7.* 是为 1.17.1 版本设计的，v1.8.* 是为 1.18.1 版本设计的。

任何官方版本都将由 leijurv（44A3EA646EADAC6A）使用 GPG 签名。请验证你下载的文件的哈希值是否在 `checksums.txt` 中，并且 `checksums_signed.asc` 是否是 `checksums.txt` 中公钥的有效签名。

构建是完全确定性和可重复的，你可以通过运行 `docker build --no-cache -t cabaletta/baritone .` 来验证 Travis 是否正确执行，并比较 shasum。这同样适用于 Travis、Mac 和 Linux（如果你在 Windows 上有 Docker，我很感激如果你能告诉我它是否在那里也能工作）。

## 构建物

构建 Baritone 将在 `dist` 目录中生成 5 个构建物。这些与 [发布](https://github.com/cabaletta/baritone/releases) 中创建的构建物相同。

**Forge 和 Fabric 版本可以直接添加为 Forge/Fabric 模组。**

如果你的其他 Forge 模组有 Baritone 集成，你需要 `baritone-api-forge-VERSION.jar`。否则，你需要 `baritone-standalone-forge-VERSION.jar`

- **API**：仅非 API 包被混淆。这应该用于其他模组希望使用 Baritone 功能的环境。
- **Forge/Fabric API**：与 API 相同，但为 Forge/Fabric 打包。这应该用于其他模组有 Baritone 集成的环境。
- **独立**：所有内容都被混淆。这应该用于没有其他模组希望使用 Baritone 功能的环境。
- **Forge/Fabric 独立**：与独立相同，但为 Forge/Fabric 打包。这应该用于 Baritone 是唯一的 Forge/Fabric 模组，或者你的其他 Forge/Fabric 模组没有与 Baritone 集成。
- **未优化**：没有任何内容被混淆。这永远不应该在生产环境中使用。
- **Forge/Fabric 未优化**：与未优化相同，但为 Forge/Fabric 打包。

## 自己构建
- 克隆或下载 Baritone

  ![图片](https://i.imgur.com/kbqBtoN.png)
  - 如果你选择下载，请确保你解压了 ZIP 压缩包。
- 根据你的偏好，按照以下其中一个指令集进行操作

## 命令行
在 Mac OSX 和 Linux 上，使用 `./gradlew` 而不是 `gradlew`。

如果你遇到缺少包的错误，请确保你已经设置了环境，并且使用 Oracle JDK 8（对于 1.12.2-1.16.5 版本）或 JDK 16+（对于 1.17.1 版本）或 JDK 17+（对于 1.18.1 版本）。

要检查你正在使用的 Java 版本，请运行 `java -version` 命令提示符或终端。
如果你使用的是 JDK 8 之上的 OpenJDK 8，它可能无法工作，因为 JDK 8 之上的 Java 发行版可能没有需要的 javax 类。

下载 Java：https://adoptium.net/
#### macOS 指南
为了获取 JDK 8，尝试运行以下命令：
`% /usr/libexec/java_home -V`
如果它不起作用，请尝试这个指南：https://stackoverflow.com/questions/46513639/how-to-downgrade-java-from-9-to-8-on-a-macos-eclipse-is-not-running-with-java-9

如果你在列表中看到类似

`% 1.8.0_VERSION, x86_64:	"Java SE 8"	/Library/Java/JavaVirtualMachines/jdk1.8.0_VERSION.jdk/Contents/Home`

的内容，那么你已经安装了 JDK 8。
为了在 **当前终端窗口** 中运行 JDK 8，你需要运行这个命令：

`% export JAVA_HOME=$(/usr/libexec/java_home -v 1.8)`

要将 OpenJDK 8 添加到你的 PATH，将 export 行添加到 `.zshrc / .bashrc` 的末尾，以便每次新终端都适用。如果你使用的是 bash，请更改 .bashrc；如果你使用的是 zsh，请更改 .zshrc。

### 构建 Baritone

这些任务依赖于 Minecraft 版本，但（大部分情况下）构建模组的标准步骤。

更多详情，请参见 [构建 CI 动作](/.github/workflows/gradle_build.yml)

## IntelliJ
- 将项目作为 Gradle 项目在 IntelliJ 中打开
- 刷新 Gradle 项目（或，为了安全起见，重新启动 IntelliJ）
- 根据 Minecraft 版本，你可能需要运行 `setupDecompWorkspace` 或 `genIntellijRuns` 以确保一切正常工作
