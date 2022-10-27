[toc]



# Java核心技术 小记

> Java是世界上最好的语言。
>
> ​                                                                                                                                                                ——鲁迅
>
> <img src="https://pics4.baidu.com/feed/a8014c086e061d95951cb88dd06216db63d9ca4a.png@f_auto?token=33b34cc3046836828188561da1a11ffb" alt="img" style="zoom: 50%;" />
>
> 
>
> ​                                                                                                                                                          

## Chapter 3 Java的基本程序设计结构

### 基本

#### 定义类名

- 名字必须以字母开头，后面跟字母和数字组合，长度无限制。不能用保留字。

- 类名以大写字母开头，多个单词组成每个单词第一个字母大写。（骆驼命名法）

- 源代码的文件名必须与**公共类**的名字相同。

  

#### 注释

- //用于**单行注释**。
- /*        */用于比较长的注释。
- /**    */用来自动生成文档。



####  数据类型



:key:Java中一共有8种基本类型。4种整型，2种浮点类型，1种用于表示Unicode编码的字符单元的字符类型char，一种表示真值的boolean



##### 整型

> 整型用于表示没有小数部分的数值。







### 字符串:key:



> 从概念上讲，Java字符串就是Unicode字符序列。



Java提供了一个预定义类:**String**



#### 字符串的子串



>  String类的substring方法可以提取出一个子串。



```java
String substring(int beginIndex)
String substring(int beginIndex,int endIndex)    
```

:warning:该方法返回的新字符串是从beginIndex到串尾，或者到**endIndex-1!!!!!**



#### 拼接



> Java语言允许使用 + 号连接两个字符串。



:warning: 当将一个字符串与一个非字符串的值进行拼接时，会将非字符串转换成为字符串。



:key: 如果需要把多个字符串放在一起，用一个定界符分隔，可以使用**静态join方法**。

``` java
String all = String.join("/","S","M","L","XL");
// all is the string "S/M/L/XL"
```



#### 不可变字符串

> String类没有提供用于**修改**字符串的方法。在Java文档中将String类对象称为**不可变字符串**。



:key:**优点** :arrow_down_small:



编译器可以让字符串共享。



#### 检测是否相等



> 使用equals方法检测两个字符串是否相等。



```java
s.equals(t)
```

如果s与t相等，则返回true;否则返回false。

:warning:

- s,t可以是字符串变量，也可以是字符串字面量。

如：

```
"Hello".equals(greeting)
```

检测两个字符串是否相等，而不区分大小写，则使用***equalsIgnoreCase***方法。

- **一定不要**使用**==**检测两个字符串是否相等，这个运算符只能确定两个字符串是否放置在同一个位置上。

 :arrow_forward:字符串位置相同，必然相等。内容相同的字符串拷贝可能被放在不同位置上。



#### 空串与null



空串""是长度为0的字符串，有自己的串长度(0)和内容（空）。



null表示目前没有任何对象和该变量关联。



#### 构建字符串



> 有些时候，需要由较短的字符串构建字符串。



:warning:采用字符串连接的方式效率较低，**每次**连接字符串，都会构建新的String对象。



因此，使用StringBuilder类。

常用API如下:arrow_double_down:

```java
StringBuilder() //构造一个空的字符串构造器
int length() //返回构建器或缓冲器中的代码单元数量
StringBuilder append(String str)//追加一个字符串并返回this
String toString()//返回一个与构建器或缓冲器内容相同的字符串
StringBuilder insert(int offset,String str)
StringBuilder insert(int offset,char c)
    //在offset位置添加字符串/代码单元，并返回this
```



### 输入输出







## Chapter 4 对象与类

### 面向对象程序设计概述

#### 类

> 类是构造对象的模板或蓝图。



一些基本概念：:arrow_double_down:

*创建类的实例*



由类构造对象的过程。

*实例字段*

对象中的数据。

*方法*

操作数据的过程。

*继承*

通过扩展一个类来建立另外一个类的过程。



:warning:实现封装的关键：

绝对不能让类中的方法**直接访问**其他类的**实例字段**。



在Java中，所有类都扩展自于Object类。

#### 对象

:key:对象的三个主要特性：

- 对象的行为——可以对对象完成哪些操作，应用哪些方法？

- 对象的状态——当调用方法时，对象会如何响应？

- 对象的标识——如何区分具有相同行为与状态的不同对象？

  

#### 类之间的关系

> 在类之间，最常见的关系有：

- 依赖（一个类的方法使用或操纵另一个类的对象）
- 聚合（类A的对象包含类B的对象）
- 继承（一个更特殊的类与一个更一般的类之间的关系）



:warning: 应尽可能地将相互依赖的类减至最少。



> UML常见的箭头样式如下：



![image-20221019142022344](C:\Users\21964\AppData\Roaming\Typora\typora-user-images\image-20221019142022344.png)



### 使用预定义类


#### 对象与对象变量

> 要想使用对象，首先必须构造对象，并指定其初始状态，然后对对象应用方法。
>
> 在Java中，要使用构造器构造新实例。



:information_desk_person:构造器是一种特殊的方法，用来构造并初始化对象。构造器的名字应该与类名相同。

要构造一个对象，需要在构造器前面加上new操作符。

``` java
new Date()
```

然后可以将这个对象传递给一个方法，或应用一个方法。

:warning:在Java中，任何对象变量的值都是对存储在另外一个地方的某个对象的引用。

#### LocalDate类

> 标准Java类库分别包含了两个类：一个用来表示时间点的Date类，一个用日历表示法表示日期的LocalDate类。



:warning:不要用构造器来构造LocalDate类的对象。应当使用**静态工厂方法**。

```java
LocalDate.now()
```

会构造一个新对象。表示构造这个对象时的日期。

提供年月日构造一个特定日期：

```java
LocalDate.of(1992,12,30)
```

通常将构造的对象保存在对象变量中。

```java
LocalDate newYearsEve = LocalDate.of(1999,12,31);
```

接着可以使用getYear,getMonthValue,getDayOfMonth得到年月日的值。



#### 更改器方法和访问器方法



:person_fencing:

更改器方法:arrow_double_down:

访问并更改对象的方法。

访问器方法:arrow_double_down:

访问对象而不修改对象的方法。



### 用户自定义类



在Java中，最简单的类定义形式为：

```java
class ClassName  //类名
{
    field1 
    field2
    ...
    constructor1
    constructor2
    ...
    method1
    method2
}
```



:warning:

- 只有一个类有main方法。

- 在一个源文件中，只能有一个公共类，但可以有**任意数目**的非公共类。

  

#### 构造器

> 在构造对象时，构造器会运行，从而将实例字段初始化为所希望的初始状态。

:pushpin:

- 构造器与类同名。

- 构造器总是结合new运算符使用。不能对一个已经存在的对象调用构造器来重新设置实例字段。

- 每个类可以有一个以上的构造器。

- 构造器可以有0个，1个或多个参数。

- 构造器没有返回值。

  

:warning:**不要在构造器中定义与实例字段同名的局部变量**！（会遮蔽同名的实例字段）



#### 用var声明局部变量

在**Java10**中，如果可从变量的初始值推导出它们的类型，可以用**var**关键字声明局部变量，无须指定类型。

:pushpin:

**只能用于方法中的局部变量，参数和字段的类型必须声明。**



#### 使用null引用

> 对null值应用一个方法，会产生一个NullPointerException异常.

有两种解决办法：:arrow_double_down:

宽容型

把null参数转换为一个适当的非null值。

严格型

拒绝null参数。

#### 隐式参数与显式参数

> 方法用于操作对象以及存取它们的实例字段。

:pushpin:

**隐式参数**:arrow_right:出现在方法名前的对象。有人称为方法调用的*目标*或*接收者*。

**显式参数**:arrow_right:位于方法名后面括号中的数值。



可以看出，显式参数显式地列在方法声明中。

**关键字this指示隐式参数。**可以将实例字段与局部变量明显地区分开来。



#### 封装的优点



字段访问器:arrow_right:只返回实例字段值。



> 想要获得或设置实例字段的值。需要提供下面三项内容。

- 一个**私有**的数据字段。
- 一个公共的字段访问器方法。
- 一个公共的字段更改器方法。



有以下的好处:arrow_double_down:

1. 可以改变内部实现。而除了该类的方法之外不会影响其他代码。
2. 更改器方法可以完成错误检查。



:warning:不要编写返回可变对象引用的访问器方法！（**会破坏封装性）**

如需要返回一个可变对象的引用，首先应该进行克隆。



#### 基于类的访问权限



> 一个方法可以访问**所属类**的**所有对象**的私有数据。



#### 私有方法

>  在Java中实现私有方法，只需将public改成private即可。

只要方法是私有的，类的设计者就可以确信它不会在别处使用。

如果一个方法是公共的，就不能简单地删除，因为可能会有其他代码依赖这个方法。



#### final实例字段

> 可以将实例字段定义为final，这样必须在构造对象时初始化。



必须确保在构造器执行之后，这个字段的值已经设置，并且**不能再修改**这个字段。

final修饰符对于类型为**基本类型**或者**不可变类**的字段尤其有用。（类中所有方法都不会改变对象就是不可变类。）

对可变的类使用final可能会造成混乱。

final关键字只是表示变量中的对象引用不会再指示另一个不同的对象。不过这个对象可以更改。



### 静态字段与静态方法



#### 静态字段

> 如果将一个字段定义为static,每个类只有一个这样的字段。



#### 静态常量

例如：

``` java
public class Math{
public static final double PI = 3.1415926;
}
```

可以通过Math.PI来访问这个常量。

省略static使得PI变成Math类的实例字段，需要通过Math的对象来访问。



#### 静态方法

> 静态方法是不在对象上执行的方法。

:cowboy_hat_face:可以认为静态方法是没有this参数的方法。

使用静态方法的情况如下:arrow_double_down:

- 方法不需要访问对象状态。
- 方法只需要访问类的静态字段。



#### 工厂方法

> 有的类使用静态工厂方法来构造对象，如LocalDate类。



常见的工厂方法例如：LocalDate.now和LocalDate.of

使用工厂方法的常见原因:arrow_double_down:

- 无法命名构造器。
- 使用构造器时，无法改变所构造对象的类型。

#### main方法

> 可以调用静态方法而不需要任何对象。

:key:main方法不对任何对象进行操作。

在启动程序时还没有任何对象，静态的main方法执行并构造程序所需要的对象。

















## Chapter 6 接口、lambda表达式与内部类





#### 变量作用域

> lambda表达式组成部分

* 一个代码块

* 参数

* 自由变量的值   **（非参数且不在代码中定义）**

  

<strong>表示lambda表达式的数据结构必须存储自由变量的值</strong>



> lambda表达式可以捕获外围作用域中变量的值。



在Java中，要确保所捕获的值是明确定义的。（只能引用值不会改变的变量:rage:)

```java
public static void countDown(int start,int delay)
{
ActionListener listener = event ->
{
start --; // 错误，变量值改变了
System.out.println(start);
};
new Timer(delay,listener).start;
}
```



原因是在并发执行时不安全:sweat_smile:

引用变量，而变量可能在外部改变，也是不合法的。

```java
public static void repeat(String text,int count)
{
for(int i=1,i <= count,i++)
{
ActionListener listener = event -> {
System.out.println(i+":"+text);//错误，i在循环中改变了值
}
new Timer(1000,listener).start;}
}
```



lambda表达式中捕获的变量必须实际上是**事实最终变量**

:arrow_forward: **这个变量初始化之后就不会再为它赋新值**



> lambda表示式的体与嵌套块有相同的作用域。

声明一个局部变量同名的参数或局部变量是不合法的:rage:

```java
Path first = Path.of("/usr/bin");
Comparator<String> comp 
 = (fisrt,second) ->first.length() - second.length(); //错误，first已经被定义了
```

> 在lambda表达式中使用this关键字，是指创建这个lambda表达式的方法的this参数。

### 内部类

内部类是定义在**另一个类**中的类。

- 内部类可以对同一个包中的其他类隐藏。
- 内部类方法可以访问定义这个类的作用域中的数据。包括原本私有的数据。

####  使用内部类访问对象状态



> 一个内部类方法可以访问自身的数据字段，也可以访问创建它的外围类对象的数据字段。



内部类的对象总有一个隐式引用，指向创建它的外部类对象。

![image-20220928194535541](C:\Users\21964\AppData\Roaming\Typora\typora-user-images\image-20220928194535541.png)



:warning:**这个引用在内部类的定义中是不可见的。**



#### 内部类的特殊语法规则

```OuterClass.this```  :arrow_forward: 表示外围类引用

编写内部类对象的构造器:arrow_double_down:

```outerObject.new InnerClass(construction parameters)```

例如：

```ActionListener listener = this.new TimerPrinter();```

在外围类的作用域之外可以这样引用内部类：

``` OuterClass.InnerClass```



 * ***内部类中声明的所有静态字段都必须是final，并初始化为一个编译时常量***。
 * ***内部类不能有static方法。***



#### 局部内部类



*只是在方法中创建了这个类型的对象时使用了一次，可以在这个方法中局部地定义这个类。*

优势在于对外部世界是完全隐藏的。



例如：

```java
public void start()
{
        class TimePrinter implements ActionListener //此处的TimePrinter即为局部内部类
        {
         public void actionPerformed(ActionEvent event) 
         {
            System.out.println("At the tone,the time is " + Instant.ofEpochMilli(event.getWhen()));
            if (beep) Toolkit.getDefaultToolkit().beep();
        }
    }
}
}
```



- **:warning: 声明局部类时不能有访问说明符。（public 或  private）**
- :warning: **作用域被限定在声明这个局部类的块中。**



##### 由外部方法访问变量



:facepunch:**局部类不仅能够访问外部类的字段，还可以访问局部变量。**



##### 匿名内部类  



只想创建这个类的一个对象，甚至不需要为类制定名字。

语法如下:arrow_down_small:

```java
new SuperType(construction parameters)
{
  inner class methods and data
}
```

*SuperType可以是接口，也可以是一个类。*



:warning:**匿名内部类不能有构造器！构造参数要传递给超类构造器。** 



:pencil2:**只要内部类实现一个接口，就不能有任何构造参数。仍然要提供一组小括号。**

如下:arrow_down_small:

```java
new Interface()
{
  methods and data
}
```



*如果构造参数列表的结束小括号后面跟一个开始大括号，就是在定义匿名内部类。*



:key:**匿名内部类用来实现事件监听器和其他回调。如今最好用lambda表达式。**



#### 静态内部类

> 有时候，使用内部类只是为了把一个类隐藏在另外一个类的内部，并不需要内部类有外围类对象的一个引用。
>
> 可以将内部类声明为static，这样就不会生成那个引用。



注意事项如下：:arrow_double_down:

* :warning:只有**内部类**可以声明为static
* :warning:静态内部类可以有静态字段和方法。
* :warning:在接口中声明的内部类自动是static和public。





## Chapter 7  异常、断言和日志



### 处理错误



#### 异常分类

![image-20221004140629069](C:\Users\21964\AppData\Roaming\Typora\typora-user-images\image-20221004140629069.png)

> :key: 异常对象**都是**派生于Throwable类的一个类实例。



 :warning:**所有**的异常都是从Throwable继承而来，但在下一层立即分解为两个分支：*Error* 和 *Exception*。

:arrow_forward:*Error*   

Java运行时系统的内部错误和资源耗尽错误



:arrow_forward:*Exception*

可分解为两个分支：*RuntimeException*和*其他异常*



由**编程错误**导致的异常属于RuntimeException。

通常包括

- 错误的强制类型转换。
- 数组访问越界。
- 访问null指针。



不是派生于RuntimeException的异常包括:arrow_down:

- 试图超越文件末尾继续读取数据。
- 试图打开一个不存在的文件。
- 试图根据给定的字符串查找Class对象，而这个字符串表示的类并不存在。



派生于Error类或RuntimeException类的所有异常称为*非检查型异常*。

**所有**其他的异常称为*检查型*异常。



:warning:编译器将检查你是否为**所有**的**检查型异常**提供了**异常处理器**。



#### 声明检查型异常



>  在下面4种情况时会抛出异常：

- 调用了一个抛出检查型异常的方法。**（必须告诉有可能抛出异常）**

- 检测到一个错误，并且利用throw语句抛出一个检查型异常。**（必须告诉有可能抛出异常）**

- 程序出现错误。

- Java虚拟机或运行时库出现内部错误。

  

  

> 有些Java方法包含在对外提供的类中，应该通过方法首部的*异常规范*声明这个方法可能抛出异常。

如下所示:arrow_down_small:

```java
class MyAnimation
{
...
public Image loadImage(String s) throws IOException
{
...
}

}
```



如果一个方法有可能抛出**多个**检查型异常类型，**必须**在方法的首部列出**所有**的异常类，每个异常类之间用**逗号**隔开。



如下所示:arrow_down_small:

```java
class MyAnimation
{
...
public Image loadImage(String s) throws FireNotFoundException,EOFException
{
...
}

}
```



:warning:

- 不需要声明Java的内部错误，即从*Error*继承的异常。同样，也不应该声明从RuntimeException继承的那些非检查型异常。
- 一个方法必须声明**所有**可能抛出的**检查型**异常。
- 如果在子类中覆盖了超类的一个方法，子类方法中声明的**检查型异常**不能比超类方法中声明的异常更通用。如果超类方法没有抛出任何检查型异常，子类也不能抛出任何检查型异常。
- 如果类中的一个方法声明它会抛出一个异常，而这个异常是某个特定类的实例，那么这个方法抛出的异常可能属于这个类，也可能属于这个类的任意一个子类。



#### 如何抛出异常



> 如果一个已有的异常类能够满足要求，抛出异常非常容易。

1. 找到一个合适的异常类。

2. 创建这个类的一个对象。

3. 将对象抛出。

   

:key:一旦方法抛出了异常，这个方法就不会返回到调用者。



以抛出EOFException为例：:arrow_double_down:

``` throw new EOFException();```

或者是：

``` java
var e = new EOFException();
throw e;
```

具体例子如下：

```java
String readData(Scanner in) throws EOFException
{
    ...
    while(...)
    {
        if(!in.hasNext()) // 遭遇EOF
        {
            if(n<len)
                 throw new EOFException();
        }
        ...
    }
    return s;
}
```



EOFException类还有一个带一个字符串参数的构造器。可以利用这个构造器来描述异常。

``` java
String gripe = "Content-length" + len +",Received,"+n;
throw new EOFException(gripe);
```



#### 创建异常类



> 自定义的这个异常类应该包含两个构造器，一个是默认的构造器，另一个是包含详细描述信息的构造器。



:key:超类Throwable的toString方法会返回一个字符串。



具体如下:arrow_double_down:

```java
class FileFormatException extends IOFException
{
    public FileFormatException(){}
    public FileFormatException(String gripe)
    {
        super(gripe);
    }
}
```



现在可以抛出自己定义的异常类型了。

```
String readData(BufferedReader in) throws FileFormationException
{
    ...
    while(...)
    {
        if(!in.hasNext()) // 遭遇EOF
        {
            if(n<len)
                 throw new EOFException();
        }
        ...
    }
    return s;
}
```





### 捕获异常



#### 捕获异常



> 想捕获一个异常，需要设置try/catch语句块。



try语句块的基本格式如下:arrow_double_down:

```java
try{
    code 
    more code
    more code
}
catch(ExceptionType e)
{
    handler for this type
}
```



如果try语句块中的任何代码抛出了catch字句中制定的一个异常类：

1. 程序将跳过try语句块的其余代码。
2. 程序将执行catch子句中的处理器代码。



:warning:

- 如果try语句块中的代码没有抛出任何异常，那么程序将跳过catch子句。
- 如果代码抛出了catch子句中没有声明的一个异常类型，方法就会立即退出。(希望调用者提供了这种异常的catch子句)









## Chpater 8 泛型程序设计



### 为什么要使用泛型程序设计

:key:**泛型程序设计**

意味着编写的代码可以对**多种不同类型**的对象重用。

#### 类型参数的好处

> 在Java中添加泛型类之前，泛型程序设计是用**继承**实现的。ArrayList类只维护一个Object引用的数组。

:warning:存在两个问题：

- 当获取一个值时必须进行强制类型转换。

- 没有错误检查，可以向数组列表中添加任何类的值。

  

泛型提供了一个更好的解决办法：*类型参数*。:arrow_down_small:

ArrayList类有一个类型参数用来指示元素的类型。

```java
var files = new ArrayList<String>(); //String即为此处的类型参数
```

类型参数使得程序更加易读，也更安全。

### 定义简单泛型类

> 泛型类就是有**一个或多个**类型变量的类。



此处用泛型Pair类为例:arrow_down_small:：

```java
class Pair<T> {
    private T first;
    private T second;

    public Pair() {
        first = null;
        second = null;
    }

    public Pair(T first, T second) {
        this.first = first;
        this.second = second;
    }

    public T getFirst() {
        return first;
    }

    public T getSecond() {
        return second;
    }

    public void setFirst(T newValue) {
        first = newValue;
    }

    public void setSecond(T newValue) {
        second = newValue;
    }


}
```



泛型类可以有多个类型变量。例如可以定义Pair类，在第一个字段与第二个字段使用不同的类型。

```java
public class Pair<T,U> {...}
```



类型变量在整个类定义中用于**指定方法的返回类型**以及**字段和局部变量的类型**。



:key:类型变量使用**大写字母**。

- E表示集合的元素类型。
- K和V分别表示表的键和值的类型。
- T（U,S)表示“任意类型”。



可以使用具体的类型替换类型变量来实例化泛型类型，如:

``` java
Pair<String>
```

即，泛型类相当于普通类的**工厂**。



:key:*compareTo*的作用：

- 如果字符串相同，返回0。
- 按照字典顺序，如果第一个字符串比第二个字符串靠前，返回一个负整数。
- 否则，返回一个正整数。



### 泛型方法



> 除了定义泛型类之外，还可以定义一个带有类型参数的方法。



在定义泛型方法时，类型变量放在**修饰符**的后面，**返回类型**的前面。

如：

```java
public static <T> T getMiddle(T ...a)
```



泛型方法可以在普通类中定义，也可以在泛型类中定义。

当调用一个泛型方法时，可以把具体类型包围在尖括号中，放在方法名前面。

```java
String middle = ArrayAlg.<String>getMiddle("John","Q","Public");
```

方法调用可以省略*String*类型参数。编译器可以推断出。



### 类型变量的限定



> 有时，类或方法需要对类型变量加以约束。



可以对类型变量T设置一个限定来实现这一点。

```java
public static <T extends Comparable> T min(T[] a)...
```

现在min方法只能在实现了Comparable接口的类的数组上调用。



```java
<T extends BoundingType>
```

表示T是限定类型的子类型。

T和限定类型可以是类，也可以是接口。



一个类型变量或通配符可以有多个限定，如:arrow_down_small:

```java
T extends Comparable & Serializable
```

限定类型用“&”分隔，逗号分割类型变量。



在Java的继承中，可以根据需要拥有多个接口超类型。但**最多**有一个限定可以是类，且这个作为限定的类**必须是限定列表中的第一个**限定。



### 泛型代码与虚拟机
