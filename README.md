# c

## long

64位系统下

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