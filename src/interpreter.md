# 使用解释器

Python 解释器通常位于 `/usr/local/bin/python3.6`，将 `/usr/local/bin` 置入系统变量 PATH，可以在命令行直接调用 python。

可以使用 `python -c command [arg] ...`，传入命令。比如：

```bash
python -c 'print(2+3)'
```

一些模块也可以在命令行中直接调用，使用形式比如：`python -m module [arg]`。

可以使用 `-i` 选项首先执行一个脚本，然后进入命令行。

## 命令行参数

命令行传入的参数存储在一个数组中，具体来说就是 `sys` 模块的 `argv` 变量。

```py
import sys

print(sys.argv) # 数组内容依次为脚本命令，第一个参数，第二个参数...
```

## 源码编码

Python 源码默认使用 UTF-8 编码。

若要修改默认编码格式，可以在第一行增加如下命令：

```py
# -*- coding: encoding -*-
```

其中 `encoding` 是 Python 支持的编码代码，具体详见[手册][codecs]。

若脚本可执行，编码脚本需位居第二行：

```py
#!/usr/bin/env python3
# -*- coding: cp-1252 -*-
```

## REF

- [Using the Python Interpreter][doc]
- [Python Codecs][codecs]

[doc]: https://docs.python.org/3.6/tutorial/interpreter.html
[codecs]: https://docs.python.org/3.6/library/codecs.html#module-codecs