###1.1 什么是View

> 1,View是Android中所有控件的基类.
> 
> 2,不论是Button还是RelativeLayout和ListView都继承自View.
> 
> 3,View是界面层的抽象,它代表了一个控件.
> 
> 4,ViewGroup控件组,ViewGroup包含了许多控件,即一组View.
> 
> 5,View本身可以是一个控件也可以由多个控件组成一组控件,通过这种关系就形成了VIew树的结构.

![View继承树](http://img.blog.csdn.net/20160907001116020)

###1.2 View的位置参数

> 1,View的位置由它的四个顶点来决定:top,left,right,bottom.
> 
> 2,top左上角纵坐标,left左上角横坐标,right右下角横坐标,bottom右下角纵坐标.

> 3,坐标都是相对View的父容器来说的,因此它是一个相对坐标.

> 4,在Android中,x轴和y轴的正方向分别为向右和向下.

![View坐标系](http://img.blog.csdn.net/20160907001137848)

####根据view的宽高和坐标关系:
> width = right - left;
> 
> height = bottom - top;

####获取View的四个参数
> - Left = getLeft();
> - Right = getRight();
> - Top = getTop();
> - Bottom = getBottom();

####3.0后增加的参数
> - x、y、translationX和translationY
> - x和y相对View的左上角坐标
> - translationX和translationY是View左上角相对于容器的偏移量.默认值为0.
> - view为其提供了get/set方法.
> - x = left + translationX; y = top + translationY;
> 
> tips:在平移过程中top和left始终为原始位置左上角的信息.此时发生变化的是x、y、translationX和translationY.

> 如想要view不断移动需要不断加大translationX或translationY的值.


###1.3 MotionEvent和ThouchSlop
> 1,MotionEvent : 
> 
> 手指触摸事件中,典型事件类型如下
> 
> - ACTION_DOWN : 手指触摸按下时
> 
> - ACTION_MOVE : 手指在屏幕上以活动
> 
> - ACTION_UP : 手指在屏幕上松开一瞬间.

> 正常情况下,一次手指触摸屏幕的行为所触发的一系列点击事件:

> - 点击松开:DOWN - > UP
> - 点击滑动松开 : DOWN - > MOVE.....MOVE - > UP

> 通过MotionEvent对象可以获得点击事件发生的x和y坐标.

> 系统提供了两种获取坐标的方法

> - getX / getY : 返回相对于当前View的x和y的坐标.
> - getRawX / getRawY : 返回相对于手机屏幕的坐标.

> 2,TouchSlop:

> - 系统所能识别出的被认为是滑动的最小距离.
> - 两次滑动的距离小于这个常量,系统不认为是在滑动操作.
> - 这是一个常量,和设备有关,不同设备上的值可能不同.
> - 通过ViewConfiguration.get(getContext().getScaledThouchSlop());获取.
> - 两次滑动事件的距离小于这个值,可以认为没有达到滑动的临界值.