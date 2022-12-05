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

**所有** 的这些命令可能需要在它们之前有一个前缀，如上图^。

`帮助`。

要切换一个布尔设置，只需在聊天中说出它的名字（例如，说 "allowBreak "可以切换Baritone是否会考虑断块）。对于数字设置，先说它的名字，然后说新的值（如`primaryTimeoutMS 250`）。这是不区分大小写的。要重置一个设置为其默认值，说`acceptableThrowawayItems reset`。要重置所有设置，说`reset`。要查看所有已经从默认值修改过的设置，说`modified`。

Commands in Baritone:
- `thisway 1000` then `path` to go in the direction you're facing for a thousand blocks
- `goal x y z` or `goal x z` or `goal y`, then `path` to set a goal to a certain coordinate then path to it
- `goto x y z` or `goto x z` or `goto y` to go to a certain coordinate (in a single step, starts going immediately)
- `goal` to set the goal to your player's feet
- `goal clear` to clear the goal
- `cancel` or `stop` to stop everything, `forcecancel` is also an option
- `goto portal` or `goto ender_chest` or `goto block_type` to go to a block. (in Impact, `.goto` is an alias for `.b goto` for the most part)
- `mine diamond_ore iron_ore` to mine diamond ore or iron ore (turn on the setting `legitMine` to only mine ores that it can actually see. It will explore randomly around y=11 until it finds them.) An amount of blocks can also be specified, for example, `mine 64 diamond_ore`.
- `click` to click your destination on the screen. Right click path to on top of the block, left click to path into it (either at foot level or eye level), and left click and drag to select an area (`#help sel` to see what you can do with that selection).
- `follow player playerName` to follow a player. `follow players` to follow any players in range (combine with Kill Aura for a fun time). `follow entities` to follow any entities. `follow entity pig` to follow entities of a specific type.
- `wp` for waypoints. A "tag" is like "home" (created automatically on right clicking a bed) or "death" (created automatically on death) or "user" (has to be created manually). So you might want `#wp save user coolbiome`, then to set the goal `#wp goal coolbiome` then `#path` to path to it. For death, `#wp goal death` will list waypoints under the "death" tag (remember stuff is clickable!)
- `build` to build a schematic. `build blah.schematic` will load `schematics/blah.schematic` and build it with the origin being your player feet. `build blah.schematic x y z` to set the origin. Any of those can be relative to your player (`~ 69 ~-420` would build at x=player x, y=69, z=player z-420).
- `schematica` to build the schematic that is currently open in schematica
- `tunnel` to dig and make a tunnel, 1x2. It will only deviate from the straight line if necessary such as to avoid lava. For a dumber tunnel that is really just cleararea, you can `tunnel 3 2 100`, to clear an area 3 high, 2 wide, and 100 deep.
- `farm` to automatically harvest, replant, or bone meal crops. Use `farm <range>` or `farm <range> <waypoint>` to limit the max distance from the starting point or a waypoint. 
- `axis` to go to an axis or diagonal axis at y=120 (`axisHeight` is a configurable setting, defaults to 120).
- `explore x z` to explore the world from the origin of x,z. Leave out x and z to default to player feet. This will continually path towards the closest chunk to the origin that it's never seen before. `explorefilter filter.json` with optional invert can be used to load in a list of chunks to load.
- `invert` to invert the current goal and path. This gets as far away from it as possible, instead of as close as possible. For example, do `goal` then `invert` to run as far as possible from where you're standing at the start.
- `come` tells Baritone to head towards your camera, useful when freecam doesn't move your player position.
- `blacklist` will stop baritone from going to the closest block so it won't attempt to get to it.
- `eta` to get information about the estimated time until the next segment and the goal, be aware that the ETA to your goal is really unprecise.
- `proc` to view miscellaneous information about the process currently controlling Baritone.
- `repack` to re-cache the chunks around you.
- `gc` to call `System.gc()` which may free up some memory.
- `render` to fix glitched chunk rendering without having to reload all of them.
- `reloadall` to reload Baritone's world cache or `saveall` to save Baritone's world cache.
- `find` to search through Baritone's cache and attempt to find the location of the block.
- `surface` or `top` to tell Baritone to head towards the closest surface-like area, this can be the surface or highest available air space.
- `version` to get the version of Baritone you're running
- `damn` daniel

All the settings and documentation are <a href="https://github.com/cabaletta/baritone/blob/master/src/api/java/baritone/api/Settings.java">here</a>. If you find HTML easier to read than Javadoc, you can look <a href="https://baritone.leijurv.com/baritone/api/Settings.html#field.detail">here</a>.

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
