---
layout: post
title:  AI定制化学习的尝试：Flutter 和 Dart 入门记
date: 2025-11-07 16:33:00 +0800
category: tech
---


这两天突然想把移动开发补上来，一方面想扩展技能栈，另一方面也想认真试试“让 AI 把学习这件事全包了”到底会是怎样的体验。我本人的定位很简单：一个有多年 Java、Python 背景的工程师，后端和脚本写得多，对 iOS 完全没经验，对移动端也只停留在“能跑个 Demo”的程度。这次就把过程完整记录下来，看看用 Gemini 2.5 Pro（我聊天时常用 Gemini 2.5 Flash，响应更快）能不能把学习路径、踩坑避坑、日常琐碎都串起来。


## 第一轮交流：路线先定下来

开局第一问，我把自己的状况丢给它：

> 我是一个对 iOS 开发完全没有经验的一个 Java Python 软件工程师。如果我想快速开发一个 iOS 应用，我应该怎么开始，用什么样的开发语言和框架？

它的回答大意是：你有编程基础，缺的是苹果生态和特定语言框架（Swift/SwiftUI）。如果要“快”，主要有两条路：

- 跨平台方案：Flutter。
- 原生方案：Swift + SwiftUI。

之后，它把两条路的优缺点、可能的坑、学习曲线都列了一遍，并且站在“快速出成果”的角度首推 Flutter。这个阶段的信息收集，以前至少要半小时在博客和视频里跳来跳去，现在几分钟就把决策点清楚了。

## 学习路径：五个阶段的“台阶”

我接着让它给出可执行的学习路径：

> 帮我设计一个基于 Flutter 和 Dart 的学习路径图，包含概念理解、入门应用，并且你充当教练按步骤带我学。

它给了一个很清晰的五段式结构，我基本照着这个来推进：

- 打地基：Dart 语言基础（类型系统、集合、异步、空安全）。  
- 核心概念：Flutter 的 Widget、布局、路由、状态。  
- 入门应用：一个小而完整的 App（有页面、有交互、有数据）。  
- 进阶技能：网络请求、持久化、平台能力调用。  
- 发布与高级主题：性能优化、打包、测试、国际化。

每段它都给了关键词和建议时长。我不严格卡时间，但有这个“纲”，心里很踏实。

## 环境与工具：把地面铺平

我的设备是 macOS，目标优先 iOS，同时希望一套代码也能跑 Android，于是先做环境准备。

- 检查 Flutter 版本：`flutter --version`。  
- 检查 Dart 版本：`dart --version`。  
- 运行诊断：`flutter doctor`。  

如果是第一次配置，通常会遇到这些待办：

- 安装 Xcode：从 App Store 安装后运行一次，再执行 `xcode-select --install`。  
- 安装 CocoaPods：`brew install cocoapods` 或 `sudo gem install cocoapods`。  
- Android 侧的 SDK/模拟器：安装 Android Studio，创建一个模拟器。  

有一说一：`flutter doctor` 的清单很友好，基本照着做就能把红叉变成绿钩。我在跑完 `flutter doctor` 后，还是遇到了一些环境的问题。

```
Doctor summary (to see all details, run flutter doctor -v):

[✓] Flutter (Channel stable, 3.35.7, on macOS 15.7.1 24G231 darwin-arm64, locale en-CN)

[!] Android toolchain - develop for Android devices (Android SDK version 36.1.0)

    ✗ cmdline-tools component is missing.

      Try installing or updating Android Studio.

      Alternatively, download the tools from https://developer.android.com/studio#command-line-tools-only and make sure to set the

      ANDROID_HOME environment variable.

      See https://developer.android.com/studio/command-line for more details.

    ✗ Android license status unknown.

      Run `flutter doctor --android-licenses` to accept the SDK licenses.

      See https://flutter.dev/to/macos-android-setup for more details.

[!] Xcode - develop for iOS and macOS (Xcode 26.1)

    ✗ CocoaPods not installed.

        CocoaPods is a package manager for iOS or macOS platform code.

        Without CocoaPods, plugins will not work on iOS or macOS.

        For more info, see https://flutter.dev/to/platform-plugins

      For installation instructions, see https://guides.cocoapods.org/using/getting-started.html#installation

[✓] Chrome - develop for the web

[✓] Android Studio (version 2025.2)

[✓] VS Code (version 1.105.1)

[✓] Connected device (2 available)

[✓] Network resources
```

后续经过两三轮的对话，成功的把问题解决，非常顺利。

之后AI就给我布置练习题了。正如之前的体验一样，它只关注在那些我“需要”知道的知识点上，不会从零开始讲起。比如 Dart 的类型系统，它直接给我列了几个常见的类型和用法，并且告诉我Dart和Java以及Python的区别，然后让我写代码练习，加深印象。练习的要求也非常的详细，对每个方法的命名、参数、返回值都交代得很清楚。我只要照着写就行了。等到我本地运行通过后，我照着它的要求提交了整段代码，他也能很快的给出反馈，指出我哪里写得好，哪里可以改进。**全程都给足了情绪价值**， 什么“太棒了“、”你已经具备了行动力“、”非常出色“、”你的代码非常漂亮“之类的鼓励话语，让整个学习过程非常的愉快。

到目前开始，基于AI的变成自学过程还是非常不错的，等后续再做进一步的尝试。