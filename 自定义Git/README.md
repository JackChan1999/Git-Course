# 第9章 自定义Git

在安装Git一节中，我们已经配置了user.name和user.email，实际上，Git还有很多可配置项。

比如，让Git显示颜色，会让命令输出看起来更醒目：

```
$ git config --global color.ui true
``

这样，Git会适当地显示不同的颜色，比如git status命令：

![git-color](http://www.liaoxuefeng.com/files/attachments/0013849265828833012fe6261a54c5794959d6c1883590b000/0)

文件名就会标上颜色。

我们在后面还会介绍如何更好地配置Git，以便让你的工作更高效。