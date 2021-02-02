面向对象的程序设计中，程序由各种相互交互的对象组成。

### using关键字

using关键字用来在程序中包含命名空间

### class关键字

class关键字用来声明一个类

### 成员变量

类的属性或数据成员，用来存储数据

### 成员函数

类内声明的函数

# 第1章、变量

## 1.1、数据类型

### 1.1.1、类型分类（按变量）

变量只是供程序操作存储器的名字，而类型决定了变量的空间大小和布局，以及可以对变量进行的一系列操作。

| 1    | 值类型（value types）       |
| ---- | --------------------------- |
| 2    | 引用类型（reference types） |
| 2    | 指针类型（pointer types）   |

### 1.1.2、值类型（value types）

值类型变量时可以直接分配一个值，他们是从System.ValueType中派生。

| 别名    | 类型 | 描述                                 | 范围                                                    | 默认值 |
| ------- | ---- | ------------------------------------ | ------------------------------------------------------- | ------ |
| bool    |      | 布尔值                               | true或false                                             | false  |
| byte    |      | 8 位无符号整数                       | 0 到 255                                                | 0      |
| sbyte   |      | 8 位有符号整数类型                   | -128 到 127                                             | 0      |
| char    |      | 16 位 Unicode 字符                   | U +0000 到 U +ffff                                      | '\0'   |
| short   |      | 16 位有符号整数类型                  | -32,768 到 32,767                                       | 0      |
| ushort  |      | 16 位无符号整数类型                  | 0 到 65,535                                             | 0      |
| int     |      | 32 位有符号整数类型                  | -2,147,483,648 到 2,147,483,647                         | 0      |
| uint    |      | 32 位无符号整数类型                  | 0 到 4,294,967,295                                      | 0      |
| long    |      | 64 位有符号整数类型                  | -9,223,372,036,854,775,808 到 9,223,372,036,854,775,807 | 0L     |
| ulong   |      | 64 位无符号整数类型                  | 0 到 18,446,744,073,709,551,615                         | 0      |
| float   |      | 32 位单精度浮点型                    | -3.4 x 1038 到 + 3.4 x 1038                             | 0.0F   |
| double  |      | 64 位双精度浮点型                    | (+/-)5.0 x 10-324 到 (+/-)1.7 x 10308                   | 0.0D   |
| decimal |      | 128 位精确的十进制值，28-29 有效位数 | (-7.9 x 1028 到 7.9 x 1028) / 100 到 28                 | 0.0M   |
|         |      |                                      |                                                         |        |

若需要得到类型或变量在某一平台上的准确大小，可使用sizeof（type）方法产生以字节文单位的存储对象或类型的存储尺寸

```c#
using System ;
namespace DataTypeApp{
    class Program{
     	static void Main(string[] args){
            Console.WriteLine("Size of the int type size is :{0}",sizeof(int)) ;
            Console.ReadKey() ;
        }   
    }    
}
```

### 1.1.3、引用类型（reference type）

引用类型不包含存储在变量中的实际数据，但他们包含对变量的引用。即（引用类型指定是一个内存位置，当使用多个变量时，引用类型可以指向一个内存位置，若该内存位置的数据通过一个变量修改时，其他的变量会自动反映出这个值的变化）。

内置的引用类型有3个：object（System.Object)、dynamic、string(System.String)

用户自定义的引用类型有：class、interface、delegate

1、对象（object）类型

```c#
//对象（object）类型是C#通用类型系统(Common Type System,CTS)中所有数据类型的终极基类。所以对象（object）类型可以被分配任何其他类型的值（值类型、引用类型、预定义类型、用户自定义类型）。但是，在分配值之前需要先进行类型转换。
//当一个值类型转换成对象类型时被称为装箱，反之，当一个对象类型转换为值类型时称为拆箱：如
Object obj ;
obj = 100 ;		//	这就是装箱
```

2、动态（dynamic）类型

```c#
//动态类型变量中可以存储任何类型的值。动态类型与对象类型相似，但是对象类型变量的类型检查发生在编译时，而动态类型变量的类型检查发生在运行时
//动态类型的语法格式如下：
dynamic  <variable_name>  = value ;
//例如：
dynamic  d = 100 ;
```

3、字符串（string）类型

```c#
//字符串（string）类型允许分配任何字符串值。他是从对象（object）类型派生。
//字符串类型的值可以通过两种形式进行分配：引号和@引号

//1、双引号
String  str = "hello world!" ;

//2、@引号（也称逐字字符串）：将转义字符\也作为普通字符串对待，除“号外其他的换行符及缩进空格都计算在字符串长度之内
String  str = @"c:\windows" ; 
//等价于
String  str = "c:\\windows"
string  str = @"<hell world

> !" ;
```

### 1.1.4、指针类型（pointer types）

指针类型变量存储另一种类型的内存地址，C#中的指针与C++中的指针功能相同（在不安全代码章节，详细讨论指针类型）

```c
//指针类型的声明语法
type*  identifier ;
//例如
char *cptr ;
int  *iptr ;
```

## 1.2、类型转换

### 1.2.1、类型转换形式分类

类型转换从根本上是类型铸造。将数据从一种类型转换成另一种类型

| 隐式类型转换 | 默认的以安全方式进行的转换，不会导致数据丢失。如：从派生类转换为基类，从小整数类型转换为大整数类型 |
| ------------ | ------------------------------------------------------------ |
| 显示类型转换 | 即：强制类型转换，显示类型转换需要强制转换运算符，而且会造成数据丢失 |

```c#
//举例一个显式的类型转换
namespace TypeConversionAPP{
    class ConversionTest{
        static void Main(string[] args){
            double num = 3.33 ;
            int i  ;
            
            i = (int)num ;
            System.Console.WriteLine(i) ;
            System.Console.ReadKey();
        }
    }
}
//执行结果是：3
```

### 1.2.2、常用内置类型转换方法

| 序号 | 方法       | 描述                                          |
| ---- | ---------- | --------------------------------------------- |
| 1    | ToBoolean  | 若可能的话，将类型转换成布尔型                |
| 2    | ToByte     | 把类型转换为字节类型                          |
| 3    | ToSbyte    | 把类型转换成有符号字节类型                    |
| 4    | ToChar     | 若可能的话，将类型转换为单个Unicode字符类型   |
| 5    | ToDateTime | 把类型（整数或字符串类型）转换为日期-时间结构 |
| 6    | ToDecimal  | 把浮点型或整数类型转换为10进制类型            |
| 7    | ToDouble   | 把类型转换为双精度浮点型                      |
| 8    | ToInt16    | 把类型转换为16位整数类型                      |
| 9    | ToInt32    | 把类型转换为32位整数类型                      |
| 10   | ToInt64    | 把类型转换为64位整数类型                      |
| 11   | ToSingle   | 把类型转换成小浮点数类型                      |
| 12   | ToString   | 把类型转换为字符串类型                        |
| 13   | ToType     | 把类型转换为指定的类型                        |
| 14   | ToUint16   | 把类型转换为16位无符号整数类型                |
| 15   | ToUint32   | 把类型转换为32位无符号整数类型                |
| 16   | ToUint64   | 把类型转换为64位无符号整数类型                |

## 1.3、标识符

### 1.3.1、标识符命名规则

必须以字母、下划线或@开头

### 1.3.2、关键字总体表格

1、保留关键字

关键字是C#编译器预定义的保留字，不能用作标识符。但若要将其作为标识符，可加前缀@

| abstract  | as                    | base     | bool     | break      |
| --------- | --------------------- | -------- | -------- | ---------- |
| byte      | case                  | catch    | char     | checked    |
| class     | const                 | continue | decimal  | default    |
| delegate  | do                    | double   | else     | enum       |
| event     | explicit              | extern   | false    | finally    |
| fixed     | float                 | for      | foreach  | goto       |
| if        | in(generic modifier)  | in       | implicit | int        |
| interface | internal              | is       | lock     | long       |
| namespace | new                   | null     | object   | operator   |
| out       | out(generic modifier) | override | params   | private    |
| protected | public                | readonly | ref      | return     |
| sbyte     | sealed                | short    | sizeof   | stackalloc |
| static    | string                | struct   | switch   | this       |
| throw     | true                  | try      | typeof   | uint       |
| ulong     | unchecked             | unsafe   | ushort   | using      |
| virtual   | void                  | volatile | while    |            |

2、上下文关键字

有些关键字在代码上下文中有特殊意义

| add    | alias  | ascending | descending    | dynamic          |
| ------ | ------ | --------- | ------------- | ---------------- |
| from   | get    | global    | group         | into             |
| join   | let    | orderby   | partial(type) | partical(method) |
| remove | select | set       |               |                  |

## 1.4、常量

常量可被看成常规的变量，只是他们的值在定义之后就不能再被修改

### 1.4.1、整数常量

整数常量可以是十进制、八进制或十六进制。前缀指定基数：0x 或 0X 表示十六进制，0 表示八进制，没有前缀则表示十进制。

整数常量也可以有后缀，可以是U（unsigned）和L（long）的组合 。后缀可以是大写或者小写，多个后缀以任意顺序进行组合

```c#
211			//合法
215u		//合法
0xFeeL		//合法
078			//非法，8不是一个八进制数字
032UU		//非法，不能重复后缀
```

```c#
85			//十进制
0213		//八进制
0x46		//十六进制
    
30			//int
30u			//无符号 int
30l			//long
30ul		//无符号long
```

### 1.4.2、浮点常量

使用小数形式表示时，必须包含小数点、指数或两者同时包含。

使用指数形式表示时，必须包含整数部分、小数部分或两者同时包含。

有符号的指数是用e或E表示的

```c#
3.14159			//合法
314159E-5L		//合法
510E			//非法，不完全指数
210f			//非法，没有小数或指数
.e55			//非法，缺少整数或小数
```

### 1.4.3、字符常量

字符常量是括在单引号中且可以存储在一个简单的字符类型变量中。

一个字符常量可以是：一个普通字符（如‘x’)、一个转义字符（如‘\t）’、或一个通用字符（如‘\u02c0’）

### 1.4.4、字符串常量

字符串常量是括在双引号“ ”或者@" "中。可以包含：普通字符、转义序列、通用字符

```c#
string a = "hello, world";                  // hello, world
string b = @"hello, world";               // hello, world
string c = "hello \t world";               // hello     world
string d = @"hello \t world";               // hello \t world
string e = "Joe said \"Hello\" to me";      // Joe said "Hello" to me
string f = @"Joe said ""Hello"" to me";   // Joe said "Hello" to me
string g = "\\\\server\\share\\file.txt";   // \\server\share\file.txt
string h = @"\\server\share\file.txt";      // \\server\share\file.txt
string i = "one\r\ntwo\r\nthree";
string j = @"one
two
three";
```

1.4.5、定义常量

使用const关键字来定义，语法格式为：const   <data_type>   <constant_name>  =  value

```c#
using System;

public class ConstTest{
    class SampleClass{
        public int x,y;      
        public const int c1 = 5;
        public const int c2 = c1 + 5;

        public SampleClass(int p1, int p2){
            x = p1;
            y = p2;
        }
    }

    static void Main(){
        SampleClass mC = new SampleClass(11, 22);
        Console.WriteLine("x = {0}, y = {1}", mC.x, mC.y);
        Console.WriteLine("c1 = {0}, c2 = {1}",SampleClass.c1, SampleClass.c2);
    }
}
//执行结果
x = 11, y = 22
c1 = 5, c2 = 10
```

## 1.5、运算符

运算符是一种告诉编译器执行特定的数学或逻辑操作的符号

### 1.5.1、算术运算符

+

-

*

/

%

++

--

### 1.5.2、关系运算符

==

!=

＞

＜

＞=

＜=

### 1.5.3、逻辑运算符

&&

||

！

### 1.5.4、位运算符

位运算符作用于位，并逐位执行操作； & 、| 、^ 、~ 、<< 、>>

| 运算符 | 描述             | 示例                             |
| ------ | ---------------- | -------------------------------- |
| &      | 按位与           | 60 & 13，结果为12                |
| \|     | 按位或           | 60 \| 13，结果为61               |
| ^      | 按位异或         | 60 ^ 13，结果为49                |
| ~      | 按位取反(一元)   | A=60，~A结果为-61，即11000011    |
| <<     | 二进制左移运算符 | A=60，A <<2结果为240，即11110000 |
| >>     | 二进制右移运算符 | A=60，A >>2结果为15，即00001111  |

### 1.5.5、赋值运算符

| 运算符 | 描述 |
| ------ | ---- |
| =      |      |
| +=     |      |
| -=     |      |
| *=     |      |
| /=     |      |
| %=     |      |
| <<=    |      |
| \>>=   |      |
| &=     |      |
| ^=     |      |
| \|=    |      |

### 1.5.6、其他运算符

| 运算符     | 描述                                 | 示例                                           |
| ---------- | ------------------------------------ | ---------------------------------------------- |
| sizeof（） | 返回数据类型的存储字节数量           | sizeof（int），返回4                           |
| typeof（） | 返回class的类型                      | typeof(StreamReadre)                           |
| &          | 返回变量的地址                       | &a，将得到变量a的实际地址                      |
| *          | 变量的指针                           | *a,将指向一个变量                              |
| ？ ：      | 条件表达式                           | 如果条件为真？则为X：否则为Y                   |
| is         | 判读对象是否为某一类型               | if(Ford is Car)//检查Ford是否是Car类的一个对象 |
| as         | 强制转换，即使转换失败也不会抛出异常 | Object obj = new StringReader("Hello");        |
|            |                                      | StringReader  r = ojb  as  StringReader        |

### 1.5.7、运算符优先级

| 类别       | 运算符                                          | 结合性   |
| ---------- | ----------------------------------------------- | -------- |
| 后缀       | () 、 [] 、 -> 、 .  、 ++  、- -               | 从左到右 |
| 一元       | +、 - 、! 、~、 ++ 、- - 、(type)* 、&、 sizeof | 从右到左 |
| 乘除       | * / %                                           | 从左到右 |
| 加减       | + -                                             | 从左到右 |
| 移位       | << >>                                           | 从左到右 |
| 关系       | < <= > >=                                       | 从左到右 |
| 相等       | == !=                                           | 从左到右 |
| 位与 AND   | &                                               | 从左到右 |
| 位异或 XOR | ^                                               | 从左到右 |
| 位或 OR    | \|                                              | 从左到右 |
| 逻辑与 AND | &&                                              | 从左到右 |
| 逻辑或 OR  | \|\|                                            | 从左到右 |
| 条件       | ?:                                              | 从右到左 |
| 赋值       | = += -= *= /= %=>>= <<= &= ^= \|=               | 从右到左 |
| 逗号       | ,                                               | 从左到右 |

## 封装的概念

封装被定义为“把一个或多个项目封闭在一个物理或逻辑包中”。为了防止对实现细节的访问。

C#封装根据具体的需要，设置使用者的访问权限，并通过访问修饰符来实现。

| 访问修饰符         |                                        |
| ------------------ | -------------------------------------- |
| public             | 所有对象都可以访问                     |
| private            | 对象本身在对象内部可以访问             |
| protected          | 只有该类的对象及其子类的对象可以访问   |
| internal           | 同一个程序集的对象可以访问             |
| protected internal | 访问限于当前程序集或派生自包含类的类型 |

### public访问修饰符

public访问修饰符允许一个类将其成员变量和成员函数暴露给其他的函数和对象，任何公有成员都可以被外部的类访问

```c#
using System;

namespace RectangleApplication{
    class Rectangle{
        public double length;
        public double width;

        public double GetArea(){
            return length * width;
        }
        
        public void Display(){
            Console.WriteLine("长度： {0}", length);
            Console.WriteLine("宽度： {0}", width);
            Console.WriteLine("面积： {0}", GetArea());
        }
    }

    class ExecuteRectangle{
        static void Main(string[] args){
            Rectangle r = new Rectangle();
            r.length = 4.5;
            r.width = 3.5;
            r.Display();
            Console.ReadLine();
        }
    }
}
//成员变量 length 和 width 被声明为 public，所以它们可以被函数 Main() 使用 Rectangle 类的实例 r 访问
//成员函数 Display() 也被声明为 public，所以它也能被 Main() 使用 Rectangle 类的实例 r 访问
```

### private访问修饰符

Private 访问修饰符允许一个类将其成员变量和成员函数对其他的函数和对象进行隐藏。

只有同一个类中的函数可以访问它的私有成员。即使是类的实例也不能访问它的私有成员

```c#
using System;

namespace RectangleApplication{
    class Rectangle{
        private double length;
        private double width;

        public void Acceptdetails(){
            Console.WriteLine("请输入长度：");
            length = Convert.ToDouble(Console.ReadLine());
            Console.WriteLine("请输入宽度：");
            width = Convert.ToDouble(Console.ReadLine());
        }
        public double GetArea(){
            return length * width;
        }
        public void Display(){
            Console.WriteLine("长度： {0}", length);
            Console.WriteLine("宽度： {0}", width);
            Console.WriteLine("面积： {0}", GetArea());
        }
    }//end class Rectangle  
    
    class ExecuteRectangle{
        static void Main(string[] args){
            Rectangle r = new Rectangle();
            r.Acceptdetails();
            r.Display();
            Console.ReadLine();
        }
    }
}
//成员变量 length 和 width 被声明为 private，所以它们不能被函数 Main() 访问
//成员函数 AcceptDetails() 和 Display() 可以访问这些变量
//成员函数 AcceptDetails() 和 Display() 被声明为 public，所以它们可以被 Main() 使用 Rectangle 类的实例 r 访问
```

### protected访问修饰符

Protected 访问修饰符允许子类访问它的基类的成员变量和成员函数。这样有助于实现继承

### internal访问修饰符

Internal 访问说明符允许一个类将其成员变量和成员函数暴露给当前程序中的其他函数和对象。换句话说，带有 internal 访问修饰符的任何成员可以被定义在该成员所定义的应用程序内的任何类或方法访问

```c#
using System;

namespace RectangleApplication{
    class Rectangle{
        internal double length;
        internal double width;
       
        double GetArea({
            return length * width;
        }
       public void Display(){
            Console.WriteLine("长度： {0}", length);
            Console.WriteLine("宽度： {0}", width);
            Console.WriteLine("面积： {0}", GetArea());
        }
    }//end class Rectangle  
                       
    class ExecuteRectangle{
        static void Main(string[] args){
            Rectangle r = new Rectangle();
            r.length = 4.5;
            r.width = 3.5;
            r.Display();
            Console.ReadLine();
        }
    }
}
//请注意成员函数 GetArea() 声明的时候不带有任何访问修饰符。如果没有指定访问修饰符，则使用类成员的默认访问修饰符，即为 private
```

### protected internal

Protected Internal 访问修饰符允许在本类,派生类或者包含该类的程序集中访问。这也被用于实现继承

## 方法

### 方法的定义语法格式

```c#
<Access Specifier>  <Return type>  <Method name> (parameter  list){
    method Body
}
```

### 递归方法

一个方法可以自我调用，即所谓的递归。示例：实现一个数的阶乘：

```c#
using System;

namespace CalculatorApplication{
    class NumberManipulator{
        public int factorial(int num){
            /* 局部变量定义 */
            int result;

            if (num == 1){
                return 1;
            }
            else{
                result = factorial(num - 1) * num;
                return result;
            }
        }
   
        static void Main(string[] args){
            NumberManipulator n = new NumberManipulator();
            //调用 factorial 方法
            Console.WriteLine("6 的阶乘是： {0}", n.factorial(6));
            Console.WriteLine("7 的阶乘是： {0}", n.factorial(7));
            Console.WriteLine("8 的阶乘是： {0}", n.factorial(8));
            Console.ReadLine();
        }
    }
}
//执行结果：
//6 的阶乘是： 720
//7 的阶乘是： 5040
//8 的阶乘是： 40320
```

### 方法的3种参数传递方式

| 参数传递方式    | 描述                                                         |
| --------------- | ------------------------------------------------------------ |
| 按值传递参数    | 复制参数的实际值给函数的形式参数，实参和形参使用的是两个不同内存中的值，当形参的值发生改变时，不会影响实参的值，从而保证了实参数据的安全。 |
| 按引用传递参数  | 复制参数的内存位置的引用给形式参数，即，当形参的值发生改变时，同时也会改变实参的值 |
| 按输出c传递参数 | 可以返回多个值                                               |

1、按值传递参数

```c#
using System;
namespace CalculatorApplication{
   class NumberManipulator{
      public void swap(int x, int y){
         int temp;
         
         temp = x; /* 保存 x 的值 */
         x = y;    /* 把 y 赋值给 x */
         y = temp; /* 把 temp 赋值给 y */
      }
     
      static void Main(string[] args){
         NumberManipulator n = new NumberManipulator();
         /* 局部变量定义 */
         int a = 100;
         int b = 200;
         
         Console.WriteLine("在交换之前，a 的值： {0}", a);
         Console.WriteLine("在交换之前，b 的值： {0}", b);
         
         /* 调用函数来交换值 */
         n.swap(a, b);
         
         Console.WriteLine("在交换之后，a 的值： {0}", a);
         Console.WriteLine("在交换之后，b 的值： {0}", b);
         
         Console.ReadLine();
      }
   }
}
//执行结果
在交换之前，a 的值：100
在交换之前，b 的值：200
在交换之后，a 的值：100
在交换之后，b 的值：200
```

2、按引用传递参数

```c#
using System;
namespace CalculatorApplication
{
   class NumberManipulator{
      public void swap(ref int x, ref int y){
         int temp;

         temp = x; /* 保存 x 的值 */
         x = y;    /* 把 y 赋值给 x */
         y = temp; /* 把 temp 赋值给 y */
       }
   
      static void Main(string[] args) {
         NumberManipulator n = new NumberManipulator();
         /* 局部变量定义 */
         int a = 100;
         int b = 200;

         Console.WriteLine("在交换之前，a 的值： {0}", a);
         Console.WriteLine("在交换之前，b 的值： {0}", b);

         /* 调用函数来交换值 */
         n.swap(ref a, ref b);

         Console.WriteLine("在交换之后，a 的值： {0}", a);
         Console.WriteLine("在交换之后，b 的值： {0}", b);
 
         Console.ReadLine();

      }
   }
}
//执行结果
在交换之前，a 的值：100
在交换之前，b 的值：200
在交换之后，a 的值：200
在交换之后，b 的值：100
```

3、按输出传递参数

return语句可用来只从函数中返回一个值，但是，可以使用输出参数来从函数中返回两个值。

输出参数会把方法输出的数据赋给自己，其他方面与引用参数相似

```c#
using System;

namespace CalculatorApplication
{
   class NumberManipulator
   {
      public void getValue(out int x )
      {
         int temp = 5;
         x = temp;
      }
   
      static void Main(string[] args)
      {
         NumberManipulator n = new NumberManipulator();
         /* 局部变量定义 */
         int a = 100;
         
         Console.WriteLine("在方法调用之前，a 的值： {0}", a);
         
         /* 调用函数来获取值 */
         n.getValue(out a);

         Console.WriteLine("在方法调用之后，a 的值： {0}", a);
         Console.ReadLine();

      }
   }
}
//执行结果：
在方法调用之前，a 的值： 100
在方法调用之后，a 的值： 5
```

提供给输出参数的变量不需要赋值。当需要从一个参数没有指定初始值的方法中返回值时，输出参数特别有用

```c#
using System;

namespace CalculatorApplication
{
   class NumberManipulator
   {
      public void getValues(out int x, out int y )
      {
          Console.WriteLine("请输入第一个值： ");
          x = Convert.ToInt32(Console.ReadLine());
          Console.WriteLine("请输入第二个值： ");
          y = Convert.ToInt32(Console.ReadLine());
      }
   
      static void Main(string[] args)
      {
         NumberManipulator n = new NumberManipulator();
         /* 局部变量定义 */
         int a , b;
         
         /* 调用函数来获取值 */
         n.getValues(out a, out b);

         Console.WriteLine("在方法调用之后，a 的值： {0}", a);
         Console.WriteLine("在方法调用之后，b 的值： {0}", b);
         Console.ReadLine();
      }
   }
}
//执行结果
请输入第一个值：
7
请输入第二个值：
8
在方法调用之后，a 的值： 7
在方法调用之后，b 的值： 8
```

可空类型（Nullable）

单问号？用来对int、double、bool等无法直接赋值为null的数据类型进行null的复制

```c#
int?  i=3 ;
//等同于
Nullable<int>  i = new  Nullable<int>(3) ;

int i ;		//默认值为0
int? i ;	//默认值为null
```

双问号??，用来判断一个变量在为null时返回一个指定的值



C#提供了一个特殊的数据类型，Nullable类型（可空类型），可空类型可以表示其基础类值类型正常范围内的值，再加上一个null值

例如：Nullable<Int32>,读作“可空的Int32”，可以被赋值为 -2,147,483,648 到 2,147,483,647 之间的任意值，也可以被赋值为 null 值

类似的，Nullable< bool > 变量可以被赋值为 true 或 false 或 null。

在处理数据库和其他包含可能未赋值的元素的数据类型时，将 null 赋值给数值类型或布尔型的功能特别有用。例如，数据库中的布尔型字段可以存储值 true 或 false，或者，该字段也可以未定义

