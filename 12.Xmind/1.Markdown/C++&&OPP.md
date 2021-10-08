# C++&&OPP

## 宏观知识

### 编程范式

- 面向对象编程(类)

	- 特性

		- 封装
		- 继承
		- 多态

	- 自下而上，分析时:从对象->类->类上的类
设计与问题本质特性相对应的数据格式

		- 关注存储:数据结构

- 面向过程编程(c)

	- 自顶向下，将大型程序分解成小型
让语言满足问题要求

		- 关注逻辑:算法

- 泛型编程(模板)

	- 数据层->通用自然规律
忽略数据类型

- 函数式编程(lambda)

	- 告诉操作规则,而非提前

- 元编程

	- 基于模板的编译时期运算的编程方式，这种编程通常被称为模板元编程
(template meta-programming)
	- constexpr元编程
	- constexpr元编程与template元编程一样，都是图灵完备的
 即任何程序中需要表达的计算，都可以通过constexpr元编程的方式来表达

- 开发效率 = 编写代码+测试+维护的时间
- 首先确定编程范式;然后学习相应的语法特性;

### 程序=数据结构+算法

### C++设计哲学

- 尽可能在编译器报错:编译错误优于运行错误
- 异常处理:以抛异常的方式,尽可能使程序不崩溃而能够运行

### C++是C语言的超集

- 头文件:58个

	- C语言头文件29个

		- STL

			- 模板
			- lambda

## 程序生成

### 源代码.cpp

### 预编译器.i

- -E 只激活预处理
- gcc -E hello.c -o hello.i 或者 gcc  hello.c > hello.i
- 所有的 “#define” 删除，并展开所有的宏定义
处理所有的条件预编译指令，比如：" #if #ifdef #elif #else #endif "
处理所有的 “#include” 预编译指令
删除所有的注释 “//” 、 “/* */”
添加行号和文件名标识，以便编译时产生的行号信息以及用于编译错误或警告时能够显示行号
保留所有的 “#pragma” 编译器指令

### 编译器.s

- -S 只激活预处理和编译，就是指把文件编译成为汇编代码
-  gcc -S hello.i -o hello.s 或者  gcc -S hello.c -o hello.s
- 编译过程是编译器把预处理完的文件进行词法分析、语法分析、语义分析及优化后生成相应的汇编代码

### 目标代码.o

- -c

	- 只激活预处理,编译,和汇编，生成obj文件

- 汇编器

	- gcc -c hello.s -o hello.o 或者 gcc -S hello.c -o hello.o
	- 汇编是把汇编代码转变成中间目标文件

### 连接程序

- 启动代码

	- 程序与操作系统的接口
设置堆栈，调用main函数

- 库代码

	- 静态链接库.a
	- 动态链接库.so
	- 二者的区别仅在于程序执行时所需的代码是在运行时动态加载的，还是在编译时静态加载的

- 链接器ld

	- 从程序员角度，函数库实际上是一些头文件（.h）和库文件（so、或lib、dll）的集合。Linux下的大多数函数都默认将头文件放到/usr/include/目录下，而库文件则放到/usr/lib/目录下

### 可执行代码

-  gcc hello.c；默认会产生一个a.out 的可执行文件
- gcc−o test hello.c；会产生一个test的可执行文件

### g++选项

- -Dmacro

	- 相当于 C 语言中的 #define macro:-D_D自定义debug输出

- -Dmacro=defn

	- 相当于 C 语言中的 #define macro=defn

- -Umacro

	- 相当于 C 语言中的 #undef macro

- -undef

	- 取消对任何非标准宏的定义

- -include file

	- 功能就相当于在代码中使用#include<filename>

- -C

	- 在预处理的时候, 不删除注释信息, 一般和-E使用

- -Idir

	-  指定额外的头文件搜索路径dir
	- 在用 #include "file" 时, gcc/g++ 会先在当前目录查找你所指定的头文件, 如果没找到, 他回到默认的头文件目录找, 如果使用 -I 制定了目录,他会先在你所制定的目录查找, 然后再按常规的顺序去找。
	- 对于 #include<file>, gcc/g++ 会到 -I 制定的目录查找, 查找不到, 然后将到系统的默认的头文件目录查找 

- -llibrary

	- 链接时搜索指定的函数库library如-lpthread,-lm

- -Ldir

	- 指定额外的函数库搜索路径dir;比如你自己的库,不然编译器将只在标准库的目录找

- -O0 、-O1 、-O2 、-O3

	- 编译器的优化选项的 4 个级别，-O0 表示没有优化, -O1 为默认值，-O3 优化级别最高。

- -static

	- 禁止使用动态库，所以编译出来一般很大，不需要动态连接库，就可以运行。

- -std=

	- 指定编译语言版本

- -shared

	- 生成共享目标文件。通常用在建立共享库

- -g

	- 只是编译器，在编译的时候，产生调试信息。

- -w

	- 不生成任何警告信息

- -Wall

	- 生成所有警告信息

## C++相关命令

### ob

### nm -C

### strings

### c++filt

## C++基础

### 输入输出

- endl：控制符
\n：换行符

	- endl保证程序继续运行前刷新输出（立即显示，刷新缓存）
	- endl:插入换行符到输出序列 os 并冲入它，如同调用 os.put(os.widen('\n')) 后随 os.flush() 

- stdio

	- 格式化数据

- iostream

	- 流式数据

### 参数void

- c++中(空)与(void)等效，不接受任何参数
- c中(空)，对是否接受参数沉默

### 类型

- short至少16位， int至少和short等大
long至少32位，long至少和int等大

### 名称空间

- using编译指令

	- using 命名空间名::标识符名;
 //指定的某一个标识符暴露在当前的作用域内
using namespace 命名空间; 
//直接引用整个命名空间
//命名空间也是允许嵌套的，
namespace Outer{ 
    namespace Inner{  
        	class Class{ }; 
    }
} 
using Outer::Inner::Class;

- using相比与typedef可以定义模板类型

	- typedef void (*func_t)(int, int);
using func_t = void (*)(int, int);
	- template <typename T>
struct func_t
{
    typedef void (*type)(T, T);
};
// 使用 func_t 模板
func_t<int>::type xx_1;
/* C++11 */
template <typename T>
using func_t = void (*)(T, T);
// 使用 func_t 模板
func_t<int> xx_2;

- 名字空间的目的是分割全局共享的名字空间
- namespace worst {
     namespace n1 {}
     namespace n2{}
     using namespcace n1; 
     using namespcace n2;
}
- 内联的名字空间允许程序员在父名字空间定义或特化子名字空间的模板

### 类

- 数据抽象和行为抽象，对象是创建的实体

### 计算机存储数据

- 信息存储的位置
- 存储的值
- 存储信息的类型

	- 决定数据对象所占的内存
	- 决定如何解释内存中的位
	- 决定可使用的操作或方法

### 整型库

- inttypes

	- int64_t

- climtis

	- 包含整型限制信息
	- INT_MAX   INT_MIN

### 整型字面值

- 第一位
1~9
0
0

	- 第二位


x或X

		-  
十进制
八进制
十六进制

### 确定常量类型

- 整型常量

	- 默认为int，除非有后缀或值太大
	- 后缀

		- l或L long
u或U unsigned int

- 浮点常量

	- 默认为double
	- 后缀

		- f或F float
2.2L long double
2.3E10 double

### 浮点数

- 小数点表示法
- E或e表示法

	- d.dddE+n小数点右移n位
           -n小数点左移n位
浮点：小数点可移

### 算术运算符

- %

	- 满足：a%b = a - (a/b)*b

- /

	- 整型/整型 = 整型
有一个操作数为浮点，结果为浮点

- ++和--

	- 对于类而言：前缀是将值加1然后放回结果
后缀首先复制一个副本，将其加1然后将复制的副本返回
	- 对于用户定义的类型，前缀效率更高

- ，

	- 确保先计算第一个然后第二个表达式
逗号表达式的值是最后一部分的值

-  :: 范围解析运算符

	- 1. 全局作用域符（`::name`）：用于类型名称（类、类成员、成员函数、变量等）前，表示作用域为全局命名空间
2. 类作用域符（`class::name`）：用于表示指定类型的作用域范围是具体某个类的
3. 命名空间作用域符（`namespace::name`）:用于表示指定类型的作用域范围是具体某个命名空间的

		- int count = 11;         // 全局（::）的 count

class A {
public:
	static int count;   // 类 A 的 count（A::count）
};
int A::count = 21;

### 类型转换

- 初始化和赋值时转换：潜在数值转换

	- 可能造成结果不确定

- 列表初始化：{}初始化

	- 不允许缩窄
	- initializer_list 列表初始化
用花括号初始化器列表初始化一个对象，其中对应构造函数接受一个 `std::initializer_list` 参数.
	- #include <initializer_list>
template <class T>
struct S {
    std::vector<T> v;
    S(std::initializer_list<T> l) : v(l) {
         std::cout << "constructed with a " << l.size() << "-element list\n";
    }
    void append(std::initializer_list<T> l) {
        v.insert(v.end(), l.begin(), l.end());
    }
    std::pair<const T*, std::size_t> c_arr() const {
        return {&v[0], v.size()};  // 在 return 语句中复制列表初始化
                                   // 这不使用 std::initializer_list
    }
};
	- for (int x : {-1, -2, -3}) // auto 的规则令此带范围 for 工作
        std::cout << x << ' ';
	- vector<int> func() {
    return {3,5};
}

		- 返回一个初始化列表，通常会导致构造一个临时变量

	- const vector<int> &func() {
    return {3, 5};
}

		- 如果返回值是一个引用类型的话，则会返回一个临时变量的引用
		-  必须要加const限制符,该规则与返回一个字面常量是一样的

- 表达式转换

	- 整形提升

- 传参时的转换

	- 由函数原型控制，也可取消。取消时会对char，short整形提升，float提升为double

- 强制类型转换

	- (typename) value C语言
typename (value) c++支持，表现的像函数
	- 强制类型转换运算符

		- static_cast<>等4个

### auto

- 变量的类型设置初始值的类型

### 数组

- 初始化

	- {}：对部分元素初始化，其他元素则设置为0
	- 自动计数
int array[] = {1,2,3,4};
cnt = sizeof(array) / sizeof(int);

- int arr[10]

	- arr = &arr[0] 是第一个元素的地址
&arr 是整个数组的地址
&arr + 1 = arr + 10 + 1

- int (*ptr)[10] = &arr

	- *ptr = arr
ptr = &arr

### 字符串

- 初始化

	- 数组初始化，则末尾元素为‘\0'
	- ""初始化，隐式包含空字符

- 字符串常量(字符串字面值)

	- 表示字符串第一个祖父所在的内存地址
char *，char []也是
	- c++不保证字符串字面值被唯一存储

### 结构

- 对齐

	- #pragma pack(n)
设定结构体、联合以及类成员变量以 n 字节方式对齐
	- #pragma pack(push)  // 保存对齐状态
#pragma pack(4)     // 设定为 4 字节对齐

struct test
{
    char m1;
    double m4;
    int m3;
};

#pragma pack(pop)   // 恢复对齐状态

- struct结构体

	- struct

- union共用体

	- 限制

		- 默认访问控制符为 public
		- 可以含有构造函数、析构函数
		- 不能含有引用类型的成员
		- 不能继承自其他类，不能作为基类
		- 不能含有虚函数
		- 匿名 union 在定义所在作用域可直接访问 union 成员
		- 匿名 union 不能包含 protected 成员或 private 成员
		- 全局匿名联合必须是静态（static）的

	- union UnionTest {
    UnionTest() : i(10) {};
    int i;
    double d;
};

static union {
    int i;
    double d;
};

		- int main() {  
    UnionTest u;
    union {
        int i;
        double d;
    };
    std::cout << u.i << std::endl;  // 输出 UnionTest 联合的 10
    ::i = 20;
    std::cout << ::i << std::endl;  // 输出全局静态匿名联合的 20
    i = 30;
    std::cout << i << std::endl;    // 输出局部匿名联合的 30
}

	- C++11

		- 何非引用类型都可以成为联合体的数据成员，这样的联合体即所谓的非受限联合体（Unrestricted Union）

- enum枚举

	- 类中可替代const，常见符号常量
	- 显示设置枚举值,只能为整数
未被初始化默认比前面加+1，默认从0开始

		- enum  bits {zero one , nine = 9, ten};

	- 设定

		- 具名的enum类型的名字，以及enum的成员的名字都是全局可见的。这与C++中具名的namespace、class/struct及union必须通过“名字::成员名”的方式访问相比是格格不入的（namespace等被称为强作用域类型，而enum则是非强作用域类型）

	- 限定作用域的枚举类型或叫强类型枚举

		- enum class Color : int { red, green = 20, blue };
Color r = Color::blue;
switch(r)
{
    case Color::red  : std::cout << "red\n";   break;
    case Color::green: std::cout << "green\n"; break;
    case Color::blue : std::cout << "blue\n";  break;
}
// int n = r; // 错误：不存在从有作用域枚举到 int 的转换
int n = static_cast<int>(r); // OK, n = 21

	- 不限定作用域的枚举类型

		- 无作用域枚举类型的值可隐式转换为整型类型
		- enum color { red, yellow, green };
		- enum { floatPrec = 6, doublePrec = 10 };

	- 强类型作用域

		-  强作用域

			- 限定作用域用于解决重名
			- 强类型枚举成员的名称不会被输出到其父作用域空间

		- 转换限制

			- 强类型枚举成员的值不可以与整型隐式地相互转换

		- 可以指定底层类型

			-  强类型枚举默认的底层类型为int,
			-  但也可以显式地指定底层类型，具体方法为在枚举名称后面加上“：type

	- 检查枚举是否完备

		- #define assert_static(expr) \
    do {enum {assert_static__ = 1 / (expr)}; } while (0)
enum FeatureSupports {
    One   = 0x00001,
    Two   = 0x00002,
    Three = 0x00004,
    Four  = 0x00008,
    MAX   = 0x00010,
};

int main() {
    //检查枚举值的完备性
    assert_static((MAX - 1) == (One | Two | Three | Four));
} 

### 指针

- 空指针

	- C语言宏NULL：0

		- 0可用做地址和整型

	- nullptr(c++11)

- *运算符被称为间接值或解除引用运算符
- 指针不是整型，即使计算机通常把地址当做整型处理
- 静态联编和动态联编

	- 编译时给数组分配内存，指定长度
	- 运行时创建，动态数组。new分配空间

### 指针和数组

- 指针和数组基本等价在于指针运算和c++内部处理数组的方式
- 指针的值可修改，数组名是变量
- sizeof(array) = 数组长度
sizeof(ptr) = 指针长度
- sizeof

	- sizeof((Class *)0->member);

		-  技巧:强制转换0为一个Class类的指针，继而通过指针的解引用获得其成员变量，并用sizeof求得该成员变量的大小

	- sizeof(Class::member);(C++11)

- 当且仅当在函数头和函数原型中int *arr 与int arr[]含义相同。表示arr是一个int指针
在其他上下文两者不同
int arr[] 表示arr不仅指向一个int类型，还指向数组的一个元素

### typedef：类型别名

- 为已有类型建立新名称，而不是建立新类型

### EOF：文件末尾

- ~scanf
scanf != EOF

### cctype库

- isalnum 字母或数字
isalpha 字母
isdigit 数字

## 函数

### 函数

- 函数不能直接返回数组，却可以把数组当做结构或对象的组成部分
- 结构变量和数组都可以存储多个数据项，但结构变量行为更接近于基本的单值变量 
- 函数指针 :typedef returnType (*ptr)(arg...);
- 函数的执行

	- 函数调用后立即存储该指令的内存地址，并将参数参数复制到堆栈(保留的内存块)，跳到标记函数起点的内存单元，执行函数代码（也需需要保存返回值到寄存器），然后跳回到原来被保存的指令处

- 单定义规则：所有非内联函数只可以在一个文件中包含函数定义，同一内联函数所有定义相同
- 所有函数静态存储；默认外部链接：可在文件间共享，static可设为内部；静态函数覆盖外部定义
- 查找函数

	- 若该函数原型指出函数是静态的（static），则只在该文件查找函数定义。否则在所有程序（包括链接程序）中查找函数定义。未找到则在库中搜索
	- 定义一个与库函数同名的函数，程序员定义的版本将覆盖库函数

### inline内联函数

- 特征

	- 相当于把内联函数里面的内容写在调用内联函数处；
相当于不用执行进入函数的步骤，直接执行函数体；
相当于宏，却比宏多了类型检查，真正具有函数特性；
	- 编译器一般不内联包含循环、递归、switch 等复杂操作的内联函数；
	- 在类声明中定义的函数，除了虚函数的其他函数都会自动隐式地当成内联函数。

- 使用

	- 函数定义或声明时：inline int functionName(int first,...);
一般定义时使用
	- 可将内联函数定义放在头文件，c++要求就同一函数的所有内联定义必须相同

- 步骤

	- 1. 将 inline 函数体复制到 inline 函数调用点处；
	- 2. 为所用 inline 函数中的局部变量分配内存空间；
	- 3. 将 inline 函数的的输入参数和返回值映射到调用方法的局部变量空间中； 
	- 4. 如果 inline 函数有多个返回点,将其转变为 inline 函数代码块末尾的分支(使用 GOTO)

- 优缺点

	- 优点

		- 1. 内联函数同宏函数一样将在被调用处进行代码展开,省去了参数压栈/栈帧开辟与回收,结果返回等.从而提高程序运行速度
		- 2. 内联函数相比宏函数来说，在代码展开时，会做安全检查或自动类型转换（同普通函数），而宏定义则不会。 
		- 3. 在类中声明同时定义的成员函数，自动转化为内联函数，因此内联函数可以访问类的成员变量，宏定义则不能。
		- 4. 内联函数在运行时可调试，而宏定义不可以。

	- 缺点

		- 1. 代码膨胀。内联是以代码膨胀（复制）为代价，消除函数调用带来的开销。消耗更多的内存空间。
		- 2. inline 函数无法随着函数库升级而升级。inline函数的改变需要重新编译，不像 non-inline 可以直接链接。
		- 3. 是否内联，程序员不可控。内联函数只是对编译器的建议，是否对函数内联，决定权在于编译器。

### 引用&

- 引用是变量的别名
- 必须在声明引用变量时进行初始化
- 返回引用

	- 注意引用对象不可是临时变量

		- 返回函数参数中的引用
		- new来分配新空间

### 函数默认参数

- 从右向左添加默认值

### 函数重载（函数多态）

- 函数特征标：函数的参数列表

	- 参数的数目，类型，排列顺序
	- 类型引用和类型本身为统一特征标
int func(int x); int func(int &x);
void func(char *bits);    //overload
void func(const char *bits); //overload
不区分const

- C++跟踪每一个重载函数通过名称修饰：根据名称类型对函数名加密，根据编译器

### 模板

- template

## 内存模型

### 存储持续性

- 自动存储

	- 局部变量，函数参数等
	- 栈

		- 两个指针（栈底和栈顶）根据栈，

- 静态存储

	- static定义的变量，以及全局变量

- 动态存储

	- 自由存储或堆

- 线程存储（C++11）

	- thread_local声明，生命周期与所属线程一样长

### 作用域

- 同名变量（一个外部代码块，一个内部）隐藏

### 链接性

- 外部链接性：可在其他文件访问
- 内部链接性：只能在当前文件访问
- 无链接性：只能在当前函数或代码块访问

### extern

- 外部:被 extern 限定的函数或变量是 extern 类型的
- exrten “C”

	- 被 `extern "C"` 修饰的变量和函数是按照 C 语言方式编译和链接的

		- #ifdef __cplusplus
extern "C" {
#endif

void *memset(void *, int, size_t);

#ifdef __cplusplus
}
#endif

	- `extern "C"` 的作用是让 C++ 编译器将 `extern "C"` 声明的代码当作 C 语言代码处理，可以避免 C++ 因符号修饰导致代码不能和C语言库中的符号进行链接的问题。

- __cplusplus这个宏只有“被定义了”和“未定义”两种状态。事实上却并非如此，__cplusplus这个宏通常被定义为一个整型值,_一般会是一个比以往标准中更大的值
- #if __cplusplus < 201103L
   #error "should use C++11 implementatinon"
#enif

### static

- 1. 修饰普通变量，修改变量的存储区域和生命周期，使变量存储在静态区，在 main 函数运行前就分配了空间，如果有初始值就用初始值初始化它，如果没有初始值系统用默认值初始化它。
- 2. 修饰普通函数，表明函数的作用范围，仅在定义该函数的文件内才能使用。为了防止与他人命名空间里的函数重名，可以将函数定为 static。
- 3. 修饰成员变量，修饰成员变量使所有的对象只保存一个该变量，而且不需要生成对象就可以访问该成员。
- 4. 修饰成员函数，修饰成员函数使得不需要生成对象就可以访问该函数，但是在 static 函数内不能访问非静态成员。

### const

- 作用

	- const修饰的全局变量的链接性为内部；保证了每个文字使用自己的一组常量，而非所有文件共享一组
const int var = 10; 相当于 static const int var = 10;
若定义为外部，则可extern const int state = 10; 但只可以在一个文件初始化
	- 1. 修饰变量，说明该变量不可以被改变；
	- 2. 修饰指针，分为指向常量的指针（pointer to const）和自身是常量的指针（常量指针，const pointer）；
	- 3. 修饰引用，指向常量的引用（reference to const），用于形参类型，即避免了拷贝，又避免了函数对值的修改；没有 const reference，因为引用本身就是 const pointer
	- 4. 修饰成员函数，说明该成员函数内不能修改成员变量。

- code

	- // 类
class A
{
private:
    const int a;                
// 常对象成员，只能在初始化列表赋值
public:
    // 构造函数
    A() : a(0) { };
    A(int x) : a(x) { };        // 初始化列表
   // const可用于对重载函数的区分
    int getValue();             // 普通成员函数
    int getValue() const;  
     // 常成员函数，不得修改类中的任何数据成员的值
};

		- void function()
{
    // 对象
    A b;               // 普通对象，可以调用全部成员函数、更新常成员变量
    const A a;         // 常对象，只能调用常成员函数
    const A *p = &a;    // 指针变量，指向常对象
    const A &q = a;     // 指向常对象的引用
    // 指针
    char greeting[] = "Hello";
    char* p1 = greeting;                // 指针变量，指向字符数组变量
    const char* p2 = greeting;  
  // 指针变量，指向字符数组常量(const 后面是 char，说明指向的字符(char)不可改变)
    char* const p3 = greeting; 
 // 自身是常量的指针，指向字符数组变量(const 后面是 p3，说明 p3 指针自身不可改变)
    const char* const p4 = greeting;    // 自身是常量的指针，指向字符数组常量
}

			-  //函数
void function1(const int Var);           // 传递过来的参数在函数内不可变
void function2(const char* Var);         // 参数指针所指内容为常量
void function3(char* const Var);         // 参数指针为常量
void function4(const int& Var);          // 引用参数在函数内为常量

// 函数返回值
const int function5();      // 返回一个常数
const int* function6();     // 返回一个指向常量的指针变量，使用：const int *p = function6();
int* const function7();     // 返回一个指向变量的常指针，使用：int* const p = function7();

### volatile

- volatile 关键字是一种类型修饰符，用它声明的类型变量表示可以被某些编译器未知的因素（操作系统、硬件、其它线程等）更改。所以使用 volatile 告诉编译器不应对这样的对象进行优化。
- volatile 关键字声明的变量，每次访问时都必须从内存中取出值（没有被 volatile 修饰的变量，可能由于编译器的优化，从 CPU 寄存器中取值） 
- const 可以是 volatile （如只读的状态寄存器）
- 指针可以是 volatile

### new和delete

- 使用

	- new和delete成对出现，而且new分配的内存只可用delete，同样delete也应只释放new分配的内存
	- new[]和delete[]成对
	- delete不可重复释放一块内存两次
	- 空指针使用delete是安全的

- 作用

	- 1. new / new[]：完成两件事，先底层调用 malloc 分配了内存，然后调用构造函数（创建对象）
	- 2. delete/delete[]：也完成两件事，先调用析构函数（清理资源），然后底层调用 free 释放空间
	- 3. new 在申请内存时会自动计算所需字节数，而 malloc 则需我们自己输入申请内存空间的字节数
	- new分配失败引发异常：std::bad_alloc

- new初始化

	- int *ar = new int[4] {2, 4, 6, 7};
int *pi = new int(6); 
int *pi = new int {6);

- 定位new

	- 定位 new允许我们向 new 传递额外的地址参数，从而在预先指定的内存区域创建对象。
	- code

		- place_address 是个指针
initializers提供一个（可能为空的）以逗号分隔的初始值列表
		- new (place_address) type
new (place_address) type (initializers)
new (place_address) type [size]
new (place_address) type [size] { braced initializer list }
		- int buffer[20]; //全局
int main{
    int *p = new (buffer) int[20]; 
}

- delete this

	- 须保证 this 对象是通过 new(不是 new[]、不是 placement new、不是栈上、不是全局、不是其他对象成员)分配的
	- 必须保证 delete this后不在调用this以及相关成员函数

### 原地构造

- template<typename T>
vector<T>::vector(int n) : __capacity(n), __size(0), data(nullptr) {
     data = (T *)malloc(sizeof(T) * __capacity);
 }

template<typename T>
vector<T>::vector(const vector<T> &v) {
     __size = v.__size;
     __capacity= v.__capacity;
     data = (T *)malloc(sizeof(T) * __size);
     for (int i = 0; i < __size; i++) {
         //data[i] = v.data[i];
         //原地构造
         new (data + i)T(v.data[i]);
     }
 }

### 限定对象的存储区

- 只能在堆上

	- 将析构函数设置为私有或delete

		- C++ 是静态绑定语言，编译器管理栈上对象的生命周期，编译器在为类对象分配栈空间时，会先检查类的析构函数的访问性。若析构函数不可访问，则不能在栈上创建对象。

- 只能在栈上

	- 将 new 和 delete 重载为私有

		- 在堆上生成对象，使用 new 关键词操作，其过程分为两阶段：第一阶段，使用 new 在堆上寻找可用内存，分配给对象；第二阶段，调用构造函数生成对象。将 new 操作设置为私有，那么第一阶段就无法完成，就不能够在堆上生成对象。

## 面向对象

### 特征

- 封装

	- 数据隐藏

		- public成员：可以被任意实体访问
		- protected成员：只允许被子类及本类的成员函数访问
		- private成员：只允许被本类的成员函数、友元类或友元函数访问
		- class默认为private，struct默认为public

- 继承

	- 继承(泛化)

		- 实现继承
		- 可视继承

	- 组合(聚合)

		- 接口继承
		- 纯虚类

- 多态

	- 覆盖

		- 虚函数
		- 接口

	- 重载

		- 同名函数

	- 类型

		- 1. 重载多态（编译期）：函数重载、运算符重载
		- 2. 子类型多态（运行期）：虚函数
		- 3. 参数多态性（ 编译期）：类模板、函数模板
		- 4. 强制多态（编译期/运行期）：基本类型转换、自定义类型转换

###  explicit(显式)

- explicit 修饰构造函数时，可以防止隐式转换和复制初始化
-  explicit 修饰转换函数时，可以防止隐式转换，但按语境转换除外
- code

	- struct A {
	A(int) { }
	operator bool() const { return true; }
};
struct B {
	explicit B(int) {}
	explicit operator bool() const { return true; }
};
void doA(A a) {}
void doB(B b) {}

	return 0;
}

		- int main()
{
	A a1(1);		// OK：直接初始化
	A a2 = 1;		// OK：复制初始化
	A a3{ 1 };		// OK：直接列表初始化
	A a4 = { 1 };		// OK：复制列表初始化
	A a5 = (A)1;		// OK：允许 static_cast 的显式转换 
	doA(1);			// OK：允许从 int 到 A 的隐式转换
	if (a1);		// OK：使用转换函数 A::operator bool() 的从 A 到 bool 的隐式转换
	bool a6（a1）;		// OK：使用转换函数的隐式转换
	bool a7 = a1;		// OK：使用转换函数 的隐式转换
	bool a8 = static_cast<bool>(a1);  // OK ：static_cast 进行直接初始化


			-  B b1(1);		// OK：直接初始化
	B b2 = 1;		// 错误：被 explicit 修饰构造函数的对象不可以复制初始化
	B b3{ 1 };		// OK：直接列表初始化
	B b4 = { 1 };	// 错误：被 explicit 修饰构造函数的对象不可以复制列表初始化
	B b5 = (B)1;		// OK：允许 static_cast 的显式转换
	doB(1);			// 错误：被 explicit 修饰构造函数的对象不可以从 int 到 B 的隐式转换
	if (b1);		// OK：被 explicit 修饰转换函数 的按语境转换
	bool b6(b1);		// OK：被 explicit 修饰转换函数的按语境转换
	bool b7 = b1;		// 错误：被 explicit 修饰转换函数 B::operator bool() 的对象不可以隐式转换
	bool b8 = static_cast<bool>(b1);  // OK：static_cast 进行直接初始化

- const，explicit等约束目的：在编译阶段出错优于在运行阶段出错

## 封装

### 类

- 类对象

	- 初始化

		- Stock s = Stock(argu);

			- 创建指定值的对象，可能会创建临时对象

	- 赋值

		- Stock s;  s = Stock(argu);

			- 开辟对象数据区,匹配构造函数->匹配拷贝构造函数->完成构造

- 类成员函数

	- 外部定义成员函数时，使用作用域解析符(::)表示函数所属类
	- 类方法可访问类的private数据
	- 在类声明中定义的函数，除了虚函数，都会自动隐式地当成内联函数 ，类外需显式
	- 初始化列表

		- 就相当于调用构造函数,若未显式调用,则隐式调用默认构造函数

- 成员属性和方法

	- 对于成员属性,谁新建,谁就销毁

- 类属性和方法

	- static修饰成员属性和方法

		- 对于非const属性的整型，以及非constexpr属性需要类外定义，类内只是声明
		- 静态成员的定义最后只存在于一个目标文件中

	- Class_name::static_member
Class_name::static_func

### RVO
返回值优化

- ClassName func() {
    ClassName temp_a("info");
    return temp_a;
}
int main() {
   ClassName a = func();
   return 0;
}

	- 1.开辟a对象数据区
	- 2.调用函数func
	- 3,开辟对象temp_a数据区
	- 4.调用temp_a对象的构造函数
	- 5.使用temp_a调用临时匿名变量的拷贝构造函数
	- 6.销毁temp_a对象
	- 7.使用临时匿名变量调用a的拷贝构造函数
	- 8.销毁临时匿名变量
	- 9.销毁a对象

- 原来3个对象a,temp_a,临时匿名对象;将复制方式改为剪切,内存对临时变量进行了优化;
- 根据编译环境的不同优化层级不一定
- g++ -fno-elide-constructors RVO.cpp

	- 关闭RVO

### 类的默认函数
由编译器提供

- 成员函数

	- 构造函数❑
拷贝构造函数 
拷贝赋值函数(operator =)
移动构造函数
移动拷贝函数
析构函数

- 全局默认操作符函数

	- operator,
operator &
operator &&
operator *
operator ->
operator ->*
operator new
operator delete

- 一旦程序员实现了这些函数的自定义版本，则编译器不会再为该类自动生成默认版本
- 在C++11中，如果用户已经声明了一个拷贝复制操作符或者一个析构函数，那么编译器不会隐式声明一个拷贝构造函数。同样，如果用户已经声明了一个拷贝构造函数或者析构函数，编译器则不会隐式地声明一个拷贝复制操作符
- Class() {}
Class() = default;

	- 前者非POD,编译器失去了优化这样简单的数据类型的可能

### 特殊成员函数

- 默认构造函数

	- 先构造属性在构造类
	- 零参(缺省)构造函数
	- Class_name::Class_name() : mem(显示) 调用默认构造函数 {}
	- default关键字

		- 解决对于创建未初始化的对象的二义性
		- 由编译器生成一个缺省的构造函数

			- 如果类的某个成员变量的类型不存在缺省构造函数，那编译器就没有办法生成一个缺省构造函数，即使强行指定=default，它的意思也是“生成一个缺省的=delete”

		- 局限于成员函数

	- delete关键字

		- delete修饰的函数为删除（deleted）函数
		- 可用于成员函数和普通函数

- 默认析构函数

	- ~Class_name::Class_name() {}

- 赋值运算符重载函数

	- Class_name& Classname::operator=(const Class_name &);
	- 对已有对象赋值给另一对象：Stock init(argu); Stock s;  s = init;
初始化对象时不一定
	- 避免对同一对象进行赋值操作：if (this == &add) return *this;
	- 默认功能

		- 逐个复制非静态成员（浅复制），复制成员的值

- 地址运算符

	- 默认功能

		- 返回this指针的值

- 默认拷贝构造函数

	- Class_name(const Class_name &);

		- const &

			- 如果传值会重复调用拷贝构造
所以要使用引用

	- 功能

		- 逐个复制非静态成员（浅复制），复制成员的值

- 移动赋值运算符(C++11)
- 移动构造函数(C++11)

	- 移动语义一定是要修改临时变量的值
	- Moveable(const Moveable &&)

		- 会使得的临时变量常量化，成为一个常量右值，那么临时变量的引用也就无法修改，从而导致无法实现移动语义。因此在实现移动语义一定要注意排除不必要的const关键字 

	- 应该尽量编写不抛出异常的移动构造函数，通过为其添加一个noexcept关键字,否则可能导致一些指针就成为悬挂指针

		- 导致一些指针就成为悬挂指针

- 拷贝、移动构造函数

	- T Object(T &)
T Object(const T &)
T Object(T &&)

- 构造函数

	- 创建未初始化的对象 Stock s;

		- 为构造函数所有参数提供默认值
		- 函数重载一个没有参数的构造函数

	- Class_name::Class_name A = 2;

		- 初始化时调用构造函数

	- A = 3;

		- 默认是调用构造函数,如果对operator=重载,调用重载

	- 转换构造函数(参数个数为1的构造函数)

		- 普通转换构造函数的应用
		- 函数传值过程中的转换构造函数的应用
		- explicit

- 析构函数

	- 创建对象前，c++会检测是否可以析构

		- 析构函数写成 private ，或者写成 =delete ，那么这个类就不能被继承了，因为⼦类的析构函数⽆法调⽤⽗类的析构函数

	- 不应显式调用
应由系统调用

		- 需要资源回收的时候调用
		- 静态存储类对象，程序结束时调用
		- 自动存储类对象，程序执行玩对应代码块（其定义）时
		- 通过new创建的对象，delete时
		- 程序创建临时对象完成特定操作，结束对该对象的使用时

	- 栈区
int main () {
    A a;
    A b = 8;
    A c(a);
}

		- a,b,c依次调用构造函数

			- c,b,a依次调用构造函数

		- 栈底     栈顶
a     b   c

			- 在栈空间依次出栈

	- 全局静态区
A aa;
A bb(&aa);
A cc(&bb):
int main(){}
	- 构造顺序一定与析构顺序相反

		- 因为后面的构造的可能依赖于前面的信息;信息的依赖关系

- 拷贝构造函数

	- 调用

		- Class_name ditto = motoo;
Class_name ditto = Class_name(motoot);

			- 可能通过复制构造函数直接创建，也可能生成一个临时对象，再赋值给ditto

		- 复制构造函数：将新对象初始化为一个同类对象
初始化一个匿名对象，并将新对象地址赋值给ptr

			- Class_name ditto(motoo);
Class_name *ptr = new Class_name(motoo);

		- 程序生成对象副本时：函数按值传递或函数返回对象时调用，生成临时对象时

- 系统的拷贝构造函数和构造函数不同，该函数不可重载；析构函数不可重载
- 赋值操作运算符重载函数，其default和delete型和拷贝函数一致
- 拷贝操作保留源对象，移动操作可修改源对象，还可能转让所有权，而不做任何复制
- 继承基类成员函数

	- 子类可以通过使用using声明来声明继承基类的构造函数
	- using Base::func

- 继承构造函数

	- using Base::Base
	- 有的时候，基类构造函数的参数会有默认值。对于继承构造函数来讲，参数的默认值是不会被继承的。事实上，默认值会导致基类产生多个构造函数的版本，这些函数版本都会被派生类继承。
	- 多继承情况

		- 通过显式定义继承类的冲突的构造函数，阻止隐式生成相应的继承构造函数来解决冲突。

	- 如果一旦使用了继承构造函数，编译器就不会再为派生类生成默认构造函数

- 委派构造函数

	- 原则上，编译器不允许在构造函数中调用构造函数
	- 委派构造的一个很实际的应用就是使用构造模板函数产生目标构造函数
	- class TDConstructed {
public :
    TDConstructed(vector<short> &v) : TDConstructed(v.begin(), v.end()) {}
    TDConstructed(deque<int> &d) :TDConstructed(d.begin(), d.end()) {}
private :
    template<typename T> 
    TDConstructed(T first, T last) : l(first, last) {}
    list<int> l;
};

### 三/五法则
拷贝构造，
拷贝赋值函数，
析构函数

- 需要析构函数的类也需要拷贝构造函数和拷贝赋值函数

	- 深拷贝

- 需要拷贝操作的类也需要赋值操作，反之亦然。
- 析构函数不能是删除的

	- 不能定义局部变量：delete析构函数、private 析构函数
	- 可以newA :*p = new A(); 不可以delete

- 如果一个类成员有删除的或不可访问的析构函数，那么其默认和拷贝构造函数会被定义为删除的
- 如果一个类有const或引用成员，则不能使用合成的拷贝赋值操作。
（无法默认构造的const成员的类 则该类就无默认构造函数）

	- 只能使用初始化列表的方式
	- 函数内部并不是严格的初始化，初始化是构造函数；
初始化列表是调用相关成员的构造函数，能用初始化列表，绝不在内部实现；函数内部应是逻辑代码
	- class A {
public :
    A() : z(0),w(this->x) {};
    A(const A &a) : z(8), w(this->x) {
        this->x = a.x;
        this->y = a.y;
    }
    A(int x, int y) : w(x), x(x), y(y), z(7) {}
private:
    int x, y;
    const int z;
    int &w;
};


### 成员初始化列表

- 按着类声明顺序构造而非列表顺序，构造和赋值（先构造在赋值）不一样
- 少了一次调用默认构造函数的过程
- 1. 常量成员，因为常量只能初始化不能赋值，所以必须放在初始化列表里面
- 2. 引用类型，引用必须在定义的时候初始化，并且不能重新赋值，所以也要写在初始化列表里面
- 3. 没有默认构造函数的类类型，因为使用初始化列表可以不必调用默认构造函数来初始化

### 深浅拷贝

- 浅拷贝:拷贝的是对象的地址而不是对象的值
- 深拷贝:新建空间进行对象的整体拷贝
-     修改拷贝值是否会更改原值：是：浅；否：深
    如果是拷贝构造，会定义成深拷贝;浅拷贝，不要创建对象，只做指针的引用

### 返回对象

- 返回指向const对象的引用

	- 返回对象调用拷贝构造函数，返回引用不会
引用指向的对象应存在
参数为const，返回参数，其返回类型也应是const

- 返回非const对象的引用

	- operator=()的返回值用于连续赋值：提高效率 s3 = s2 = s1;
	- operator<<()的返回值用于串接输出：必须这样做

- 返回对象
- 返回const对象

	- 检错

### 就地初始化

- 类内就地初始化与构造函数中是用成员初始化效果等同
class Name { int val = 10;};
Name::Name() : val(10) {...};
- 在C++11中,允许使用等号=或者花括号{}进行就地的非静态成员变量初始化
- 限制

	- 1.需要初始化的数据为公有性访问
	- 2.不要显式定义默认的构造函数
	- TIPS：上述两点在于保证其就地初始化的“数据性”
	- 3.定义与其匹配的构造函数
	- 就地圆括号式的表达式列表初始化非静态成员导致编译出错

		- struct A {
    A(int i) : val(i) {}
    int val;
};

struct init {
    
    A x = 1; //ok
    A z{1}; // ok
    A y(1); // not allow 
    string b("hello"); // not allow
};
		- 子主题 2

### const
static
mutable

- static 修饰的是类成员函数和类成员变量
 所有的对象拿到的都是同一份类成员变量
 类成员函数可以使用普通对象调用，也可以使用类调用
- const 对象只能调用const函数;非const对象即能调用非const也能调用const
const成员变量初始化必须使用初始化列表
const成员函数里不可修改成员变量的值;如果成员变量定义前加了mutable，表示成员可以在const成员函数里修改;
在部分场景下，需要定义const版本和非const两个版本的函数

### 友元

- (1) 友元关系不能被继承。 
(2) 友元关系是单向的，不具有交换性。
 若类B是类A的友元，类A不一定是类B的友元,要看在类中是否有相应的声明。
(3) 友元关系不具有传递性。
若类B是类A的友元，类C是B的友元，类C不一定是类A的友元，同样要看类中是否有相应的声明
- 友元的作用，使外部也可以访问私有成员
 声明友元函数
    friend void showMe(SomeBody &);
 声明为友元类 友元类里的所有成员函数都可以访问被友元的类的私有变量
    friend class Friend;

### 转换函数

- 类转换为其他类型
- 转换函数必须是类方法
不能指定返回类型
不能有参数

	- operator typenaem();

### 对象数组

- 必须有默认构造函数；使用默认构造函数穿件数组元素，然后{}中的构造函数建创建临时对象，然后复制到对应元素
- code

	- Stock array[4] = {Stock(1), stock(2)};

### 作用域为类的常量

- 枚举

	- enum {X = 12};

- 静态

	- static const int X = 12;

		- 类内静态整型常量：const只可为int，char，long等整型实现就地初始化

	- static constexpr Type obj = value;

		- Type 任意类型

- 只是const int X = 12; 不可行；创建对象前没有存储空间

### 类成员函数指针

- int(Class:*func)() = &Class:TestFunc;
(obj.*func)();

	- typedef int(Class::*func)();
func f = &Class::TestFunc
	- using func = int(Class::*)();

## 继承

### 继承

- 继承的类， 对于父类当中成员函数,系统会隐式调用其默认的构造函数,如果没有，必须显示调用-->成员初始化列表()
- 继承权限

	- 影响子类对外的访问权限
	- public：可以被任意实体访问
	- protected：只允许当前类类的派生类访问
	- private：不允许访问
	- class默认为private，struct默认为public

- 继承封装

	- private 本类当中可以访问，派生类不可访问
	- protected   public降为protected
	- public      不更改任何权限

- 对于private继承派生类： 其父类的protected ，public相当于放在当前private下
-     继承只能缩减封装，不能扩充封装权限
    继承权限的限制是影响下一代的
    如果没有后继类，可以设置为private私有继承
    如果不希望更改任何原先的成员权限，可以设置为public
    如果希望数据对外部保护，内部公开，设置为protected
- 谁构造谁释放
在讨论继承的时候，脑⼦⾥要想的是：cat ∈ {animal}。
- ⾥⽒代换原则的内容只有⼀句话：⼦类的对象能够替换其基类的对象被使⽤。举 个例⼦，任何使⽤ Animal 的地⽅，我们都可以放 Cat 进去，⽽完全不扰乱程序的逻 辑。⽽且程序⾥⾯关于 Animal 的假设， Cat 都不能打破。

### 基类与派生类

- 派生类不继承构造函数，析构函数，赋值运算符，和友元
- 关系

	- 派生类对象可以使用基类的非私有方法
	- 基类指针（引用）可以隐式类型转换指向派生类对象

		- virtual

- 继承

	- is-a关系：水果-苹果

- 作为数据成员

	- has-a关系：水果-午饭

### 构造

- 创建派生类时，首先创建基类，初始列表完成
- Cat() : Animal("cat") {}
- B->A->A:->{A}->B:->{B}

	- X 开辟X的数据区
X 执行初始化列表
{X} 执行构造逻辑

- 存储区域:父类属性,子类属性

	- 子类包含父类的所有属性,但不一定能访问
	- 内存空间排列顺序

		- 类的首地址
		- 父类属性

			- 前半部分

		- 子类属性

			- 后半部分

- 拷贝&赋值--继承

	- 拷贝构造函数

		- 显式调用父类拷贝构造函数
		- Cat(const Cat &a) : Animal(a),__member(a.__member) {}

	- 赋值运算符

		- 显式调用父类的赋值运算函数
		- Cat &operatro=(const Cat &a) {
   this->__member = a.__member;
   this->Animal::operator=(a);
   return *this;
}

### 虚继承

- 解决歧异性问题

	- 1.指定访问的域
	- 2.virtual 虚继承

		- 虚基类

- 针对菱形继承，可以使用虚继承

	- 1.此时无法在访问到基类（父类）对应的值
	- 2.产生的对象的空间因此发生改变

- code

	- struct B { int n; };
class X : public virtual B {};
class Y : virtual public B {};
class Z : public B {};
// 每个 AA 类型对象拥有一个 X，一个 Y，一个 Z 和两个 B：
// 其一是 Z 的基类，另一者为 X 与 Y 所共享
struct AA : X, Y, Z {
    void f() {
        X::n = 1; // 修改虚 B 子对象的成员
        Y::n = 2; // 修改同一虚 B 子对象的成员
        Z::n = 3; // 修改非虚 B 子对象的成员
 
        std::cout << X::n << Y::n << Z::n << '\n'; // 打印 223
    }
};

- 实现

	- 底层实现原理与编译器相关，一般通过虚基类指针和虚基类表实现，每个虚继承的子类都有一个虚基类指针（占用一个指针的存储空间）和虚基类表（不占用类对象的存储空间）（需要强调的是，虚基类依旧会在子类里面存在拷贝，只是仅仅最多存在一份而已，并不是不在子类里面了）；当虚继承的子类被当做父类继承时，虚基类指针也会被继承。
	- 实际上，vbptr 指的是虚基类表指针（virtual base table pointer），该指针指向了一个虚基类表（virtual table），虚表中记录了虚基类与本类的偏移地址；通过偏移地址，这样就找到了虚基类成员，而虚继承也不用像普通多继承那样维持着公共基类（虚基类）的两份同样的拷贝，节省了存储空间。

### nocopy

- 如果⽗类不存在认的复制构造函数和赋值操作符重载这些函数的话，那么⼦类默认也不会⽣成。那么最简单的做法就是让 Student 去private继承⾃ NotCopyable 
class NotCopyable {
 public : 
    NotCopyable() = default;
    NotCopyable(const NotCopyable &) = delete; 
    NotCopyable(NotCopyable &&) = delete; 
    NotCopyable & operator=(const NotCopyable &) = delete;
    NotCopyable & operator=(NotCopyable &&) = delete;
};

## 运算符重载

### 部分运算符重载

- 可重载运算符

	- 	双目算术运算符	+ (加)，-(减)，*(乘)，/(除)，% (取模)
关系运算符	==(等于)，!= (不等于)，< (小于)，> (大于>，<=(小于等于)，>=(大于等于)
逻辑运算符	||(逻辑或)，&&(逻辑与)，!(逻辑非)
单目运算符	+ (正)，-(负)，*(指针)，&(取地址)
自增自减运算符	++(自增)，--(自减)
位运算符	| (按位或)，& (按位与)，~(按位取反)，^(按位异或),，<< (左移)，>>(右移)
赋值运算符	=, +=, -=, *=, /= , % = , &=, |=, ^=, <<=, >>=
空间申请与释放	new, delete, new[ ] , delete[]
其他运算符	()(函数调用)，->(成员访问)，,(逗号)，[](下标)

- 不可重载运算符

	- .：成员访问运算符
.*, ->*：成员指针访问运算符
::：域运算符
sizeof：长度运算符
?:：条件运算符
#： 预处理符号
typeid
强制类型转换运算符

- 重载规则

	- （1）不可臆造运算符；
（2）运算符原有操作数的个数、优先级和结合性不能改变；
（3）操作数中至少一个是自定义类型；防止标准类型重载运算符
（4）保持重载运算符的自然含义。
	- （1）当重载为成员函数时，会隐含一个this指针；当重载为友元函数时，不存在隐含的this指针，需要在参数列表中显示地添加操作数。
（2）当重载为成员函数时，只允许右参数的隐式转换；当重载为友元函数时，能够接受左参数和右参数的隐式转换。
	- 一般规则为：单目成员，双目友元
	- =:赋值、():函数调用、[]:下标、以及 ->:指针访问类成员操作符只能被类的成员函数重载
	- << >>定义为友元

- 特例

	- -负号和减号

		- type operator-() const;
type operator-(const type &b) const;

- ++和--

	-  iterator &operator++() {                                                    前缀++it
        //pt = pt->next;
        return *this;
    }
    自增运算符有两个版本
    后置++，当中int是一个哑元
    哑元：重载发生。参数的个数不同，类型不同；
   iteratror operator++(int x) {//可省略x，不指定名称      后缀it++
        iterator tmp = *this;
        //pt = pt->next;
        return tmp;
    }

### 重载方式

- 类内的重载成员函数:
sum  = x + y;等价于sum = x.operator+(y);
- 类外运算符重载函数:
ostream &operator<<(ostream &out, const Class_name &obj) { 
    out << .. ; return out;
}
- 类内重载优先级高于类外重载优先级

## 多态

### 静态多态(必须在编译期给定类型>对应的数据类型)

- 指针包含多层含义
        -1 空间地址
        -2 空间长度
        -3 从空间读取出的值的类型
编译期已经确定其寻址方式

###  动态多态（运行期)

- 虚函数：用 virtual 修饰成员函数,C11实现多态最关键的手段

	- virtual跟着对象走 
	- 非virtual跟着类走
	- 语义:子类与父类方法可能不同
	- 子类的该成员函数默认为virtual

- 对于基类声明为virtual的函数，之后的重载版本都不需要再声明该重载函数为virtual(C++11)
- override
final
描述符非关键字

	- 指定一个虚函数覆盖另一个虚函数

		- void func override {}

			- override明确编译器是在覆盖子类虚函数,语言严谨性

	- 指定某个虚函数不能在子类中被覆盖，
或者某个类不能被子类继承。

		-  void foo() final;
struct B final : A // struct B 为 final {
    void foo() override; // 错误：foo 不能被覆盖，因为它在 A 中是 final
}; 
struct C : B // 错误：B 为 final
{};

- 重新定义将隐藏基类方法

	- 1.重新定义继承方法，原型应一致
	- 2.基类声明被重载，派生类要重新定义所有基类版本，否则其他版本被隐藏
	- 非虚函数调用:object.Base::func();

- 注意

	- inline virtual 唯一可内联的时候是：编译器知道所调用的对象是哪个类（如 Base::who()），这只有在编译器具有实际对象而不是对象的指针或引用时才会发生。
class Base {
public:
	inline virtual void who() { cout << "I am Base\n"; }
	virtual ~Base() {}
};
	- 普通函数（非类成员函数）不能是虚函数,友元不可是虚函数，友元不是成员函数
静态函数（static）不能是虚函数
构造函数不能是虚函数（因为在调用构造函数时，虚表指针并没有在对象的内存空间中，必须要构造函数调用完成后才会形成虚表指针）

- 发生条件

	- 1.必须有继承
2.必须有方法重写
3.基类的指针或引用绑定子类的对象
4.发生多态的函数必须为虚函数
	- 注意：函数按引用传递对象和按值传递

- 当一个类中，没有虚函数时，程序在编译期间会生成该函数的静态地址， 通过对象指针，可以访问到该地址
- 设置一个函数为虚函数后，对象空间中就一个虚函数表(在程序只读数据段.rodata section)，如果一个对象搜索不到该虚函数表。产生segmentation fault    
- 动态绑定用于传递结果
- 消耗资源

	- 对象增大，存储地址
	- 对于每个类，编译都创建一个虚函数表
	- 函数调用需要额外到表中查找地址

### typeid

- 运行时确定对象的类型,可用于判断多态绑定
- 返回typeinfo对象
- 包含成员函数

	- name()
	- hash_code()

### code

- class Animal {
public :
    Animal() {
        x = 8827, y = 65123;
    }
    virtual void say(int x) {
        cout << "I don't know how to say" << endl;
    }
    virtual void run() {
        cout << "I don't know how to run" << endl;
    }
protected :
    int x, y;
};

	- class Cat : public Animal {
public :
    void say(int x) override {
        cout << this << endl;
        cout << this->x  << " " << this->y << endl;
        cout << x << endl;
        cout << "miao~ miao~ miao~" << endl;
    }
    void run() override {
        cout << "I can run with four legs" << endl;
    }
};

		- void output_raw_data(void *q, int n) {
    printf("%p : ", q);
    unsigned char *p = (unsigned char *)q;
    for (int i = 0; i < n; i++) {
        printf("%02X ", p[i]);
    }
    printf("\n");
    return ;
}
typedef void (*func)(void *, int x);
int main() {
    Cat a, b;
    output_raw_data(&a, sizeof(a));
    output_raw_data(&b, sizeof(b));
    ((func **)(&a))[0][0](&a, 123);
    return 0;
}

			- address :0x7ffd4f01d580 18 DD FE 19 2B 56 00 00 FB E0 01 00 DB 4F 05 00 
address :0x7ffd4f01d590 18 DD FE 19 2B 56 00 00 FB E0 01 00 DB 4F 05 00 
address :0x7ffd4f01d5a0 18 DD FE 19 2B 56 00 00 FB E0 01 00 DB 4F 05 00 
0x7ffd4f01d580
123131 348123
miao~ miao~ miao~

### 虚函数指针、虚函数表

- 虚函数指针：在含有虚函数类的对象中，指向虚函数表，在运行时确定,虚函数指针位于对象首8个字节(指针大小)
- 每个类独立维护一个虚函数表; 注意：基类与派生类的虚函数指针的值并不同
- 虚函数表：在程序只读数据段（.rodata section，存放虚函数指针，如果派生类实现了基类的某个虚函数，则在虚表中覆盖原本基类的那个虚函数指针，如果定义新的虚函数，添加到虚函数表，在编译时根据类的声明创建。

### this指针

- 1. this 指针是一个隐含于每一个非静态成员函数中的特殊指针
- 2. 当对一个对象调用成员函数时，编译程序先将对象的地址赋给this指针,是成员函数的首个参数,自动传递一个隐含的参数然后调用成员函数，每次成员函数存取数据成员时，都隐式使用this指针。
- 4. `this` 指针被隐含地声明为: ClassName *const this，不能给 this`指针赋值；在 ClassName类的const 成员函数中，`this` 指针的类型为：`const ClassName* const`，不能对 `this` 指针所指向的这种对象是不可修改
- 5. this并不是一个常规变量，而是个右值，所以不能取得 this 的地址（不能 &this）
- 显式引用

	- 1. 为实现对象的链式引用；
2. 为避免对同一对象进行赋值操作；
3. 在实现一些数据结构时，如 `list`。

### 纯虚函数

- virtual int func() = 0;

	- 语义:定义接口

- 类里如果声明了虚函数，这个函数是实现的，哪怕是空实现，它的作用就是为了能后期绑定来达到多态了
纯虚函数只是一个接口，是个函数的声明而已，在基类中不能对虚函数给出有意义的实现，它要留到子类里去实现。 
-  虚函数在子类里面可以不重写；但纯虚函数必须在子类实现才可以实例化子类。
- 虚函数的类用于 “实作继承”，继承接口的同时也继承了父类的实现。纯虚函数关注的是接口的统一性，实现由子类完成 

### 抽象类

- 拥有纯虚函数的类，称为抽象类;抽象类不可以构造对象;
接口类:只有虚函数
- 派生类没有对纯虚函数进行实现，那么派生类也是抽象类
- 和泛化关系的区别在于，泛化的类可以生产对象。

### 虚析构函数

- 做基类析构函数应为虚函数：解决基类的指针指向派生类对象，并用基类的指针删除派生类对象,否则不调用派生类的析构函数。
- delete释放内存时，先调用子类析构函数，再调用基类析构函数，防止内存泄漏。

## 泛型
编程

### 程序=数据结构+算法

- 数据结构

	- 能存储任意类型

- 算法

	- 能操作存储任意类型的数据结构

### 泛型编程

- 面向过程编程

	- 将相关过程抽象成函数，对参数抽象
	- 模板函数

- 面向对象编程

	- 模板类
	- 将相关对象抽象成类，对类型抽象

### 模板声明：编译器实现的模板的实例化

- 声明与定义不可分开
- template<typename T, typename U>
auto add(T a, U b) -> decltype(a + b) {
    return a + b;
}

### SFINEA

- 中文直译即是“匹配失败不是错误”。条规则表示的是对重载的模板的参数进行展开的时候，如果展开导致了一些类型不匹配，编译器并不会报错。

### template <class AnyType>  C++98之前使用class
template <typename AnyType>
template<> 模板特化,参数(数据类型)确定

- 模板函数偏特化

	- 举例:template<typename T>
T add(T *, T *)

### 可变参数模板

- template<typename T, typename ...ARGS>

	- void Print(const T&a, ARGS...args) {
   cout << a << endl;
   Printf(args...);
}

		- ARGS:模板中剩余部分的模型

	- template<typename T>
void Print(

### 最终目标文件不包含任何模板，只包含为程序生成的实际函数，每个函数都有独立的定义,模板生产代码

- 模板是有逻辑,而宏是简单的代码替换
- 通过static 证明

### 函数版本的选择

- 步骤

	- 1.创建候选函数列表：同名的函数和模板函数
	- 2.创建可行函数列表：参数数目正确的函数，隐式转换，如float到double
	- 3.确定最佳可行，没有则报错

- 优先级

	- 1.完全匹配

		- 指向const数据的指针和引用，优先与为const参数的匹配
		- 非模板版本>模板特化>模板版本
		- void  swap(job &, job &);
template <> 
void swap<job>(job &, job &); 显示具体化,特化
template <typename T>
void swap(T &, T &);

	- 2.提升转换，如char，short到int， float到double 
	- 3.标准转换，如int到char，long到double
	- 4.用户定义的转换，如类声明中定义

### 过程

- 1.预处理展开宏 typeof
- 2.模板的实例化
- 3.模板阶段decltype

### 引用折叠

- 主要用于模板

	- 奇数:左值引用

		- X&& & 可折叠成 X&

	- 偶数:右值引用

		-  X&& && 可折叠成 X&&

	- template<typename T>
void swap(T &&a, T &&b) { //&&表示传引用：左值和右值引用; &表示左值引用
    //T c = a; //error 引用折叠
    //去除引用
    typename remove_reference<T>::type c;
    c = a; 
    a = b; b = c;
    return ;
}


### 类型转换

- C++有一套

	- remove_reference
	- remove_pointer

### 模板的图灵完备性

- 输入、输出、内部状态、计算规则
- 任何程序中需要表达的计算，都可以通过元编程的方式来表达

## C++新特性

### 综述

- 通过内存模型、线程、原子操作等来支持本地并行编程（Native Concurrency）
- 通过统一初始化表达式、auto、declytype、移动语义等来统一对泛型编程的支持
- 通过constexpr、POD（概念）等更好地支持系统编程
- 通过内联命名空间、继承构造函数和右值引用等，以更好地支持库的构建。

### 语言可用性

- 常量

	- nullptr(11)

		- 空指针类型

			- 可能实现
#define NULL 0
// C++11 起
#define NULL nullptr

		- nullptr是一个“指针空值类型”的编译期右值常量

			- nullptr_t类型数据可以隐式转换成任意一个指针类型
			-  nullptr_t类型数据不能转换为非指针类型，即使使用reinterpret_cast<nullptr_t>()的方式也是不可以的
			- nullptr_t类型数据不适用于算术运算表达式
			- nullptr_t类型数据可以用于关系运算表达式，但仅能与nullptr_t类型数据或者指针类型数据进行比较

		- 在把nullptr_t应用于模板中时候，我们会发现模板却只能把它作为一个普通的类型(nullptr_t)来进行推导,并不会将其视为T*指针

			- 要让编译器成功推导出nullptr的类型，必须做显式的类型转换

		- C 中，宏 NULL 可以拥有类型 void* ，但这在 C++ 中不允许
		- NULL 是0

			- 0既是整型又是指针类型

	- constexptr(11/14)

		- int a = 10, b = 100;
(a > b ? a : b) = 666;
constexptr res = (a > b ? a : b);
		- const int a = n + 2;
		- const int num = 10;

			- 编译器可能做优化,在编译期直接将num替换为10

		- constexpr int f(int i) { 
//可以返回一个编译期常量对象,
//而不是必须,也可以返回运行期对象
    return 2 * i;
}

			- 函数必须返回值（不能是void函数）
// C++11 constexpr 函数必须把一切放在单条 return 语句中
// （C++14 无此要求）

		- 常量表达式的构造函数

			- struct A {
    constexpr A(int x, int y) : x(x), y(y) {}
    int x, y;
};
			- int main() {
    int n = 3;
    cin >> n;
    const int a = n + 123; //运行期常量,不可修改的量,只读的变量
    constexpr int b = 3; //编译期常量,替代宏
    constexpr int c = f(123) + 567; 
    constexpr A d(2, 3);
    return 0;
}
			- 约束

				- 函数体必须为空
				-  初始化列表只能由常量表达式来赋值

		- 编译期常量替代define宏
		-  constexpr即常量表达式(constant expression)
		- 验证表达式是否具备常性，避免函数返回值等隐式改变

- 变量及其初始化

	- if/switch初始化(17)

		- if(int a = 10; a < 11) {}

	- 初始化列表(11)

		- {}

	- 结构化绑定(11/14/17)

		- tuple元组

			- tuple<type1, type2> func() { return make_tuple(v1, v2)}
auto [x, y] = func();
cout << x << y;
			- 函数多返回值，相比结构体更直观

- 类型推导

	- auto(11)

		- 编译期确定：静态编译类型推导，需要初始化
		- auto并非一种“类型”声明，而是一个类型声明时的“占位符”，编译器在编译时期会将auto替代为变量实际的类型
		- auto来声明多个变量类型时，只有第一个变量用于auto的类型推导，然后推导出来的数据类型被作用于其他的变量
		- 限制

			- 不可做函数形参
			- 不可用实例化模板的时候使用的模板参数

				- vector<auto> v

			- 不可声明数组

				- auto z[3]

			- 不可用于类的非静态成员变量

				- 编译器阻止auto对结构体中的非静态成员进行推导即使成员拥有初始值

		- cout << typeid(T).name();
		- 1.模板,lambda后置返回
2.STL迭代器,遍历

	- decltype(11)

		- 只推导,不计算

			- 与模板实例化在同一时期

		- decltype以一个普通的表达式为参数，返回该表达式的类型

			- 函数名不可做参数

		- int x; double y;
decltype(x + y) z;
		- 后置返回类型

			- template <typename It>
auto fcn(It beg, It end) -> decltype(*beg) {
    // 处理序列
    return *beg;    // 返回序列中一个元素的引用
} 
			- auto func(int a, int b)->decltype(a + b) {}

		- 四规则

			- 1.无括号

				-  const double * x; decltype(x) 为const double *
				- 2.函数调用

					- 查看函数原型确定返回值类型，而不实际调用
long func(int x); decltype(func(x)) 为long

			- 2.是一个将亡值

				- 如果e是一个将亡值(xvalue)，那么decltype(e)为T&&。

			- 3.是一个左值

				- double xx;
decltype ((xx)) 为 double &
decltype (xx) 为double

			- 4.其他

				- 表达式的类型
int &k = x, &n = x;  decltype(&k + &n)位int

	- cv限制符

		- 与auto类型推导时不能“带走”cv限制符不同，decltype是能够“带走”表达式的cv限制符的

- 控制流

	- if constexpr

		- constexpr编译期常量

	- 区间for迭代

### 语言运行期强化

- lambda表达式

	- 函数式编程

		- λ演算

			- 闭包特性

				- 闭包(closure):捕获并持有了外部作用域变量的函数

		- 把函数当成对象
		- 把函数对象当成参数
		- lambda的类型被定义为“闭包”（closure）的类而每个lambda表达式则会产生一个闭包类型的临时对象（右值）。因此，严格地讲，lambda函数并非函数指针。不过C++11标准却允许lambda表达是向函数指针的转换，但前提是lambda函数没有捕捉任何变量，且函数指针所示的函数原型，必须跟lambda函数有着相同的调用方式

	- 原理

		- c++实现原理是不同于FP语言(因为其他语言大多数是带GC和通过引用传递)
		- 事实上，在C++11中lambda也被处理为匿名的仿函数。当创建lambda函数的时候，编译器内部会生成这样一个仿函数，并从其父作用域中取得参数传递给lambda函数。不过，真正会改变人们思维方式的是，lambda是一个局部函数
		- 链接

		- auto a = [] {
        int x = 0;
        auto b = [x]() mutable {
            return ++x;
        };
        return b;
    };

			- static，并引用方式捕获  
auto a = []() {
        static int value = 0;           // 重点
        auto b = [&]() {                // 重点
            return ++value;
        };
        auto c = [&]() {
            return ++value;
        };
        return std::make_pair(b, c);
    };

				- C++14,绑定到函数对象并使用引用方式捕获x   
auto a = [x = 0]() mutable {        // 重点
        auto b = [&]() {                // 重点
            return ++x;
        };
        auto c = [&]() {
            return ++x;
        };
        return std::make_pair(b, c);
    };

					- 智能指针  
  auto a = []() {
        auto x = std::make_shared<int>(0);  // 重点
        auto b = [=]() {
            return ++(*x);
        };
        auto c = [=]() {
            return ++(*x);
        };
        return std::make_pair(b, c);
    };

		- c++不能延长栈变量生命周期,因为局部变量永远都需要在作用域结束后析构
RAII:保证在任何情况下，使用对象时先构造对象，最后析构对象。

			- b拷贝了一份x到自己的函数对象(闭包)中。因为在语义上，lambda是作为一个语句块的，语句块结束后变量都要析构。也就是x不管怎样都要销毁的。而不像fp语言，能做到延长它的生命

		- 占用空间

			- 不捕获其他值的lambda，等价于一个空对象，一般只占用1个字节
			- 因为c++要确保两个不同对象的地址不同，一个对象至少要有一个字节(哪怕是空的)
			- 有捕获的，字节数等于按值捕获的值的字节数+按引用捕获的值的个数* 8
			- 因为引用捕获实际上是指针实现

	- 基础

		- auto func = [捕获列表](参数列表)说明符 异常属性->返回类型 {函数体}
		- auto推导返回值类型

			- 第一个return语句和->返回类型
auto确定类型function<()>

		- 捕获

			- []

				- 默认不可以访问外部变量

					- function<int()> Temp_func() {
    int a = 23;
    return [=]()->int { 
//默认不可以访问外部变量
        return a; };
}
auto func = Temp_func();

						- 如果[]可以捕获外部变量,就会产生段错误

			- 默认捕获符
&、=

				- &（以引用隐式捕获）
				- = （以复制隐式捕获）

					- 复制捕获的对象在 lambda 体内为 const

				- 任何捕获符只可以出现一次
				- code

					- struct S2 { void f(int i); };
void S2::f(int i)
{
    [&]{};          // OK：默认以引用捕获
    [&, i]{};       // OK：以引用捕获，但 i 以值捕获
    [&, &i] {};     // 错误：以引用捕获为默认时的以引用捕获
    [&, this] {};   // OK：等价于 [&]
    [&, this, i]{}; // OK：等价于 [&, i]
}

			- this

				- 可访问类的成员函数内部，成员变量

		- 形参

			- 当以 auto 为形参类型时，该 lambda 为泛型 lambda(14)
			- ret operator()(形参) const { 函数体 }(未使用mutable)
ret operator()(形参) { 函数体 }(使用了 mutable)

		- 说明符

			- mutable：允许函数体修改各个复制捕获的对象，以及调用其非const成员函数

		- 可以完成一种功能委托和通信方式交流
		- 函数指针是单向的，lambda是双向的

	- code

		- auto Data = [](int a, int b) {
    return [=](auto func) {
        return func(a, b);
    };
};

	- 泛型化

		- 参数列表为auto

			- 可以支持隐式推导功能，制作类似于模板的功能
			- auto是静态编译时确定，lambda是动态运行时确定
			- auto add = [](auto a, auto b) { return a + b; }
cout << add(string("1"), string("b"));

- std::function

	- 类似于函数对象的概念；就是以对象的方式说明函数指针的作用 
	- virtual void helpMeShow(std::function<void (WINDOW *)> helpfunc);
	- (模板中)不可进行间接类型推导

		- template <typename T>
void add(T &&a, T &&b) { 
//&和&&都表示传引用
    a += 3;
    b += 4;
}

			- void func(function<void(int &, Int &)>) //错误
void func(void (*p)(int &, int &), int &a, int &b) {
    p(a, b);
    return ;
}

	- 可以指向任意可调用对象

- std::bind和std::placeholder

	- #include <functional>
	- std::placeholders 表示调用时传递的参数
	- int func(int a, int b, int c) { return max(max(a, b), c); }
int main() {
    auto bindFunc = bind(func, std::placeholders::_1, 10, 20);
}

		- void func(double x, int y, int z) {}
		-     std::function<void(int, double)>
		- f = bind(func, std::placeholders::_2,

			-  123, 

				- std::placeholders::_1);

	- 默认时拷贝(传值),使用ref(arg)为传引用

- 值的类型
表达式

	- 左值和右值是值

		- 左值，右值(纯右值，将亡值)
		- 判断

			-  越过该行代码,还能否通过单一变量访问相关的值,能左值,不能右值
			- 有名能取地址的是左值

		-     cout << (n++) << endl; //右值,简单理解:临时的变量,不可以修改的
    cout << (++n) << endl; //左值,简单理解:可以操作的变量,可引用
    //结合重载++运算符理解
    cout << (++n)++ << endl;
    //cout << (n++)++ << endl;
		- 右值可以理解为即将消亡

			- 只要能够绑定右值的引用类型，都能够延长右值的生命期

		- 判断左值

			- is_lvalue_reference

	- tip

		- 左绑左，右绑右
		- 不管啥，先看const

			- const左值引用可以绑定任意类型

				- 所以ostream参数是const T &类型

	- 左值引用&和右值引用&&

		- 是引用,变量的别名

	- std::move和std::forword

		- move强制变右值
forward变成任意类型的值
为了解决完美传值过程

			- move(x)
forward<int &&>(x)

				- std::move基本等同于static_cast<T&&>(lvalue)

		- 主要是因为重载

			- 调用正确的重载函数

		- 完美转发perfect forwarding

			- 在函数模板中，完全依照模板的参数的类型，将参数传递给函数模板中调用的另外一个函数

	- 引用折叠

		- 主要用于模板

			- 奇数:左值引用
			- 偶数:右值引用

	- 值的类型

		- 左值

			- 可以被引用的数据对象，如：变量，数组元素，结构成员，引用和解除引用的指针,字符串变量等。
非左值包括字面常量和包含多项的表达式
const变量属于不可修改的左值（可通过地址访问所以是左值）

	- 表达式

		- 拥有身份且不可被移动的表达式
左值 (lvalue)表达式；

			- 常见

				- 变量、函数、模板形参对象 (C++20 起)或数据成员的名字，不论其类型，例如 std::cin 或 std::endl
				- 返回类型为左值引用的函数调用或重载运算符表达式，例如 str1 = str2 或 ++it；
				- a = b，a += b，a %= b，以及所有其他内建的赋值及复合赋值表达式,连续赋值
				- ++a 和 --a，内建的前置自增与前置自减表达式；
				- *p，内建的间接寻址表达式；
				- 字符串字面量，例如 "Hello, world!"；只读的左值
				- 转换为左值引用类型的转型表达式，例如 static_cast<int&>(x)；
				- 返回类型是到函数的右值引用的函数调用表达式或重载的运算符表达式；c++11
				- 转换为函数的右值引用类型的转型表达式，如 static_cast<void (&&)(int)>(x)  c++11

		- 不拥有身份且可被移动的表达式
纯右值 (prvalue)表达式；

			- 常见

				- 除了字符串字面量之外的）字面量，例如 42、true 或 nullptr；
				- 返回类型是非引用的函数调用或重载运算符表达式，例如 str.substr(1, 2)、str1 + str2 或 it++；
				- a++ 和 a--，内建的后置自增与后置自减表达式；
				- a + b、a % b、a & b、a << b，以及其他所有内建的算术表达式；
				- a && b、a || b、!a，内建的逻辑表达式；
				- a < b、a == b、a >= b 以及其他所有内建的比较表达式；
				- &a，内建的取地址表达式；
				- 转换为非引用类型的转型表达式，例如 static_cast<double>(x)、std::string{} 或 (int)42；
				- this 指针；
				- 枚举项;
				- lambda 表达式，例如 [](int x){ return x * x; }；(C++11 起)

		- 拥有身份且可被移动的表达式
亡值 (xvalue)表达式；

			- 常见

				- 返回类型为对象的右值引用的函数调用或重载运算符表达式，例如 std::move(x)；
				- a[n]，内建的下标表达式，其操作数之一是数组右值；
				- a.m，对象成员表达式，其中 a 是右值且 m 是非引用类型的非静态数据成员；
				- a.*mp，对象的成员指针表达式，其中 a 为右值且 mp 为数据成员指针；
				- 转换为对象的右值引用类型的转型表达式，例如 static_cast<char&&>(x)；
				- 在临时量实质化后，任何指代该临时对象的表达式

		- 不拥有身份且不可被移动的表达式无法使用

- 移动构造函数

	- A *p = new A();
A a = move(*p); //节约开辟对象空间,深拷贝,直接移动相关存储区的指向 O(n)->O(1)
delete p;

		-     A(A &&obj) : n(obj.n), arr(obj.arr) { //移动构造:右值引用
        cout << "move constructor" << endl;
        obj.arr = nullptr;
    }

	- RVO返回值优化：
return value optimization

		- 把使用权直接给新空间，无序销毁临时空间，类似于剪切
		- 创建临时空间
存储数据到临时空间
再从临时空间中数据传递到新空间
销毁临时空间

### 智能指针
内存管理

- 内存问题

	- 野指针

		- 一些内存单元已被释放，之前指向它的指针却还在被使用

	- 重复释放

		- 程序试图去释放已经被释放过的内存单元，或者释放已经被重新分配过的内存单元，就会导致重复释放错误

	- 内存泄漏

		- 不再需要使用的内存单元如果没有被释放就会导致内存泄漏

- 头文件：#include <memory>
- std::auto_ptr<std::string> ps (new std::string(str))；
- 1. shared_ptr

	- 共享式拥有.多个智能指针指向相同对象,该对象和其相关资源会在“最后一个 reference 被销毁”时被释放.通过引用计数

- 4. auto_ptr（被 C++11 弃用）

	- 缺乏语言特性如 “针对构造和赋值” 的std::move 语义，以及其他瑕疵。
	- auto_ptr 可以赋值拷贝,复制拷贝后所有权转移;unqiue_ptr 无拷贝赋值语义,但实现了std::move 语义；
	- auto_ptr 对象不能管理数组(析构调用delete),unique_ptr 可以管理数组(析构调用 delete[] );

- 2. unique_ptr取代 auto_ptr

	- 独占式拥有或严格拥有概念，保证同一时间内只有一个智能指针可以指向该对象。你可以移交拥有权。它对于避免内存泄漏（resource leak）——如 new 后忘记 delete ——特别有用。
	-  unique_ptr则是一个删除了拷贝构造函数、保留了移动构造函数的指针封装类型

		- 所有权”仅能够通过标准库的move函数来转移

- 3. shared_ptr的辅助类weak_ptr

	- 不建立强关系

		- 不进行引用计数加1，可能只使用而不修改
		- 防止环形引用

	- 在 default 和 copy 构造函数之外，weak_ptr 只提供 “接受一个 shared_ptr” 的构造函数。
	- weak_ptr成员lock

		- 返回其指向内存的一个shared_ptr对象，且在所指对象内存已经无效时，返回指针空值nullptr

- 面向对象语言

	- Java->Android

		- 内存管理：GC->garbage colletion垃圾回收机制

	- OC->iOS

		- MRC：手动引用计数 reference count
		- ARC：自动引用计数 automatic reference count

	- C#(C sharp)

		- 内存管理：自动管理，采用垃圾回收机制
不再提供对指针类型的支持，使得程序不能随便访问内存地址空间

	- 垃圾回收机制

		-  基于引用计数
(reference counting garbage collector)

			- 引用计数主要是使用系统记录对象被引用（引用、指针）的次数。当对象被引用的次数变为0时，该对象即可被视作“垃圾”而回收
			- 难处理“环形引用”问题，此外由于计数带来的额外开销

		-  基于跟踪处理(tracing garbage collector)

			- 标记-清除(Mark-Sweep)

### 强制类型转换

- dynamic_cast<新类型>(表达式)		

	- 新类型	-	指向完整类类型的指针、到完整类类型的引用，或指向（可选的 cv 限定）void 的指针
	- 表达式	-	若 新类型 为引用，则为完整类类型的左值 (C++11 前)泛左值 (C++11 起)表达式，若 新类型 为指针，则为指向完整类类型的指针纯右值。
	- 若转型成功，则 dynamic_cast 返回 新类型 类型的值。若转型失败且 新类型 是指针类型，则它返回该类型的空指针。若转型失败且 新类型 是引用类型，则它抛出与类型 std::bad_cast 的处理块匹配的异常。
	- 限制

		- 用于多态类型的转换
执行行运行时类型检查
只适用于指针或引用
对不明确的指针的转换将失败（返回 nullptr），但不引发异常
可以在整个类层次结构中移动指针，包括向上转换、向下转换
		- 基类与派生类的转换原理是虚指针

- static_cast<新类型>(表达式)

	- 用隐式和用户定义转换的组合在类型间转换
	-     // 1: 初始化转换    
    int n = static_cast<int>(3.14); 
    std::vector<int> v = static_cast<std::vector<int>>(10);
    std::cout << "v.size() = " << v.size() << '\n';  //10
    // 2: 静态向下转型
    D d;
    B& br = d; // 通过隐式转换向上转型
    br.hello();
    D& another_d = static_cast<D&>(br); // 向下转型
    another_d.hello();
    // 3: 左值到右值
    std::vector<int> v2 = static_cast<std::vector<int>&&>(v);

		-  struct B {
    int m = 0;
    void hello() const {
        std::cout << "Hello world, this is B!\n";
    }
};
struct D : B {
    void hello() const {
        std::cout << "Hello world, this is D!\n";
    }
};

- static_cast与dynamic_cast

	- static_cast 跟 dynamic_cast 的区别就是，他不回去检查 pAnimal 到底是不是 Cat ，就直接转换给你。如果不是的话，你就会拿到⼀个野指针，使⽤它就会发⽣ undefined behavior。
	- 另外要提到的是， dynamic_cast 也可以在⽗类的⼏个⼦类下转换，如果不返回 nullptr 就代表你的转换成功了，这个指针指向的的确是你需要的类型的对象。⽽ static_cast 这样做会有语法错误

- const_cast

	- 用于删除 const、volatile 和 __unaligned 特性（如将 const int 类型转换为 int 类型 ）

- reinterpret_cast

	- 用于位的简单重新解释

		- 不管类型之间的关系，强⾏将⼀个指针重新解释成另 ⼀个类型

	- 不能丢掉 const、volatile 或 __unaligned 特性
	- reinterpret_cast 的一个实际用途是在哈希函数中，即，通过让两个不同的值几乎不以相同的索引结尾的方式将值映射到索引

### RTTI
运行时类型信息

- dynamic_cast

	- 用于多态类型的转换
	- 虚函数指针

- typeid

	- 运行时确定对象的类型,可用于判断多态绑定
	- 返回typeinfo对象的引用
	- 包含成员函数

		- name()
		- hash_code()

### POD

- 平凡的(trivial)

	- 拥有平凡的默认构造函数,析构函数

		- 平凡的默认构造函数就是说构造函数:什么都不干
		- 一旦定义了构造函数，即使构造函数不包含参数，函数体里也没有任何的代码，那么该构造函数也不再是“平凡”的
		- 编译器默认生成或使用default

	- 拥有平凡的拷贝构造函数和移动构造函数

		- 平凡的拷贝构造函数基本上等同于使用memcpy进行类型的构造

	- 有平凡的拷贝赋值运算符和移动赋值运算符
	- 不能包含虚函数以及虚基类
	- 判断

		- #include <type_traits>
    cout << is_trivial<Trivial>::value << endl;
    cout << is_trivial<NoTrivial>::value << endl;

- 标准布局的(standard layout)

	- 所有非静态成员有相同的访问权限（public, private,protected）
	- 在类或者结构体继承时

		- 满足以下两种情况之一

			- 派生类中有非静态成员，且只有一个仅包含静态成员的基类
			-  基类有非静态成员，而派生类没有非静态成员

		- 非标准

			- 实际上使得非静态成员只要同时出现在派生类和基类间，其即不属于标准布局的
			- 多重继承:一旦非静态成员出现在多个基类中，派生类也不属于标准布局的

		- struct B1 { static int a; };
struct B2 { int a; };
struct D1 : B1 { int d; };                       //1  
struct D2 : B2 { static int d; };          //1
struct D3 : B2, B1 { static int d;  };   //1
struct D4 : B2 { int d;  };                  //0
struct D5 : B2, D1 {};                        //0  

	- 类中第一个非静态成员的类型与其基类不同

		- 该规则实际上是基于C++中允许优化不包含成员的基类而产生的
		- 在C++标准中，如果基类没有成员，标准允许派生类的第一个成员与基类共享地址。因为派生类的地址总是“堆叠”在基类之上的，所以这样的地址共享，表明了基类并没有占据任何的实际空间（可以节省一点数据）。但是如果基类的第一个成员仍然是基类，在我们的例子中可以看到，编译器仍然会为基类分配1字节的空间。分配为1字节空间是由于C++标准要求类型相同的对象必须地址不同（基类地址及派生类中成员d的地址必须不同）

	- 没有虚函数和虚基类
	- 所有非静态数据成员均符合标准布局类型，其基类也符合标准布局
	- 判断

		- is_standard_layout<D1>::value

- 判断是否是POD

	- is_pod<Type>

- 作用

	- 字节赋值，代码中我们可以安全地使用memset和memcpy对POD类型进行初始化和拷贝等操作
	- 提供对C内存布局兼容。C++程序可以与C函数进行相互操作，因为POD类型的数据在C与C++间的操作总是安全的
	- 保证了静态初始化的安全有效。静态初始化在很多时候能够提高程序的性能，而POD类型的对象初始化往往更加简单（比如放入目标文件的.bss段，在初始化中直接被赋0）

## 异常处理

### 相比于断言适用于排除逻辑上不可能存在的状态，异常通常是用于逻辑上可能发生的错误

### try

- 抛出异常

### catch

- 捕捉异常
- 栈展开

	- 从内部往外抛，若最终捕获不到就结束程序
	- 异常机制会带来一些额外开销，比如函数抛出异常，会导致函数栈被依次地展开（unwind），并依帧调用在本帧中已构造的自动变量的析构函数等。

- catch(...)

### exception类

### noexcept

- void func noexcept;

	- 不带常量表达式的noexcept相当于声明了noexcept(true)，即不会抛出异常

- void func noexcept(常量表达式);

	- 常量表达式的结果会被转换成一个bool类型的值。该值为true，表示函数不会抛出异常，反之，则有可能抛出异常

- C++11标准中让类的析构函数默认也是noexcept(true)的

### static_assert

- static_assert接收两个参数，一个是断言表达式，这个表达式通常需要返回一个bool值；一个则是警告信息，它通常也就是一段字符串

### CPU异常分类

- fault

	- 执行时触发，保存当前状态，异常处理后返回当前语句
	- 如除0

- tarp

	- 执行后触发，异常处理后返回下一句
	- 如断点

- abort

	- 执行后宕机

### 含义

- 异常本身是一个转移控制流的机制
- 如缺页异常

## C知识

### assert

- #define NDEBUG          // 加上这行，则 assert 不可用
#include <assert.h>

assert( p != NULL );    // assert 不可用

	- #ifndef _HEAD
  #error "error sequence"
#endif
	- 通过#error在预处理阶段断言

- 断言，是宏，而非函数;
- 断言assert宏作用与运行期

	- 如果它的条件返回错误，则终止程序执行

- 静态断言

	- #define assert_static(expr) \
    do {enum {assert_static__ = 1 / (expr)}; } while (0)

### 如今GNU的属性（attribute）几乎无所不在，所有的编译器都在尝试支持它，以用于修饰类型、变量和函数等。不过__attribute__((attribute-name))这样的写法，除了不怎么好看外，每一个编译器可能还都有它自己的变体

- 属性的真正强大之处在于它们能够让编译器供应商创建他们自己的语言扩展，同时不会干扰语言或等待特性的标准化。

### #pragma是一条预处理的指令（preprocessor directive）。简单地说，#pragma是用来向编译器传达语言标准以外的一些信息。

- #pargma once
效果等同于
#ifndef THIS_HEADER
#define THIS_HEADER

#endif

### #define log(frm, args...) {\
    printf("[%s : %d] %s ", __func__, __LINE__, #args);\
    printf(frm, ##args);\
    printf("\n");\
}

### va_arg则通过改变指针的方式（每次增加sizeof(double)字节）来返回下一个指针所指向的对象。

*XMind - Trial Version*