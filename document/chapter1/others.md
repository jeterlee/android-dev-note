## 其他


### 启动模式
- [Activity的四种启动模式-图文并茂eclipse设置详解](http://blog.csdn.net/guofengpu/article/details/52058454)
- [**Activity的四种启动模式-图文并茂【Android】**](http://blog.csdn.net/qq_31753145/article/details/50833754)
- [activity的四种启动模式区别_launchmode图文详解](http://blog.csdn.net/androidstar_cn/article/details/52730476)
- [Activity的四种启动模式和onNewIntent()](http://blog.csdn.net/linghu_java/article/details/17266603)

---

### Android-Intent与Bundle
- [**Android-Intent与Bundle在传值上的区别**](http://blog.csdn.net/u014657752/article/details/47301569)
- [Android中Bundle和Intent的区别](https://www.cnblogs.com/jeffen/p/6835622.html)
- [Android细节问题 —— 有了Intent，为什么还要有Bundle？](https://www.jianshu.com/p/e9db0797293b)

```
总结：
Intent内部还是用bundle来实现数据传递的，只是在外面封装了一层。
Bundle的内部实际上是使用了HashMap<String, Object>类型的变量来存放putXxx()方法放入的值。简单地说，Bundle就是一个封装好的包，专门用于导入Intent传值的包。

Bundle在存取数据是比较灵活的，而Intent在存取数据的种类很少且没有指定数据类型；

想对数据进行比较灵活的操作如批量操作的话就用bundle；
Bundle是可以对对象进行操作的，而Intent不可以。Bundle相对于Intent比较偏下层，比Intent接口更多，更灵活，但Bundle仍需要借助Intent才能在Activity之间传递。

概括一下，Intent旨在数据传递，bundle旨在存取数据，当然intent也提供一部分数据的存取，但比起bundle就显得很不灵活。
```


### 开发工具
- [30款android开发高效必备工具（附下载地址）](http://www.cniao5.com/forum/thread/1744a590cb5f11e7b6be00163e0230fa)

### 转换
- [Android中 Bitmap和Drawable相互转换的方法](http://blog.csdn.net/hezhipin610039/article/details/7899248/)

### 字符串
- [JAVA字符串格式化-String.format()的使用](http://www.cnblogs.com/happyday56/p/3996498.html)

### 正则表达式
- [聊一聊正则表达式，最全最常用总结](https://www.jianshu.com/p/4513caf3eb7a)

### 混淆

## 其他
- [ Android 探究 LayoutInflater setFactory](http://blog.csdn.net/lmj623565791/article/details/51503977)

