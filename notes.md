2023/1/9
content: 0 -> 2-1
1. literal: constants, fixed value that the program may not alter
2. test: argc argv
```cpp
//in .cpp file
int main(int argc, char** argv) {
  // argc: argument count, argv: argument vector
  for (int i = 0; i < argc; i++) {
    std::cout << argv[i] << std::endl;
  }
}

// command line: 编译运行
g++ -o filename filename.cpp  // -o: 自定义编译文件名
./filename argv1 argv2

// 输出
./filename 
argv1 
argv2

```

2023/1/10 2-2
1. MakeFile Commands
* `-Wall` enable all warnings
* `-o` output a new file with customized name.
* `-g` debug
* Refer to http://www.cs.cmu.edu/~cburch/211-sp96/gnu_devel/gpp.html

2023/1/12 2-3
1. 引用 reference
	- bind to a local variable
	- not bind literal/ constant
2. 指针 pointer
![refNpointer](https://user-images.githubusercontent.com/101420550/212225338-4ceda4ff-8b3e-4e95-b686-e43a4be3ace7.png)

2023/1/13 2-4
1. const: 不变，但需初始化; non-const可以赋给const，但const不能赋给non-const
2. low-level const & top-level const:(从右往左读)

low-level：const修饰base type of compound types  
top-level: const修饰对象object
```cpp
// num:int类型的常量， top-level
eg.1 const int num = 123; 	

/* 
1. pvalue是一个指针，
2.指针的值是一个常量，但是指针的指向未被限制（非常量，可变化）
*/
eg.2 const int * pvalue = &value;

/*
1.pvalue是一个常量object，
2.pvalue是一个常量指针（指向被限制，常量，不可变，只能指向这一个地址），
3.指向的值是int类型，
4.该int类型是常量，不可变化。
*/
eg.3 const int * const pvalue = &value;		
```

2-5
1. alias: using, auto, decltype
- using std::cout; // using namespace std;
- auto: 自动选取正确的type。建议：能看出来的直接写type名。
- decltype： eg. int i = 1; decltype(i) j = 2; 		// j的类型等同于i

2023/1/16 3-1
1. namespace(::)
- 避免naming conflict
- 不在头文件中使用using

3-2
1. string初始化， eg. string s = "hello world"; string s1("hello word"); string s3 = (10, 'x');
2. string的function，eg. size(返回值的类型为size_t: unsigned integer)
3. getline(std::cin, input);

2023/1/17 vector 3-3
1. 直接赋值：vector<string> vec_str = {"123", "234", "345"};  
	拷贝：vector<string> vec_str{"123", "234", "345"};  
2. vector越界时，不一定会报错，可能为垃圾值。  
3. push_back()与emplace_back():
	eg. vec_str.push_back("x");  
	**emplace_back()** (未详讲)  
4. 判断相等 “==”：**?**  
	eg. vector<string> vec_str = {"123", "456", "567"};  
	vector<string> vec_str2{"123", "456", "567"};  
	vec_str == vec_str2 // 1: 相等 （若不等，返回0）；先判断长度是否相等，若相等再判断每个element是否相等

3-4 迭代器
1. auto -> vector<int>::iterator  
auto -> vector<int>::const_iterator
2. vec.begin()  
vec.end()	// one element pass the last element
3. (*it).size() 相当于 it->size()
4. vector和array的区别

2023/1/18 4-1
1. unary, binary
2. overload：可以改变操作方式，不能改变优先级和操作数
3. lvalues, rvalues **？**
	
2023/1/20 4-2
1. 不要在同一个表达式中同时改变值并且引用他， 
	eg. *beg = touper(*beg++);  //avoid: 不知道++和函数哪个先执行  
	->  *beg = touper(*beg); beg++;	//correct

2023/1/23 5-1
1. null statement
2. mismatch -> if, for, while 加括号
3. if else 嵌套问题，加括号；（python 对齐）
	
5-2
1. try catch，<stdexcept>库
	
2023/1/24 6-1
1. 全局变量 & static变量的区别：全局变量包括外部变量和static变量 **?**   
https://www.runoob.com/w3cnote/cpp-static-usage.html
	
2023/1/25 6-2-1
1. passed by value & passed by ref/pointer  

6-2-2
const
	
2023/1/30 6-2-3
1. initializer_list：可以传可变参数，需要先调包
思考：与vector有什么区别
	
6-3
1. 函数不要return a **reference or pointer** to a local object，有概率会返回垃圾值
	
6-4
overload重载：
```cpp
// high-level const 可以省略，eg.
Record lookup(Phone);
Record lookup(const Phone);	// 报错
Record lookup(Phone*);
Record lookup(Phone* const);	// 报错
// low-level const 不能省略，相当于不同类型变量
Record lookup(Phone*);
Record lookup(const Phone*);	// 重载函数
Record lookup(Phone&);
Record lookup(const Phone&);	// 重载函数
	
```

6-5
1. default argument
从左到右匹配，不允许func(,,10);
2. inline: a request to the compiler, 避免function call overhead，增加运行速度。  
ps. 迭代，含有static变量的函数compiler通常不会inline。 
3. constexpr()：not required to return a constant expression
```cpp
constexpr int add(int cnt) {return 5 + cnt};
int arr[add(2)];
```
条件:  
1. return 类型和所有参数类型都必须是literal type.   
2. 必须只包括一个return statement  
为什么不能用一个变量代替？  
优点：在编译时就提前执行
	
2023/2/1 6-6  
1.debug: assert(expre); 加上 NDEBUG( #define NDBUG) 会使assert失效  
2. func match : exact match > conversion match    

6-7
1. pointers to functions
