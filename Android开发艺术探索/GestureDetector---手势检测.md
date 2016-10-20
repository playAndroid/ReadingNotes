> ###GestureDetecor
> 手势检测,用于辅助检测用户单击、滑动、长按、双击等行为.
> 代码如下

```

    private final GestureDetector mGestureDetector;

    public StudyViewGestureDetector(Context context) {
        super(context);

        //GestureDetector 手势检测 用于辅助检测用户的单机、滑动、长按、双击等行为
        mGestureDetector = new GestureDetector(context, 
        new GestureDetector.SimpleOnGestureListener() {
            //双击
            @Override
            public boolean onDoubleTap(MotionEvent e) {
                return super.onDoubleTap(e);
            }

            //单击
            @Override
            public boolean onSingleTapUp(MotionEvent e) {
                return super.onSingleTapUp(e);
            }

            //快速滑动
            @Override
            public boolean onFling(MotionEvent e1, MotionEvent e2, 
            float velocityX, float velocityY) {
                return super.onFling(e1, e2, velocityX, velocityY);
            }

            //拖动
            @Override
            public boolean onScroll(MotionEvent e1, MotionEvent e2, float distanceX, 
            float distanceY) {
                return super.onScroll(e1, e2, distanceX, distanceY);
            }

            //长按
            @Override
            public void onLongPress(MotionEvent e) {
                super.onLongPress(e);
            }

        });
        //解决长按无法拖动的现象
        mGestureDetector.setIsLongpressEnabled(false);
    }

    @Override
    public boolean onTouchEvent(MotionEvent event) {
        //是否消费
        return mGestureDetector.onTouchEvent(event);
    }
```