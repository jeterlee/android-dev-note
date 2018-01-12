## Dagger2
- [Dagger2 @Component 和@SubComponent 区别解惑](http://blog.csdn.net/soslinken/article/details/70231089)
- [步骤 Dagger2 的 @Scope 和 @Subcomponent](http://www.zhimengzhe.com/Androidkaifa/163191.html)


### Dagger2（重点推荐）
- [**Dagger2 入门详解（一）**](http://blog.csdn.net/xx326664162/article/details/53695558)
- [**@Scope 看这一篇就够了——Dagger2 （二）**](http://blog.csdn.net/xx326664162/article/details/67640509)

> **注意事件（重要）**
>
> 1. @Component 的 inject 方法接收父类型参数，而调用时传入的是子类型对象，则无法注入（继承类是无效，只认当前注入的类）。  
> 2. @Component 关联的 @Module 中不能有重复的 Provide （关联对象是使用返回值匹配的，如果有重复就不知道使用那个，此时要使用修饰符 @Qualifier 或 @Named 注解，进行区分。）。  
> 3. @Module 的 provide 方法使用了 @Scope ，那么 @Component 就必须使用同一个注解（都要有域，即生命周期。）。  
> 4. @Module 的 provide 方法没有使用 @Scope ，那么 @Component 和 @Module 是否注解都无关紧要，可以通过编译。
> 5. @Component 的 dependencies 的 @Scope 与 @Component 自身的 @Scope 不能相同，即组件之间的 @Scope 不同。  
> 6. @Singleton 的组件不能依赖其他 @Scope 的组件，只能其他 @Scope 的组件依赖 @Singleton 的组件（@Singleton 范围是 Application级别的，只能依赖比其范围小的 @Scope ， 范围只能缩小 ）。  
> 7. 没有 @Scope 的 @Component 不能依赖有 @Scope 的 @Component。  
> 8. 一个 @Component 不能同时有多个 @Scope （@Subcomponent除外）。  
> 9. @Singleton 的生命周期依附于 @Component ，同一 Module、Provide、Singleton 不同， Component也是不一样的。  


### Dagger2神器入门
- [Dagger2神器入门（一）](http://www.jianshu.com/p/dce5382fec5d)
- [Dagger2神器入门（二）](http://www.jianshu.com/p/c673e6e73c8b)
- [Dagger2神器入门（三）](http://www.jianshu.com/p/91b9b0e4cf8c)
- [Dagger2神器入门（四）](http://www.jianshu.com/p/e76c1e0e7b40)


### Dagger2从入门到补胎
- [Dagger2从入门到补胎(一)](http://rkhcy.github.io/2017/11/15/Dagger2%E4%BB%8E%E5%85%A5%E9%97%A8%E5%88%B0%E8%A1%A5%E8%83%8E\(%E4%B8%80\)/)
- [Dagger2从入门到补胎(二)](http://rkhcy.github.io/2017/11/16/Dagger2%E4%BB%8E%E5%85%A5%E9%97%A8%E5%88%B0%E8%A1%A5%E8%83%8E\(%E4%BA%8C\)/)


