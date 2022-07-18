# c#面向对象

面向过程 -----> 面向对象

面向过程： 面向的是完成这件事的过程，强调的是完成这件事的动作

面向对象： 找个对象帮你做事。意在写出一个通用的代码，屏蔽差异。

我们在代码中描述一个对象，通过描述这个对象的属性和方法

我们把这些具有相同属性和相同方法的对象进行进一步的封装，抽象出来 类这个概念。

对象就是根据类创建出来的。

类就是一个盖大楼的图纸  对象 就是盖出来的大楼

## 类

语法：

```C#
        [public] class 类名
        {
            字段；
            属性；
            方法；
        }
```

写好了一个类之后，我们需要创建这个类的对象，

那么，我们管创建这个类的对象过程称之为类的实例化。

使用关键字 ： **new**

**this** : 当前类的对象

类是不占内存的，而对象是占内存的

## 属性

属性的作用是保护字段、对字段的赋值和取值进行限定。

属性的本质就是两个方法，一个叫get(),一个叫set()

1) Fields字段
2) Methods方法
3) Properities属性

```csharp
    private string name;
    public string Name 
            { 
                //当你输出属性的值的时候 会执行get方法
                get => name;
                //当你给属性赋值的时候 首先会执行set方法
                set => name = value; 
            }        
```

## 访问修饰符

public : 公开的公共的，在哪都能访问。

private : 私有的，只能在当前类的内部访问。

当我们创建好一个类的对象后，需要给这个对象的每个属性去赋值。

我们管这个过程称之为对象的初始化。

## 静态和非静态的区别

1) 在非静态类中，可以有实例成员，也可以有静态成员。
2) 在调用实例成员的时候，需要对象名.实例成员（）
3) 在调用静态成员的时候，需要使用类名.静态成员名（）

### 总结

+ 静态成员必须使用类名去调用，而实例成员使用对象名调用。
+ 静态函数中，只能访问静态成员，不允许访问实例成员。
+ 实例函数中，既可以使用静态成员，也可以使用实例成员。
+ 静态类中，只允许有静态成员，不允许有实例成员。

### 使用

1) 如果你想要你的类当作一个"工具类”去使用，这个时候可以考虑将类写成一个工具类。

2) 静态类在整个项目资源中资源共享。

==只有在程序全部结束之后静态类才会释放资源==

静态的存储区域 ： 堆 栈

![l](https://raw.githubusercontent.com/THENSMASH/Markdown/main/C%23Photo/%E9%9D%99%E6%80%81%E7%B1%BB%E7%9B%B8%E5%85%B31.png)

释放资源。GC Garbage Collection 垃圾回收器

## 构造函数

作用 ： 帮助我们初始化对象（给对象的每个属性依次的赋值）

构造函数是一个特殊方法 ：

1) 构造函数没有返回值，连void也不能写。

2) 构造函数的名称必须跟类名一样。

创建对象的时候会执行构造函数

构造函数可以有重载
***
类当中会有一个默认无参数的构造函数，当你写一个新的构造函数后，不管是有参还是无参数的，那个默认的无参数构造函数都被干掉了
***

## 关键字

### new 关键词

1) 在内存中开辟一块空间
2) 在开辟的空间中创建对象
3) 调用对象的构造函数进行初始化对象
4) 隐藏从父类哪里继承过来的同名成员。
隐藏后果就是子类调用不到父类的成员。

```csharp
    Person p = new Person();
```

```csharp
    public new void SayHello()//父类中也有同名函数 
```

### this关键字

1) 代表当前类的对象
2) 在类当中显示的 调用自己类的构造函数 `:this`

```csharp
//类中
 public Student(string name,int age,char gender,int chinese,int math,int english)
        {
            this.Name = name;
            this.Age = age;
            this.Gender = gender;
            this.Chinese = chinese;
            this.English = english;
            this.Math = math;
        }

        public Student(string name, int age, char gender) : this(name, age,gender,100,100,100)
        {
            /*this.Name = name;
            this.Age = age;
            this.Gender = gender;*/
        }

//main中
  Student zs = new Student("zhangsan", 18, '男');//即可
```

### base关键字

在子类中显示的调用父类的构造函数，使用关键字： `base()`

```csharp
//父类中有name,age,gender的构造函数，子类中只需要添加自己的work
public Reporter(string name,int age,char gender,string work):base(name,age,gender)
        {
            this.Work = work; 
        }
```

### 关键字总结

+ **new**

1) 创建对象
--->在堆中开辟空间
--->在开辟的堆空间中创建对象
--->调用对象的构造函数
2) 隐藏父类的成员

+ **this**

1) 代表当前类的对象
2) 显示的调用自己的构造函数

+ **base**

1) 显示调用父类的构造函数
2) 调用父类的成员

## c#中的访问修饰符

public : 公开的，公共的
private : 私有的，只能在当前类的内部访问
protected : 受保护的，只能在当前类的内部访问以及该类的子类访问
internal : 只能在当前程序集（项目）中访问。在同一个项目中，internal和public的权限是一样的。
protected internal : protected + internal

1) 能够修饰类的访问修饰符只有两个： public , internal
2) 可访问性不一致。子类的访问权限不能高于父类的访问权限，会暴露父类的成员。  

## 设计模式

设计这个项目的一种方式。

### 单例设计模式

在整个程序中，我们要保证对象必须是唯一的。

实现：
    ---->第一步：构造函数私有化
    ---->第二步：声明一个静态字段，作为全局唯一的单例对象
    ---->第三步：声明一个静态函数，返回全局唯一的对象

### 简单工厂设计模式

核心：把所有的子类都当做父类来看待
练习：
提示用户分别的输入两个数字：
再输入运算符：返回一个计算的父类，并调用方法得到结果。
Add Sub Cheng Chu
>建筑行业最早应用到设计模式这个概念
>1、注册一个公司
>2、招兵买马
>3、投标买地
>4、安排施工队开始施工
>5、卖楼

![4](https://raw.githubusercontent.com/THENSMASH/Markdown/cee19dc858c63455563ed8a1f316fb132bb23f10/C%23Photo/%E7%AE%80%E5%8D%95%E5%B7%A5%E5%8E%82%E8%AE%BE%E8%AE%A1%E6%A8%A1%E5%BC%8F.png)

```csharp
 class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("想要的品牌");
            string brand = Console.ReadLine();
            NoteBook nb = GetNodeBook(brand);
            nb.SayHello();
            Console.ReadKey();

        }
        /// <summary>
        /// 简单工厂的核心 根据用户的输入创建对象赋值给父类
        /// </summary>
        /// <param name="brand"></param>
        /// <returns></returns>
        public static NoteBook GetNodeBook(string brand)
        {
            NoteBook nb = null;
            switch (brand)
            {
                case "Lenovo": nb = new Lenovo();
                    break;
                case "Acer": nb = new Acer();
                    break;
            }
            return nb;
        }
    }

    public abstract class NoteBook
    {
        public abstract void SayHello();
    }

    public class Lenovo : NoteBook
    {
        public override void SayHello()
        {
            Console.WriteLine("联想笔记本");
        }
    }
    public class Acer : NoteBook
    {
        public override void SayHello()
        {
            Console.WriteLine("宏基笔记本");
        }
    }
```

### 类库

.dll文件，我们使用类库来帮助我们封装一些常用的功能
