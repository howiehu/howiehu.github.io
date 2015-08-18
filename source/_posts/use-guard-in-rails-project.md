title: "在Rails项目中使用Guard"
date: 2013-06-05 10:31
comments: true
categories:
- Ruby
tags:
- Guard
---

[Guard](https://github.com/guard/guard "Guard on github") 是一个 Ruby 项目中非常著名且强大的“文件系统变更事件处理工具”，换句话说，就是能够监视任何文件系统的变化并允许你对相应变化进行处理。

Guard 能够兼容 Mac OS X、Linux 以及 Windows 三个平台，鉴于 Windows 平台在 RoR 社区是非主流，所以以下内容仅针对 Mac OS X 和 Linux 平台。

<!-- more -->

首先，在 Gemfile 的 develpment 组中引用相关的 gem：

```ruby
group :development do
  # If you need to use rspec, please replace this by 'guard-rspec'.
  gem 'guard'
  # Use for notify on Mac OS X, you must install growl and growlnotify before.
  gem 'growl'
end
```

如上面的代码所示，一般情况下，我们在 Rails 开发时，主要使用 Guard 配合 RSpec 来进行实时集成测试，所以可以直接使用 ***guard-rspec*** 来代替 ***guard*** 。

另外，***growl*** 这个 gem 是用来配合 Mac OS X 平台下的 [Growl](http://growl.info/ "Growl") 通知程序来提供消息通知的（***如果您使用的是 Linux 发行版，比如 Ubuntu，那么 Guard 会很好的自动识别并调用相应的通知中心。***），你必须安装 [Growl](http://growl.info/downloads "Download Growl") 和 [GrowlNotify](http://growl.cachefly.net/GrowlNotify-2.0.zip "Download GrowlNotify") 才能生效。

其中 **Growl** 需要从 App Store 中付费下载，不贵，而如果您不喜欢用上面链接中的压缩包安装 **GrowlNotify** 的话，您可以考虑使用 [Homebrew](http://mxcl.github.io/homebrew/ "Homebrew") + [Homebrew-Cask](https://github.com/phinze/homebrew-cask "Homebrew-Cask") 来方便快速的安装：

```
$ brew cask install growlnotify
```

另外可能您在很多相关教程中看到使用 Guard 还要引入 ***rb-fsevent***、***rb-inotify***、***rb-fchange*** 这三个 gem 来捕获不同平台下的文件系统事件，但是当前版本 Guard 自身已经使用了 ***listen*** 来[替代](https://github.com/guard/guard/wiki/Efficient-Filesystem-Handling "Efficient Filesystem Handling")了它们，所以已经完全不需要再引用他们了。

**有关 Guard 的更详细信息请查看 [Guard Wiki](https://github.com/guard/guard/wiki "Guard Wiki")。**
