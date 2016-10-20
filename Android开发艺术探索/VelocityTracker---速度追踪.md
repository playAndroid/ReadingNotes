
> ###VelocityTracker
> 速度追踪,用于追踪手指在滑动过程中的速度.
> 
> 在View的onTouchEvent方法中追踪手指的速度


```

   	@Override
   	public boolean onTouchEvent(MotionEvent event) {
   	/**
   	* 速度追踪,用于追踪手指在滑动过程中的速度
   	* 追踪当前单击的速度
   	*/
	VelocityTracker obtain = VelocityTracker.obtain();
	obtain.addMovement(event);
	/**
 	* 获取当前滑动速度
 	* 速度是指在一段时间内手指划过的像素 左->右 正值  右->左 负值
 	* 速度 = (终点位置 - 起点位置)/时间段	
 	*/
	int action = event.getAction();
	switch (action) {
	case MotionEvent.ACTION_MOVE:
	obtain.computeCurrentVelocity(1000);//1000毫秒
	float xVelocity = obtain.getXVelocity();
	float yVelocity = obtain.getYVelocity();
	UtilsLog.e(this.getClass().getSimpleName(), "xVelocity" + xVelocity);
	UtilsLog.e(this.getClass().getSimpleName(), "yVelocity" + yVelocity);
	/**
 	* 获取速度之前必须计算速度 在get之前必须调用compute方法
 	*/
	break;
	}
	/**	
 	* 不使用时 重置并回收内存
 	*/
	obtain.clear();
	obtain.recycle();//回收
	return super.onTouchEvent(event);

```