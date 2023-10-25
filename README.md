# c

### long类型

### 64位系统下

```c
int main()
{
	static unsigned int g_uiA = ~0UL;
	printf("%ld\n", g_uiA ); //输出结果是-1。
    printf("%lld\n", g_uiA ); //输出结果是4294967295。因为ld用于32系统，lld用于64位系统。
	return 0;
}

```

2的32次方：4,294,967,296

```c
#include<stdio.h>
void print_binary(unsigned int value) {
    unsigned int mask = 1U << (sizeof(unsigned int) * 8 - 1);  // 获取掩码
    while (mask > 0) {
        putchar(value & mask ? '1' : '0');  // 根据位的取值输出0或1
        mask >>= 1;  // 移动掩码
    }
}
int main()
{
	static unsigned int g_uiA = ~0UL;
	printf("%ld\n", g_uiA );
	printf("%lld\n", g_uiA );
	printf("%u\n", g_uiA );
	unsigned int value = 42;
    printf("binary value of %d: %u\n", value, value);  // 使用"%u"格式化输出符输出二进制
    print_binary(value);
	printf("\n");
	print_binary(g_uiA);
	return 0;
}
```

输出结果：

```
-1
4294967295
4294967295
binary value of 42: 42
00000000000000000000000000101010
11111111111111111111111111111111
```

研究下如何输出二进制



### 类型大小

```c
#include<stdio.h>
#include<stdint.h>
int main()
{
	//整数
	printf("%d\n", sizeof(char));
	printf("%d\n", sizeof(short));
	printf("%d\n", sizeof(int));
	printf("%d\n", sizeof(long));
	printf("%d\n", sizeof(long long));
	printf("INT 拓展：\n");
	printf("%d\n", sizeof(uint8_t));
	printf("%d\n", sizeof(uint16_t));
	printf("%d\n", sizeof(uint32_t));
	//浮点数
	printf("浮点数\n");
	printf("%d\n", sizeof(float));
	printf("%d\n", sizeof(double));
	return 0;
}

```





####  1.unsigned会影响类型的字节数吗

**不，`unsigned`并不会直接影响类型的字节数。**

`unsigned`是一个类型修饰符，用于指定整数类型的无符号版本。它只表示整数不能有负值，并不直接影响类型的字节数。

类型的字节数取决于编译器和系统架构。虽然在大多数情况下，`unsigned int`和`int`在同一架构下有相同的字节数，但这并不是由`unsigned`修饰符所决定的。

例如，在大多数系统上，`unsigned int`和`int`都占用4个字节（32位），无论是否使用`unsigned`修饰符。

如果您需要确切控制整数类型的字节数，请使用精确的整数类型，例如 `uint8_t`、`uint16_t` 等，这些类型具有明确定义的字节数。这些类型定义在 stdint.h 头文件中，并且它们的大小是固定的，不会因为使用 signed 或 unsigned 进行修改。



#### 2.uint32_t与int的区别是什么 

**2,147,483,648是2的31次方**

`uint32_t` 是一个 32 位无符号整数类型，而 `int` 是一个有符号整数类型。这两个类型之间的主要区别在于它们是有符号还是无符号，以及它们能够表示的数值范围。

`int` 类型是由编译器实现决定其大小的，但通常情况下，它占用 32 位（4 个字节）的存储空间。这意味着 `int` 可以表示从 -2,147,483,648 到 2,147,483,647 的整数范围，其中一个位用于表示正负号。

相比之下，`uint32_t` 是一个固定大小的类型，它占用 32 位（4 个字节）的存储空间。由于它是无符号的，因此它只能表示非负数。它的范围是从 0 到 4,294,967,295。