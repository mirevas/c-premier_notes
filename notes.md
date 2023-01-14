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
