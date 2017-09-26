# 从0开始学习 GitHub 系列之「07.GitHub 常见的几种操作」

之前写了一个 GitHub 系列，反响很不错，突然发现竟然还落下点东西没写，前段时间 GitHub 也改版了，借此机会补充下。

我们都说开源社区最大的魅力是人人多可以参与进去，发挥众人的力量，让一个项目更完善，更强壮。那么肯定有人疑问，我自己目前还没有能力开源一个项目，但是想一起参与到别的开源项目中，该怎么操作呢？那么今天，就来给大家一起介绍下 GitHub 上的一些常见的操作，看完之后你就知道方法了。

我们姑且以 Square 公司开源的 Retrofit 为例来介绍。

打开链接：

[https://github.com/square/retrofit](https://github.com/square/retrofit)

然后看到如下的项目主页：

![GitHub](http://stormzhang.com/image/github_project_home.png)

可以看到一个项目可以进行的操作主要就是两部分，第一部分包括 Watch、Star、Fork ，这三个操作之前的系列介绍过了，这里就不啰嗦了。

我们着重来介绍第二部分，分别包括 Code、Issues、Pull requests、Projects、Wiki、Pulse、Graphs。接下来我们来一个个解释下。

- Code

这个好理解，就是你项目的代码文件而已，这里说明一下，每个项目通常都会有对该项目的介绍，只需要在项目的根目录里添加一个 README.md 文件就可以，使用 markdown 语法，GitHub 自动会对该文件进行渲染。

- Issues

Issues 代表该项目的一些问题或者 bug，并不是说 Issues 越少越好，Issues 被解决的越多说明项目作者或者组织响应很积极，也说明该开源项目的作者很重视该项目。我们来看下 Retrofit 的 Issues 主页，截至目前 close（解决） 了 1305 个 Issue，open （待解决）状态的有 37 个，这解决问题的比例与速度值得每位开源项目的作者学习。

![GitHub](http://stormzhang.com/image/github_issues.png)

同样的，大家在使用一些开源项目有问题的时候都可以提 Issue，可以通过点击右上角的 New Issue 来新建 Issue，需要添加一个标题与描述就可以了，这个操作很简单。

- Pull requests

我们都知道 GitHub 的最大魅力在于人人都可参与，比如别人开源一个项目，我们每个人都可以一起参与开发，一起来完善，而这都通过 Pull requests 来完成，简称 PR。这个没法在 Retrofit 演示，下面我就以我自己在 GitHub 上的一个项目 9GAG 来给大家详细演示下怎么给一个项目发起 PR：

提前说明下，你必须确保你可以正常向 GitHub 提交代码，如果不可以的话，请看我之前的系列文章。

第一步登录你的 GitHub 账号，然后找到你想发起 PR 的项目，这里以 [9GAG](https://github.com/stormzhang/9GAG) 为例，点击右上角的 Fork 按钮，然后该项目就出现在了你自己账号的 Repository 里。

请注意，这个项目原本是属于 GitHub 账号 stormzhang 下的，为了演示，我自己又重新注册了另一个账号叫 googdev 单纯为了演示而用。

Fork 之后，在账号 googdev 下多了一个 9GAG 的项目，截图显示如下：

![GitHub](http://stormzhang.com/image/github_fork.png)

可以看到 Fork 过来的项目标题底部会显示一行小字：fork from stormzhang/9GAG ，除此之外，项目代码跟原项目一模一样，对于原项目来说，相当于别人新建了一个分支而已。

第二步，把该项目 clone 到本地，然后修改的 bug 也好，想要新增的功能也好，总之把自己做的代码改动开发完，保存好。为了方便演示，我这里只在原项目的 README.md 文件添加了一行文字：Fork from stormzhang !

接着，把自己做的代码改动 push 到 你自己的 GitHub 上去。

相信看过我前面教程的同学这一步应该都会，不会的可以滚回去看前面的教程了。

第三步，点击你 Fork 过来的项目主页的 Pull requests 页面，

![GitHub](http://stormzhang.com/image/github_new_pr.png)

点击 New pull request 按钮紧接着到如下页面：

![GitHub](http://stormzhang.com/image/github_compare_pr.png)

这个页面自动会比较该项目与原有项目的不同之处，最顶部声明了是 stormzhang/9GAG 项目的 master 分支与你 fork 过来的 googdev/9GAG 项目 master 分支所做的比较。

然后最顶部可以方便直观的看到到底代码中做了哪些改动，你们也看到我就是加了一句 Fork from stormzhang !

同样的我写好标题和描述，然后我们点击中间的 Create pull request 按钮，至此我们就成功给该项目提交了一个 PR。

然后就等着项目原作者 review 你的代码，并且决定会不会接受你的 PR，如果接受，那么恭喜你，你已经是该项目的贡献者之一了。

- Projects

这个是最新 GitHub 改版新增的一个项目，这个项目就是方便你把一些 Issues、Pull requests 进行分类，反正我觉得该功能很鸡肋，起码到目前为止基本没人用该功能，你们了解下就好。

- Wiki

一般来说，我们项目的主页有 README.me 基本就够了，但是有些时候我们项目的一些用法很复杂，需要有详细的使用说明文档给开源项目的使用者，这个时候就用到了 Wiki。

![GitHub](http://stormzhang.com/image/github_wiki.png)

使用起来也很简单，直接 New Page ，然后使用 markdown 语法即可进行编写。

- Pulse

Pulse 可以理解成该项目的活跃汇总。包括近期该仓库创建了多少个 Pull Request 或 Issue，有多少人参与了这个仓库的开发等，都可以在这里一目了然。

根据这个页面，用户可以判断该项目受关注程度以及项目作者是否还在积极参与解决这些问题等。

![GitHub](http://stormzhang.com/image/github_pulse.png)

- Graphs

Graphs 是以图表的形式来展示该项目的一个整体情况。比如项目的全部贡献人，比如 commits 的围度分析，比如某天代码提交的频繁程度等。

![GitHub](http://stormzhang.com/image/github_graphs.png)

- Settings

如果一个项目是自己的，那么你会发现会多一个菜单 Settings，这里包括了你对整个项目的设置信息，比如对项目重命名，比如删除该项目，比如关闭项目的 Wiki 和 Issues 功能等，不过大部分情况下我们都不需要对这些设置做更改。感兴趣的，可以自行看下这里的设置有哪些功能。

![GitHub](http://stormzhang.com/image/github_settings.png)

以上就包含了一个 GitHub 项目的所有操作，相信大家看完之后对 GitHub 上一些常用的操作都熟悉了，从现在开始，请一起参与到开源社区中来吧，开源社区需要我们每个人都贡献一份力，这样开源社区才能越来越强大，也才能对更多的人有帮助！

#### 相关阅读

[从0开始学习 GitHub 系列之「初识 GitHub」](http://stormzhang.com/github/2016/05/25/learn-github-from-zero1/)

[从0开始学习 GitHub 系列之「加入 GitHub」](http://stormzhang.com/github/2016/05/26/learn-github-from-zero2/)

[从0开始学习 GitHub 系列之「Git 速成」](http://stormzhang.com/github/2016/05/30/learn-github-from-zero3/)

[从0开始学习 GitHub 系列之「向GitHub 提交代码」](http://stormzhang.com/github/2016/06/04/learn-github-from-zero4/)

[从0开始学习 GitHub 系列之「Git 进阶」](http://stormzhang.com/github/2016/06/16/learn-github-from-zero5/)

[从0开始学习 GitHub 系列之「团队合作利器 BRANCH」](http://stormzhang.com/github/2016/07/09/learn-from-github-from-zero6/)

[从0开始学习 GitHub 系列之「如何发现优秀的开源项目？」](http://stormzhang.com/github/2016/07/28/learn-github-from-zero7/)

> 本文原创发布于[微信](http://lib.csdn.net/base/wechat)公众号 AndroidDeveloper ，转载请务必注明出处！
