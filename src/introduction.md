# 非正式介绍

## 数字

整数类型是 `int`，浮点数类型是 `float`。除号 `/` 总是返回浮点数。使用整除符号 `//` 可以返回整数，丢弃小数点后的部分。

```py
2 + 2
50 - 5 * 6
4 / 2 # 2.0
8 / 5 # 1.6
8 // 5 # 1
5 ** 2 # 25
```

在交互模式下，`_` 是最后一次表达式的值。

除 `int` 和 `float` 外，Python 还提供了有理数 `fractions.Fraction`:

```py
from fractions import Fraction

f = Fraction(1024, 768)
print(f) # 4/3
```

To Be Continue...

## REF

- [An Informal Introduction to Python][doc]
- [fractions - 有理数][fraction]

[doc]: https://docs.python.org/3.6/tutorial/introduction.html
[fraction]: https://docs.python.org/3.6/library/fractions.html#fractions.Fraction