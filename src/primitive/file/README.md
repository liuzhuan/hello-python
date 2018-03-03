# 文件

内置 `open` 函数会创建一个 Python 文件对象。

## 打开文件

`open` 函数的参数先是**文件名**，然后是**处理模式**。还有一个可选的第三参数，用来控制**输出缓存**。

典型的处理模式包括：`r` 读 `w` 写 `a` 追加。

其他处理模式有：

- `b` 二进制数据处理（关闭行末转换和 Python 3.0 Unicode 编码）
- `+` 同时打开读写

输出缓存为 `"0"` 意味着输出无缓存。

文件迭代器是最好的读取行工具。

以下是一个完整的写入和读取文件的样例：

```py
# write into file
>>> myfile = open('myfile.txt', 'w')
>>> myfile.write('hello text file\n')
16
>>> myfile.write('goodbye text file\n')
18
>>> myfile.close()

# read each line one by one
>>> myfile = open('myfile.txt')
>>> myfile.readline()
'hello text file\n'
>>> myfile.readline()
'goodbye text file\n'
>>> myfile.readline()
''

# read all content into a string
>>> open('myfile.txt').read()
'hello text file\ngoodbye text file\n'

# use file iterators
>>> for line in open('myfile.txt'):
...     print(line, end='')
...
hello text file
goodbye text file
```

## 文本和二进制文件

Python 3.0 的文本和二进制文件有明显的区别：

- 文本文件把内容表示为常规的 `str` 字符串，自动执行 Unicode 编码和解码，并且默认执行末行转换。
- 二进制文件把内容表示为一个特殊的 `bytes` 字符串类型，并且允许程序不修改地访问文件内容。

以下是一个读取二进制的例子：

```py
>>> data = open('qr.jpg', 'rb').read()
>>> data
b'\xff\xd8\xff\xe0\x00\x10JFIF\x00\x01\x01\x00\x00\x01\x00\x01\x00\x00\xff\xdb\x00C\x00\x0b\t\t\x07\t\...'
>>> data[6:10]
b'JFIF'
>>> data[0]
255
>>> bin(data[0])
'0b11111111'
```

## 在文件中存储并解析 Python 对象

```py
>>> X,Y,Z = 43, 44, 45
>>> S = 'Spam'
>>> D = { 'a': 1, 'b': 2 }
>>> L = [1, 2, 3]
>>> F = open('datafile.txt', 'w')
>>> F.write(S + '\n')
5
>>> F.write('%s,%s,%s\n' % (X, Y, Z))
9
>>> F.write(str(L) + '$' + str(D) + '\n')
27
>>> F.close()

# read
>>> chars = open('datafile.txt').read()
>>> chars
"Spam\n43,44,45\n[1, 2, 3]${'a': 1, 'b': 2}\n"
```