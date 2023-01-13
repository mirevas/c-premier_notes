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
