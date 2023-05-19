---
title: Unity项目架构设计与开发管理
date: 2022-1-19 09:53:35
link: unity-manager-intro
tags: unity-framework
categories: Unity
---

笔者是观摩刘钢先生讲解的[Unity项目架构设计与开发管理](https://v.qq.com/x/page/d016340mkcu.html)后所总结记录的。

## EmptyGo
将所有的代码放到一个空的游戏对象中；
使用 `GameObject.Find()` 来找到目标进行使用。
架构设计的雏形实现，缺点是当我们的项目越来越大的时候难以灵活管理；不适合大型项目。

## Simple GameManager

```csharp
GameManager.Instance.playSound("menu");
```

优点是： 是把EmptyGO做成一个单例来使用；比较适合小型项目；空物体进行全局引用。 缺点是： 把所有的逻辑都放在一个脚本中，不利于编译；而且会造成单一文件过于庞大；NO 即插即用。

## Manager Of Managers
类似于分级结构，各司其职；比如音频管理，场景管理，关卡管理等，每一个都是一个单例脚本，配合使用。结构相对清晰。

* MainManager
* EventManager：消息传递管理
* AudioManager：音效管理
* GUIManager：图形视图管理
* PoolManager：GO管理
* LevelManager： 关卡管理
* GameManager：核心机制管理
* SaveManager：游戏进度管理
* MenuManager：菜单行为动画管理
* …

## MVCS（StrangeIOC）

![Unity3D-StrongeIOC框架结构图](https://static.huozk.cn/20220805-c9b698b02061b94348a99223603d3f67a303aecd808fa203be7e055d417b37b6.jpg)  

Strange是一个超轻量级且高度可扩展的控制反转控制（IoC）框架，专为C＃和Unity编写。 它包含以下功能，其中大部分是可选的：

* 一个核心绑定框架，几乎可以让你将一个或多个任何东西绑定到一个或多个其他任何东西。
* 依赖注入
* 反射绑定显著降低了采用反射效率的开销
* 共享事件系统，EventDispatcher 和 Signals。
* MonoBehaviour 调配
* 可选的MVCS（模型/视图/控制器/服务）结构
* …

这个框架的想法很有意思；可以研究一下它的原理即源码。 地址：https://github.com/strangeioc/strangeioc

## MVVM（uFrame）

![Unity3D-uFrame框架结构](https://static.huozk.cn/20220805-d667d7787dff6b65113088cd5c2f4ffc978de68a89d11cbc26b11d6e6456d5c1.jpg)  

uFrame 是为 Unity Engine 设计的 MVVM / MV * 框架。它配备了大量功能，包括图形界面 / 图表引擎，可生成代码甚至处理一些重新分解。图形界面显著提高所有团队成员开发和实施一致编码模型的效率。随着微软全息镜头的崛起和Unity的跨平台功能，uFrame 是构建下一个大型应用程序或游戏的终极解决方案。 包含以下功能：

* 高质量的图形引擎
* 可编辑的代码生成模板
* UGUI绑定
* IOC /依赖注入
* 完整的MV *实现 – 事件聚合
* 场景管理（将场景加载为具有附加加载的预制件）
* 在极大型项目上测试运行
* 开源框架
* …

## 实体组件系统（ECS）

在2018年，Unity又重点推荐ECS；ECS是一种编写代码的方式，专注于您正在解决的实际问题：组成游戏的数据和行为。其中心为Entity，Component，System。除了出于设计原因更好地接近游戏编程之外，使用ECS可以使您更好的利用Unity的C＃job系统和Burst Compiler，充分利用当今的多核处理器。

* Entity 是实例,作为承载组件的载体,也是框架中维护对象的实体.
* Component 只包含数据,具备这个组件便具有这个功能.
* System 作为逻辑维护,维护对应的组件执行相关操作.
  
而且使用ECS，可以让你从面向对象转向数据导向设计，这意味着重用代码更容易，并且更容易让其他人掌握并做出贡献。
