## 内存泄露
- [Android应用内存泄露分析、改善经验总结](https://www.jianshu.com/p/33d3f89f7941)


### 造成内存泄露的原因（重点推荐）
> **case1：单例造成的内存泄露**  
> **case2：InnerClass匿名内部类**  
> **case3：Activity，Context的不正确使用**  
> **case4：Handler引起的内存泄露**  
> **case5：注册监听器的泄露**  
> **case6：Cursor，Stream没有close，view没有recycle**  
> **case7：集中对象没有清理造成的内存泄露**  
> **case8：webview造成的内存泄露，AIDL**  
> **case9：构造Adapter时，没有使用缓存的convertview**  


