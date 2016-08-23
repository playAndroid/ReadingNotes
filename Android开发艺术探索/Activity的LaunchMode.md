###Activity的LaunchMode分为四种

> 1,standard:标准模式,默认模式,每个Activity都会创建实例,不管是否已存在.
> 
> 2,singleTop:栈顶复用模式.如果Activity已位于栈顶,那么复用,并回调onNewIntent()方法.否则创建新的实例.
> 
> 3,singleTask:栈内复用模式.单实例模式,只要栈内存在要启动的Activity的实例,就不会创建新的实例.
> 
> 4,singleInstance:此模式Activity只能单独的位于一个任务栈中,且只有一个实例.

###Activity设置启动模式的方法

####1,通过AndroidMenifest为Activity指定启动模式

```
<activity
            android:name=".NormalActivityLife"
            android:launchMode="singleInstance" />
```
####2,通过Intent设置标志位为Activity设置启动模式

```
 Intent intent = new Intent(this,NormalActivityLife.class);
        intent.addFlags(Intent.FLAG_ACTIVITY_NEW_TASK);
        startActivity(intent);
```
> Tips:
> 1,第二种启动方式优先级高于第一种,当两种都存在的时候,以第二种为准
> 
> 2,清单文件中无法为Activity设置FLAG_ACTIVITY_CLEAR_TOP标识.
> 
> 3,代码中无法为Activity指定singleInstance模式.

###Activity的常见Flags

>1,FLAG_ACTIVITY_NEW_TASK:为Acitivity指定"singleTask"模式.
>
>2,FLAG_ACTIVITY_SINGLE_TOP:为Activity指定"singleTop"模式.
>
>3,FLAG_ACTIVITY_CLEAR_TOP:具有此标记的Activity启动时,位于其上的Activity都要出栈,一般会与singTask启动模式一起出现.被启动的Acitivity如果存在,系统会调用它的onNewIntent.
