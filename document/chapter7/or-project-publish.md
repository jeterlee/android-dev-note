## 开源库的发布
- [**放弃JitPack，发布Android Library到Bintray、JCenter**](https://www.jianshu.com/p/9f81d5b5a451)
- [**Android Studio提交库至Bintray jCenter从入门到放弃**](https://www.jianshu.com/p/31410d71eaba)
- [**优雅的发布Android开源库(论JitPack的优越性)**](http://www.jianshu.com/p/4cfa850c01f5)
- [**利用bintray-release插件上传到jcenter**](http://blog.csdn.net/roly_yu/article/details/53486731)
- [**使用Android Studio把自己的Android library分发到JCenter**](http://sherlockshi.github.io/2016/09/29/15_Android/1555_Maven/%E4%BD%BF%E7%94%A8Android%20Studio%E6%8A%8A%E8%87%AA%E5%B7%B1%E7%9A%84Android%20library%E5%88%86%E5%8F%91%E5%88%B0jCenter/)
- [关于自己写的aar包发布到maven过程中的一些问题解决](http://blog.csdn.net/huangxuanheng/article/details/52495968)
- [利用bintray-release插件上传到Bintray- HTTP/1.1 404 Not Found [message:Repo 'maven' was not found]问题解决](http://www.voidcn.com/article/p-bifcbrue-od.html)
- [Android 将 Library 上传到 jcenter 超简单完整图文步骤以及遇到的各种坑](https://juejin.im/entry/5844c30561ff4b006c34b133)
- [Android 项目打包到 JCenter 的坑](https://www.jianshu.com/p/c721f9297b2f)
- [Android 快速发布开源项目到jcenter](http://blog.csdn.net/lmj623565791/article/details/51148825)
- [Android Studio 发布项目到jcenter库](https://www.jianshu.com/p/4a693337e3bd)
- [上传android library 到bintray](https://www.jianshu.com/p/499a086e3bab/)
- [Android 2017 开源库总结(持续更新)](http://www.apkbus.com/blog-912299-76478.html)
- [利用Bintray五分钟上传Android library到JCenter](http://www.jianshu.com/p/eb44c482b464)
- [5分钟用Jitpack发布开源库](http://blog.csdn.net/qq_34507976/article/details/54016056)


### bintray-release系列（重点推荐）
- [bintray-release使用指南（一）](https://www.jianshu.com/p/b4c46ee78b2f)
- [bintray-release配置publish闭包（二）](https://www.jianshu.com/p/e21602730aef)
- [bintray-release自定义Publication（三）](https://www.jianshu.com/p/dfb23f0ab44b)
- [bintray-release定义额外产品（四）](https://www.jianshu.com/p/49e27d02ce2d)
- [bintray-release添加对Maven Central同步的支持（五）](https://www.jianshu.com/p/06248ed5a0f2)


### bintray坑
- **问题一**
```
FAILURE: Build failed with an exception.

* What went wrong:
Execution failed for task ':app:lint'.
> Lint found errors in the project; aborting build.

Fix the issues identified by lint, or add the following to your build script to proceed with errors:
...
android {
    lintOptions {
        abortOnError false
    }
}
...

* Try:        
Run with --debug option to get more log output.
```

**解决方法：添加下面代码（若任然出错，到要分享的module对应的build.gradle，但一个项目中还有其他的module，然而其他的module我并没有添加，我以为其他不添加也不会有什么影响，我错了，问题就出在这里。）**
```
android {
    lintOptions {
        abortOnError false
    }
}
```
-------------------------------------------------------------------------------------------------
- **问题二**
```
Could not create package 'huangxuanheng/maven/fragmentstack': HTTP/1.1 404 Not Found [message:Repo 'maven' was not found]
```

**解决方法：在我注册的bintray.com账号里面的maven仓库没有找到（这个是bintray默认的仓库名称），直接新建以maven为名的Maven仓库，或者bintray.com账号里面的仓库命名不是maven，自定义名称，这是上传时需要指定仓库名（repoName）**
-------------------------------------------------------------------------------------------------
- **问题三**
```
> Invalid publication 'release': artifact file does not exist: 'K:\...\...\...\build\outputs\aar\....aar'
```

**解决方法：添加下面代码**
```
// This copy javadoc（拷贝javadoc文件）
task copyDoc(type: Copy) {
    from "${buildDir}/docs/"
    into "docs"
}
```
-------------------------------------------------------------------------------------------------
- **问题四：错误: 编码GBK的不可映射字符->请正确配置javadoc编码**

**解决方法：添加下面代码（单纯的Java库似乎没用！）**
```
// javadoc configuration
javadoc {
    options{
        encoding "UTF-8"
        charSet 'UTF-8'
        author true
        version projectVersionName
        links "http://docs.oracle.com/javase/7/docs/api"
        title javadocName
    }
}
```

**注意下面这种写法要放到project的build.gradle（否则容易编译出错）**
```
java//生成文档
       task javadoc(type: Javadoc) {
           options.encoding "UTF-8"
           options.charSet 'UTF-8'
       }
```
-------------------------------------------------------------------------------------------------
- **问题五：错误: 不允许使用自关闭元素**

**解决方法：请删除javadoc注释里面所有的含有html标签**
-------------------------------------------------------------------------------------------------
- **问题六：错误: 程序包android.support.v7.widget不存在；错误: 找不到符号**
```
:sherlockspinner:javadoc
/path/.../xxx.java:7: 错误: 程序包android.support.annotation不存在
import android.support.annotation.ColorInt;
                                 ^
/path/.../xxx.java:8: 错误: 程序包android.support.annotation不存在
import android.support.annotation.ColorRes;
                                 ^
/path/.../xxx.java:9: 错误: 程序包android.support.annotation不存在
import android.support.annotation.DrawableRes;
                                 ^
/path/.../xxx.java:10: 错误: 程序包android.support.v4.content不存在
import android.support.v4.content.ContextCompat;
                                 ^
/path/.../xxx.java:11: 错误: 程序包android.support.v4.view不存在
import android.support.v4.view.ViewCompat;
                              ^
/path/.../xxx.java:12: 错误: 程序包android.support.v7.widget不存在
import android.support.v7.widget.AppCompatEditText;
                                ^
/path/.../xxx.java:13: 错误: 程序包android.support.v7.widget不存在
import android.support.v7.widget.ListPopupWindow;
                                ^
/path/.../xxx.java:27: 错误: 找不到符号
public class SherlockSpinner extends AppCompatEditText {
                                     ^
  符号: 类 AppCompatEditText
/path/.../xxx.java:35: 错误: 找不到符号
    private ListPopupWindow mListPopupWindow;
            ^
  符号:   类 ListPopupWindow
  位置: 类 SherlockSpinner
/path/.../xxx.java:140: 错误: 找不到符号
    public void setLineColorResource(@ColorRes int resId) {
                                      ^
  符号:   类 ColorRes
  位置: 类 SherlockSpinner
/path/.../xxx.java:149: 错误: 找不到符号
    public void setLineColor(@ColorInt int color) {
                              ^
  符号:   类 ColorInt
  位置: 类 SherlockSpinner
/path/.../xxx.java:208: 错误: 找不到符号
    public void setDropdownIcon(@DrawableRes int resId) {
                                 ^
  符号:   类 DrawableRes
  位置: 类 SherlockSpinner
/path/.../xxx.java:138: 警告: @param 没有说明
     * @param resId
       ^
/path/.../xxx.java:147: 警告: @param 没有说明
     * @param color
       ^
/path/.../xxx.java:170: 错误: 找不到引用
     * @see #setClickable(boolean)
            ^
/path/.../xxx.java:172: 警告 - 标记@see: 在com.sherlockshi.widget.SherlockSpinner中找不到setClickable(boolean)
/path/.../xxx.java:206: 警告: @param 没有说明
     * @param resId
       ^
javadoc: 警告 - 找不到类ColorRes。
javadoc: 警告 - 找不到类ColorInt。
javadoc: 警告 - 找不到类DrawableRes。
1 个错误
19 个警告
:sherlockspinner:javadoc FAILED

FAILURE: Build failed with an exception.

* What went wrong:
Execution failed for task ':sherlockspinner:javadoc'.
> Javadoc generation failed. Generated Javadoc options file (useful for troubleshooting): '/Users/sherlock/work/workspace/AndroidStudio/SherlockSpinner/sherlockspinner/build/tmp/javadoc/javadoc.options'
```

**解决方法：在javadoc中加入忽略错误配置（找不到符号——删除javadoc里所有的html标签，编码GBK的不可映射字符 ——注释不要用中文，或者修改项目的字符编码，删除@see #setClickable(boolean)这一行代码注释。）**
```
 //生成文档
  task javadoc(type: Javadoc) {
      failOnError false
  }
```
-------------------------------------------------------------------------------------------------
- **问题七：Could not create version ‘0.1’: HTTP/1.1 401 Unauthorized [message:This resource requires authentication]**

**解决方法：没有配置正确的API Key**
-------------------------------------------------------------------------------------------------
- **问题八：没有有效的POM文件**

**解决方法：一定要按步骤执行并没有配置正确的API Key**
-------------------------------------------------------------------------------------------------
- **问题九：编译上传时，提示jar包未找到**
```
:aspectratioimageview:bintrayUpload: file /Users/sherlock/work/workspace/AndroidStudio/AspectRatioImageView/aspectratioimageview/build/libs/aspectratioimageview-1.0.1-javadoc.jar could not be found.
:aspectratioimageview:bintrayUpload: file /Users/sherlock/work/workspace/AndroidStudio/AspectRatioImageView/aspectratioimageview/build/libs/aspectratioimageview-1.0.1-sources.jar could not be found.
```

**解决方法：先执行gradlew install，再执行gradlew bintrayUpload**
-------------------------------------------------------------------------------------------------
- **问题十：没有有效的POM文件**

**解决方法：一定要按步骤执行并没有配置正确的API Key**
-------------------------------------------------------------------------------------------------
- **问题十一：Execution failed for task ':library:generateDebugJavadoc'**

```
FAILURE: Build failed with an exception.

* What went wrong:
Execution failed for task ':library:generateDebugJavadoc'.
> Javadoc generation failed. Generated Javadoc options file (useful for troubleshooting): '/home/gitlab_ci_runner/gitlab-ci-runner/tmp/builds/project-9/library/build/tmp/generateDebugJavadoc/javadoc.options'
```

**解决方法：在project的build中增加以下代碼：**

```
allprojects {
    repositories {
        jcenter()
    }
    tasks.withType(Javadoc) {
        options.addStringOption('Xdoclint:none', '-quiet')
        options.addStringOption('encoding', 'UTF-8')
    }
}
```
-------------------------------------------------------------------------------------------------






















