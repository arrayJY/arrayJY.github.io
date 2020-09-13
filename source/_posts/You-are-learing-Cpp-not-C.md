---
title: 你学的是C++而不是C
date: 2020-09-13 18:51:02
tags:
---
如果是你是个计算机系学生，你所在的大学正在教授你C++，那么很多时候你不得不重新审视你学到的知识——你真的在学C++吗？
<!-- more -->
诸多大学采用他们自编的、粗制滥造的教材（最著名的比如谭某某的教材），试图将似C非C的C++灌输到学生脑子当中。如果你有那么一点追求，就应该扔掉手里的教材，换一本至少知道自己在讲什么的东西。

本文目的就是指出那些教材中的C式C++写法，并教你如何用**Modern C++** 代替他们，从而放弃混账的C式C++。**请注意，本文不是一本完整教授C++的教程。**

**本文适合：C++初学者、被学校C式C++折磨得不耐烦的人、对自己的C++技术有追求的人。**
**本文不适合：有一定基础、有自己学习方法的人。**

推荐C++入门书籍：
*《C++ Primer 5th》《Think in C++》*
推荐网站：
[Google](https://google.com)，[知乎](https://zhihu.com)，[C++参考手册](https://zh.cppreference.com)，[Stackoverflow](https://stackoverflow.com)，[Github](https://github.com)
上不去就自己想办法，翻墙不是难事。

**本文很长，可以慢慢看，可以看一半就放弃，可以看到这句话就走。**

### 0x00 为什么你要学C++

你看到这个问题时，脑子里可能很快蹦出一个答案：因为考试要考。我当然知道你要考，我也要考，但我们的人生不是为了考试，对吗？你必须得知道，C++到底对你来说意味着什么。

#### 一、对于编程初学者，C++不是一门好的语言

如果你初学编程，C++对你来说可能是**很枯燥、很繁琐**的一门语言。它包含了大量的细节、需要你拥有几乎无穷多的计算机知识才能解决的问题，以及繁复的语法。

如果你试着用Python入门编程，你可能会惊呼：编程为什么这么简单！

但是C++给予了你以下机会：

* 近乎无限接近于程序运作的底层原理
* 近乎可以掌控一切细节
* 可以在一门语言中实践各种[编程范式](https://zh.wikipedia.org/wiki/编程范型)

有了这些机会，当你在学习其他计算机知识，或者其他编程语言时感到有如天助。

*这是我个人的真实例子，那时我对C++的了解不过是看过一本入门书籍，写过不到千行代码。但当我有一天准备学习Python时，我仅用了一个晚上就看完了Python的所有语法。*

如果你对以上的内容毫无兴趣，很明显，**这篇文章不是为你写的，你可以无需在此浪费时间了。**

#### 二、“视C++为一个语言联邦”

“视C++为一个语言联邦”出自*《Effective C++》*的条款01，这本书被认为是C++进阶书籍，但是这一条，我认为C++初学者也应该了解它。

简单讲讲C++的历史（我也很烦历史，但你不了解他你就不知道我接下来讲的是啥）：

C++一开始是作为C语言的拓展出现的，一开始它的名字叫*C with classes(带类的C)*。后来人为了能让它胜任各种工作，往它上面加了各种杂七杂八的功能，这使得C++变得非常复杂，像是多门小语言组成的一个语言联邦。很多时候你不得不在各种“小语言”模式中切换，而这对初学者而言简直是个噩梦。但你必须了解它，而且其实你也不难适应它。

这门语言联邦主要包含：

* C，这简直是废话，作为C语言的拓展C++肯定要兼容C语言，**但是这不是学校把C++当成C教的理由**。
* C with classes，一个支持面向对象的C，**学校几乎是从C不明不白的跳到了这里，让人云里雾里。**
* Template，模板，**作为初学者，我们可以几乎不用管这个**，等你有一定基础之后再来学习。
* STL，全称为*Standard Template Library(标准模板库)*，**作为初学者，这是你学C++的利器，但是学校几乎不教它。**

本文将着重于**面向对象入门和STL的使用**，相信我，一定会讲的很有趣。

本文写于**2020年3月17日**，此时C++标准已经发展到*C++20*（此前还有*C++98、C++11、C++14和C++17*)，许多学校还在可怜地对着*C++98*抱残守缺，而新的标准带来了许许多多好用的工具（无论对C++初学者还是熟练使用C++的人），所以请你**一定要跟上时代的步伐**，不要做一个考古学家，至少，从*C++11*开始。

### 0x01 从选一个现代IDE开始

很多学校还在教授*Visual C++ 6.0*这个快要入土为安的东西，它开发于**1998年**，至今已有**22年**的历史。22年！海都枯了，石都烂了。我们完全可以用更好的、更先进的IDE，不是吗？我们不是考古学家，更不是山顶洞人。

推荐如下IDE：

* [Visual Studio](https://visualstudio.microsoft.com/zh-hans/)

  这是Window上写代码的不二选择，但它更偏向于大型工程，对于初学者而言，**太重了**。

* [CLion](https://www.jetbrains.com/clion/)

  Mac/Linux用户的选择，当然Windows上也可以用。然而它是收费软件，不过学生可以申请免费使用。**适合初学者。**

* [Visual Studio Code](https://code.visualstudio.com/) + [Clang](https://clang.llvm.org/)

  VSCode是严格来说不算IDE，只是一个文本编辑器，加上Clang编译器也只能说刚刚好。**特点是轻巧，对于初学者完全足够**。配置起来比较复杂，可以参考[知乎：Visual Studio Code 如何编写运行 C、C++ 程序？](https://www.zhihu.com/question/30315894/answer/154979413)。

* [XCode](https://developer.apple.com/xcode/) + [Clang](https://clang.llvm.org/)

  理由同VSCode，只是VSCode在Mac上算是个残次品，XCode也只能算勉强能用。

* [Code::Blocks](http://www.codeblocks.org/)

  这个我没有用过，不好评价。但至少它一直在更新。

如果上面的你都觉得不好用，你还可以用**Dev-C++**，这个简单易用，但它已经停止更新了，它只支持到*C++11*标准。

现代的IDE带有大量工具，比如代码补全、调试，可以快速帮我们写程序，或者找出程序错误的地方。这些工具都十分有用，**学着使用他们，搜索引擎可以帮你的忙。**

### 0x02 使用 `const` 而不是 `#define`定义常量

远古时期的C语言没有`const`常量的概念，那时候人们喜欢用`#define`来定义一个符号常量，比如像这样：

```C
#define PI 3.14
int r = 3;
double s = r * r * PI;
```

以上出现在大量**C++教材**中的例子，不知道为什么，这些教材的编写者喜欢把C的东西带入到C++中。在C++里你完全可以使用`const`：

```C++
const double PI = 3.14;
int r = 3;
double s = r * r * PI;
```

使用 `const` 常量而不是 符号常量原因有二：

1. `const`常量有生命周期（后文我们会详细讨论这个概念）而符号常量没有。
2. 在编译期，编译器会对`const`常量做类型检查。

这两个原因可以让`const`常量变得安全高效。

### 0x03 使用 `auto` 自动推断类型

在后面，我们会看到一些名字很长很长很长的类型（STL里面就有很多），如果我们为了代码整洁美观，也为了少打几个字，可以使用`auto`自动推断类型。

```C++
int a = 1;    //定义一个int变量
auto b = 1.0; //自动推断b为double变量
```

使用`auto`还有一个好处，就是可以防止使用未初始化的变量：

```C++
int a;
cout << a; //warning: variable 'a' is uninitialized when used here
auto b;    //error: declaration of variable 'b' with deduced type 'auto' requires an initializer
cout << b;
```

如果使用一个未初始化的普通变量，编译器只会发出`warning`，仍然可以编译成功，然而运行的结果是未定义的。而如果未初始化一个`auto`变量会使编译器发出`error`，则会中断编译过程，这样就强制你使用已初始化的变量。

然而如果你通篇全是`auto`，可能会显得不直观。虽然在现代IDE中你可以很方便的查看`auto`推断出的类型，但是这仍然没有直接使用类型直观。所以，`auto`使用需要自行取舍。

当然`auto`还有很多使用方法，这里只是简单介绍，如果你有兴趣，你可以通过搜索引擎找到相关内容。



### 0x04 用C++的方法进行强类型转换

想想你的老师是怎么教你强类型转换的？是不是这样子：

```C++
double a = 123.0;
int b = (int)a;
```

够了！停止使用这种旧式强类型转换，使用新式做法，其语法为：

```C++
cast-name<type>(expression);
```

* `cast-name`为转换的类型，取值有`static_cast`，`dynamic_cast`，`const_cast`和`reinterpret_cast`。
* `type`是要转换成的目标类型
* `expression`为进行转换的表达式

此处的*cast*应该被翻译成*转型*，但我貌似没有找到这个解释。

**警告：强类型转换有风险，能不使用就尽量避免使用。**

举个栗子：

```C++
int a = 123;
double b = static_cast<double>(a); //a被强类型转化为double
```

旧式转型分别具有和`static_cast`，`const_cast`和`reinterpret_cast`相似的行为，如果出现问题则更难跟踪，所以请不要使用旧式强类型转换。

由于我们是初学者，大部分时候我们只会使用到`static_cast`，如果对其他的`cast`有兴趣，可以去搜索引擎寻找答案。

**再次警告：能不使用就尽量避免使用强类型转换。**

### 0x05 使用 `std::string` 而不是 `char` 数组

如果你想要用一个字符串，你猜猜学校会教你什么？答对了，是`char`数组。一个极其难用，又不直观的东西。以下便是例子：

```C++
#include <iostream>
#include <cstring>   //字符串C库，有些教材还写成#include "string.h"这种C语言写法
using namespace std;

char str1[10], str2[10];
cin >> str1;         //输入字符数组，你猜猜输入字符大于10个会发生什么？
strcpy(str2, str1);	 //将str1拷贝到str2中，为什么不能直接用"="？
strcmp(str1, str2);  //比较str1和str2是否一样，为什么不能直接用"=="？
```

使用字符数组会使得代码非常丑陋：

1. 如果输入的字符串长度大于数组的长度，可能会造成意想不到的结果，甚至程序崩溃。
2. 使用`strcpy()`函数拷贝字符串，这个函数有安全风险，而且很不直观。
3. 使用`strcmp()`比较字符串，很不直观。

那么有没有一种“字符串”类型能让我们像使用`int`、`float`类型那样使用它呢？有的，[`std::string`](https://zh.cppreference.com/w/cpp/string/basic_string)就是了。

`std::string`来源于标准库，他是一个字符**容器**，可以**容纳任意个字符**：

```C++
#include <string> //包含<string>头文件
#include <iostream>
using namespace std;

string str1, str2;
cin >> str1;     //不用担心长度问题
str2 = str1;     //直接赋值即可拷贝
str2 == str1;    //可以直接比较
```

甚至它还有更多的功能：

```C++
str1 = "Hello World";
str2 = str1.substr(0,5);    //返回str1从下标0开始长度为5的子串，即"Hello"
char c = str2[0];           //直接取下标返回char元素, 即'H'.                     
```

你可以在*[CppReference/basic_string](https://zh.cppreference.com/w/cpp/string/basic_string)*里找到`std::string`的完整文档，这个文档很全也很枯燥，其中**大量涉及初学者不了解的概念**，你也可以配合搜索引擎来解决你的问题。

### 0x06 动态数组：使用 `std::vector`

老师可能会跟你讲，数组的长度是固定的，如果你需要在运行时候申请动态长度的数组，可以通过`new`分配动态内存来实现（我们稍后会讨论这个方法好不好）。

作为一个新手你可能对C++程序的内存模型一无所知，就算老师告诉你，你也是一知半懂。其实你不用纠结，选`std::vector`就可以解决你的问题。

`std::vector`是标准库里的一种**容器**，他可以**包含任意个数的某一类**元素。

```C++
#include <vector>  //包含<vector>头文件
using namespace std;

vector<int> a;     //一个包含元素类型为int的vector
vector<double*> b; //一个包含元素类型为double*的vector

a.push_back(1);    //在末尾添加元素，vector长度会自动增长，此时a[0]即为1
int b = 2;
a.push_back(b);    //此时a[0]为1，a[1]为2
a.pop_back();      //删除末尾元素，此时a长度为1，仅有a[0]为1
a.empty();         //vector为空返回true，否则返回false
a.size();          //返回元素的数量
```

很方便是不是！你完全无需关注内存的分配问题，`std::vector`自动帮你解决了。事实上，我们可以认为`std::string`就是一个`std::vector<char>`。

你可以在*[CppReference/vector](https://zh.cppreference.com/w/cpp/container/vector)*里找到更多关于`std::vector`的信息，当然这也是个枯燥的说明书，你也可以从搜索引擎中寻找更生动的说明。

### 0x07 当你使用 `using` 的时候你到底在做些什么

#### 一、安全的 `using`

之前我们写过很多句：

```C++
using namespace std;
```

其实这是一种偷懒的写法，这样将会把命名空间`std`中的所有内容引入进来，而这其中可能会有和你自己命名相冲突的内容。

更安全的方法是用什么就`using`什么：

```C++
#include <iostream>
#include <string>
using std::cin;
using std::string;
```

或者干脆就不使用`using`：

```C++
#include <string>
std::string a;
```

#### 二、用`using`代替`typedef`

我们知道`typedef`可以重新命名一种类型，事实上使用`using`也可以做到：

```C++
typedef int my_int;
using my_int = int; //两者是等价的
```

`使用using`重命名的好处是：`using`可以对模板进行重命名，而`typedef`不能。比如如果你想重命名`std::string`就只能使用`using`。



### 0x08 你真的懂循环语句吗

我们学过的传统循环语句是这样的，以`for`循环语句为例子：

```C++
for(init-statement; condition; expression)
    statement
```

然而事实上我们还可以花式循环。

#### 一、使用迭代器

STL中的容器几乎都有**迭代器**，迭代器是个很复杂的概念，我们只需要会简单使用即可。

```C++
#include <vector>
#include <iostream>
using std::vector;
using std::cout;

int main()
{
    vector<int> a = {1, 2, 3};                  //a中有三个元素，分别为1,2,3
    for(auto i = a.begin(); i != a.end(); i++)	//a.begin()和a.end()分别是起始、终止迭代器
        cout << *i;	                            //解引用即为当前元素
}
```

#### 二、使用基于范围的 `for` 循环

更好用的是基于范围的`for`循环，我们写一个挨个输出`std:string`里字符的例子：

```C++
#include <string>
#include <iostream>
using namespace std;

int main()
{
    string str = "abcdef";
    for(auto &i: str)
        cout << i << endl;
}
```

基于范围的`for`的括号内包含两部分。`:`左边是一个变量声明，序列中元素会挨个转换成这个和这个变量的类型。为了保证转换成功，我们使用`auto`来推测类型。`:`的右边则是个序列，比如像原生数组、`std::vector`和`std::string`都可以作为序列。

循环会将序列中的元素一一取出，然后赋值给变量。注意我们在声明中使用了引用类型`&i`，它能让你修改序列中的元素。你可以做一个实验：把`&i`改成`i`，然后在循环中修改元素，看看会发生什么。

### 0x09 引用是个好东西

想想老师一定教你写过交换两个数的函数`swap()`，他们往往教你用指针实现，比如交换两个整数的函数：

```C++
void swap(int* a, int* b)
{
    int temp = *a;
    *a = *b;
    *b = temp;
}
```

这很好理解，但我们其实可以用引用来实现这个函数：

```C++
void swap(int& a, int& b)   //int&表示是一个int值的引用
{
    int temp = a;           //引用使用方法和值一样，无需使用*解引用
    a = b;
    b = temp;
}
```

这样看来使用引用实现的`swap()`更加直观，不用反复使用`*`。

引用和指针一样，可以直接接触到原数据，而不用担心值的拷贝问题，这一特性往往用在函数参数上。比如：

```C++
void func1(std::string str);  //参数传值，会经历一次拷贝过程
void func2(std::string &str); //传引用不会进行拷贝
```

如果使用传值的方式调用函数，则会用原来的字符串生成一个新字符串str，如果字符串很大，或者这个函数被调用多次，则这个拷贝花费的时间就会很长。

而传引用不存在这个问题，函数传递的是原来的数据对象，不会进行拷贝。

当然引用也有一些弊端和局限，在此就不多讲了。

### 0x0A 一步步来：从面向过程到面向对象

在学校的教学当中，从面相过程到面向对象是一蹴而就的。然而并没有几个人听得懂他们在讲什么。为什么要使用面向对象？从面相过程如何转换到面向对象？一概不知。

这里我将一步步带领你理解这个转换过程。从一个小故事开始。

老王开了个饭馆，每天要进货各种食材，而他每天都算账算的焦头烂额，于是他打算写一个程序来帮他算账。

#### 一、面向过程的问题

老王先写了一个大致的框架：

```C++
#include <iostream>
using namespace std;

int buy(int money); //money为原来的钱
int main()
{
    int money;
    cin >> money;
    int leftMoney = buy(money); //leftMoney为剩下的钱
}
```

然后他开始填充这个框架：

```C++
const int porkMoney = 50, chickenMoney = 10 ...;
int buy(int money, int porkNumber, int chickenNumber ...)
{
    return money - porkNumber*porkMoney - chickenNumber*chickenMoney ...;
}
```

他发现了一个问题，随着他购入商品品种的增加，他传入的参数也在增加。为了把店里所有的食材容纳进去，他不得不给函数加上几十个参数！这实在又臭又长。

#### 二、使用 `struct` ：面向对象的雏形

这时候老王想了个办法：可以把这些商品归在一类事物下。于是他开始使用`struct`。

```C++
struct goods
{
	int chicken;
	int pork;
	...
};

struct money
{
	const int chicken = 10;
	const int pork = 50;
};

int buy(goods todayGoods);
```

这回不用传递一大坨参数，显得十分美观，老王非常满意。

事实上，这种把事物**归类**的思想，就是面向对象的雏形。

#### 三、改用 `class` 试试

过了几天，老王感觉支出无故变多了。他检查了一下代码，发现食材的数目是对的上，然而价格被人为改了，鸡比猪贵！有人以此中饱私囊！他很生气，但是苦于店内人手短缺，他又不敢随意怀疑别人。

于是这次他转用`class`, 在C++中`class`和`struct`几乎没有区别，唯一的区别是`class`的默认成员为`private`而后者为`public`：

```C++
class Goods
{
public:
    void setPorkNumber(int number);        //让外人调用set...Number()设置数量
    void setChickenNumber(int number);
    ...
    int buy(int money){                    //外人调用buy()来购买
        if(checkEveryIsOK())               //购买前检查一切是否安好
        return money...;
    }
private:                                   //把变量设为私有，让外人不能随意修改，修改必须
    int porkNumber = 0;                    //通过set...Number()，而且buy()之前还有检查
    int setNumber = 0;
    ...
    const int porkMoney = 50;
    const int chickenMoney = 10;
    ...
    bool checkEveryIsOK();
};

```

老王把这个类的实现编译出来，然后交给别人来使用，自己把源代码藏了起来，由此他成功的控制了店内的食材进货过程。

这个故事告诉我们，一个良好的类需要区分可以被人操作的部分，和不能被人触碰到的部分。在别人通过我们公开的函数修改不能被触碰到的部分时，我们可以对他的修改进行检查，合理的修改才予以执行。

即便程序是一个人完成的，这样的限制也是有必要的。类的访问限制可以让你不会随意的修改数据，至于与在恍惚中造成错误。而这是面向过程所难以做的。

而面向对象可以适应更大型的程序，比如那些需要多人协作完成的程序，良好的限制才能使配合更加紧密。

而面向对象还不只这些功能，它的功能还有比如**继承、多态**，这些教材中都有，我就不再赘述。

### 0x0B 使用智能指针而不是手动 `new/delete` 管理动态内存

如果我们需要使用大量的内存，或者是在运行时进行动态内存分配，老师都会教我们使用`new/delete`手动管理内存。而这对新手是一件难事，甚至很多C++老手都苦于手动管理内存。动态申请内存和普通变量所占的内存不同，普通变量占的内存会自动释放，而申请的内存必须手动释放。

在课堂上，我们学过一段内存`new`分配之后一定要`delete`释放，然而加入忘记`delete`怎么办？你说你肯定不会忘，然后写了下面这段代码：

```C++
    int* a;
    for(int i = 0; i < 3; i++)
    {
        a = new int(i);
        cout << *a;
    }
    delete a;
```

你说：你看我记得`delete`了啊，快夸我！可是你仔细看看，在循环中的前两次`new`出的内存都没有被释放，这造成了内存泄漏。

事实上，当程序复杂起来，无数人用经验证明：忘记`delete`事件时有发生。

而内存泄漏其实还不是最危险的，更危险的是*悬挂指针*问题：

```C++
int *a = new int;
delete a;
cout << *a;    //此时a就是一个悬挂指针，直接访问他可能造成程序崩溃！
```

*悬挂指针*指的是那些指向的内存已经被`delete`的指针，此时的正确做法应该是赶快将这个指针重置为`nullptr`，来防止他进行其他操作。但是有时候这个指针的使用者可能不知道指向的内存已经释放，比如使用者调用了一个函数，这个函数释放了这个指针指向的内存，但是使用者不一定知道。

*Modern C++*推荐我们使用智能指针来代替手动管理内存，智能指针定义在头文件`<memory>`当中。

智能指针的作用是，当他们的生命周期结束时，他们会自动释放指向的内存。而智能指针的使用方式和普通指针无异。

智能指针包括三种[`std::unique_ptr`](https://zh.cppreference.com/w/cpp/memory/unique_ptr)、[`std::shared_ptr`](https://zh.cppreference.com/w/cpp/memory/shared_ptr)和[`std::weak_ptr`](https://zh.cppreference.com/w/cpp/memory/weak_ptr)，我们将着重讨论前两种。

#### 一、独占指针：`std::unique_ptr`

`std::unique_ptr`表示只有单一变量持有这个指针，对这个指针进行拷贝是禁止的，你只能*移动*这个指针（这个操作不适合新手，故不在本文的讨论范围）。你可以通过`std::make_unique`来创建一个`std::unique_ptr`：

```C++
#include <memory>
using namespace std;

auto p = make_unique<int>(123); //动态分配一块int大小的内存，并将指针指向这块内存，将初值设为123
auto q = p;                     //编译错误，不能复制一个std::unique_ptr
int b = 321 + *p;               //像使用普通指针一样使用智能指针。
```

#### 二、共享指针：`std::shared_ptr`

`std::shared_ptr`则可以复制多次，其内部有一个计数器，复制一次便`+1`，有一个指针被销毁则`-1`，当计数器为0时则释放指向的内存。我们使用`std::make_shared`构造一个`std::shared_ptr`：

```C++
#include <memory>
#include <iostream>
using namespace std;

auto p = make_shared<char>('a'); //动态分配一块char大小的内存，并将指针指向这块内存，将初值设为'a'
auto q = p;                     //可以复制一个std::shared_ptr，此时计数器为2
*p = 'b';
cout << *p << *q;               //输出bb
```

使用智能指针可以避免手动管理内存，这是一个利器。然而智能指针可能引入其他问题，比如`std::shared_ptr`可能造成*循环引用*问题，这些都需要你自行了解并解决。

### 0x0C 尝试使用异常

你还记不记得`main()`函数的`return 0;`语句表示什么意思？老师可能讲过，如果程序正常退出将会返回`0`，而不正常退出则会返回其他值。而这个返回值是做什么用的呢？

让我们来编写这样一个函数，让用户输入一个字符，只有这个字符是数字的时候才返回对应的数字，否则都返回`-1`:

```C++
int input()
{
    char ch;
    cin >> ch;
    if('0' <= ch && ch <= '9')
        return ch - '0';
    return -1;
}
```

而如果我们调用这个函数，函数返回了`-1`，我们就知道用户输入的不是数字，可能是一个错误的输入。这样的机制称为**错误码机制**，即设定某些返回值代表**处理错误**，如果得到这个返回值，我们就可以对错误进行处理。

然而假如函数嵌套了很多层，当最里层的函数触发错误时，它必须一路返回到最上层处理错误，或者你不得不在每一层加入错误处理的代码。然而这样的做法并不优雅。

这时候我们就可以使用C++的错误处理机制。我们可以用`throw`抛出错误：

```C++
int input()
{
    ...;
    if('0' <= ch && ch <= '9')
        return ch - '0';
    throw ch;
}
```

无论这个函数嵌套了多少层，`throw`抛出的错误一定能被最上层直接接收到，而且如果你不处理错误的话，`throw`会直接中断程序——如果你使用错误码机制，你可以选择忽略错误码，这样相当于抱病运行。

我们可以使用`try..catch...`来处理错误：

```c++
try{
    input();         //把有可能抛出错误的代码放到try块中
}catch(char ch){     //catch会捕捉到数据类型相同的异常
    ...;             //处理异常
}
```

C++异常机制将强迫你处理异常，并且无需层层回调即可处理，当然，他也会衍生其他的问题，这些需要你自行了解。

本文到此结束，希望读者对*Modern C++*有一个大致的认识，并且能使用它来写代码。如果想要更深入学习*C++*，可以从STL入手，C++还有许许多多的内容等待你探索。



参考：

* *C++ Primer 5th*
* *Think in C++*
* *Effective C++*