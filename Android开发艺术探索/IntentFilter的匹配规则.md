###启动Activity的两种方式

> 1,显示启动 : 明确指出启动对象的组件信息,包名,类名
> 
` Intent intent = new Intent(this,LaunchModeActivityStudy.class);
        startActivity(intent);`

>2,隐式启动:需要Intent能够匹配目标组件的IntentFilter中设置的过滤信息

###IntentFilter
####过滤信息有:action,category,data.

```
<activity
            android:name=".NormalActivityLife"
            android:launchMode="singleInstance" >
            <intent-filter>
                <action android:name="com.ground.hao.a"/>
                <action android:name="com.ground.hao.b"/>
                <category android:name="com.ground.hao.c"/>
                <category android:name="com.ground.hao.d"/>
                <data android:mimeType="text/plain"/>
            </intent-filter>
        </activity>
```
> 1,需要同时匹配过滤列表中的action,category,data,否则匹配失败.
> 
> 2,多个action,category,data,只需每类匹配一个即可匹配成功.
> 
> 3,一个Activity可以有多个IntentFilter,一个Intent匹配任何一组即可.

###匹配规则

>1,action的匹配规则:Intent中的action与过滤中action字符串值完全相同.action区分大小写.
>
>2,category的匹配规则:Intent中如果含义category,那么必须与过滤规则中的一个category相同.默认情况下系统在调用startActivity和startActivityForResult时会为Intent加上"android.intent.category.DEFAULT".
>
>3,data的匹配规则:与action类似,要求Intent中必须含有data数据.并且能够完全匹配过滤规则中的一个.
>tips:如果你在 data 标签，既设置了 mimeType 又设置了 scheme 之内的,要为Intent指定完整的data,必须调用setDataAndType方法.

```
Intent intent1 = new Intent();//action
        intent1.setAction("com.ground.hao.a");
        intent1.addCategory("com.ground.hao.d");
    intent1.setDataAndType(Uri.parse("file://abc"),"text/plain");
        startActivity(intent1);
```
####data的值
> scheme, host, port, path, pathPrefix, pathPattern 是用来匹配 Intent 中的 Data Uri 的.
> 
> scheme:URI的模式:http,file,content.

> Host:URI的主机名:www.csdn.com
> 
> Port:URI的端口号
> 
> path 用来匹配完整的路径
> 
> pathPrefix 用来匹配路径的开头部分
> 
> pathPattern 用表达式来匹配整个路径.
> 
> 匹配符号：
>“*” 用来匹配0次或更多
>
>“.” 用来匹配任意字符
>
>“.*” 就是用来匹配任意字符0次或更多

>转义：
> tips:由于正则表达式的规范,如果要表达真实的字符串 "\*" 要写成   "\\*" , "\"要写成"\\\\".