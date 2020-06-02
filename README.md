# Windows Terminal美化指北

[TOC]

# 1. 准备

1. 在Microsoft Store搜索Windows Terminal并安装

   ![image-20200425092605214](http://qiniupic.yaot.xyz/20200526180537.png)

2. 右键windows徽标，打开`Windows Powershell(管理员)`，输入`Set-ExecutionPolicy RemoteSigned`设置执行策略为`RemoteSigned`并输入`Get-ExecutionPolicy`进行确认：

   ![image-20200425093142836](http://qiniupic.yaot.xyz/20200526181111.png)

3. 安装[Chocolatey](https://chocolatey.org/)。这是一个windows下的包管理器，类比ubuntu的`apt`。我们需要用这个包管理器安装一些依赖程序。注意，用choco安装软件时时必须在管理员powershell下安装。以下内容来自官网教程。

   在`Windows Powershell(管理员)`下输入以下代码进行安装。注意网络要**好**。

   ```powershell
   Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))
   ```

4. 安装[VS Code](https://code.visualstudio.com/)。VSCode用来编辑相应配置文件。由于`notepad++`作者涉及一些立场问题，这里不做任何推荐。可以去官网也可以直接用`Chocolatey`安装，在`Windows Powershell(管理员)`下输入以下代码进行安装。

   ```powershell
   choco install vscode -y
   ```

5. 安装`Git`。由于有些东西github上，我们需要git进行一些操作。同时git也有利于配置开发环境。可以去官网也可以直接用`Chocolatey`安装，在`Windows Powershell(管理员)`下输入以下代码进行安装。

   ```powershell
   choco install git -y
   ```





# 2. 安装oh_my_posh

用过linux或者macos的都知道大名鼎鼎的`oh_my_zsh`，可以用来美化终端界面。实际上对powershell，也有对应的项目，那就是[oh_my_posh](https://github.com/JanDeDobbeleer/oh-my-posh)该项目已在giuhub上开源。最终效果如下图。

![image-20200425094640032](http://qiniupic.yaot.xyz/20200526181149.png)

下面是具体教程。来自项目作者。

1. 安装`ConEmu`。同样需要在管理员powershell下。

   ```powershell
   choco install ConEmu
   ```

2. 安装`posh-git`和`oh_my_posh`。

   ```powershell
   Install-Module posh-git -Scope CurrentUser
   Install-Module oh-my-posh -Scope CurrentUser
   ```

3. 激活并编辑配置文件。

   ```powershell
   if (!(Test-Path -Path $PROFILE )) { New-Item -Type File -Path $PROFILE -Force }
   notepad $PROFILE
   ```

   在打开的配置文件中粘贴以下内容并保存。

   ```
   Import-Module posh-git
   Import-Module oh-my-posh
   Set-Theme Agnoster
   ```

   ![image-20200425095748496](http://qiniupic.yaot.xyz/20200526181149.png)

4. 此时我们打开一个powershell窗口，可以看到如下效果：![image-20200425100151262](http://qiniupic.yaot.xyz/20200526181149.png)

   可以看到和成品图还差一些。

5. 问题出在哪呢？首先就是字体上的问题。`oh_my_posh`和`oh_my_zsh`一样，如果用`Agnoster`等主题，需要使用配套的[Powerline](https://github.com/powerline/fonts)字体。这个字体也已经在github上开源。以下安装教程来自项目主页。

   ```powershell
   # 下载。当然也可不用git clone，直接下载.zip文件解压也行。
   git clone https://github.com/powerline/fonts.git --depth=1
   # 安装。等待ps1脚本执行完成。
   cd fonts
   ./install.ps1
   ```

   ![image-20200425101426805](http://qiniupic.yaot.xyz/20200526181149.png)

   安装完成后右键单击powershell的窗口图标，选择属性，更换任意powerline字体即可。最终效果如下：![image-20200425102306250](http://qiniupic.yaot.xyz/20200526181149.png)





# 3. 美化Windows Terminal

有人说欸这和你头图差太多了吧？？

别急，刚才是powershell的美化，打好基础，接下来才是重头戏。

1. 打开安装好的`Windows Terminal`，选择设置，进入vscode编辑`settings.json`文件。可以看到目前terminal也还挺丑的。我们按设置文件分区一步步美化。![image-20200425103645477](http://qiniupic.yaot.xyz/20200526181315.png)![image-20200425102932640](http://qiniupic.yaot.xyz/20200526181315.png)

2. 首先是第一部分，窗口设置。位于`"profile"`前。已经有四项，我添加了三项。详细解释见图中注释

   ![image-20200425105559675](http://qiniupic.yaot.xyz/20200526181315.png)

3. 第二部分即是`"profile"`部分。这部分可设置每个shell的显示属性。分全局属性`"defaults"`和个体属性。

   1. 全局属性下，我添加了下图中的四项。

      ![image-20200425105912448](http://qiniupic.yaot.xyz/20200526181315.png)

   2. 在`"list"`中是各个shell的属性设置。此处的设置可以覆盖全局设置。我们以powershell的设置举例。

      ![image-20200425110459842](http://qiniupic.yaot.xyz/20200526181315.png)

4. 第三部分是配色方案，即`"schemes"`。可根据个人需要进行配色。

   这里我们直接采用[iTerm2-Color-Schemes](https://github.com/mbadolato/iTerm2-Color-Schemes)。这是一个适配了多个终端的配色方案，包括zsh、powershell、windows terminal以及vscode等等等等。我们下载压缩包，找到`Windows Terminal`文件夹，可以看到一堆配色方案的json文件，将其内容复制到`"schemes"`下即可。这里推荐以下主题：![image-20200425111239496](http://qiniupic.yaot.xyz/20200526181315.png)

   复制后可以根据第三步中的配色，为每一个shell指定方案。![image-20200425111349169](http://qiniupic.yaot.xyz/20200526181411.png)

5. 第五部分是快捷键设置，这部分可以依葫芦画瓢，但是具体操作的英文需要自己查询官方文档。这里提供两个：

   ![image-20200425111617856](http://qiniupic.yaot.xyz/20200526181421.png)

改完`settings.json`后保存，设置即时生效，来看一下最终结果：

![image-20200425111742827](http://qiniupic.yaot.xyz/20200526181434.png)

比以前好看多了。





# 4. 细节调整

## 关于conda环境名前的方框

没有配置anaconda或miniconda，可以跳过此部分。

注意在上图中conda环境前有个方框，根据`oh_my_posh`开发者的说明，这应该是个符号，但不知为何，中文环境下加载出错了。为了改掉，我们可以在主题文件中加入一行代码`$sl.PromptSymbols.VirtualEnvSymbol = "ENV"`，手动替换。主题文件路径和添加位置见图。

![image-20200425112324441](http://qiniupic.yaot.xyz/20200526181511.png)

保存后重开terminal，可见已经替换为`ENV`.

![image-20200425112450254](http://qiniupic.yaot.xyz/20200526181511.png)



## 关于用户名显示

对单用户来说，这个`USER@Computer`属实有点蠢。我们在`$PROFILE`中加入一行代码`$DefaultUser = '你的用户名'`解决，路径和位置见图：

![image-20200425112758495](http://qiniupic.yaot.xyz/20200526181511.png)

注意一定要换为你自己的用户名，可以去`c:/Users/`查看具体名称。

保存后重开terminal，可见已经隐藏。

![image-20200425112949501](http://qiniupic.yaot.xyz/20200526181511.png)



## 关于自定义图标

在`"profile"`的`"icon"`项目里可以自定义图标。将下载的图标放入下图中的路径，按照3.3.2中的icon配置即可。找不到AppData的勾选隐藏文件。

![image-20200425113535373](http://qiniupic.yaot.xyz/20200526181511.png)



## 使用管理员poershell

Terminal暂时不提供管理员powershell的，开发团队说是基于安全考虑。所以不建议大家开启。当然，要是想开，这里提供一个解决方法：[gsuso](https://github.com/gerardog/gsudo)。项目主页给出了scoop、chocolatey以及powershell三种安装方法。此处采用powershell。在powershell中输入如下代码执行即可。

```powershell
PowerShell -Command "Set-ExecutionPolicy RemoteSigned -scope Process; iwr -useb https://raw.githubusercontent.com/gerardog/gsudo/master/installgsudo.ps1 | iex"
```

![image-20200425113822459](http://qiniupic.yaot.xyz/20200526181511.png)

然后在terminal设置里按如下新建一个`profile`。`"guid"`项可以百度uuid生成器自行生成。配色建议和非管理员powershell区分开。

![image-20200425114143162](http://qiniupic.yaot.xyz/20200526181618.png)

保存设置文件，在terminal下拉菜单可见管理员powershell，单击打开会有关于`gsudo`的UAC提示，点击是即可。

![image-20200425114250558](http://qiniupic.yaot.xyz/20200526181629.png)

![image-20200425114352122](http://qiniupic.yaot.xyz/20200526181639.png)

注意若是管理员powershell，`oh_my_posh`前会有一个⚡标志。



## 将Terminal添加到右键菜单

平常使用时，在空白处按住shift然后右键单击，可出现下图的powershell和wsl菜单：

![image-20200425114946413](http://qiniupic.yaot.xyz/20200526181648.png)

那么怎么添加Terminal到右键菜单呢？

其实很简单，添加注册表即可。

1. 新建一个文本文件，后缀改为`reg`

   ![image-20200425115117387](http://qiniupic.yaot.xyz/20200526181658.png)

2. 用VSCode打开，输入以下代码

   ```
   Windows Registry Editor Version 5.00
   
   [HKEY_CLASSES_ROOT\Directory\Background\shell\wt]
   @="在此处打开 Terminal"
   "Extended"=""
   
   [HKEY_CLASSES_ROOT\Directory\Background\shell\wt\command]
   @="C:\\Users\\你的用户名\\AppData\\Local\\Microsoft\\WindowsApps\\wt.exe"
   ```

   想右键单击就出现的可以去掉地5行的"Extended"。

3. 注意，必须改编码为`GB 2312`，不然中文会乱码。按下述操作：![image-20200425115707119](http://qiniupic.yaot.xyz/20200526181736.png)

   ![image-20200425115849642](http://qiniupic.yaot.xyz/20200526181727.png)

4. 保存文件后，双击文件，选择是，即可导入注册表。![image-20200425115951177](http://qiniupic.yaot.xyz/20200526181751.png)

5. 编辑3.3.2中的`"profile"`，将`"startingDiractory"`改为`"."`，这样可以接受当前目录信息。

6. 试一下，可见已经成功。![image-20200425124835842](http://qiniupic.yaot.xyz/20200526185550.png)

   ![image-20200425124924943](http://qiniupic.yaot.xyz/20200526181811.png)

## 添加SSH链接

Terminal支持自定义启动命令，因此我们可以添加ssh连接，直接启动。配置图如下。注意GUID一定不能重复。![image-20200425131815646](http://qiniupic.yaot.xyz/20200526185427.png)

只需要修改`"commandline"就可以实现，加上自定义图标、主题，就完成了。效果如下：![image-20200425132025997](http://qiniupic.yaot.xyz/20200526185536.png)

![image-20200425132032204](http://qiniupic.yaot.xyz/20200526185526.png)

![image-20200425132041531](http://qiniupic.yaot.xyz/20200526185439.png)





# 5. VSCode内powershell美化

打开vscode，我们会发现其内的powershell还是很丑。这部分专门讲一下其美化，不用vscode开发的可以跳过。

1. 字体。在vscode里打开设置，搜索font。

   在`editor.fontFamily`里添加powerline字体，将`terminal.integrated.fontFamily`改为powerline字体即可。

2. 主题&配色。打开vscode的扩展商店，搜索你喜欢的配色主题。这里推荐`Atom One Light`、`Atom One Dark`以及`One Half Dark`主题。

   在设置里搜索`theme`，我的设置如下：![image-20200425130743647](http://qiniupic.yaot.xyz/20200526185639.png)

   搜索`window.autoDetectColorScheme`，勾选。这样就可以根据windows主题自动切换vscode主题。





# 6. WSL Ubuntu

这部分我打算和下期macOS终端美化一起说。点个关注呗。





# 7. windows自动切换深色模式

上面的Terminal和vscode我都设置了主题跟随系统，怎么能不设置系统自动切换呢？

使用软件[Auto Night Mode](https://github.com/Armin2208/Windows-Auto-Night-Mode)即可实现自动切换，还可更换壁纸。

![image-20200425131132688](http://qiniupic.yaot.xyz/20200526185653.png)





# 8. 下期预告

以上就是本期全部内容。下期`macOS以及Ubuntu终端美化`。想自己动手的朋友可以搜索`oh_my_zsh`，我也是根据网上的教程做的。效果如下：

![image-20200425132132235](http://qiniupic.yaot.xyz/20200526185704.png)
