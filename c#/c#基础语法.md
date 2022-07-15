# c#基础语法

## vs中常用快捷键

**Ctrl + K + D :** 快速对齐代码

**Ctrl + Z :** 撤销

**Ctrl + S :** 保存

**Ctrl + J :** 快速弹出智能提示

**#Region 和 #EndRegion :** 折叠冗余代码

## 变量

![](https://raw.githubusercontent.com/THENSMASH/Markdown/main/Photo/%E5%8F%98%E9%87%8F.png)

用来在计算机中存储数据

存储整数
在内存中开辟的空间应该是整数类型 **int**

存储变量的语法：

变量类型 变量名

变量名 = 值

## 数据类型

1）整数类型： int 只能存储整数不能存储小数

2)小数类型: double 既可以存储整数，也可以存储小数，小数点后面的位数15~16位

3）字符串类型 ： string **""**

4）字符类型：char 用来存储单个字符 **''**

5）金钱类型： decimal 用来存储金钱，值后面加一个m

## 调试

1）F11逐句调试

2）F10逐过程调试

3）断点调试

## 变量的使用规则

先声明，再赋值，再使用

## 命名规则

现阶段变量名开头以"字母"_或@符号开头。--不要以数字开头

首先我们要保证的就是变量的名称一定要有意义(就是我们看到了变量的名字，就知道变量在这段程序中的作用)

    1）Camel：多余用给变量或者字段命名，第一个单词的首字母小写，其余每个单词的首字母大写。

    我们给字段命名，前面必须加下划线。
    _highSchoolStudent

    2）Pascal：要求我们每个单词的首字母都要大写，其余每个单词的首字母小写。用于类型名，成员名
    HighSchoolStudent

    int max= GetMax();
    int min= GetMin();

## 符号的作用

= 赋值

+连接两边字符串

占位符
        使用方法: 先挖个坑，再填个坑。

```c#
        int n1 = 10;
        int n2 = 20;
        int n3 = 30;

        Console.WriteLine("第一个数字{0}，第二个数字{1}，第三个数字{2}", n1, n2, n3);
        Console.ReadKey();
```

转义符

        就是指一个'\'+一个特殊的字符，组成了一个具有特殊意义的字符
        \n : 换行
        \" : 一个英文半角的双引号
        \t ：一个tab键的空格
        \b : 退格键,放在字符串的两边没有效果
        \r\n : windows操作系统不认识\n,只认识\r\n
        \\ : 表示一个\

@符号 ：

        1、取消 \ 的转义作用，使其单纯表示一个 \\
        2、将字符串按照原格式输出

## 算数运算符

        + - * / % =
        前++,则先给这个变量自身加一，然后带着这个加一后的值去参与运算
        后++，则先拿原值参与运算，运算完成后，变量自身加一
        --同理

        一元运算符++ -- 比二元的 +- 优先级高

        对于+ - * / % = 都需要两个操作数才能进行运算的这些运算符，我们叫做二元运算符

```c#
        int a = 5;
        int b = a++ + ++a * 2 + --a + a++;
        // 5+7*2+6+6
        //a = 7
        //b = 31
```

## 类型转换

+ 隐式类型转换

我们要求等号两边参与运算的操作数的类型必须一致，如果不一致，满足下列条件会发生自动类型转换，或者称之为隐式类型转换。

        两种类型兼容   如 int 和 double (都是数字类型)
        目标类型大于源类型 如 double > int 小的转大的

+ 显式类型转换
  
        两种类型兼容 int -- double
        大的转成小的 double -- int
        语法 ： 带转换的类型

        总结：
        自动类型转换 ： int --- double
        显式类型转换 ： double --- int

+ 对于表达式 如果一个操作数为double型，则整个表达式可提升为double型

+ 如果两个类型的变量不兼容，可以使用 **Convert.To....** 转换

## bool类型

在c#中我们用bool类型来描述对或错
bool类型的值只有两个 一个true 一个false

## 异常捕获

```c#
        try{

        }
        catch(){

        }
```

## 变量的作用域

声明变量时可以给 int double 类型赋值为0

const 变量名 变量名 = 常量 不能被重新赋值

## 枚举

语法：
```c#
[public] enum 枚举名
{
        值1，
        值2，
        值3，
        、、、、、、、
}
```

将枚举声明到命名空间下面，类的外面，表示这个命名空间下，所有的类都可以使用这个枚举。
枚举就是一个变量类型，int --- double string decimal.
只是枚举声明、赋值、使用的方式跟那些普通的变量类型不一样。

## 结构

可以帮助我们一次性声明多个不同类型的变量

语法:

```c#
[public] struct 结构名
{
        成员;
}
```

## 方法

函数就是将一堆代码进行重用的一种机制

函数的语法：

```c#
[访问修饰符][static]返回值类型 方法名([参数列表])
{
        方法体;
}
```

+ public：访问修饰符，哪都可以访问。

+ static : 静态的

+ 返回值类型 ：如果不需要，写 void

+ 方法名： pascal 

+ 参数列表 ：完成这个方法所需要的条件。

方法写好后，如果想要被执行，必须要在Main()函数中调用。

方法的调用语法 ：

```c#
            类名.方法名([参数]);
//
```
<mark>在某些情况下，类名是可以省略的，如果你写的方法跟Main（）函数同在一个类中</mark>

我们在main()函数中，调用Test()函数,我们管Main()函数称之为调用者,管Test()函数称之为被调用者。

如果被调用者想要得到调用者的值：

+ 1）传递参数
+ 2）设置全局变量
+ 3）返回值

不管是形参还是实参，都在内存中开辟了空间

方法的功能一定要单一

方法中最忌讳的是出现提示用户输入的字眼

## return

1) 在方法中返回要返回的值
2) 立即结束本次方法

## out 的使用

如果你在一个方法中，返回多个相同类型的值的时候，可以考虑返回一个数组。但是，如果返回多个不同类型的值的时候，返回数组就不行了，那么这个时候，我们就可以考虑使用out参数。

out 参数侧重于在一个方法中可以返回多个不同类型的值

## ref 参数

能够将一个变量带入一个方法中进行改变，改变完成后，再将改变后的值带出方法。

ref参数要求方法外必须为其赋值，而方法内可以不赋值。

## params 可变参数

将实参列表中跟可变参数数组类型一致的元素都当作数组元素去处理
params可变参数必须是形参列表中的最后一个元素

## 方法的重载

方法的重载指的就是方法的名称相同，但是参数不同

参数不同，分为两种情况

1）、如果参数的个数相同，那么参数的类型就不能相同

2）、如果参数的类型相同，那么参数的个数就不能相同

方法的重载和返回值无关

## 方法的递归

方法自己调用自己

## 飞行器案例

```c#
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace ConsoleApp4
{
    
    class Program
    {
        public static int[] maps = new int[100];
        public static int[] PlayerPos = new int[2];
        public static string[] PlayerNames = new string[2];
        public static bool[] Flags = new bool[2];


        static void Main(string[] args)
        {


            #region 输入玩家姓名
            Console.ForegroundColor = ConsoleColor.DarkMagenta;
            Console.WriteLine("请输入玩家姓名");
            PlayerNames[0] = Console.ReadLine();

            while (PlayerNames[0] == "")
            {
                Console.WriteLine("玩家A的姓名不能为空，请重新输入");
                PlayerNames[0] = Console.ReadLine();
            }
            PlayerNames[1] = Console.ReadLine();
            while (PlayerNames[1] == "" || PlayerNames[1] == PlayerNames[0])
            {
                if (PlayerNames[1] == "")
                {
                    Console.WriteLine("玩家B的姓名不能为空，请重新输入");
                    PlayerNames[1] = Console.ReadLine();
                }
                else
                {
                    Console.WriteLine("玩家B的姓名不能玩家A的形容，请重新输入");
                    PlayerNames[1] = Console.ReadLine();
                }
            }
            #endregion
            //玩家输入姓名后清零
            Console.Clear();
            GameShow();

            InitialMap();

            Console.WriteLine("{0}的士兵用A表示", PlayerNames[0]);
            Console.WriteLine("{0}的士兵用B表示", PlayerNames[1]);

            DrawMap();

            while (PlayerPos[0] < 99 && PlayerPos[1] < 99)
            {
                StarGame(0);
                StarGame(1);
                if (PlayerPos[0] >= 99)
                {
                    Console.WriteLine("玩家{0}无耻的赢了玩家{1}", PlayerNames[0], PlayerNames[1]);
                    break;
                }
               
                if (PlayerPos[1] >= 99)
                {
                    Console.WriteLine("玩家{0}无耻的赢了玩家{1}", PlayerNames[1], PlayerNames[0]);
                    break;
                }
            }
            Console.WriteLine("胜利！");
            Console.ReadKey();
        }

        public static void StarGame(int playnum)
        {

            Random r = new Random();
            int rNumber = r.Next(1, 7);
           

                Console.WriteLine("{0}按任意键开始掷骰子", PlayerNames[playnum]);
                Console.ReadKey(true);
                Console.WriteLine("{0}掷出了{1}", PlayerNames[playnum],rNumber);
                PlayerPos[playnum] += rNumber;
                ChangePos();
                Console.ReadKey(true);
                Console.WriteLine("{0}按任意键开始行动", PlayerNames[playnum]);
                Console.ReadKey(true);
                Console.WriteLine("{0}行动完了", PlayerNames[playnum]);
                Console.ReadKey(true);
                //玩家A有可能踩到了玩家B 方块 幸运轮盘 地雷 暂停 时空隧道
                if (PlayerPos[playnum] == PlayerPos[1- playnum])
                {
                    Console.WriteLine("玩家{0}踩到了玩家{1}，玩家{2}退6格", PlayerNames[playnum], PlayerNames[1- playnum],PlayerNames[1 - playnum]);
                    PlayerPos[1- playnum] -= 6;
                    ChangePos();
                Console.ReadKey(true);
                }
                else
                {
                    switch (maps[PlayerPos[playnum]])
                    {
                        case 0:
                            Console.WriteLine("玩家{0}踩到了方块，安全");
                            break;
                        case 1:
                            Console.WriteLine("玩家{0}踩到了幸运轮盘，请选择 1--交换位置 2--轰炸对方");
                            string input = Console.ReadLine();
                            while (true)
                            {
                                if (input == "1")
                                {
                                    Console.WriteLine("玩家{0}选择跟玩家{1}交换位置", PlayerNames[playnum], PlayerNames[1- playnum]);
                                    Console.ReadKey(true);
                                    int temp = PlayerPos[playnum];
                                    PlayerPos[playnum] = PlayerPos[1- playnum];
                                    PlayerPos[1- playnum] = temp;
                                    Console.WriteLine("交换完成！！！按任意键继续游戏！！！");
                                    Console.ReadKey(true);
                                    break;
                                }
                                else if (input == "2")
                                {
                                    Console.WriteLine("玩家{0}轰炸玩家{1}，玩家{2}退6格", PlayerNames[playnum], PlayerNames[1- playnum], PlayerNames[1- playnum]);
                                    PlayerPos[1] -= 6;
                                    ChangePos();
                                    Console.WriteLine("玩家{0}退格成功", PlayerNames[1- playnum]);
                                    Console.ReadKey(true);
                                    break;
                                }
                            else
                            {
                                Console.WriteLine("只能输入1或者2");
                                input = Console.ReadLine();
                                
                            }
                            }
                            break;
                        case 2:
                            Console.WriteLine("玩家{0}踩到了暂停", PlayerNames[playnum]);
                        Flags[playnum] = true;
                        if (Flags[playnum] == true)
                        {
                           
                            StarGame(1-playnum);
                        }
                        Flags[playnum] = false;

                        Console.ReadKey(true);
                            break;
                        case 3:
                            Console.WriteLine("玩家{0}踩到了时空隧道", PlayerNames[playnum]);
                            PlayerPos[playnum] += 10;
                            ChangePos();
                            Console.WriteLine("玩家{0}成功前进6", PlayerNames[playnum]);
                            break;

                    }
                }
            ChangePos();
            Console.Clear();
            DrawMap();
        }
        
        public static void ChangePos()
        {
            if(PlayerPos[0] < 0)
            {
                PlayerPos[0] = 0;
            }
            if(PlayerPos[0] >= 99)
            {
                PlayerPos[0] = 99;
            }
            if (PlayerPos[1] < 0)
            {
                PlayerPos[1] = 0;
            }
            if (PlayerPos[1] >= 99)
            {
                PlayerPos[1] = 99;
            }
        }

        public static void GameShow()
        {
            Console.ForegroundColor = ConsoleColor.Blue;
            Console.WriteLine("******************************************");
            Console.WriteLine("******************************************");
            Console.WriteLine("******************************************");
            Console.ForegroundColor = ConsoleColor.Red;
            Console.WriteLine("*****************飞行棋*******************");
            Console.ForegroundColor = ConsoleColor.Yellow;
            Console.WriteLine("******************************************");
            Console.WriteLine("******************************************");
            Console.WriteLine("******************************************");
        }

        public static void InitialMap()
        {
            int[] luckyturn = { 6,23,40,55,69,83};
            for(int i = 0; i< luckyturn.Length; i++)
            {
                //int index = luckyturn[i];
                maps[luckyturn[i]] = 1;
            }
            int[] landMine = { 5, 13, 17, 33, 38, 50, 64, 80, 94 };
            for(int i = 0; i < landMine.Length; i++)
            {
                maps[landMine[i]] = 2;
            }
            int[] pause = { 9, 27, 60, 93 };
            for(int i = 0;i<pause.Length;i++)
            {
                maps[pause[i]] = 3;
            }
            int[] timeTunnel = { 20, 25, 45, 63, 72, 88, 90 };
            for (int i = 0; i < timeTunnel.Length; i++)
            {
                maps[timeTunnel[i]] = 4;
            }
        }

        public static void DrawMap()
        {
            #region 第一横行
            for (int i = 0; i < 30; i++)
            {
                //如果玩家A与玩家B的坐标相同，并且都在这个地图上，画一个尖括号
                Console.Write(DrawStringMap(i));
            }
            Console.WriteLine();
            #endregion

            #region 第一竖行
            for (int i = 30; i < 35; i++)
            {
                for (int j = 0; j <= 28; j++)
                {
                    Console.Write("  ");

                }
                Console.WriteLine(DrawStringMap(i));
                
            }
            #endregion

            #region 第二横行
            for (int i = 64; i >= 35; i--)
            {
                Console.Write(DrawStringMap(i));
            }
            Console.WriteLine();
            #endregion

            #region 第二竖行
            for (int i = 65; i <= 69; i++)
            {
                Console.Write(DrawStringMap(i));
                Console.WriteLine();
            }
            #endregion

            #region 第三横行
            for (int i = 70; i <= 99; i++)
            {
                Console.Write(DrawStringMap(i));
            }
            #endregion
            Console.WriteLine();
        }

        public static string DrawStringMap(int i)
        {
            string str = "";
            //如果玩家A与玩家B的坐标相同，并且都在这个地图上，画一个尖括号
            if (PlayerPos[0] == PlayerPos[1] && PlayerPos[1] == i)
            {
                Console.ForegroundColor = ConsoleColor.Green;
                str = "<>";
            }
            else if (PlayerPos[0] == i)
            {
                str = "A";
            }
            else if (PlayerPos[1] == i)
            {
                str = "B";
            }
            else
            {
                switch (maps[i])
                {
                    case 0:
                        Console.ForegroundColor = ConsoleColor.Blue;
                        str = "□";
                        break;
                    case 1:
                        Console.ForegroundColor = ConsoleColor.Red;
                        str = "◎";
                        break;
                    case 2:
                        Console.ForegroundColor = ConsoleColor.Yellow;
                        str = "☆";
                        break;
                    case 3:
                        Console.ForegroundColor = ConsoleColor.White;
                        str = "▲";
                        break;
                    case 4:
                        Console.ForegroundColor = ConsoleColor.Cyan;
                        str = "ψ";
                        break;

                }
                
            }
            return str;
        }
    }
}
```