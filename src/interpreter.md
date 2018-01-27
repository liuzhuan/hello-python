# 使用解释器

Python 解释器通常位于 `/usr/local/bin/python3.6`，将 `/usr/local/bin` 置入系统变量 PATH，可以在命令行直接调用 python。

可以使用 `python -c command [arg] ...`，传入命令。比如：

```bash
python -c 'print(2+3)'
```

一些模块也可以在命令行中直接调用，使用形式比如：`python -m module [arg]`。

可以使用 `-i` 选项首先执行一个脚本，然后进入命令行。

## REF

- [Using the Python Interpreter][doc]

[doc]: https://docs.python.org/3.6/tutorial/interpreter.html