```
/**
 * 异常情况下的Activity,生命周期
 */
public class ExceptionActivityLife extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
    }

    @Override
    protected void onSaveInstanceState(Bundle outState) {
        super.onSaveInstanceState(outState);
        //异常销毁时调用, 在此保存当前的状态
        //调用时机在onStop之前
        //将此时保存的Bundle对象,传递给onCreate和onRestoreInstanceState方法
        outState.putChar("destory", 'a');
    }

    @Override
    protected void onRestoreInstanceState(Bundle savedInstanceState) {
        super.onRestoreInstanceState(savedInstanceState);
        //当前Activity被异常销毁重建时调用,此时可以获取销毁时保存的状态
        //在onStart之后被调用
        char destory = (char) savedInstanceState.get("destory");
        Log.e("ground", destory + "");
    }
}
```


>异常情况如:系统内存不足时将Activity回收掉.屏幕的旋转等,都会导致异常情况的发生,同时会回调以上俩个方法,所以我们可以在onSaveInstanceState方法中保存当前的数据,如:TextView的内容,ListView的position等,以待Activity恢复的时候再从onRestoreInsatanceState中取出.

>如果不是异常销毁,是不会走以上两个方法的,所以在被异常销毁时,如果要从onCreate中取出Bundle的话,需要判断是否为null,如果在onRestoreInstanceState中取出,是不用加为空判断的.