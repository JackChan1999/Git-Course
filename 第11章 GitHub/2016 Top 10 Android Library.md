# 2016 Top 10 Android Library

过去的 2016 年，开源社区异常活跃，很多个人与公司争相开源自己的项目，让人眼花缭乱，然而有些项目只是昙花一现，有些项目却持久创造价值，为开发者提供了极大的便利，这些终究由时间来判断。今天，我就来整理一篇，我个人认为的 2016 年对 [Android](http://lib.csdn.net/base/android) 开发有巨大帮助的，甚至改变了 Android 开发方式的开源库，但是，仅限个人认为，不具有任何权威性。

## 1. RxJava

地址：[https://github.com/ReactiveX/RxJava](https://github.com/ReactiveX/RxJava)

2016 年 Android 界最火的莫过于 RxJava 了，如果你还不知道 RxJava，你所在公司，或者你所在的项目还没有使用 RxJava，那真的是有点 out 了，RxJava 不仅大大简化了代码，甚至可以说改变了我们的开发方式。

RxJava 是一种函数式、响应式的异步操作库，它让你的代码更加简洁，真正的让你的代码写到爽！由于 RxJava 用过的都说好，基于此，GitHub 上衍生了一堆比如 RxAndroid、RxBus、RxPermission 等之类的开源库，足以说明它的影响力。

关于 RxJava 的文章网上一大堆，它的使用方法与好处我就不多说了，请自行去搜索了解，总之，身为 Android 开发者，到现在你还不知道 RxJava，简直了！

## 2. Retrofit

地址：[https://github.com/square/retrofit](https://github.com/square/retrofit)

如果有人问我，Android 界最好用的网络请求库是什么？在之前可能会有人回答 android-async-http、Volley、OkHttp（准确说，OkHttp 是一个 http 请求客户端） 之类的，但是 16 年过后，我会告诉你 Retrofit 是最好用的网络请求库。

Retrofit 完全 RESTful 风格的 api 网络请求库，解耦更彻底，源码设计超多的设计模式，值得大家学习，另外扩展性非常好，支持各种配置来满足你的需求，最最重要的是，如果你的项目使用了 RxJava，那么 Retrofit 可以完美结合，我只能说 Prefect！再次验证了那句话：Square 出品，必属精品！

## 3. EventBus

地址：[https://github.com/greenrobot/EventBus](https://github.com/greenrobot/EventBus)

试想这么一个场景，在 A 页面打开 B 页面，然后 B 页面打开了 C 页面，C 页面又打开了 D 页面，而且还需要传递参数，在 D 页面修改了一些信息，然后这些信息更新之后，A、B、C 页面很可能都需要对应的进行数据更新，碰到这种需求该怎么处理？

有人说用 startActivityForResult()，你可以试下，有多么难处理，还有人想到用广播，这个当然可以，因为广播是全局的，主要进行注册都可以通知到每一个页面，但是我很不喜欢用广播，每次用广播都要走那一套流程，很麻烦，而且很重。

而如果你知道 Eventbus，那么一切都非常的简单。

EventBus 是一个事件管理平台，以事件驱动的方式来简化事件传递逻辑，可以把它想象成轻量级的 BroadcastReceiver，不过，EventBus 并不是 16 年才开始进入大众视野的，很早就开源了，只是这个库太实用了，时至今日，它仍然很火，使用起来非常方便。

值得注意的是：EventBus 固然好用，但是不要过度使用，因为一旦你的代码大量使用 EventBus，会致使代码可读性稍差，而且出了问题不太好定位。所以建议只在特定的场景使用，切莫贪杯！

## 4. Glide、Fresco

图片加载可能跟网络请求一样，基本是所有 App 开发必备的功能，选择一款成熟稳定的图片加载库重要性不言而喻，目前主流的图片加载有 Picasso、Glide、Fresco，Glide 是 Google 员工基于 Picasso 基础上进行开发的，所以自然各方面比 Picasso 更有优势，而且支持 Gif，所以推荐大家优先选择 Glide 库，官方地址：

[https://github.com/bumptech/glide](https://github.com/bumptech/glide)

如果你的项目需要大量使用图片，比如是类似 Instagram 一类的图片社交 App ，那么推荐使用 Fresco。Fresco 是 Facebook 作品，关于内存的占用优化更好，但是同时包也更大，门槛也更高，初级工程师不建议使用。官方地址：

[https://github.com/facebook/fresco](https://github.com/facebook/fresco)

这两款图片加载库，基本算是在 16 年使用最多，被认可最高的两个图片加载库了。

## 5. LeakCanary

地址：[https://github.com/square/leakcanary](https://github.com/square/leakcanary)

开发者最关心的除了完成功能外，其次就是会不会造成内存泄露了，其实检测内存泄露在 [Java](http://lib.csdn.net/base/javase) 领域有很多种方法与工具，但是针对 Android 都不够方便，而良心公司 Square 开源了一款针对 Android 平台的内存泄露检测工具 LeakCanary，集成简单，使用方便，平时[测试](http://lib.csdn.net/base/softwaretest)的过程中就自动记录了内存泄露的位置，甚至帮你定位到代码级别，强烈推荐。

## 6. ButterKnife

地址：[https://github.com/JakeWharton/butterknife](https://github.com/JakeWharton/butterknife)

我想应该没有人没听过这个库了吧？ButterKnife 是 Android 之神 JakeWharton 的大作，已经开源了很长时间，然而在 2016 年它的使用热度依然不减，它可以让你避免无休止的 findViewById() 代码，具体用法我就不多说了，使用起来比较简单。

## 7. Realm

地址：[https://realm.io/](https://realm.io/)

说到 Realm 不得不提到一个 ORM 的概念。何为 ORM 呢？ORM 是 Object Relation Mapping 的缩写，翻译过来就是对象关系映射。这是相对于[数据库](http://lib.csdn.net/base/mysql)的，我们知道 Android 中使用的数据库是 SQLite，而且 Android SDK 自带操作数据库的接口，而实际我们在使用的过程往往需要把查询的数据转换到一个 [Java ](http://lib.csdn.net/base/java)Object，也就是所谓的 Model，比如一般是这样：

```java
public User selectWithId(int id) {
    User user = null;
    Cursor cursor = db.rawQuery("select * from users where id = ?", new String[]{id});
    if (cursor != null && cursor.moveToFirst()) {
        int age = cursor.getInt(cursor.getColumnIndex("age"));
        String userName = cursor.getString(cursor.getColumnIndex("user_name"));
        ...
        user = new User(age, userName, ...);
        cursor.close();
    }
    return user;
}
```

操作起来是不是很麻烦？而且可读性超差，而有了 ORM 我们写代码可能会是类似这样：

查询数据是这样：

```java
public User getUserById(int id) {
    return RealmResults<User> pups = realm.where(User.class)
                               .lessThan("id", 2)
                               .findAll();
}
```

是不是非常方便？代码写起来更像是面向对象，而不是一个个的裸写 SQL 了，这就是所谓的 ORM。

而 Android 界的 ORM 框架有很多，比如 GreenDao、SugarORM、ActiveAndroid 等等，但是我推荐大家的 ORM 框架以上都不是，是叫做 Realm。

Realm 是一种面向移动端的新型轻量数据库，而且是开源的，跟 SQLite 完全不一样，性能上秒杀 SQLite，支持 Java、Android、[iOS](http://lib.csdn.net/base/ios) 各平台，我们在实际项目中采用过，体验下来各方面都很不错，所以推荐大家尝试下 Realm。

## 8. Dagger 2

地址：[https://github.com/google/dagger](https://github.com/google/dagger)

依赖注入的概念估计大家都听过，不理解的不妨搜索了解下，Android 领域比较著名的依赖注入库莫过于 Dagger 了，基于注解，使用起来异常方便。

Dagger 起初是 Square 开源的，后来 Google 在此技术上进行了改进与优化，去除了反射，编译时进行依赖注入，性能上有大幅提升，取名 Dagger 2，Square 之前开源的 Dagger 已不建议使用。其实之前大家对 Dagger 的关注程度没有那么高，一般都是属于中、高级工程师才会关注使用，但是 16 年 Android 的[架构](http://lib.csdn.net/base/architecture)被提上日程，各种 MVP、MVVM、Clean 架构等讨论的较多，而 Dagger 作为承载这些架构重要的一环被越来越多的开发者使用，所以 16 年我们看到 Dagger 的身影越来越多，所以，Dagger 被我列为 16 年还算是比较火，比较实用的 Top 10 Android Library。

## 9. android-architecture

地址：[https://github.com/googlesamples/android-architecture](https://github.com/googlesamples/android-architecture)

上面说了，16 年 Android 架构被越来越多的开发者关注，国内外关于架构的探讨比较活跃，大家熟知的 MVC、MVP、MVVM、Clean 等，就在大家争执哪个更好，Android 开发到底该怎样架构的时候，Google 开源了一个 Android 架构的官方指导，涉及 mvp、mvp-loaders、databinding、mvp-clean、mvp-dagger、mvp-contentproviders、mvp-rxjava 等，分别在各自指定的分支下，有非常大的参考意义，可以算是 Android 界的一大步。

## 10. awesome-android-ui

地址：[https://github.com/wasabeef/awesome-android-ui](https://github.com/wasabeef/awesome-android-ui)

Android 开发中除了我们以上用到的各种实用库之外，我们往往还会涉及到各种 UI 效果的实现，对于[移动开发](http://lib.csdn.net/base/wechat)，界面开发其中是很重要的一环，而 16 年针对 Android 开发有人开源整理了这么一个库，里面网罗了所有你见过的、没见过的各种 UI 效果，涉及 Material、Layout、Button、List、ViewPager、Dialog、Menu、Parallax、Progress 等等，而且有相对应的截图、gif 展示，以后应对设计师各种效果的时候有很大的参考帮助作用。

以上就是我总结的，我个人认为的，在 2016 年的 Android 开发中，比较实用的、对你的开发有很大帮助的一些 Android Library，除了对你们的开发效率有提升之外，还能够了解其原理，阅读其优秀源码，参考其代码设计，是绝佳的一份学习资料，希望每个人在 2017 年都能在技术上取得很大进步！

> 本文原创发布于[微信](http://lib.csdn.net/base/wechat)公众号 AndroidDeveloper，欢迎关注，第一时间获取更多原创分享。
> ![img](http://img.blog.csdn.net/20161017175938156)
