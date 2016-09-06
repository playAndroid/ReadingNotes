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