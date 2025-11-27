### 相关函数

- fopen
- fseek 
- ftell
- fread
- fwrite
- rewind
- feof
- fread



#### FILE结构体

不同编译器的实现不同,下面是MingW中FILE结构体定义

```cpp
typedef struct {
	char* _ptr;
	int _cnt;
	char* _base;
	int _flag;
	int _file;
	int _charbuf;
	int _bufsiz;
	char* _tmpfname;
} FILE;
```

- _ptr: 指向当前缓冲区中下一个要读取或写入的字符位置。
- _cnt: 缓冲区中剩余的字符数量。
- _base:指向缓冲区的起始地址。
- _flag:文件状态标志位，用于记录文件的打开模式和各种状态。
- _file: 文件描述符或操作系统级别的文件句柄。
- _charbuf
- _bufsize:缓冲区的大小（以字节为单位）。
- _tmpfname:指向临时文件名的指针





#### fopen

```cpp
FILE *fopen(const char *filename, const char *mode);
```

- filename: 文件路径
- mode: 打开模式

| 模式 | 含义 | 文件是否必须存在 |   文件存在时行为   | 文件不存在时行为 |
| :--: | :--: | :--------------: | :----------------: | :--------------: |
| "r"  | 只读 |        是        |    从文件开头读    |     返回NULL     |
| "w"  | 只写 |        否        | 销毁内容，从开头写 |    创建新文件    |
| "a"  | 追加 |        否        |   在文件末尾追加   |    创建新文件    |
| "r+" | 读写 |        是        |   从文件开头读写   |     返回NULL     |
| "w+" | 读写 |        否        |      销毁内容      |    创建新文件    |
| "a+" | 读写 |        否        | 读从开头，写从末尾 |    创建新文件    |



#### fread

从一个FILE指向的文件流中读取 `size * count` 个字节的数据到ptr指向的buffer中。

```cpp
size_t fread(void *ptr, size_t size, size_t count, FILE *stream);
```

- ptr: 指向buffer的指针
- size: 每个要读取数据元素的大小
- count: 要读取的元素的个数
- stream：指向FILE结构体的指针
- 返回值： 返回实际读取元素的个数，**注意不是字节数**



#### fwrite

将数据块写入文件流。它直接将内存中的数据原样写入文件，不进行任何格式转换，特别适合处理结构化数据和二进制文件

```cpp
size_t fwrite(const void *ptr, size_t size, size_t count, FILE *stream);
```

- ptr:指向要写入文件的数据的指针
- size:每个要写入的数据元素的大小，单位是字节
- count:要写入的元素个数
- stream: fopen打开的文件流
- 返回值:返回实际成功写入的元素个数,返回值可能**小于** `count`，表示只有部分数据被写入

#### fseek

移动文件指针到一个指定的位置

```cpp
int fseek(FILE *stream,  int64 offset, int origin);
```

- stream: FILE指向的文件流
- offset: 相对于origin的偏移量
- origin: 起始位置，有以下三个默认值
  - SEEK_CUR: 当前文件指针的位置 
  - SEEK_END: 文件末尾
  - SEEK_SET: 文件开头



#### ftell

获取当前文件指针相对于文件开头的偏移量,单位是字节

```cpp
long ftell(FILE *stream);
```

- 返回值：失败返回-1。





#### rewind

将文件指针移动到文件开头，等价于 `fseek(stream, 0, SEEK_SET)`;

```cpp
void rewind(FILE *stream)
```



----------

### 代码示例



#### 1. 判断文件结束还是文件错误

