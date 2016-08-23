###实现Serializable和Parcelable接口可以完成对象的序列化

###1,Serializable接口

> 类实现Serializable接口,并声明一个serialVersionUID即可.
> 
> serialVersionUID 可为 1L,或使用IDE自动生成类的Hash值.
```
/**
 * Serializable 序列化,
 * 优点 : 使用方便  缺点 : 频繁操作IO,开销比较大
 * 存储设备或者网络传输优选
 */
public class Person implements Serializable{

    private static final long serialVersionUID = 136593883030250618L;
    private String name;
    private int age;
    
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
    
    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }
}
```
> Tips:不声明serialVersionUID也可以实现序列化,但是反序列化会受影响.

```
 /**
             * 序列化
             */
            Person person = new Person("hello", 20);
            ObjectOutputStream out = new ObjectOutputStream(new FileOutputStream("cache.txt"));
            out.writeObject(person);
            out.close();
            /**
             * 反序列化
             */
            ObjectInputStream in = new ObjectInputStream(new FileInputStream("cache.txt"));
            person = (Person) in.readObject();
            in.close();
```

###2,Parcelable接口

> 类实现此接口,并实现方法即可

```
/**
 * 实现Parcelable接口 序列化,
 * 优点 : 效率高  缺点 : 使用麻烦
 * 内存序列化优选
 */
public class Cat implements Parcelable {
    public String name;
    public int age;
    public Person person;

    public Cat(int age, String name, Person person) {
        this.age = age;
        this.name = name;
        this.person = person;
    }


    public static final Creator<Cat> CREATOR = new Creator<Cat>() {
        @Override
        public Cat createFromParcel(Parcel in) {
            return new Cat(in);
        }

        @Override
        public Cat[] newArray(int size) {
            return new Cat[size];
        }
    };

    @Override
    public int describeContents() {
        /**
         * 如果含有文件描述,返回1,否则返回0
         * 几乎所有情况都返回0
         */
        return 0;
    }

    @Override
    public void writeToParcel(Parcel out, int flags) {
        /**
         * 序列化操作
         */
        out.writeString(name);
        out.writeInt(age);
        out.writeSerializable(person);
    }

    protected Cat(Parcel in) {
        /**
         * 反序列化操作
         */
        age = in.readInt();
        name = in.readString();
        person = (Person) in.readSerializable();
    }
}
```
>Tips:系统已提供许多实现了Parcelable接口的类,如:Intent,Bindle,Bitmap等.
>
>一个类的对象实现序列化后,就可以通过Intent和Binder进行传递了.
