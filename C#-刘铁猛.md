# 1、类与命名空间  
## 类（Class）
类是构成程序的主体

## 命名空间（namespace）
命名空间是以树形结构将类（和其他类型）组合在一起的一个集合。  

```cs
using System;
using System.Collections.Generic;  
using System.Linq;
using System.Text;
using System.Threading.Tasks;
//上方为引用的类库


namespace Tools//命名空间为Tools
{
    public class Calculator //类名为Calculator
    {
        public static double Add(double a,double b)
        {
            returan a + b;
        }
    }
} 
```



## 类库的引用  
* 类库引用时使用命名空间的物理基础   
    * .dll就是类库  
    * 对象浏览器（VS重要面板）  
    * 不同的项目模板新建后，就是为了你引用不同的类库。  


* DLL引用（黑盒引用，无源代码）  
    * 编译好的DLL引用，无源代码。如果有BUG，无法修改，只能告诉dll编写人有误。  
    * NuGet：通过打包的模式，直接将所需的类库整合进一个包内，需要时，直接可以通过网络引用，并自动为你管理，无需担心类库不完整。
* 项目引用（白盒引用，有源代码）
    * 代码在项目仲，可以看到源代码  


## 依赖关系  
假如，你在编写程序的时候引用的了一个有问题的类库，那么你的程序是依赖这个类库编写的，所以你的程序也会有问题。  
* 类（或对象）之间的耦合关系  
* 优秀的程序追求“高内聚，低耦合”（教学程序往往会违反这个原则）
    * 高内聚： 一些数据、或者一些功能，该属于哪个类，就把它放到哪个类里边去，精确放到对应的类中。尽可能地减少类与类之间的依赖关系，尽可能地松。类库也是同样的原理。
* UML（通用建模语言）类图：主要用来展示类与类之间的关系。  
## 排除错误  
* 仔细阅读编译器的报错（RTFM）  
* 通过网络，阅读对应得的文档，比如[C#——Microsoft 文档](https://docs.microsoft.com/zh-cn/dotnet/csharp/)。 

# 2、类，对象，类成员简介  
* 类（class）是现实世界事物的模型  
* 类与对象的关系  
    * 什么时候叫“对象”，什么时候叫“实例”  
    * 引用变量与实例的关系  
* 类的三大成员  
    * 属性（Property)  
    * 方法（Method)  
    * 事件（Event）  
* 类的静态成员与实例成员  
    * 关于“绑定”（Bingding）  

## 类（class）是现实世界事物的模型  
类是对现实世界事物进行抽象所得到的结果  
* 事物包括“物质”（实体）与“运动”（逻辑）  
* 建模是一个去伪存真、由表及里的过程  

## 类与对象的关系  
* 对象也叫实例，是类经过“实例化”后得到的内存中的实体  
    * Formally “instance” is synonymous with “object” ————对象和实例是同一样东西，唯一的区别在于谈话的语境。  
    * “飞机”与“一架飞机”，飞机是概念，而一架飞机是实例，天上有（一架）飞机————必须是实例才能飞，概念是不能飞的  
    * 有些类是不能实例化的，比如“数学” （Math Class），不能说“一个数学”  
* 依照类，我们可以创建对象，这就是“实例化”  
    * 现实世界中常称为“对象”，程序世界中常称为“实例”  
        对象 = 实例   
* 使用new操作符创建类的实例   
```cs
namespace ClassAndInstance
{
    class Program
    {
        static void Main(string[] args)
        {
           new Form();
           //Form是一个概念，创建一个实例需要在概念前面加一个new修饰符
           //而括号代表了，在内存中创建了这个实例后，使用怎样的方法对其进行初始化，也就是构造器
        }
    }
}
```
* 引用变量与实例的关系  
```cs
namespace ClassAndInstance
{
    class Program
    {
        static void Main(string[] args)
        {
           (new Form()).Text = "My Form";
           (new Form()).ShowDialog();
        }
    }
}
```
这个程序的返回值是只有一个空白的窗口，原因是第一个被赋标题值的窗口并没有显示出来。  
最终显示的窗口是第二个空白的窗口，实际上程序中被实例化了两个对象，所以才会导致这种情况的发生。  

那么，如何才能让赋了标题值的窗口显示出来？  
```cs
namespace ClassAndInstance
{
    class Program
    {
        static void Main(string[] args)
        {
            Form myForm;//声明引用变量
            myForm = new Form();//将new Form赋值给myForm，从右往左  
            myForm.Text = "My Form!";//myForm这个变量使用了Text的方法，实际上是引用了new Form这个实例
            myForm.ShowDialog();//myForm使用ShowDialog方法，引用new Form  
        }
    }
}
```
* 通过引用变量引用这个实例之后，就可以多次访问该实例。  
举例：  
孩子与气球  
上面所展示的程序中，myForm就相当于一个孩子，new Form相当于气球。  
而孩子(myForm)可以牵住气球(new Form)，通过  "=" （赋值符号）,当你创建了气球(new Form)这个对象的时候，就可以通过“=”交给这个孩子(myForm)  

## 类的三大成员  
* 属性（Property）  
    * 存储数据，组合起来表示类或对象的当前的状态  
* 方法（Method）  
    * 由C语言中的函数（function）进化而来，表示类或对象“能做什么”  
    * 工作中90%时间都是在和方法打交道，因为它是实际做事和构成逻辑的成员  
* 事件（Event）
    * 类或对象通知其他类或对象的机制，为C#所特有（Java通过其他办法实现这个机制）  
    * 善用时间机制非常重要  
* 使用MSDN文档  
* 某些特殊类或对象在成员方面侧重点不同  
    * 模型类或对象重在属性  
    * 工具类或对象重在方法  
    * 通知类或对象重在事件  
    


