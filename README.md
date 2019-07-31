# RikkaScalableView
一个可以实现 单指移动、双击缩放、双指缩放的View。
导入就不用导入了，这是一个小Demo，仅供学习参考。
主要用到的帮助类为：

 - `GestureDetectorCompat`
`GestureDetector`的兼容类，所以用这两个的任意一个都没有关系，当然了，既然出了兼容类，那用用也没有什么关系。
它是手势监听类关于一些单击、双击的大管家类，一般用于onTouchEvent的拦截。
 - `GestureDetector.SimpleOnGestureListener`
 它是上面那个大管家类的内部类，里面有每个手势对应的方法，我们只需重写，并将其构造在大管家上，就能实现我们想要的效果。`SimpleOnGestureListener`是同时实现了单击和双击的手势，比我们分别去实现`GestureDetector.OnDoubleTapListener`和`GestureDetector.OnGestureListener`要简单的多。
 注意，我们需要在 **onDown方法返回true**，原理和onTouchEvent一样，如果不是true，就接收不到后面的事件了。
 - `ScaleGestureDetector`
 双指缩放的精髓类，它是Android专门用于解决双指缩放下缩放系数变化的API，它是个大管家类，用于onTouchEvent的拦截。
 这里注意一点，它也有个`ScaleGestureDetectorCompat`类，但是**这个类和它已经是两码事了**，所以说不上是兼容类。可能只是个扩充。
 - `ScaleGestureDetector.OnScaleGestureListener`
缩放监听类，可以监听到缩放开始、缩放时、缩放结束的状态，我们需要重写三个类，**并且在 onScaleBegin返回true**，原理和onTouchEvent一样。
 - `OverScroller`
回弹Scroller，它和`Scroller`类的区别就是它可以设置回弹边界，所以喜欢谁就用谁，因为它们的计算API都是一样的，用法上几乎没有区别。
 - `postOnAnimation(Runnable action)`
配合OverScroller食用更加美味，它的作用是展现动画的下一帧，也就是说，我们在滑动图片的时候，我们需要在滑动的过程中通过 OverScroller去计算每一帧的滑动速度、坐标，同时又要让其展现出来，所以我们需要在算完每一帧的时候，通过postOnAnimation去画出来~有没有点像异步处理，Handler什么的啊哈哈哈哈



实现效果如下：

双击缩放：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190731102745863.gif)  
双指缩放：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190731103147789.gif)

欢迎进入我的blog：
https://blog.csdn.net/rikkatheworld
