(假设你已经有了Baritone [set up](SETUP.md))

# 前缀

巴里通的聊天控制前缀默认为`#`。在Impact中，你也可以使用`.b`作为前缀。(例如，`.b click`而不是`#click`)

Baritone命令默认也可以在聊天框中输入。但是如果你打错了，比如输入 "gola 10000 10000 "而不是 "goal"，就会进入公共聊天室，这很糟糕，所以建议使用`#`。

要禁用直接聊天控制（没有前缀），请关闭`chatControl`设置。要禁用带有`#`前缀的聊天控制，请关闭`prefixControl`设置。在Impact中，`.b`不能被禁用。注意不要让自己的所有控制方式都被禁用（如果你这样做了，可以通过删除`minecraft/baritone/settings.txt`文件并重新启动来重置你的设置）。

# 适用于Baritone 1.2.10+, 1.3.5+, 1.4.2+

很多命令都改变了，但是`#help`得到了很大的改进（它可以点击！命令有标签完成！哦，我的天！）。

试试`#help`，我保证它不会让你回到这里 =)

"wtf哪里是cleararea" -- 看看`#help sel`。

"wtf where is goto death, goto waypoint" -> look at `#help wp`. 

看一下`#help`就知道了。

看这个[展示视频](https://youtu.be/CZkLXWo4Fg4)!

# 命令

[教程播放列表](https://www.youtube.com/playlist?list=PLnwnJ1qsS7CoQl9Si-RTluuzCo_4Oulpa)

**所有**的这些命令可能需要在它们之前有一个前缀，如上图^。

`帮助`。

要切换一个布尔设置，只需在聊天中说出它的名字（例如，说 "allowBreak "可以切换Baritone是否会考虑断块）。对于数字设置，先说它的名字，然后说新的值（如`primaryTimeoutMS 250`）。这是不区分大小写的。要重置一个设置为其默认值，说`acceptableThrowawayItems reset`。要重置所有设置，说`reset`。要查看所有已经从默认值修改过的设置，说`modified`。

一些常见的例子。
- `thisway 1000`然后`path`向你所面对的方向走一千个街区
- `goal x y z`或`goal x z`或`goal y`，然后`path`将目标设定在某个坐标上，然后走到该坐标上。
- `goto x y z`或`goto x z`或`goto y`前往某个坐标（一步到位，立即开始）。
- `goal`将目标设定在你的球员脚下。
- 清除球门 "来清除球门。
- 取消 "或 "停止 "来停止一切行动
- `goto portal`或`goto ender_chest`或`goto block_type`去到一个块。(在Impact中，`.goto`在大多数情况下是`.b goto`的别名)
- `mine diamond_ore iron_ore`来开采钻石或铁矿（打开`legitMine`的设置，只开采它能看到的矿石。它将在y=11附近随机探索，直到找到它们）。) 也可以指定一个区块的数量，例如，`开采64个钻石_矿石`。
- `点击`在屏幕上点击你的目的地。右键单击路径到块的顶部，左键单击路径进入它（无论是在脚的水平还是在眼睛的水平），左键单击并拖动以选择一个区域（`#help sel`可以看到你可以对该选择做什么）。
- `follow player playerName`可以跟踪一个球员。跟随玩家 "跟随范围内的任何玩家（与 "杀戮光环 "结合使用，会很有趣）。跟随实体 "可以跟随任何实体。跟随实体猪 "来跟随特定类型的实体。
- `wp'代表航点。标签 "就像 "家"（在右键点击床时自动创建）或 "死亡"（在死亡时自动创建）或 "用户"（必须手动创建）。因此，你可能想`#wp save user coolbiome`，然后设置目标`#wp goal coolbiome`，然后`#path`到它的路径。对于死亡，`#wp goal death`将列出 "死亡 "标签下的航点（记住东西是可以点击的！）。
- `build`可以建立一个示意图。`build blah.schemmatic`将加载`schematics/blah.schemmatic`并建立它，原点是玩家的脚。`build blah.schemmatic x y z`来设置原点。任何一个都可以是相对于玩家的（`~ 69 ~-420`将建立在x=玩家x，y=69，z=玩家z-420）。
- `schematica`建立当前在schematica中打开的原理图。
- `tunnel`挖掘并制作一个隧道，1x2。它只有在必要时才会偏离直线，例如避开熔岩。对于一个愚蠢的隧道，实际上只是清除区域，你可以`tunnel 3 2 100`，清除一个高3、宽2、深100的区域。
- 农场 "可以自动收割、重新种植、或者骨粉作物。
- `axis`到y=120的轴或对角线上（`axisHeight`是一个可配置的设置，默认为120）。
- `explore x z`从x,z的原点探索世界。省略x和z，默认为玩家的脚。这将不断地走向离原点最近的、以前从未见过的大块。`explorefilter filter.json`和可选的invert可以用来加载一个要加载的块的列表。
- `invert`用于反转当前目标和路径。这样可以尽可能地远离它，而不是尽可能地接近它。例如，先做`goal`，然后做`invert`，以尽可能远离你在开始时的位置。
- `version`得到你正在运行的Baritone的版本。
- `damn` daniel

对于其余的命令，你可以看一下代码[这里](https://baritone.leijurv.com/baritone/api/Settings.html)。

所有的设置和文档都在<a href="https://github.com/cabaletta/baritone/blob/master/src/api/java/baritone/api/Settings.java">这里</a>。如果你觉得HTML比Javadoc更容易阅读，你可以看看<a href="https://baritone.leijurv.com/baritone/api/Settings.html#field.detail">这里</a>。

有大约一百个设置，但这里有一些有趣的/有意思的/重要的设置，你可能想在正常使用Baritone的时候改变它们。每个设置的文档都可以在上面的链接中找到。
- `允许断裂`
- `允许打印`
- `允许地点`(allowPlace)
- `允许停车`
- `允许停放地点`
- `块放置惩罚`"。
- `renderCachedChunks`"（和 "cachedChunksOpacity"） <--非常有趣，但你需要一台强大的电脑
- `躲避`"(躲避暴徒/暴徒产卵器)
- `躲避地雷`"(legitMine)
- `跟随半径`"（followRadius
- `回填`"(在你身后填上隧道)
- `构建层数`"（buildInLayers
- `建造重复的距离` "和 `建造重复的方向`。
- `世界探索块偏移量`"（worldExploringChunkOffset）。
- `可接受的丢弃物品`"。
- `避免破坏的区块`。
- `MineScanDroppedItems`（我的删除项目）。
- `允许对角线上升`"。

# 故障排除/常见问题

## 为什么巴里通对我的任何聊天命令都不回应？
这可能是许多事情中的一个。

首先，确保它确实已经安装。一个简单的检查方法是看它是否在你的Minecraft文件夹中创建了`baritone`文件夹。

第二，确保你正确使用了前缀，并且以你期望的方式启用了聊天控制。

例如，Impact禁用了直接聊天控制。(即在聊天中输入的任何东西，如果没有前缀，将被忽略并公开发送）。) **这是一个保存的设置**，所以如果您运行一次Impact，`chatControl'将从那时起关闭，**即使在其他客户端也是如此。
所以你需要使用`#`前缀或者编辑你的Minecraft文件夹中的`baritone/settings.txt`来撤销这个设置（具体来说，删除`chatControl false`一行，然后重启客户端）。


## 为什么我可以在Impact中做`.goto x z`，但在其他地方却不能？为什么我可以在KAMI中做`.path to x z`，而在其他地方却做不到？
这些是他们添加的自定义命令；这些不是来自Baritone。
你要找的对应命令是`goto x z`。
