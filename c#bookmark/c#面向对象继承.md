# c#面向对象继承

## 命名空间

可以认为类是属于命名空间的。

如果在当前项目中没有这个类的命名空间，需要我们手动的导入这个类所在的命名空间。

1) 用鼠标去点
2) alt +shift +F10
3) 记住命名空间，手动引用。

## 值类型和引用类型

区别：

1) 值类型和引用类型在内存上存储的地方不一样。
2) 在传递值类型和传递引用类型的时候，传递的方式不一样。值类型我们称之为值传递，引用类型我们称之为引用传递。

***
我们学习的值类型和引用类型

1) 值类型：int double bool char decimal struct enum
2) 引用类型： string 自定义类 数组 集合 object 接口

***
存储：

1) 值类型的值是存储在内存的栈中
2) 引用类型是存储在内存的堆中

存储图

![1](https://raw.githubusercontent.com/THENSMASH/Markdown/main/C%23Photo/%E5%80%BC%E7%B1%BB%E5%9E%8B%E4%B8%8E%E5%BC%95%E7%94%A8%E7%B1%BB%E5%9E%8B1.png)

>1) 值类型在赋值的时候，传递的是这个值本身。
>2) 引用类型在赋值的时候，传递的是对这个对象的引用。

![5](https://raw.githubusercontent.com/THENSMASH/Markdown/e66ecfa55280a833f10d5fdcb9fd220b273549af/C%23Photo/%E5%80%BC%E7%B1%BB%E5%9E%8B%E4%B8%8E%E5%BC%95%E7%94%A8%E7%B1%BB%E5%9E%8B2.png)

```csharp
    {
        static void Main(string[] args)
        {
             Person p = new Person();
             p.Name = "张三";
             Test(p);
             Console.WriteLine(p.Name);
             Console.ReadKey();

        }
        public static void Test(Person pp)
        {
            Person p = pp;
            p.Name = "李四";
        }
    }

    public class Person
    {
        private string _name;

        public string Name { get => _name; set => _name = value; }
    }
```

## 字符串

1) 字符串的不可变性
    - 当你给一个字符串重新赋值之后，老值并没有销毁，而是重新开辟一块新的空间存储新值。
    - 当程序结束后，GC扫描整个内存，如果发现有空间没有被指向，则立即把它销毁

```csharp
//字符串的不可变性,虽然是引用类型
            string s1 = "张三";
            string s2 = s1;
            s2 = "李四";
//s1为张三，s2为李四
```

![2](https://raw.githubusercontent.com/THENSMASH/Markdown/main/C%23Photo/%E5%AD%97%E7%AC%A6%E4%B8%B21.png)

![3](https://raw.githubusercontent.com/THENSMASH/Markdown/main/C%23Photo/%E5%AD%97%E7%AC%A6%E4%B8%B22.png)

1) 我们可以将字符串看作是char类型的一个只读数组。

   - .ToCharArray();将字符串转化为char数组
   - new string(char[] chs); 能够将char 数组转换为字符串

```csharp
            char[] chs = s.ToCharArray();
            chs[0] = 'b';
            s = new string(chs);
```

大量字符串操作可用 StringBuilder sb = new StringBuilder();

## 字符串提供的各种方法

1) .Length : 获得当前字符串中字符的个数
2) ToUpper() : 将字符转换成大写形式
3) ToLower() : 将字符串转换成小写形式
4) Equals(lessonTwo,stringComparison,OrdinalIgnoreCase) :比较两个字符串
5) 分割字符串，返回字符串类型的数组。
6) Substring() : 解决字符串。在截取的时候包含要截取的那个位置
7) IndexOf() : 判断某个字符串在字符串中第一次出现的位置，如果没有返回-1。
8) LastIndexOf() : 判断某个字符串在字符串中最后一次出现的位置，如果没有同上。
9) StartsWith() : 判断以。。。开始
10) EndWith() : 判断以。。。结束
11) Replace() : 将字符串中某个字符串替换成一个新的字符串。
12) Contains() : 判断某个字符串是否包含指定的字符串
13) Trim() : 去掉字符串中前后的空格
14) TrimEnd() : 去掉字符串中结尾的空格
15) TrimStart() : 去掉字符串中前面的空格
16) string.IsNullOrEmpty() : 判断一个字符串是否为空或者为null
17) stirng.Join() : 将数组按照指定的字符串连接，返回一个字符串

## 继承

我们可能会在一些类中写一些重复的成员，我们可以将这些重复的成员，单独封装到一个类中，作为这些类的父类。

```csharp
    student\teacher\driver 子类  派生类

    Person                 父类  基类
```

子类继承了父类，那么子类从父类那里继承过来了什么?
首先，子类继承了父类的属性和方法，但是子类并没有继承父类的私有字段。
***
**问题**： 子类有没有继承父类的构造函数?

子类没有继承

但是，子类会默认调用父类**无参数的构造函数**，创建父类对象，让子类可以使用父类中的成员
![2](https://raw.githubusercontent.com/THENSMASH/Markdown/main/C%23Photo/%E7%88%B6%E5%AD%90%E7%BB%A7%E6%89%BF1.png)
***
**解决方法** :

1) 在父类中重新写一个无参数的构造函数。
2) 在子类中显示的调用父类的构造函数，使用关键字： `base()`

```c#
//父类中有name,age,gender的构造函数，子类中只需要添加自己的work
public Reporter(string name,int age,char gender,string work):base(name,age,gender)
        {
            this.Work = work; 
        }
```

***

### 继承的特性

1) 继承的单根性 ： 一个子类只能有一个父类
2) 继承的传递性

可以通过查看类图观察

## object 是所有类型基类

## new 关键词

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

## 里氏转换

1) 子类可以赋值给父类 ：如果有一个地方需要一个父类作为参数，我们可以给一个子类代替
2) 如果父类中装的是子类的对象，那么可以讲这个父类强转化为子类对象

```csharp
            Person p = new Reporter();//1
            Reporter ss = (Reporter)p;//2
            ss.ReporterSayHellow();
  ```

- 子类对象可以调用父类的成员，但父类成员永远都只能调用自己的成员

- is ：表示类型转换，如果能够转换成功，则返回一个true,否则返回一个false

- as : 表示类型转换，如果能够转换则返回对应的对象，否则返回一个null

==即使父类中放了子类的对象，里面的元素表现出来的都是父类类型，调用的都是父类自己的成员，父类不能直接调用子类的方法，需要类型强转==

```csharp
            Person p = new Student();
            if(p is Student)
            {
                Student ss = (Student)p;
                ss.Study();
                //转换成功则可输入
            }
            else
            {
                Console.WriteLine("转换失败");
            }

            Teacher t = p as Teacher;
            //转换失败，返回 t 为null
```

## 集合的学习

```csharp
        非泛型集合
            ArrayList
            Hashtable
        泛型集合
            List<T>
            Dictionary<Tkey,Tvalue>
```

### ArrayList集合

每次集合中实际包含的元素个数(count)超过了可以包含的元素的个数(capacity)的时候，集合就会向内存中申请多开辟一倍的空间，来保证集合的长度一直够用。

```csharp
        ArrayList list = new ArrayList();
            Random r = new Random();
            for (int i = 0;i<10;i++)
            {
                int  rNum = r.Next(0, 10);
                if (!list.Contains(rNum))
                {
                    list.Add(rNum);

                }
                else
                {
                    i--;
                }
            }
            
            for(int i = 0; i < list.Count; i++)
            {
                Console.WriteLine(list[i]);
            }

```

### HashTable 键值对集合

在键值对中是根据键找值的

通过 **foreach** 循环 遍历键值

**var ：** 必须有赋值告知其类型

### List<>泛型集合

```csharp
    Add()：添加单个元素
    AddRange():添加一个集合
    Insert():插入一个元素
    InsertRange():插入一个集合
    Remove():移除指定的元素
    RemoveAt():根据下标移除元素
    RemoveRange():移除一定范围内的元素
    ToArray():集合转换成数组
    ToList():数组转换成集合 
```

### 字典

## 装箱和拆箱

装箱 ：值类型---->引用类型

拆箱 ：引用类型--->值类型

>我们判断是否发生了拆箱或者装箱，首先要判断这两种数据类型是否存在继承关系。
>你装箱的时候拿什么类型装的箱，你拆的时候，就得拿什么类型去拆。

## 文件流

将创建文件对象的过程写在using当中，会自动帮助我们释放流所占用的资源。

## 编码格式

```csharp
 将字符串是怎样的形式保存为二进制。
    ascii 256

    6000 GB2312
    GBK  GB18030

    ISO
        Unicode
            utf-16
            utf-8
    出现乱码的原因：我们保存这个文件的时候采取的编码跟打开这个文件的时候采取的编码格式不一致。
```

## 序列化和反序列化

- 序列化 ： 就是将对象转换为二进制

- 反序列化：就是将二进制转换为对象
  
  >作用：传输数据

序列化 ： 将这个类标记为可以被序列化的
