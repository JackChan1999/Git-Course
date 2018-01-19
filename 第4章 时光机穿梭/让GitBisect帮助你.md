# 4.6 让GitBisect帮助你

Git 提供来很多的工具来帮助我们改进工作流程。 **bisect** 命令就是其中之一, 虽然由于使用得不多而不广为人知，但是当你想知道一个本来好的分支从什么时候开始变坏时，它就能派上用场了。到底是哪一次提交把事情搞砸了呢，让 bisect 来告诉你吧。

Bisect 基于[二分查找算法](http://en.wikipedia.org/wiki/Binary_search_algorithm)。给定一个有序的元素序列，它会返回要你要查找的元素的序号（或者告诉你该元素是否在序列中）。它基于如下的不变式：当你对比完一个元素，你就能根据比较的结果抛弃掉它之前或者之后的所有元素（从而大大缩小下次查找的范围）。

如果你有去过图书馆，那你可能注意到了每个专区内的书籍都是按作者姓名来排序的。比方说你要找的一本书的作者的姓为 Martin，而你刚刚看到某个书架上的最后一本书的作者的姓是 F 开头的，那么你就能确定你要找的书一定放在后面的某个书架上。依此方法继续下次，你就能快速的缩小搜索范围直到找到你要的书为止。

二分查找法亦是如此。如果你想在有 n 个元素的序列（有序的）中查找元素 x，你挑出第 n/2 个元素并将其与元素 x 比较。如果 x 大，那么就对从 n/2+1 到 n 的子序列重复上述步骤，反之，就对从 1 到 n/2-1 的子序列重复上述步骤, 这样一直递归下去。这里就有一个 [关于此算法的有趣的演示](http://www.cs.armstrong.edu/liang/animation/web/BinarySearch.html)。

二分查找算法所需的比较次数通常都比你傻傻的去拿序列中的每个元素与 x 比较所需的比较次数少得多。事实证明在有序序列中查找元素，二分查找更快更有用。

## Bisect

Bisect 就是利用二分查找发来查找在你的某一分支中到底是哪一次提交引入了特定的变更。
首先，也是最起码的，你得有办法检测出一个给定的提交点是不是有 bug。通常你可以写个测试代码，如果这也不可能的话，那至少你得有一套步骤来使 bug 再现出来。

有了这套检测方法，你就可以开始用 bisect 查找你的提交历史来以最快的速度发现引入 bug 的时间点了。等等，你还得准备好两个提交点：一个是你确定 bug 还没有被引入的提交点，另一个则是确定 bug 已经引入了的提交点（这样就缩小了初始的查找范围）。在 bisect 命令上，你可以用哈希值（hash）或者标签（tag）来引用这两个提交点。bisect 查找时，查找范围里的提交点要么被标记为好的（通过测试，没有 bug 的），要么被标记为坏的（通不过测试，有 bug 的）。

上图演示了 bisect 的执行步骤（绿点是好的提交点，红点的就是坏的）：bisect 被要求在提交点 1 到 8 这个范围内查找首次引入 bug 的提交点（看图一目了然是提交点 6），这里提交点 1 和 8 就是上段中提及的，我们需要首先准备好给 bisect 命令的两个（一好一坏）提交点。bisect 首先用调用者提供的检测方法来测试 1 到 8 中间的提交点 4，如果它是好的（图上的情况），那么 bisect 就缩小范围为它右边的区域，重复上述步骤，反之，则选择其左边的区域为新的搜索范围。如此递归下去，在上图的例子中，只需要 3 步就确定了罪魁祸首是提交点 6.

我这里创建了一个 [git 仓库](https://github.com/rodrigoflores/bisect-example)，里面共有 1024 个提交记录，每个提交都往一个文本文件后面添加一个递增的数字，从 1 到 1024，一行一个数字。我们的任务是要找出是哪个提交点向文本文件附加了 1013 这个数字（我们假定它就是一个 bug）。

首先，我们定出一个方法来判断文件里面有没有这个数字。这就是一个测试了。方法很简单：

```bash
$ grep 1013 file.txt
```

有了这条命令，我们就可以开始 bisect 了:

```bash
$ git bisect start
```

对 master 分支（的头部提交点）运行这个测试，没有得到想要的结果（就是没有任何输出），所以我们把它标记为坏的。

```bash
$ git bisect bad
```

现在让我们指定一个好的提交点：假设第一个提交点（7c0dcfa）是没有 bug 的。我们可以检出（check out）这个提交点并标记它为好的提交点（git bisect good + 该提交点的哈希值）。

```bash
$ git bisect good 7c0dcfa
Bisecting: 511 revisions left to test after this (roughly 9 steps)
[8950f7db7e7cad0b2dc394ff9b75fc3d38c9d72a] added 512
```

也可以用下面的命令，完成上面的所有步骤：

```bash
$ git bisect start master 7c0dcfa
```

git bisect start 命令可以接受两个参数，第一个是坏的提交点，第二是好的提交点。


很好，git bisect 自动检出了正中间的提交点，运行我们的检测命令，没有任何的输出（没有 bug），因此我们把该提交点标记为好的。

```bash
$ grep 1013 file.txt

$ git bisect good
Bisecting: 剩余 255 个修订待测试 (大概还需要 8 步)
[a01ba83f3500b48da97c5f5c33052623aaa4161a] added 768
```

译者注：按照二分查找算法，bisect 根据你标记的结果，决定是检出左半边的中间提交点（如果你标记为 bad）还是右半边的中间提交点（如果你标记为 good）
在 bisect 新检出的提交点上，我们再次运行测试命令。这次依然是个好的提交点。

```bash
$ grep 1013 file.txt

$ git bisect good
Bisecting:剩余 127 个修订待测试 (大概还需要 7 步)
[4a4a668bf3363d09af5fd1906bc4272aacdb4495] added 896
```

再次检测，还是好的提交点。

```bash
$ grep 1013 file.txt

$ git bisect good
Bisecting: 剩余 63 个修订待测试 (大概还需要 6 步)
[9059c5b8b898159e8d1d797bff3b1febd1fd6a1c] added 960
```

让我们看看这些消息：除了告诉你当前新检出的提交点以及新的搜索范围内有多少个待测试的提交点外，它还估计出你最多还需要重复多少次测试命令就能找到你要的提交点。这次又是一个好的提交点。

```bash
$ grep 1013 file.txt

$ git bisect good
Bisecting: 剩余 31 个修订待测试 (大概还需要 5 步)
[0c844d0b33ef297b742206ebc293f4925705b083] added 992
```

继续，依然是一个好的提交点。

```bash
$ grep 1013 file.txt

$ git bisect good
Bisecting: 剩余 15 个修订待测试 (大概还需要 4 步)
[0ee17eb17bd96b321a01c73eb13a8929a68b1239] added 1008
```

还有 4 步，这次依然 good。

```bash
$ grep 1013 file.txt

$ git bisect good
Bisecting: 剩余 7 个修订待测试 (大概还需要 3 步)
[dfb1e71736dcfffa2a30aecd7299f45f757c057e] added 1016
```

这次测试命令终于有了输出，bug 现身了！我们把这个提交点标记为坏的。

```bash
$ grep 1013 file.txt
1013
$ git bisect bad
Bisecting: 剩余 3 个修订待测试 (大概还需要 2 步)
[6e6d08c374df5162fed65fed82859b69f86b936e] added 1012
```

终点近在咫尺，测试通过，我们把它标记为好的。

```bash
$ grep 1013 file.txt

$ git bisect bad
Bisecting: 剩余 1 个修订待测试 (大概还需要 1 步)
254efa859d7fc66f1f58a59f0] added 1014
```

坏的提交点。

```bash
$ grep 1013 file.txt
1013
$ git bisect bad
Bisecting: 剩余 0 个修订待测试 (大概还需要 0 步)
8e16d98ec7039a7c53855dd9ed6] added 1013
```

最后一步，这次是坏的。

```bash
$ git bisect bad
458eab0eb8d808e16d98ec7039a7c53855dd9ed6 is the first bad commit
commit 458eab0eb8d808e16d98ec7039a7c53855dd9ed6
Author: Rodrigo Flores <mail@rodrigoflores.org>
Date:   Tue Oct 21 22:31:05 2014 -0200

    added 1013

:100644 100644 7bc3db7f48a43ccf1a8cc7c26146912cc88c1009 b393a2138a96c1530f41f70
1ab43cca893226976 M  file.txt
```

我们终于得到了那个引入 1013 数字的提交点。命令 git bisect log 可以回放整个过程。

```bash
$ git bisect start
# bad: [740cdf012013dc41a39b41d4b09b57a970bfe38f] added 1024
git bisect bad 740cdf012013dc41a39b41d4b09b57a970bfe38f
# good: [7c0dcfa7514379151e0d83ffbf805850d2093538] added 1
git bisect good 7c0dcfa7514379151e0d83ffbf805850d2093538
# good: [8950f7db7e7cad0b2dc394ff9b75fc3d38c9d72a] added 512
git bisect good 8950f7db7e7cad0b2dc394ff9b75fc3d38c9d72a
# good: [a01ba83f3500b48da97c5f5c33052623aaa4161a] added 768
git bisect good a01ba83f3500b48da97c5f5c33052623aaa4161a
# good: [4a4a668bf3363d09af5fd1906bc4272aacdb4495] added 896
git bisect good 4a4a668bf3363d09af5fd1906bc4272aacdb4495
# good: [9059c5b8b898159e8d1d797bff3b1febd1fd6a1c] added 960
git bisect good 9059c5b8b898159e8d1d797bff3b1febd1fd6a1c
# good: [0c844d0b33ef297b742206ebc293f4925705b083] added 992
git bisect good 0c844d0b33ef297b742206ebc293f4925705b083
# good: [0ee17eb17bd96b321a01c73eb13a8929a68b1239] added 1008
git bisect good 0ee17eb17bd96b321a01c73eb13a8929a68b1239
# bad: [dfb1e71736dcfffa2a30aecd7299f45f757c057e] added 1016
git bisect bad dfb1e71736dcfffa2a30aecd7299f45f757c057e
# good: [6e6d08c374df5162fed65fed82859b69f86b936e] added 1012
git bisect good 6e6d08c374df5162fed65fed82859b69f86b936e
# bad: [1d23b7045a8accd254efa859d7fc66f1f58a59f0] added 1014
git bisect bad 1d23b7045a8accd254efa859d7fc66f1f58a59f0
# bad: [458eab0eb8d808e16d98ec7039a7c53855dd9ed6] added 1013
git bisect bad 458eab0eb8d808e16d98ec7039a7c53855dd9ed6
# first bad commit: [458eab0eb8d808e16d98ec7039a7c53855dd9ed6] added 1013
```

这个例子里一共有 1024 个提交点，遍历他们我们只用了 10 步。如果提交点数量再多一倍变成 2048 个，根据二分查找算法，我们仅仅需要多加一步就能找到想要的提交点，因为二分查找算法的时间复杂度为 O(log n)。

尽管已经如此高效，一遍又一遍的运行测试命令还是很枯燥的。因此，让我们再进一步，将这个过程自动化吧。


## 自动化

Git bisect 能接受一个脚本文件名作为命令参数，通过它的返回代码判断当前提交点的好坏。如果返回 0，就是好的提交点，返回其他值就是坏的提交点。凑巧的是，grep 命令如果找到了匹配行就会返回 0，反之返回 1。你可以使用 echo $? 命令来检查测试命令的返回值。

grep 的返回值正好和我们的测试标准相反，所以我们需要写一个脚本来反转它的值（我不太习惯写 shell 脚本，如果大家有更好的方法，感谢告知）。

```
#!/bin/sh

if [[ `grep 1013 file.txt` ]]; then
  exit 1
else
  exit 0
fi
```

保存上述代码为 test.sh，并赋予它执行权限。

接着在给 bisect 命令指定了初始的好/坏提交点之后，你只需要运行：

```bash
git bisect run ./test.sh
running ./ola.sh
Bisecting: 255 revisions left to test after this (roughly 8 steps)
[a01ba83f3500b48da97c5f5c33052623aaa4161a] added 768
running ./ola.sh
Bisecting: 127 revisions left to test after this (roughly 7 steps)
[4a4a668bf3363d09af5fd1906bc4272aacdb4495] added 896
running ./ola.sh
Bisecting: 63 revisions left to test after this (roughly 6 steps)
[9059c5b8b898159e8d1d797bff3b1febd1fd6a1c] added 960
running ./ola.sh
Bisecting: 31 revisions left to test after this (roughly 5 steps)
[0c844d0b33ef297b742206ebc293f4925705b083] added 992
running ./ola.sh
Bisecting: 15 revisions left to test after this (roughly 4 steps)
[0ee17eb17bd96b321a01c73eb13a8929a68b1239] added 1008
running ./ola.sh
Bisecting: 7 revisions left to test after this (roughly 3 steps)
[dfb1e71736dcfffa2a30aecd7299f45f757c057e] added 1016
running ./ola.sh
Bisecting: 3 revisions left to test after this (roughly 2 steps)
[6e6d08c374df5162fed65fed82859b69f86b936e] added 1012
running ./ola.sh
Bisecting: 1 revision left to test after this (roughly 1 step)
[1d23b7045a8accd254efa859d7fc66f1f58a59f0] added 1014
running ./ola.sh
Bisecting: 0 revisions left to test after this (roughly 0 steps)
[458eab0eb8d808e16d98ec7039a7c53855dd9ed6] added 1013
running ./ola.sh
458eab0eb8d808e16d98ec7039a7c53855dd9ed6 is the first bad commit
commit 458eab0eb8d808e16d98ec7039a7c53855dd9ed6
Author: Rodrigo Flores <mail@rodrigoflores.org>
Date:   Tue Oct 21 22:31:05 2014 -0200

    added 1013

:100644 100644 7bc3db7f48a43ccf1a8cc7c26146912cc88c1009 b393a2138a96c15
30f41f701ab43cca893226976 M  file.txt
bisect run success
```

不费吹灰之力，你就得到了出问题的提交点。


## 结论

你很可能不会每天都用到 bisect。也许一周用一次，甚至一个月只用到一次。但是当你想要排查出带入问题的提交点时，bisect 确实能帮你一把。尽管并非必须，控制好每次提交的改动规模不要太大将对 bisect 排查大有帮助。如果每个提交都包含了大量的改动，那么就算 bisect 帮你找到这个提交，你也不得不埋头于大量的改动中苦苦搜寻 bug 的踪迹。因此，我推荐的提交策略是嫌大不嫌多。

你呢？你经常使用 bisect 吗？
