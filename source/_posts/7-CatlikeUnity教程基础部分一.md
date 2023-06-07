---
title: "[译]Unity基础教程：(一)创建一个时钟"
date: 2022-06-15 10:46:42
link: catlike-base-building-a-clock
tags: unity-base
categories: Catlike Coding Unity Tutorial
---

> 使用简单的对象构建一个时钟。
> 
> 写一个C#脚本。
> 
> 转动时钟的指针以显示时间。
> 
> 对钟臂进行动画处理。

这是关于学习使用Unity基础知识的系列教程中的第一个教程。在本教程中，我们将创建一个简单的时钟，并对脚本组件进行编程，让它显示当前时间。你不需要有任何使用Unity编辑器的经验，但需要你有一些使用多窗口编辑器应用程序的经验。

在我所有教程的底部，你可以找到教程许可证的链接，包含完成的教程项目的资源库，以及教程页面的PDF版本。

本教程是用Unity 2020.3.6f1制作的。

![这是时钟的最终效果](https://static.huozk.cn/20220814-4585c7a8fa39ec03fbfc78ffaccc5b41555bc348a1e5f61f605b11e12c84ccca.jpg)

# Creating a Project

在开始使用Unity编辑器之前，我们必须首先创建一个项目。

## 1.1 新项目

当你打开Unity时，你会看到Unity Hub。这是一个启动器和安装程序，在这里你可以创建或打开项目，以及安装管理Unity版本，并做一些其他事情。如果你没有安装Unity2020.3或更高版本，现在就请添加它吧。

<details>
	<summary>哪些Unity版本是合适的？</summary>
	<p>Unity每年会发布很多个新版本。其中有两个平行版本发布时间表。最稳定和安全的是LTS版本。LTS代表长期支持，在Unity说明下是支持两年。</p>
	<p>我的教程坚持使用LTS版本，其中2020.3是最新版本。本教程特别使用2020.3.6。版本号的第三部分表示补丁版本。补丁版本包含错误修复，很少有新功能。另一个f1后缀表示官方最终版本。任何2020.3版本都可以用于本教程。</p>
</details>

最高的Unity版本，如2021.1 通常属于开发分支，它很可能引入了新的功能，也可能删除了旧的功能。这些版本并不像LTS版本那样可靠，每个版本仅有几个月的支持时间。

偶尔教程中包含一些提问回答环节，~~它们被包装在灰色的格子里，就像上面那样。在页面中，答案默认是隐藏的。可以通过点击问题来打开关闭。~~（注：译文中使用引用格式处理！）

当我们创建一个新项目时，可以选择它的Unity版本和初始化模板。我们将使用标准的3D模板。一旦它被创建，它就会被添加到项目列表中，并在Unity编辑器的选定版本中被打开。

<details>
	<summary>我可以用不同的渲染管线来创建一个项目吗？</summary>
	<p>可以，唯一的区别是，项目的默认场景中会有更多的东西，你的材质看起来也会不同。你的项目也会包含相应的包。</p>
</details>

## 1.2 编辑界面布局

如果你还没有设置编辑器布局，最终将使用默认的窗口布局。

![默认的编辑器布局。](https://static.huozk.cn/20220814-32bf9f548c61a327ae415929fa14c15bc12eea0f61fe28f4ca68d8a0db25d3c7.jpg)  

默认布局包含了我们需要的所有窗口，但可以按照你自的意思，通过重新排布和分组窗口来设置。也可以打开和关闭某些窗口，比如资源商店(Asset Store)的窗口。每个窗口都有自己的配置选项，可以通过窗口右上角的三点按钮进入。除此之外，大多数窗口都有一个带有更多选项的工具条。如果你的窗口看起来与教程中的不一样；例如，场景窗口(Scene)有一个统一的背景而不是一个天空盒，那么它的某个选项是不一致的。

还可以通过Unity编辑器右上方的下拉菜单切换到一个预先配置好的布局。也可以在那里保存你当前的布局，这样可以在以后需要的时候恢复。

## 1.3 包

Unity的功能是基于模块化的。除了核心功能，还有一些额外的包可以下载并且引入到你的项目中。默认的3D项目中也包含了一些默认的包，你可以在项目窗口(Project)的*Packages*下看到这些包。

![3D模板默认引入包](https://static.huozk.cn/20220814-947cc4a052fa4e80a127116c11a25c1a41b0061a7e9727a6c5dc511af86f8e5c.png)  

这些包可以被隐藏，方法是点击项目窗口(Project)右上方类似眼睛的按钮，上面有一个破折号。这纯粹是为了减少编辑器中的视觉混乱，这些包仍然是项目的一部分。这个按钮还显示有多少个这样的包。

你可以通过包管理器来管理哪些包可以被包含在你的项目中，包管理器可以通过 *Window/Package Manager* 选项打开。

![包管理器，只显示项目中已经引用的包。](https://static.huozk.cn/20220814-fc45df6641f8f925649df9bdab8c6be338bbaba172494fe4ab93eb3bc2c04166.png) 

这些包为Unity增加了额外的功能。例如，Visual Studio Editor增加了对Visual Studio编辑器的支持，用于编写代码。本教程不会使用项目中已引用包的功能，所以我把它们都删除了。唯一的例外是Visual Studio Editor，因为那是我用来写代码的编辑器。如果你使用其他的编辑器，如果它的集成包存在的话，你可以导入它。

<details>
	<summary>你不也需要Visual Studio代码编辑器包吗？</summary>
	<p>尽管名字相似，但Visual Studio和Visual Studio Code是两个不同的编辑器。你只需要其中一个包，这取决于你使用哪一个编辑器。</p>
</details>

移除软件包的最简单方法是，首先使用工具栏将软件包列表限制为只在项目中(In Project)。然后依次选择一个包并使用窗口右下方的移除按钮(Remove)。Unity在每次删除后都会重新编译，所以需要几秒钟才能完成这个过程。

移除除了Visual Studio Editor以外的所有引入包后，可以看到在项目窗口(Project)中只剩下三个包：Custom NUnit, Test Framework, 和Visual Studio Editor。其他两个仍然存在，因为Visual Studio Editor依赖于它们。

你还可以通过项目设置窗口(Project Settings)使依赖和隐藏导入的包在包管理器中可见，通过*Edit / Project Settings...*打开。选择其包管理器类别，然后在高级设置下启用*Show Dependencies*。

![包管理项目设置，打开Show Dependencies。](https://static.huozk.cn/20220814-0c97bc29349d4873128f9656cd7c7c95876d2162400b6e36d68df5e446ea1914.jpg) 

包管理项目设置，打开Show Dependencies。

## 1.4 颜色空间

现在的渲染通常是在线性色彩空间中进行的，但是Unity仍然默认配置为使用伽马色彩空间。为了获得最佳的视觉效果，选择项目设置窗口(Project Settings)中的播放器(Player)类别，打开其他设置(Other Settings)面板，向下滚动到其渲染部分(Rendering)。确保色彩空间(Color Space)被设置为线性(Liner)。Unity会显示警告，这可能需要很长的时间，但对于一个几乎是空的项目来说，不会出现这种情况。确认切换。

![色彩空间设置为线性。](https://static.huozk.cn/20220814-4114a4a838a9023df3955f44ede2be51a9f8f9ebb926e02c5f3dacb0ec00b0ab.png)

<details>
	<summary>有理由使用伽马色彩空间吗？</summary>
	<p>只有当你的目标平台是旧硬件或旧的图形API的时候。OpenGL ES 2.0和WebGL 1.0不支持线性空间，此外，在老旧的移动设备上，伽玛可以比线性空间更快。</p>
</details>

## 1.5 示例场景(Sample Scene)

新项目中包含一个名为Sample Scene的示例场景，默认打开。你可以在项目窗口(Project)的*Assets/Scenes*下找到它。

![项目窗口中的样例场景。](https://static.huozk.cn/20220814-8db777a39687111a3ec7195e6366c8d026b436e949238365ac0c94e1bafc7fdb.png)  

默认情况下，项目窗口(Project)使用两栏式布局(Two Column Layout)。你可以通过它的三点式配置菜单选项切换到单栏布局(One Column Layout)。

![一栏式布局。](https://static.huozk.cn/20220814-f489bed22ccbcceb4c1b0ee18e86e90f97130aa780bd5f90e2ac13d6b8049aa6.png)  

这个样本场景包含一个主摄像机(Main Camera)和一个定向灯光(Direction Light)。这些都是游戏对象。它们被列在层次结构窗口(Hierarchy)中，在场景的下面。

![场景中的对象层次。](https://static.huozk.cn/20220814-2a53fe3188f81a7d7ac2d4d69cb3ec910b308539ae50a3dcd1437f505a594d1f.png)  

你可以通过层次结构窗口(Hierarchy)或场景窗口(Scene)选择一个游戏对象。相机有一个场景图标，看起来像一个老式的胶片相机，而定向灯的图标则看起来像一个太阳。

![场景窗口中的图标。](https://static.huozk.cn/20220814-b6c136e50147c5f6e402b12a1640242f94c5e8355e4cb6cb9d128b45964bd3bf.png)  

<details>
	<summary>如何在场景窗口中进行导航？</summary>
	<p>你可以使用alt或option键与鼠标结合来旋转视图。也可以使用方向键来移动视点，并通过鼠标滚轮进行缩放。另外，按F键可以将视角聚焦到当前选定的游戏对象上。当然，还有其他更多的可操作性，但这些足以让你在场景中找到方向。</p>
	<p>当一个物体被选中时，关于它的详细信息将显示在检查器窗口(Inspector)中，但我们会在需要时再介绍这些。我们不需要修改摄像机和灯光，所以我们可以通过点击层次结构窗口(Hierarchy)中它们左边的眼睛图标来把它们在场景中隐藏起来。这个图标在默认情况下是不可见的，但是当我们把鼠标光标悬停在游戏对象前面时，就会出现。这么做纯粹是为了减少场景窗口中的视觉杂乱。</p>
</details>

![隐藏的物体。](https://static.huozk.cn/20220814-76790001af396bbcb80832b277a3da8159715bd03abe06ad015f0cd8717603da.png)  

<details>
	<summary>眼睛旁边的手状图标是做什么的？</summary>
	<p>在包含眼睛图标的那一列旁边，有着类似手的图标。这些图标在默认情况下也是不可见的。只有当一个游戏对象的手部图标处于活动状态时，不可以通过场景窗口(Scene)选择该对象。这样你就可以通过在场景窗口(Scene)点击选中的反应来控制对象。</p>
</details>

# 创建一个简单的时钟

现在我们的项目已经正确设置好了，可以开始创建我们的时钟了。

## 2.1 创建一个游戏对象

首先需要一个游戏对象来表示时钟。我们将从最简单的游戏对象开始，也就是一个空的游戏对象(空物体)，可以通过*GameObject/Create Empty*选项来创建。另外，你也可以使用层次结构窗口(Hierarchy)的上下文菜单中的*Create Empty*选项，还可以通过另一种方式点击打开，通常是右击或用两根手指敲击。这将把创建的游戏对象添加到场景中。它显示在SampleScene场景下的层次结构窗口(Hierarchy)中，并处于被选中状态，现在场景名字旁边被标记为星号，表示它有未保存的修改，记得保存。现在你可以修改名字，或者以后再做更改。

![选择了新游戏对象的层次结构窗口。](https://static.huozk.cn/20220814-0a1a02dff4309ed83b76a6d74d67178e31226f072dcf7847b4d49d0518c5a890.png)  

选择了新游戏对象的层次结构窗口。

只要游戏对象处于被选中的状态，检查器窗口(Inspector)就会显示它的详细信息。顶部是标题，上面有对象的名称和一些其他的配置。默认情况下，该对象是被启用的，且不是静态的，没有被更改标签，位于默认层级上。这些设置都不用做修改，我们需要把它重命名为时钟(Clock)。

![选定时钟的检查器窗口。](https://static.huozk.cn/20220814-a297cb552889d22d43f21775b0b5af0c0d3dcdcdce89e36ee94b93feff7813e8.png)  

标题下面是该游戏对象的所有组件列表。每个3D对象的顶部总会有一个`Transform`组件，这就是时钟目前拥有的所有组件。它的作用主要是控制游戏对象的位置、旋转角度和大小比例。现在确保所有时钟的位置和旋转角度都设置为0，其大小比例应该统一为1。

<details>
	<summary>2D对象怎么办？</summary>
	<p>当使用的是2D而不是3D对象时，你可以忽略三个维度中的一个。对于专门用于2D的对象，如UI，通常有一个<code>RectTransform</code>来代替<code>Transform</code>，它是一个特殊的<code>Transform</code>组件。</p>
</details>

因为游戏对象是空的，它在场景窗口(Scene)中是处于不可见的。不过，在游戏对象的位置，也就是在世界的中心，可以看到一个操作工具。

![用移动工具选择。](https://static.huozk.cn/20220814-5c2cc39e31c9260e95c9afe10a0d7113ac714ef955d2b36fdda6a79ce723738b.png)  

<details>
	<summary>为什么我在选择时钟(clock)后没有看到操纵工具？</summary>
	<p>操纵工具存在于场景窗口(Scene)中。请确保你看到的是场景窗口(Scene)，而不是游戏窗口(Game)。</p>
</details>

当前处于哪个操纵工具，可以通过编辑器工具栏左上方的按钮来控制。这些模式也可以通过快捷键Q、W、E、R、T和Y键激活。该组中最右边的按钮是用来启用自定义编辑器工具的，我们没有这个工具。默认情况下，移动工具是激活的。

![操纵模式工具栏。](https://static.huozk.cn/20220814-557da9fe4bd16dfa2d2b8c1debbc3dabbd0ee418135b696ef1144be2a38cf395.jpg)  

在模式按钮旁边还有三个按钮，用来控制操作工具的位置、方向和捕捉。

## 2.2 创建时钟的表盘

虽然我们已经拥有一个时钟对象，但还没有看到任何东西。现在必须给它添加3D模型，这样才能有物体被渲染出来。Unity内置了一些原始游戏对象，可以通过使用它们来建立一个简单的时钟。让我们首先通过*GameObject/3D Object/Cylinder*向场景添加一个圆柱体，确保它具有与我们的时钟相同的`Transform`数值。

![代表一个圆柱体的游戏对象。](https://static.huozk.cn/20220814-679b08215ae6851c0d5949401baf85bbf6d8e8ed58e37689960d6293d2c07dc4.png)  

新对象比一个空对象多了三个组件。首先，它有一个`MeshFilter`，它包含了对内置圆柱体网格的引用。

![MeshFilter组件，设置为圆柱体。](https://static.huozk.cn/20220814-03e3e6c3f509647df6cb084ba720a3c7967b05693e7a0cb713f2f08a1bb1555d.png)  

其次是一个`MeshRenderer`。这个组件的作用是确保对象的网格被渲染出来。它也决定了渲染时使用什么材质，也就是默认材质。这个材质也会显示在检查器中，在组件列表的最下面。

![MeshRenderer组件，设置为默认材质。](https://static.huozk.cn/20220814-571f9f5b5ba1ab3dbc226892abf0183cd27403f108de6c37370c3a9ee91acf99.png)  

第三个是`CapsuleCollider`，它用于3D物理模拟。这个物体代表一个圆柱体，但它有一个胶囊碰撞器，因为Unity没有一个原始的圆柱体碰撞器。而且我们不需要它，所以可以删除这个组件。如果你想让时钟具有物理效果，最好使用`MeshCollider`组件。组件可以通过其右上角的三点式下拉菜单来移除(Remove Compont)。

![没有碰撞器的圆柱体。](https://static.huozk.cn/20220814-e26c420c9e2cd19202493b4848acc26c95b1d5316fb49ae198ffb7daff8b3010.png)  

我们将通过压扁圆柱体来把它变成时钟的表盘。这是通过减少其大小比例的Y值来实现，把它减少到0.2。由于圆柱体的网格有两个单位高，它的有效高度变成了0.4个单位。让我们制作一个比较大的时钟，所以应该将其比例的X和Z值增加到10。

![缩放的圆柱体。 ](https://static.huozk.cn/20220814-8d148be27b36dc1fba347eadd0cafd209298f10ef68a7bbf80dca7a3fa8192c6.png)  

时钟应该是竖直立在或挂在墙面上的，但它的表盘目前是平躺着的。我们可以通过将圆柱体旋转四分之一圆的角度来解决这个问题。在Unity中，X轴指向右边，Y轴指向上方，Z轴指向前方。为了让我们在设计时钟时考虑到相同的方向，也就是说，当我们沿着Z轴看它时，我们可以看到它的正面。需要设置圆柱体的X值即旋转角度为90，并调整场景视图，使时钟的正面可见，所以移动工具的蓝色Z轴箭头指向远离你的方向，穿透屏幕。

![旋转的圆柱体。](https://static.huozk.cn/20220814-8595906dbe17dfa15317e5991459bbc2c01b177b531d9eea875edb690cb8790b.png)  

将圆柱体对象的名称改为*Face*，因为它代表了时钟的表盘。但是它只是时钟的一个部分，所以让它成为时钟对象的一个子对象。我们通过在层次结构窗口(Hierarchy)中把表盘(Face)拖到时钟上来实现这一点。

![钟表子对象表盘。](https://static.huozk.cn/20220814-f6e2da5748997972c9bd89c085bab25b05db3939f6c23679f50dc3d9348741df.png)  

子对象受制于其父对象的变换。这意味着当时钟(Clock)改变位置时，表盘(Face)也会跟随改变。这就好像它们是一个单一的实体。旋转和缩放也是如此。你可以用它来制作复杂的对象层次。

## 2.3 创建时钟刻度

钟表表面的外环通常有标记，有助于表明显示的时间。这就是所谓的时钟刻度。让我们用方块来表示一个12小时的时钟时间。

通过*GameObject/3D Object/Cube*向场景添加一个立方体对象，将其命名为*Hour Indicator 12*，同时使其成为Clock的子对象。子对象在层次结构中的顺序并不重要，可以把它放在表盘的上方或下方。

![钟表的子对象-刻度点。 ](https://static.huozk.cn/20220814-2b4aaa7060b80fb5c1084ad226427e8d88c7ddaeba9c23a1b851064940aaafcc.png)  

将它的比例(Scale)X轴设置为0.5，Y轴设置为1，Z轴设置为0.1，这样它就变成了一个狭长的扁平块。然后设置它的位置(Position)X轴为0，Y轴为4，Z轴为-0.25。这样就会把它放在表盘的上面，在表示刻度12点的位置，同时删除它的`BoxCollider`组件。

![刻度12点位置显示信息](https://static.huozk.cn/20220814-8071c8b7ace5696a20d6c2e384497d52cad20eba54bfd86709be57ba82033985.png)  

现在这个刻度标记很难看到，因为它的颜色与表盘相同。让我们通过*Assets/Create/Material*，或者通过项目窗口(Project)的加号按钮和鼠标右键菜单，为它创建一个单独的材质。这时我们获得了一个拥有默认材质的材质球资源。更改它的名字为*Hour Indicator*。


![项目窗口中的小时指示器，单列和双列布局。](https://static.huozk.cn/20220814-7a09348e7be79cdd0e5a0878b4c7df880e54664bd416ed3c49d8a489dd76029b.png)  

选中该材质球，并通过点击检查面板(Inspector)的颜色字段(Albedo)，将其反照率改为其他的值。这将打开一个颜色弹出窗口，提供各种方式来选择颜色。这里使用了深灰色，对应于十六进制的494949，这与RGB 0-255模式的73相同。我们不使用alpha透明通道，所以它的值不用关注。可以让其他所有属性保持原样。

![深灰色的反照率。 ](https://static.huozk.cn/20220814-b43a9f4fb861c918e9a865e364d18d5ffbc99f66135abe0e8038bde1e54b4434.png)  

<details>
	<summary>什么是反照率？</summary>
	<p>反照率是一个拉丁词，意思是白度。它是一个东西被白光照亮时的颜色。</p>
</details>

如何让表盘刻度使用这个材质球。你可以通过把材质球拖到场景(Scene)或层次窗口(Hierarchy)中的物体上来实现。也可以在选择游戏对象时把它拖到检查器窗口(Inspector)的底部，或者改变其`MeshRenderer`的`Materials`数组中的第0个元素。

![深灰色刻度信息。](https://static.huozk.cn/20220814-0cf61417acba764869116d2840e0419357deb9b7fc4867f647f73cc48b12f187.png)  
深灰色刻度信息。

## 2.4 十二个小时的刻度

现在我们可以为每个小时都做一个指示刻度。首先，我们要调整场景中摄像机的方向，使我们能够直视Z轴。通过点击场景视图(Scene)右上角的摄像机轴锥来做到这一点。也可以通过网格工具栏上的按钮将场景网格的轴线改为Z轴。

![沿着Z轴直视时钟。](https://static.huozk.cn/20220814-11ae7e688187bfae0ce5517510890e557337997b2947a67dc57bf8083d6e9386.jpg)  
沿着Z轴直视时钟。

复制*Hour Indicator 12*游戏对象。可以通过*Edit/Duplicate*，或通过指定的键盘快捷键Ctrl+D，或通过层次结构窗口(Hierarchy)中的上下文菜单来完成。复制的对象将出现在层次结构窗口(Hierarchy)中原对象的下面，也是时钟的一个子对象。它的名称被设置为*Hour Indicator 12 (1)*。把它重命名为*Hour Indicator 6*，对其位置(Position)Y轴设置为相反的值，使其表示小时刻度6。

![小时6和12的指示器信息。](https://static.huozk.cn/20220814-dcbbee1771e4faa1c090b93cc55c8def10e5ae68da2a65a3db91e336547c3430.png)  
小时6和12的指示器信息。

用同样的方法创建小时刻度3和9。在这种情况下，它们的(Position)X轴位置应该是4和-4，Y轴位置应该是0。另外将旋转角度(Rotation)Z轴设置为90°，这样它们就转了四分之一圈。

![四个小时刻度。](https://static.huozk.cn/20220814-66ed1e1bcf5dd67a7f3238f641f849bd2ad67bef519eb73b8775127102e849dd.jpg)  

然后创建另一个小时刻度12的复制体，这次为小时刻度1。 将其位置(Position)X轴设为2，Y轴设为3.464，其旋转角度(Rotation)Z轴设为-30°。然后将其复制到小时刻度2，交换其位置(Position)X轴和Y轴的值，并将其旋转角度(Rotation)Z轴增加至-60°。

![第1和第2小时的指示刻度。](https://static.huozk.cn/20220814-e5ba9c9e9d6a6e3d2342d477eb4576ee9a5efc5ce55fb138ef4698c1e065880a.jpg)  

<details>
	<summary>这些数字是怎么来的？</summary>
	每一个小时沿Z轴顺时针旋转30°。在这种情况下，我们使用负旋转，因为Unity的旋转是逆时针的。我们可以通过三角函数找到第一小时的位置。30°的正弦是$\dfrac{1}{2}$，它的余弦是$\dfrac{\sqrt{\smash[b]{3}}}{2}$。 我们用小时刻度与中心的距离来衡量，即4。 因此，我们最终得到$2\sqrt{\smash[b]{3}}\approx3.464$。 则第2个小时指针的旋转角度应该是60°，对此我们可以简单地变换正弦和余弦。
</details>

复制这两个小时刻度并设置它们的位置Y轴和旋转角度为相反的值，接着创建第4和第5小时的刻度对象。然后对第1、2、4、5小时刻度使用同样的技巧来创建其余的刻度对象，这次要设置它们的位置X轴为相反的值，并再次设置相反的旋转角度。

![所有的表盘刻度 1](https://static.huozk.cn/20220814-754a3c2910ea3282e1244ddf08d6830c30bfe88bfa42de2a712efa382ec34f3a.jpg)  

## 2.5 创建指针

下一步是创建时钟的指针。我们从时针开始。再次复制*Hour Indicator 12*，并将其命名为*Hours Arm*。然后创建一个时钟的材质，并让时钟使用它。我们把它设置为纯黑色，十六进制的000000。将时针的比例(Scale)X轴降低到0.3，将其Y轴增加到2.5。然后把它的位置Y轴改为0.75，这样它就指向小时刻度12的位置。但也有一点问题，旋转的时候看起来好像手臂有一点配重。

![时针信息。](https://static.huozk.cn/20220814-6b9e8c0cf76c1a06a84d43dac0af1f4aca05239e4581f98b1183ca920b328cf4.png)  

指针必须围绕时钟的中心旋转，通过改变它的旋转角度(Rotation)Z轴旋转,但是它却围绕自己的中心旋转。

![时针围绕自己的中心点旋转。](https://static.huozk.cn/20220814-f62238da498f775095239b577465d4baee2f6afedf64b3faefec22611d51fc4e.gif)  

发生这种情况是因为旋转相对于游戏对象的局部位置(Local Position)而言的。为了创建适合的旋转，我们必须引入一个支点对象，代替该对象进行旋转。因此，创建一个新的空游戏对象，并使其成为时钟(Clock)的子对象。你可以通过层次结构窗口(Hierarchy)中时钟的上下文菜单直接创建这个对象。把它命名为*Hours Arm Pivot*，并确保它的位置和旋转角度是0，比例是1。

![时针与支点。](https://static.huozk.cn/20220814-7efafda35ec9c359271ece644b719622ce55dff957ecf9d24c94ea9c8a1b18c6.png)  

现在试着旋转这个支点。如果你通过场景视图(Scene)做这个，确保工具手柄的位置模式被设置为枢轴(旋转轴)而不是中心。

![时针围绕支点旋转。 ](https://static.huozk.cn/20220814-387977e6766ebd133a521cd3a29820ef83f7dd3c50e1f94e0f44ef1d9e0ccad2.gif)  

复制*Hours Arm Pivot*两次，创建一个*Minutes Arm Pivot*和*Seconds Arm Pivot*。对它们进行相应的重命名，包括支点的子对象。

![所有的指针及其支点对象。 ](https://static.huozk.cn/20220814-aa6ad8dc0c67a04c9aa4df92c5bcfd8207fd1de386e27c4ea870de3adb4bda21.png)  

分钟指针应该比时针更窄更长，所以将其比例(Scale)X轴设置为0.2，Y轴设置为4，然后将其位置(Position)Y轴增加到1。同时将它的Z轴改为-0.35，以便它位于时针的顶部。注意，这是指针，而不是它的父物体支点。

![分针的位置。 1](https://static.huozk.cn/20220814-3f3c2e3ddc3388dcb119304ca1bf6c1f58cf319e99ec10e746def4b644d6fd8d.jpg) 

也要调整秒针。这次使用0.1和5作为比例(Scale)的XY值，1.25和-0.45作为位置(Position)YZ轴。

![秒针的位置。](https://static.huozk.cn/20220814-9eace68b672c11d872b93503f160dcbaa2c616d55713c86a1a8cb9f963f639eb.jpg)  

让我们通过为秒针创建一个单独的材质来使其效果突出。我给它设置一个暗红色，十六进制的B30000。另外，我在场景窗口(Scene)中关闭了网格效果，因为已经完成了时钟的制作。

![三条指针的时钟，最终效果。 1](https://static.huozk.cn/20220814-43ae2a025e0d1462f727178d437f8f8a9a30a36ebaeaaa9a4ebec8d9a1e3daf0.jpg)  

如果你还没有保存，可以通过*File/Save*或指定的键盘快捷方式Ctrl+S保存更改。

保持项目资源有序性也是一个好习惯。由于我们有三种材质，需要把它们放在一个材质文件夹(Materials)里，通过*Assets/Create/Folder*或通过项目窗口(Project)创建。然后你可以把材质拖到那里面。

![项目窗口中材质文件夹。 1](https://static.huozk.cn/20220814-ad60ea159890841df4f5677c16febe418cfb21b8c66178c0fddb9d1a23f75470.jpg)  

# 给时钟添加动画效果

我们的时钟目前不显示时间，它总是停留在十二点钟。为了使它拥有动画效果，必须给它添加一个自定义行为。可以通过创建一个脚本类型文件来实现。

## 3.1 C#脚本资源

通过*Assets/Create/C#创建*一个新的脚本资源到项目中，并命名为Clock。C#是用于Unity脚本的编程语言，发音为C-sharp。我们也需要把它放在一个新的Scripts文件夹里，以保持项目的整洁。

![项目窗口中的脚本文件，放在专门的Sceipts文件夹中。 1](https://static.huozk.cn/20220814-4d546351d91226b63a81580c641ea19d132768e0d3cdb2087637620e528baf09.png)  

当脚本被选中时，检查器窗口(Inspector)将显示其内容。但是要编辑代码，我们就必须使用代码编辑器。你可以通过按检查器中的*Open*按钮或双击资脚本资源文件打开编辑。使用哪个应用程序编辑脚本可以通过Unity的首选项(Preferences)进行配置。

![Clock的C#文件显示信息。 1](https://static.huozk.cn/20220814-d61f03da1a69f44a7ee61f873073d74cc065c25ea8df066cb8e5eb2e727f2177.png)  

## 3.2 定义一个组件类型

一旦脚本加载到你的代码编辑器中，就可以删除标准模板代码，我们将从头开始创建组件类型。

一个空的文件没有定义任何东西。它必须包含我们时钟组件的定义。我们要定义的并不是一个组件的单一实例。相反，我们定义的是被称为时钟的一般类或类型。一旦确定了这一点，我们就可以在Unity中创建多个这样的组件，尽管我们在本教程中只限于一个时钟。

在C#中，我们定义时钟类型时，首先说明我们正在定义一个类，然后是它的名字。~~在下面的代码片段中，改变后的代码有一个黄色背景，如果你使用深色网页主题查看本教程，则为暗红色。~~由于我们从一个空文件开始，它的内容应该是字面上的Clock类，而不是其他东西，不过你可以在字与字之间添加空格和换行。

```csharp
class Clock
```

<details>
	<summary>技术上讲，什么是类？</summary>
	你可以把类看作是一个蓝图，它可以用来创建驻留在计算机内存中的对象。蓝图定义了这些对象包含哪些数据以及它们具有哪些功能。<br>类也可以定义不属于对象实例的数据和功能，而属于类本身。这通常被用来提供全局可用的功能。我们将使用其中的一些功能，但时钟不会有这些功能。
</details>

因为不想限制其他代码可以访问我们的Clock类型，所以需要在它前面加上public访问修饰符。

```csharp
public class Clock
```

<details>
	<summary>类的默认访问修饰符是什么？</summary>
	如果没有访问修饰符，就好像我们写的是内部类Clock。这将限制为可以对同一程序集的代码访问，当你使用打包在不同程序集的代码时，这就变得很重要了。为了确保它总是可访问，默认情况下是让类成为公共的。
</details>

目前，我们还写入有效的C#语法。如果你要保存文件并回到Unity编辑器，那么编译将会出错且将被记录在Unity控制台窗口(Console)。

现在表示正在定义一个类型，所以我们必须实际定义它是什么样的。这是由声明后面的一个代码块完成的。代码块的边界用大括号表示。现在没有写任何内容，所以只写{}。

```csharp
public class Clock {}
```

我们代码现在是有效的。保存文件并切换回Unity。Unity编辑器将检测到脚本资产已经改变，并触发重新编译。完成后，选择我们的脚本。检查器会通知我们，该资源不包含`MonoBehaviour`脚本。

![纯C#脚本信息显示](https://static.huozk.cn/20220814-68c5af18aceb984dac04e65c5fca5bff941da7b59a532ff31d01f1fd2e32be6e.png)  

这意味着我们不能用这个脚本在Unity中创建组件(不能挂在到游戏对象上)。在这一点上，我们的时钟定义了一个基本的C#对象类型。我们的自定义组件类型必须扩展Unity的`MonoBehaviour`类型，继承其数据和功能。

<details>
	<summary>MonoBehaviour是什么意思？</summary>
	意思是，我们可以对自己的组件进行编程，为游戏对象添加自定义行为。这就是行为部分所指的内容。它只是碰巧使用了英式拼写，比较老旧。mono部分指的是对自定义代码的支持被添加到Unity的方式。它使用了Mono开源项目，这是一个.NET框架的多平台运行解决方案。因此，<code>MonoBehaviour</code>，这是一个旧的名字，由于向后兼容的原因，我们坚持使用。
</details>

为了把`Clock`变成`MonoBehaviour`的一个子类型，我们必须改变我们的类型声明，使其扩展该类型，这可以在我们的类型名称后面加上冒号，然后是它所扩展的内容。这使得`Clock`继承了`MonoBehaviour`类的所有类型。

```csharp
public class Clock : MonoBehaviour {}
```

然而，这也会导致编译出错。编译器会抱怨找不到`MonoBehaviour`类型。是因为该类型包含在一个命名空间中，也就是`UnityEngine`。要访问它，我们必须使用它的全称，`UnityEngine.MonoBehaviour`。

```csharp
public class Clock : UnityEngine.MonoBehaviour {}
```

<details>
	<summary>什么是命名空间？</summary>
	命名空间就像一个网站的域名，但对于代码来说。就像域名可以有子域名，命名空间可以有子命名空间。最大的区别是，它是反过来写的。因此，代替forum.unity.com的将是com.unity.forum。命名空间是用来组织代码和防止命名冲突的。
</details>

包含`UnityEngine`代码的程序集是与Unity一起的，你不需要单独上网去获取它。如果你导入了合适的编辑器集成包，代码编辑器使用的项目文件应该可以自动识别。

在访问Unity类型时，总是要包括`UnityEngine`的前缀，这是很不方便的。幸运的是，我们可以声明命名空间应该被自动搜索以完成C#文件中的类型名称。这可以通过在文件的顶部添加`using UnityEngine;`来实现。分号需要用来标记语句的结束。

```csharp
using UnityEngine;

public class Clock : MonoBehaviour {}
```

现在我们可以将我们的自定义组件添加到Unity中的*Clock*游戏对象中。这可以通过将脚本资源拖到对象上，或者通过对象检查器(Inspector)底部的添加组件按钮来完成。

![三个指针全部拖拽到脚本定义上](https://static.huozk.cn/20220814-652973b91146191463b602820e429cc5243b10c16f200ee46a6e2fd802b87a78.png)

请注意，我的教程中的大多数代码类型都可以链接到在线文档。例如，`MonoBehaviour`是一个链接，可以带你到Unity的该类型的在线脚本API页面。

## 3.3 获取一个指针

要旋转指针，Clock对象需要获取它们。让我们从时针开始。像所有的游戏对象一样，它可以通过调整它的Transform组件来旋转。所以我们必须将指针父物体的Transform组件添加到Clock中。这可以通过在它的代码块中添加一个数据字段来完成，定义为一个名称，后面加一个分号。

时针支点(Hours Pivot)这个名字对这个字段来说是合适的。然而，名称必须是连贯的。惯例是将字段名的第一个词首字母小写，其他词首字母大写(即驼峰命名法)，然后把它们连在一起。最终将它命名为*hoursPivot*。

```csharp
public class Clock : MonoBehaviour {
	hoursPivot;
}
```

<details>
	<summary>using语句去哪儿了？</summary>
	它还在那里，只是上面没有显示出来。代码片段将只包含现在编辑代码，这样你更能知道编辑的内容。
</details>

我们还必须声明字段的类型，在本例中是`UnityEngine.Transform`。它必须写在字段名的前面。

```csharp
Transform hoursPivot;
```

我们的类现在定义了一个字段，它可以持有对另一个对象的引用，其类型必须是`Transform`。我们必须确保它持有一个对时钟支点的`Transform`组件的引用。

字段默认是私有的，这意味着它们只能被属于时钟(Clock)的代码访问。但是这个类不知道我们的Unity场景，所以没有直接的方法来将字段与正确的对象联系起来。我们可以通过将该字段声明为可序列化来改变这种情况。这意味着当Unity保存场景时，它可以被包含在场景的数据中，它是通过把所有的数据放在一个序列中-Serializing-然后把它写到一个文件中。

将一个字段标记为可序列化是通过给它附加一个属性来完成的，在这里是`SerializeField`。它被写在字段声明的前面，包括在方括号中，通常在它上面的一行，但也可以放在同一行。

```csharp
[SerializeField]
Transform hoursPivot;
```

<details>
	<summary>我们不能直接把它变成公共的吗？</summary>
	是的，但一般来说，使类字段可以公开访问是不好的形式。以往的经验是，只有当其他类型的C#代码需要访问类的内容时，才将其公开，然后优先选择方法或属性而不是字段。越是不能访问的东西就越容易维护，因为可能直接依赖它的代码越少。在本教程中，我们唯一的C#代码是Clock，所以没有理由将其内容公开。
</details>

一旦这个字段是可序列化的，Unity将检测到这一点，并在我们的Clock游戏对象的Clock组件的检查器窗口(Inspector)中显示它。

![时针支点字段显示。](https://static.huozk.cn/20220814-66f363bf7f1e035be22cd6e20b8801ef0000ebce553101dc73ae0aad28987ddf.png)  

为了连接他们，将*Hours Arm Pivot*从层次结构(Hierarchy)中拖到*Hours Pivot*字段上。或者，使用该字段右侧的圆形按钮，在弹出的列表中搜索该时针支点。在这两种情况下，Unity编辑器都会获取*Hours Arm Pivot*的`Transform`组件，并将其引用到我们的字段中。

![连接状态的时针字段。](https://static.huozk.cn/20220814-4d3702519e411884875e00672ddd8cf430fe0de70d535e0c7cb32d019d9984fc.png) 

## 3.4 获取所有三条指针

我们必须为分钟和秒臂枢轴做同样的事情。因此，再给Clock添加两个可序列化的Transform字段，并加上适当的名字。

```csharp
[SerializeField]
Transform hoursPivot;

[SerializeField]
Transform minutesPivot;

[SerializeField]
Transform secondsPivot;
```

可以使这些字段声明变得更简洁吗？，因为它们共享相同的属性、访问修饰符和类型。所以可以合并为由逗号分隔开的字段名列表，跟在属性和类型声明后面。

```csharp
[SerializeField]
Transform hoursPivot, minutesPivot, secondsPivot;

//[SerializeField]
//Transform minutesPivot;

//[SerializeField]
//Transform secondsPivot;
```

<details>
	<summary>//是做什么的？</summary>
	双斜线表示一个注释。它们之后直到行尾的所有文本都会被编译器忽略。如果需要的话，它可以用来添加文本以说明代码。我也用它来表示已经被删除的代码。除此之外，被删除的代码有一条线穿过它。
</details>

在编辑器中把另外两个指针支点也挂上。

![所有三条指针都处于连接状态。](https://static.huozk.cn/20220814-51f0e91864bcd62544af15f427a71f5dd0e22fab557ced1d3ee4f8c19af8a758.png)  

## 3.5 唤醒

现在，我们可以访问指针支点了，下一步是旋转它们。要做到这一点，我们需要时钟(Clock)执行一些代码。通过在类中添加一个代码块来完成，也就是所谓的方法。这个代码块的前缀是一个名字，按照惯例，这个名字是大写的。我们将它命名为`Awake`，说明这些代码应该在脚本被唤醒时执行。

```csharp
public class Clock : MonoBehaviour {

	[SerializeField］
	Transform hoursPivot, minutesPivot, secondsPivot;

	Awake {}
}

```

方法有点像数学函数，例如$\textit{f}(x) = 2x+3$。该函数需要一个数字-由变量参数表示的$x$-将其加倍，然后再加上3。它对一个单一的数字进行操作，其结果也是一个单一的数字。在方法的情况下，它更像$\textit{f}(p)=c$是其中$p$代表输入参数，而代表它所执行的任何代码。

像数学函数一样，方法可以产生一个结果，但这并不是必须的。我们必须声明结果的类型--就像它是一个字段一样，这里通过写成`void`来表示没有结果。在我们的例子中，我们只是想执行一些代码，而不提供一个结果值，所以使用`void`。

```csharp
void Awake {}
```

我们也不需要任何输入数据。然而，我们仍然要定义方法的参数，作为圆括号之间的逗号分隔的列表。在我们的例子中，它只是一个空列表。

```csharp
void Awake () {}
```

我们现在有了一个有效的方法，尽管它还没有做任何事情。就像Unity检测到我们的字段一样，它也检测到了这个`Awake`方法。当一个组件有一个`Awake`方法时，Unity会在该组件被唤醒时调用该方法。这发生在它被创建或在游戏模式下被加载之后。我们目前处于编辑模式，所以这还没有发生。

<details>
	<summary>Awake不是必须是公共的吗？</summary>
	Awake和其他一些方法被认为是特殊的Unity事件方法。不管我们如何声明它们，Unity引擎会找到它们并在适当的时候调用它们。这发生在托管的.NET环境之外。详细内容可以查阅Unity脚本生命周期。
</details>

请注意，`Awake`和其他特殊的Unity事件方法在~~我的教程中有粗体字~~，并链接到其在线Unity脚本API页面。

## 3.6 通过代码进行旋转

为了旋转指针，我们必须创建一个新的旋转角度。我们可以通过给`Transform`的`localRotation`属性分配一个新的旋转角度来旋转它。

<details>
	<summary>什么是属性？</summary>
	属性是一种方法，它假装是一个字段。它可能是只读或只写的。C#的惯例是将属性大写，但Unity的代码并没有这样做。
</details>

虽然`Transform`组件的旋转角度在检查器(Inspector)中是用欧拉角(Euler)定义的，单位是每轴度数，但在代码中我们必须用四元数(Quaternion)来设置。

<details>
	<summary>什么是四元数？</summary>
	四元数是基于复数的，用来表示三维旋转。虽然比单独的X、Y和Z旋转角的组合更难理解，但它们有一些有用的特性。例如，它们不会受到万向节锁的影响。
</details>

通过调用`Quaternion.Euler`方法创建一个基于欧拉角的四元数。具体做法是在`Awake`中写入，然后用分号来结束语句。

```csharp
void Awake() {
	Quaternion.Euler;
}
```

该方法有用于描述所需旋转的参数。在这种情况下，我们将提供一个逗号分隔的包含三个参数的列表，都在圆括号之间，在方法名称之后。我们为X、Y和Z的旋转轴提供三个数值。前两个使用0，Z旋转角度使用-30。

```csharp
Quaternion.Euler(0, 0, -30);
```

这个调用的结果是一个四元数结构值，包含围绕Z轴的30°顺时针旋转，与我们时钟上的小时数相匹配。

<details>
	<summary>什么是结构？</summary>
	结构是结构体的简称，是一种蓝图，就像一个类。不同的是，无论它创建的是什么，都被视为一个简单的值，如整数或颜色，而不是一个对象。它没有身份感。定义自己的结构与定义类的工作原理相同，只是你写的是结构而不是类。
</details>

为了将这个旋转应用于时针，使用=赋值语句将`Quaternion.Euler`的结果分配给`hoursPivots.localRotation`。

```csharp
	hoursPivot.localRotation = Quaternion.Euler(0, 0, -30);
```

<details>
	<summary>localRotation和Rotation之间有什么区别？</summary>
	<code>localRotation</code>属性表示<code>Transform</code>组件单独描述的旋转，因此它是一个相对于其父级的旋转角度。这是你在其检查器(Inspector)中看到的旋转角度。相比之下，<code>Rotation</code>属性表示世界空间中的最终旋转角度，将整个对象的层次结构都考虑在内。如果我们将时钟作为一个整体进行旋转，设置该属性会产生奇怪的结果。因为该属性在对时钟的旋转角度进行补偿时，指针会忽略这一点。
</details>

<details>
	<summary>难道不应该有一个警告说hoursPivot从未被初始化吗？</summary>
	编译器可以检测到没有任何代码为该字段赋值，确实可以发出这样的警告，因为它不知道我们通过Unity的检查器(Inspector)设置了它。然而，这个警告在默认情况下是被关闭。可以通过项目设置(Project Settings)来控制开关。在<em>Player/Other Settings/Script Compilation</em>下有一个抑制普通警告的切换键。它关闭了关于未初始化和未使用的私有字段的警告。
</details>

现在编辑器中进入播放模式。你可以通过 *Edit/Play，* 指定的键盘快捷键或按编辑器窗口顶部中间的播放按钮来实现。Unity将把焦点切换到游戏窗口(Game)，它将渲染场景中主摄像机看到的所有东西。时钟(Clock)组件将被唤醒，时钟(Clock)将被设置为一点钟状态。

![播放模式下，总是保持在1点钟状态。](https://static.huozk.cn/20220814-f49558a4f07eecf9b16ec8fd985831e2fb69035094b69b916fb7f594f1f6b80c.jpg)  

如果摄像机没有聚焦在时钟上，你可以移动它使时钟变得可见，但请记住，当退出游戏模式时，场景会被重置，所以你在游戏模式(Play)中对场景所做的任何改变都不会持续。但对资源来说不是这样的，它们的改变总是会被保存的。你也可以在游戏模式(Play)中打开场景窗口(Scene)，甚至是多个场景(Scene)和游戏窗口(Play)。在继续之前退出游戏模式(Play)。

## 3.7 获取当前的时间

下一步是弄清我们醒来时的当前时间。我们可以使用`DateTime`结构来访问我们正在运行的设备的系统时间。`DateTime`并不是一个统一的类型，它可以在`System`命名空间中找到。它是.NET框架核心功能的一部分，Unity就是用它来支持脚本的。

`DateTime`有一个`Now`属性，产生一个包含当前系统日期和时间的`DateTime`值。为了检查它是否正确，我们将在`Awake`开始时，通过把它传递给`Debug.Log`方法来实现把它记录到控制台(Control)。

```csharp
using System;
using UnityEngine;

public class Clock : MonoBehaviour {
	[SerializeField]
	Transform hoursPivot, minutesPivot, secondsPivot;

	void Awake() {
		Debug.Log(DateTime.Now);
		hoursPivot.localRotation = Quaternion.Euler(0, 0, -30);
}
```

现在，我们每次进入播放模式都会得到一个时间戳的记录。你可以在控制台窗口(Control)和编辑器窗口底部的状态栏中看到它。

## 3.8 转动指针

我们越来越接近一个可以工作的时钟了。让我们再次从小时开始。`DateTime`有一个`Hour`属性，可以获得`DateTime`值的小时部分。在当前的时间戳上调用这个属性，我们就可以得到当前的小时时间。

```csharp
	Debug.Log(DateTime.Now.Hour);
```

因此，为了让时针显示出当前的小时，我们必须将-30°的旋转角度值乘以当前的小时。乘法是用星号*字符完成的。我们也不再需要记录当前时间，现在可以去掉这个语句。

```csharp
	~~//Debug.Log(DateTime.Now.Hour);~~
	hoursPivot.localRotation = Quaternion.Euler(0, 0, -30 * DateTime.Now.Hour);
```

![播放模式下，时针指定的方向，由于我是零点设置的，所以跟原来一样的效果。 1](https://static.huozk.cn/20220814-29154618857e1bbba5f2f0ba25238d0fad46387a784be121c082f384b0128f84.jpg)  

为了明确我们是从小时时间到角度的转换，我们可以定义一个包含转换系数的`hoursToDegrees`字段。`Quaternion.Euler`的角度被定义为浮点值，所以我们将使用浮点类型。我们已经知道了这个数字，可以立即把它作为字段声明的一部分。然后与`DateTime`中的值字段相乘，而不是与`Awake`中的字面数字`-30`相乘。

```csharp
float hoursToDegrees = -30。

[SerializeField]
Transform hoursPivot, minutesPivot, secondsPivot;

void Awake() {
	hoursPivot.localRotation =
		Quaternion.Euler(0, 0, hoursToDegrees * DateTime.Now.Hour);
}
```

<details>
	<summary>什么是浮点数？</summary>
	计算机不能存储所有的数字，它们必须可以在其二进制存储器中被表示，而二进制存储器是由不是0就是1的比特组成，这使得许多数字不可能在有限的内存大小内精确地存储；例如$\dfrac{1}{3}$，就像我们不能精确地用十进制符号来写这个数字一样。我们能做的最好的事情就是写0.3333333，然后在某个点上停止。<br>
	假设我们决定在点的后面最多写三位数，而在点的前面只写一位数。那么$\dfrac{1}{3}$就近似于0.333。如果我们要用$\dfrac{1}{3}$除以100，那么我们就会被迫写成0.003，这意味着我们失去了两位数的精度。为了提高小数值的精度，让我们添加一个单独的指数，表示我们数字的数量级。那么$0.333\times10^{-2}$可以表示$\dfrac{1}{3}$除以100，而不会失去有意义的数字。而且我们可以用$0.333\times10^{2}$来表示100的乘法，同时在点的前面只保留一个数字。因此，点可以被认为是浮动的，因为它并不指定一个固定的数量级。这使得我们可以只用几个数字来表示大量的数字。<br>
	浮点数在计算机中的工作原理是一样的，只是它们使用二进制而不是十进制的数字，而且还必须表示一些特殊的数值，如无穷大和非数字。一个浮点数就是这样一个存储在四个字节中的值，这意味着它有32位。
</details>

如果我们声明一个没有后缀的整数，那么它被认为是一个整数，这是一个不同的值类型。尽管编译器会自动进行转换，但让我们通过给它们加上f后缀来明确说明我们所有的数字都是float类型的。

```csharp
float hoursToDegrees = -30f;

[SerializeField]
Transform hoursPivot, minutesPivot, secondsPivot;

void Awake() {
	hoursPivot.localRotation = 
		Quaternion.Euler(0f, 0f, hoursToDegrees * DateTime.Now.Hour);
}
```

每小时的度数总是相同的。我们可以通过在`hoursToDegrees`的声明中加入`const`前缀来执行这一点。这将它变成一个常量而不是一个字段。

<details>
	<summary>const值有什么特殊之处？</summary>
	const关键字表示一个值永远不会改变，不需要成为一个字段。相反，它的值将在编译过程中被计算出来，并被替换为常量的所有用法。这只适用于像数字这样的原始类型。
</details>

让我们使用`DateTime`的适当属性，对另外两个指针进行同样的处理。一分钟和一秒钟都用负六度的旋转来表示。

```csharp
const hoursToDegrees = -30f, minutesToDegrees = -6f, secondsToDegrees = -6f;

[SerializeField]
Transform hoursPivot, minutesPivot, secondsPivot;

void Awake() {
	hoursPivot.localRotation =
		Quaternion.Euler(0f, 0f, hoursToDegrees * DateTime.Now.Hour);
	minutesPivot.localRotation =
		Quaternion.Euler(0f, 0f, minutesToDegrees * DateTime.Now.Minute);
	secondsPivot.localRotation =
		Quaternion.Euler(0f, 0f, secondsToDegrees * DateTime.Now.Second);
}
```

![根据当前时间显示指针](https://static.huozk.cn/20220814-ec4d63a7c396d582136103b9350c0a91a95013a848485fae8499b3bc9dea04f5.jpg)  


我们使用了三次`DateTime.Now`，来检索小时、分钟和秒。每一次我们都要重新访问这个属性，这需要一些间隔，理论上可能会导致不同的时间值。为了确保这种情况不会发生，我们应该只检索一次时间。可以通过在方法内部声明一个变量并将时间赋值给它，然后在之后使用这个值来做到这一点。让我们把它命名为`time`。

<details>
	<summary>什么是变量？</summary>
	变量的作用类似于字段，只不过它只在方法执行时存在。它属于这个方法，而不是属于这个类。
</details>


```csharp
void Awake() {
	DateTime time = DateTime.Now;
	hoursPivot.localRotation =
		Quaternion.Euler(0f, 0f, hoursToDegrees * time.Hour);
	minutesPivot.localRotation =
		Quaternion.Euler(0f, 0f, minutesToDegrees * time.Minute);
	secondsPivot.localRotation =
		Quaternion.Euler(0f, 0f, secondsToDegrees * time.Second);
}
```

在变量的情况下，可以省略类型声明，用`var`关键字来代替。这可以缩短代码，但只有当变量的类型可以从声明时分配给它的内容中推断出来时才可以使用。另外，我倾向于只在语句中明确提到类型时才这样做，这里就属于这种情况。

```csharp
	var time = DateTime.Now;
```

## 3.9 给指针做动画

当我们进入播放模式时会得到了当前的时间，但之后，时钟仍然保持不动。为了保持时钟与当前时间的同步，将我们的`Awake`方法的名字改为`Update`。这是另一个特殊的事件方法，只要我们保持在游戏模式中，每一帧都会被Unity调用，而不是只调用一次。

```csharp
void Update() {
	var time = DateTime.Now;
	hoursPivot.localRotation =
		Quaternion.Euler(0f, 0f, hoursToDegrees * time.Hour);
	minutesPivot.localRotation =
		Quaternion.Euler(0f, 0f, minutesToDegrees * time.Minute);
	secondsPivot.localRotation =
		Quaternion.Euler(0f, 0f, secondsToDegrees * time.Second);
}
```

![不连贯时针动画](https://static.huozk.cn/20220814-1092f9e5eda796a113b0355e5d93fd2ccde8dc6ef40dae4a1a92f16656acf6d3.gif)  


<details>
	<summary>什么是一帧？</summary>
	在游戏模式下，Unity不断地从主摄像机的视角渲染场景。一旦渲染完成，结果就会呈现在显示屏上。然后显示器将显示该帧，直到得到下一帧。在渲染新的一帧之前，一切都会被更新。所以Unity经历了一个更新、渲染、更新、渲染等的序列。通常情况下，一个单一的更新步骤和渲染一次场景被认为是一个单一的帧，尽管在现实中，时间是比较复杂的。
</details>

请注意，我们的时钟组件在检查器(Inspector)中的名字前面有一个切换按钮。这允许我们禁用它，可以防止Unity调用其更新方法。

![可以通过按钮暂停脚本使用](https://static.huozk.cn/20220814-ba36c650471fd0a12daa3f26fd9404a1ae2b3904bc4435def84bd2575ce3e53e.png)  


## 3.10 持续旋转

我们的时钟指针准确地表明了当前的小时、分钟和秒。它的行为就像一个数字钟，离散的，但有指针。通常情况下，通过提供时间的模拟表示，时钟有缓慢连续旋转的指针。让我们修改我们的方法，使时钟成为真实模拟状态。

`DateTime`不包含小数点数据。幸运的是，它确实有一个`TimeOfDay`属性。这给了我们一个`TimeSpan`值，它包含了我们需要格式的数据，通过它的`TotalHours, TotalMinutes, 和TotalSeconds`属性。

首先，从`DateTime.Now`中获取`TimeOfDay`结构值，并将其存储在变量中。由于该语句中没有提到`TimeSpan`的类型，我将使变量的类型更明确。然后调整我们用来旋转指针的属性。

```csharp
void Update () {
	TimeSpan time = DateTime.Now.TimeOfDay;
	hoursPivot.localRotation =
		Quaternion.Euler(0f, 0f, hoursToDegrees * time.TotalHours);
	minutesPivot.localRotation =
		Quaternion.Euler(0f, 0f, minutesToDegrees * time.TotalMinutes);
	secondsPivot.localRotation =
		Quaternion.Euler(0f, 0f, secondsToDegrees * time.TotalSeconds);
}
```

这将导致编译器错误，告知我们不能从双数转换为浮点数。发生这种情况是因为`TimeSpan`属性产生的值是双精度浮点类型，即所谓的`double`。这些值提供了比浮点值更高的精度，但是Unity的代码只适用于单精度的浮点值。

<details>
	<summary>单精度够吗？</summary>
	对于大多数游戏来说，是的。当处理非常大的距离或比例差异时，这就成为一个问题。那么你就必须使用一些技巧，比如传输或对于相机的渲染来保持活动区域在世界原点附近。虽然使用双精度可以解决这个问题，但它也会使所涉及的数字的内存大小增加一倍，从而导致其他性能问题。游戏引擎通常使用单精度浮点值，而GPU也是如此。
</details>

我们可以通过强制地将双数转换为浮点数来解决这个问题。这个过程被称为转换，通过在要转换的值前面的圆括号中写上新的类型来完成。

```csharp
	hoursPivot.localRotation =
		Quaternion.Euler(0f, 0f, hoursToDegrees * (float)time.TotalHours);

	minutesPivot.localRotation =
		Quaternion.Euler(0f, 0f, minutesToDegrees * (float)time.TotalMinutes);

	secondsPivot.localRotation =
		Quaternion.Euler(0f, 0f, secondsToDegrees * (float)time.TotalSeconds);
```

![最终效果](https://static.huozk.cn/20220814-f97ced0a10c8c397c2d393016a2749eb2aea30e1969eeed3bed5f8b5d3f5387a.gif)  

现在你知道了在Unity中创建对象和编写代码的基本原理。下一个教程是建立一个图形(Graph)。

> 源码仓库地址：https://github.com/huozk0804/UnityTutorialsOfBasics
> 该文章原文地址：https://catlikecoding.com/unity/tutorials/basics/game-objects-and-scripts/
> 授权文件：https://huozk.cn/2022/08/cd3d674a/