## 其他

### 1、四大组件

#### 1.1、Application
- [ContextWrapper中attachBaseContext()方法使用技巧](https://www.2cto.com/kf/201709/686874.html)
- [ Android之Content和activity、service、Application关系和attachBaseContext函数调用的时候](http://blog.csdn.net/u011068702/article/details/70768653)

```
说明：

ContextWrapper类的源码，ContextWrapper中有一个attachBaseContext()方法，这个方法会将传入的一个
Context参数赋值给mBase对象，之后mBase对象就有值了。
Application中在onCreate()方法里去初始化各种全局的变量数据是一种比较推荐的做法，但是如果你想把初始
化的时间点提前到极致，也可以去重写attachBaseContext()方法

执行顺序：构造方法 -> attachBaseContext() -> onCreate()
```

---

#### 1.2、Activity

###### 1.2.1、启动模式
- [Activity的四种启动模式-图文并茂eclipse设置详解](http://blog.csdn.net/guofengpu/article/details/52058454)
- [**Activity的四种启动模式-图文并茂【Android】**](http://blog.csdn.net/qq_31753145/article/details/50833754)
- [activity的四种启动模式区别_launchmode图文详解](http://blog.csdn.net/androidstar_cn/article/details/52730476)
- [Activity的四种启动模式和onNewIntent()](http://blog.csdn.net/linghu_java/article/details/17266603)

```
说明：

大家遇到一个应用的Activity供多种方式调用启动的情况，多个调用希望只有一个Activity的实例存在，
这就需要Activity的onNewIntent(Intent intent)方法了。只要在Activity中加入自己的onNewIntent(intent)
的实现加上Manifest中对Activity设置lanuchMode=“singleTask”就可以。

onNewIntent（）非常好用，Activity第一启动的时候执行onCreate()---->onStart()---->onResume()
等后续生命周期函数，也就时说第一次启动Activity并不会执行到onNewIntent(). 而后面如果再有想启动
Activity的时候，那就是执行onNewIntent()---->onResart()------>onStart()----->onResume(). 
如果android系统由于内存不足把已存在Activity释放掉了，那么再次调用的时候会重新启动Activity
即执行onCreate()---->onStart()---->onResume()等。

当调用到onNewIntent(intent)的时候，需要在onNewIntent() 中使用setIntent(intent)赋值给
Activity的Intent.否则，后续的getIntent()都是得到老的Intent。
```

---

###### 1.2.2、Android-Intent与Bundle
- [**Android-Intent与Bundle在传值上的区别**](http://blog.csdn.net/u014657752/article/details/47301569)
- [Android中Bundle和Intent的区别](https://www.cnblogs.com/jeffen/p/6835622.html)
- [Android细节问题 —— 有了Intent，为什么还要有Bundle？](https://www.jianshu.com/p/e9db0797293b)

```
总结：

Intent内部还是用bundle来实现数据传递的，只是在外面封装了一层。
Bundle的内部实际上是使用了HashMap<String, Object>类型的变量来存放putXxx()方法放入的值。
简单地说，Bundle就是一个封装好的包，专门用于导入Intent传值的包。

Bundle在存取数据是比较灵活的，而Intent在存取数据的种类很少且没有指定数据类型；

想对数据进行比较灵活的操作如批量操作的话就用bundle；
Bundle是可以对对象进行操作的，而Intent不可以。Bundle相对于Intent比较偏下层，比Intent接口
更多，更灵活，但Bundle仍需要借助Intent才能在Activity之间传递。

概括一下，Intent旨在数据传递，bundle旨在存取数据，当然intent也提供一部分数据的存取，但比起bundle就显得很不灵活。
```

---

#### 1.3、Service

---

#### 1.4、ContentProvider

---

### 2、开发工具
- [30款android开发高效必备工具（附下载地址）](http://www.cniao5.com/forum/thread/1744a590cb5f11e7b6be00163e0230fa)

### 3、转换
- [Android中 Bitmap和Drawable相互转换的方法](http://blog.csdn.net/hezhipin610039/article/details/7899248/)

### 4、字符串
- [JAVA字符串格式化-String.format()的使用](http://www.cnblogs.com/happyday56/p/3996498.html)

### 5、正则表达式
- [聊一聊正则表达式，最全最常用总结](https://www.jianshu.com/p/4513caf3eb7a)

### 6、混淆

## 7、其他
- [ Android 探究 LayoutInflater setFactory](http://blog.csdn.net/lmj623565791/article/details/51503977)

