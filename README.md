# 我的世界Java版服务器启动批处理(命令提示符脚本)
**警告:该批处理仅适用于Windows平台!不适用于Linux、Unix、MacOS等平台!**

## 项目仓库(存储库)与项目文件下载

若访问缓慢,可尝试前往以下站点的项目仓库查看/下载项目文件:

  - GitHub: [GitHub项目地址](https://github.com/anjisuan608/Minecraft-Java-Edition-Server-Launcher) [GitHub仓库下载](https://github.com/anjisuan608/Minecraft-Java-Edition-Server-Launcher/releases/)
  - GitCode: [GitCode项目地址](https://gitcode.com/anjisuan608/Minecraft-Java-Edition-Server-Launcher) [GitCode仓库下载](https://gitcode.com/anjisuan608/Minecraft-Java-Edition-Server-Launcher/releases/)
  - Gitee: [Gitee项目地址](https://gitee.com/anjisuan608/Minecraft-Java-Edition-Server-Launcher) [Gitee仓库下载](https://gitee.com/anjisuan608/Minecraft-Java-Edition-Server-Launcher/releases/)
  - AtomGit: [AtomGit项目地址](https://atomgit.com/anjisuan608/Minecraft-Java-Edition-Server-Launcher) [AtomGit仓库下载](https://atomgit.com/anjisuan608/Minecraft-Java-Edition-Server-Launcher/tags?tab=release)
  - GitLab:(停止维护)
  - JiHuLab:(暂无)


## 核心列表

[跳转至核心列表](#%E6%94%AF%E6%8C%81%E7%9A%84%E6%9C%8D%E5%8A%A1%E5%99%A8%E6%A0%B8%E5%BF%83)

## 跨平台支持(实验性)

[PowerShell](https://learn.microsoft.com/zh-cn/powershell/scripting/install/installing-powershell-on-windows)版暂缓开发  
[点击跳转](#第三方Python版本实验性)至第三方Python版本说明  

## 若查看或编辑批处理文件时出现乱码,请使用"GB 2312"或"GBK"编码打开文件!

## 批处理功能
### 第三方认证服务器
批处理添加了对于authlib-injector的支持，允许用户使用 **[LittleSkin](https://littleskin.cn/)** 、 **[MUA(Minecraft高校联盟)](https://skin.mualliance.ltd/)** 作为认证服务器，参考 [LittleSkin帮助文档](https://manual.littlesk.in/yggdrasil/authlib-injector)，同时允许添加自定义的认证服务器  
集成了authlib-injector的下载，支持了 [官方下载源](https://authlib-injector.yushi.moe/) 和 [BMCLAPI](https://bmclapi2.bangbang93.com/mirrors/authlib-injector/) (实验性功能)  
这 **不是强制** 启用的，可以在启动时停用，或在服务器停止后的菜单中停用该功能  
*需要注意的是，服务器配置文件 `server.properties` 的 **online-mode** 必须处于 **true***  
*若online-mode处于false则为离线模式，则认证不生效*  


### 自动重启(无人值守)
批处理添加了对于无人值守的支持，允许用户在启用自动重启功能后实现当服务器停止运行后自动重启，直到批处理关闭  
若中途不想继续使用自动重启功能，也可以在服务器停止后的菜单中关闭自动重启功能  


### eula文件生成/同意
批处理添加了对于服务器目录下的eula.txt文件检测  
用于检测当前服务器许可协议状态  
若不存在许可协议，则会指引用户确认是否通过批处理创建并同意  
若许可协议存在，但处于false状态会引导用户确认是否通过批处理写入true  


### server.properties文件online-mode相关检测
在启用第三方认证时，将会检测online-mode状态

  1. 如果online-mode不存在，则添加online-mode=true
  2. 如果online-mode=false，则修改online-mode=true
  3. 如果online-mode后面没有值，则将online-mode设置为true



### 服务器GUI窗口显示/隐藏(仅部分核心可用)
可以通过批处理实现控制部分服务器核心的GUI是否显示  


## 变量说明
### Java环境配置
#### %JVM%
`%JVM%`用于指定Java路径，默认配置的是"`java`"，该值会根据系统的环境变量调用Java  
若要指定请在 **`set "JVM="`** 等号后面输入Java安装路径，一直写到 `.\bin\java.exe`  
此处也支持系统环境变量，如: **`%ProgramFiles%`**  


### 服务器核心配置
#### %ServerJar%
`%ServerJar%`变量用于指定服务器核心(`jar`)文件路径，当前批处理中的是一个例子，请替换成你所使用的核心文件名， **以 `.jar` 结尾**  
如果没有特殊需求建议将服务器核心(`jar`)文件与该批处理放在相同目录下  


#### %ServerTXT%
`%ServerTXT%`用于解决部分Forge、NeoForge核心的启动问题  
部分Forge、NeoForge核心使用安装时生成的批处理文件,指向一个记录参数的txt文件启动服务器  
当前批处理中的是一个例子，请替换成你所使用的引导核心txt文件路径  
请在安装目录中找到Forge、NeoForge服务器安装器生成的 **"`run.bat`"** 文件,右键-->编辑  
找到当中的 **"`java @user_jvm_args.txt @libraries/net/xxxforge/xxxforge/x.x.x-xx.xx.xx/win_args.txt %*`"** 语句  
复制当中的 **"`@libraries/net/xxxforge/xxxforge/x.x.x-xx.xx.xx/win_args.txt`"** 字段  
粘贴到下方ServerTXT变量的等号后面  
**注:请务必看清文件扩展(后缀)名!当中的 `run.sh` 文件适用于 **Linux** 平台,请勿复制该文件的字段!**  
*开启文件扩展名显示 :文件夹选项 -->查看 ,在下方的选项框中找到 "隐藏已知文件类型的扩展名 "取消勾选 ,应用并确定*  
**注:当 `%ServerJar%` 变量有内容时, `%ServerTXT%` 变量不生效**  


### 内存设置
注:此处换算为:`1024K`=`1M`;`1024M`=`1G`;`1024G`=`1T`  


#### %Xmx%
用于指定最大可用内存， **在变量等号后键入数字,单位 `MB`**  


#### %Xms%
<p>用于指定最小内存用量，<strong>在变量等号后键入数字,单位<em>MB</em></strong></p>


### GUI模式(仅部分核心可用)
<p>变量%gui%用于控制服务器的GUI显示和隐藏</p>
<p>默认情况下这个变量是空的<em>(即显示服务器GUI[如果支持])</em></p>
<p>若设置变量为"nogui"则为始终不显示服务器GUI</p>


## 支持的服务器核心
### Vanilla
<p>原版服务器核心</p>
<p><a href="https://www.minecraft.net/zh-hans/download/server" title="Vanilla">Minecraft官网</a></p>


### LeavesMC
<p>LeavesMC 改善了 Minecraft 的生态系统，提供快速、安全和稳定的软件，作为最特立独行的组织提供快速迭代和健康支持。</p>
<p><a href="https://leavesmc.org/" title="LeavesMC">LeavesMC官网</a></p>
<p><a href="https://leavesmc.org/downloads/leaves" title="Leaves">Leaves 下载</a></p>
<p><a href="https://leavesmc.org/software/lumina" title="Lumina">Lumina 简介</a></p>


### PaperMC
<p>PaperMC 通过快速、安全的软件和不断扩展的插件 API 改进了 Minecraft 的生态系统，作为使用最广泛、性能最强和最稳定的软件，提供快速发布和有用的支持。</p>
<p><a href="https://papermc.io/" title="PaperMC">PaperMC核心官网</a></p>
<p><a href="https://papermc.io/downloads/paper" title="Paper">Paper 下载</a></p>
<p><a href="https://papermc.io/software/folia" title="Folia">Folia 简介</a></p>


### Leaf
<p>一个 Paper 分支, 专注于寻找性能优化, Vanilla, 稳定之间的平衡, 为大型网络, 密集和高承载量场景设计</p>
<p>注: Leaf 包含所有 Purpur 的补丁[来自<a href="https://www.leafmc.one/zh/docs/faq#%E2%9D%93-%C2%B7-leaf-%E6%98%AF%E5%90%A6%E5%8C%85%E6%8B%AC-purpur-yml" title="docs">Leaf-docs:常见问题与解答</a>]</p>
<p><a href="https://www.leafmc.one/zh/" title="Leaf">Leaf核心官网</a></p>
<p><a href="https://www.leafmc.one/zh/download" title="Leaf">Leaf 下载</a></p>


### Purpur
<p>Purpur 是基于 Paper 的 Minecraft 服务器软件。它支持为 Bukkit、Spigot 和 Paper API 设计的插件。Purpur 专注于提供尽可能多的可配置性，以允许服务器所有者根据自己的喜好自定义他们的服务器。</p>
<p><a href="https://purpurmc.org/" title="Purpur">Purpur核心官网</a></p>
<p><a href="https://purpurmc.org/download/purpur" title="Purpur">Purpur 下载</a></p>


### Sponge
<p><a href="https://spongepowered.org/downloads/" title="海绵端官网下载站">海绵端官网(汇总)下载站</a></p>
<p><a href="https://spongepowered.org/downloads/spongevanilla" title="海绵香草">海绵原版(香草)(SpongeVanilla)端官网-下载站</a></p>
<p><a href="https://spongepowered.org/downloads/spongeneo" title="海绵新">海绵新(SpongeNeo)端官网-下载站</a></p>
<p><a href="https://spongepowered.org/downloads/spongeforge" title="海绵锻造">海绵锻造(SpongeForge)端官网-下载站</a></p>


### ArcLight
<p>使用 Mixin 在模组环境中实现 Bukkit 服务器</p>
<p><a href="https://github.com/IzzelAliz/Arclight" title="ArcLight">ArcLight 核心GitHub仓库</a></p>
<p><a href="https://arclight.izzel.io/" title="ArcLight">ArcLight 核心构建站(下载站)</a></p>
<p>注:部分版本的服务器核心(jar)文件部署后存放于libraries文件夹下的版本请参考批处理注释完成配置</p>


### Bukkit
<p><a href="https://getbukkit.org/download/craftbukkit" title="CraftBukkit">CraftBukkit 官网-下载站</a></p>
<p><a href="https://getbukkit.org/download/spigot/" title="Spigot">Spigot 官网-下载站</a></p>


### CatServer
<p>高性能和高兼容性的1.12.2/1.16.5/1.18.2版本Forge+Bukkit+Spigot 服务端</p>
<p><a href="https://catmc.org/" title="CatServer">CatServer 核心官网</a></p>


### Fabric
<p>Fabric 官方服务器核心</p>
<p><a href="https://fabricmc.net/" title="Fabric">Fabric 官网</a></p>
<p><a href="https://fabricmc.net/use/installer/" title="Fabric Server">Fabric 下载</a></p>


### Quilt
<p>Quilt 官方服务器核心</p>
<p><a href="https://quiltmc.org/install/" title="Quilt Server">Quilt 官网</a></p>
<p><a href="https://quiltmc.org/install/server/" title="Quilt Server">Quilt 下载</a></p>


### NeoForge
<p>NeoForge 官方服务器核心</p>
<p><a href="https://projects.neoforged.net/neoforged/neoforge" title="NeoForge">NeoForge 官网-下载站</a></p>
<p>注:该核心的jar文件部署后存放于libraries文件夹下，请参考批处理注释完成配置</p>


### Forge
<p>Forge 官方服务器核心</p>
<p><a href="https://files.minecraftforge.net/" title="Forge">Forge 官网-下载站</a></p>
<p>注:部分版本的服务器核心(jar)文件部署后存放于libraries文件夹下的版本请参考批处理注释完成配置</p>


### Mohist
<p><a href="https://mohistmc.com/" title="Mohist">Mohist官网</a></p>
<p>注:部分版本的服务器核心(jar)文件部署后存放于libraries文件夹下的版本请参考批处理注释完成配置</p>
<p>警告:尚未测试该核心与启动批处理的可用性与兼容性，建议移步本项目的<a href="#%E7%AC%AC%E4%B8%89%E6%96%B9python%E7%89%88%E6%9C%AC%E5%AE%9E%E9%AA%8C%E6%80%A7" title="第三方Python版本">第三方Python版本</a>以获得支持，开发者已完成对Mohist核心及其Fabric/NeoForge版本的启动测试!</p>


## 代理服务器
### Velocity
<p>Velocity 是一款现代、高性能的代理服务器。它以性能和稳定性为核心设计理念，是 Waterfall 的完整替代方案，并拥有自己的插件生态系统。</p>
<p><a href="https://papermc.io/downloads/velocity" title="Velocity">Velocity 下载</a></p>


### Waterfall
<p><strong>Waterfall 已达到生命周期终点！它不再接受维护或支持。</strong><em>[来自<a href="https://papermc.io/software/waterfall" title="Waterfall - Software">官网</a>]</em></p>
<p>Waterfall 是 BungeeCord 的分支，旨在改进性能和稳定性。</p>
<p><a href="https://papermc.io/downloads/waterfall" title="Waterfall">Waterfall 下载</a>


### BungeeCord
<p>BungeeCord 是由 SpigotMC 团队内部编写的软件。它充当玩家客户端和连接的 Minecraft 服务器之间的代理。</p>
<p><a href="https://ci.md-5.net/job/BungeeCord/" title="BungeeCord - Jenkins">BungeeCord 下载</a></p>



## 第三方Python版本(实验性)

<p>第三方Python版——由<a href="https://space.bilibili.com/34270103" title="Stever-java"> @Steverjava </a>开发</p>
<p>注: 第三方版本与该项目无关,请勿套用该项目相关条款处理第三方版本!</p>

  <li>GitHub: <a href="https://github.com/Steverjava/" title="Steverjava's GitHub user profile">开发者主页</a> <a href="https://github.com/Steverjava/Minecraft-Server-Launcher" title="Steverjava's GitHub Project profile">项目仓库</a></li>
  <li>Gitee: <a href="https://gitee.com/Steverjava/" title="Steverjava's Gitee user profile">开发者主页</a> <a href="https://gitee.com/Steverjava/Minecraft-Server-Launcher" title="Steverjava's Gitee Project profile">项目仓库</a></li>
  <li>GitCode: <a href="https://gitcode.com/Steverjava/" title="Steverjava's GitCode user profile">开发者主页</a> <a href="https://gitcode.com/Steverjava/Minecraft-Server-Launcher" title="Steverjava's GitCode Project profile">项目仓库</a></li>
  <li>AtomGit: <a href="https://atomgit.com/Steverjava/" title="Steverjava's AtomGit user profile">开发者主页</a> <a href="https://atomgit.com/Steverjava/Minecraft-Server-Launcher" title="Steverjava's AtomGit Project profile">项目仓库</a></li>





