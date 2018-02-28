# 数字类型

## 小数数字

Python 2.4 引入一种新的核心类型：小数。小数就像浮点数，只不过它们有固定的位数。

我们还可以定义如何省略和截断额外的小数。

```py
0.1 + 0.1 + 0.1 - 0.3
# => 5.551115123125783e-17

from decimal import Decimal
Decimal('0.1') + Decimal('0.1') + Decimal('0.1') - Decimal('0.3')
# => Decimal('0.0')
```

`decimal` 模块的一个上下文对象允许指定精度（小数位数）和舍入模式（舍去、进位等）。

```py
import decimal
decimal.Decimal(1) / decimal.Decimal(7)
# => Decimal('0.1428571428571428571428571429')

decimal.getcontext().prec = 4
decimal.Decimal(1) / decimal.Decimal(7)
# => Decimal('0.1429')
```

## 分数类型

分数类型（Python 2.6 引入）实现了一个有理数对象。

```py
from fractions import Fraction
x = Fraction(1, 3)
y = Fraction(4, 6)
x
# => Fraction(1, 3)
y
# => Fraction(2, 3)
print(y)
# => 2/3
```

一旦创建了分数，就可以像平常一样用于数学表达式：

```py
x + y
# => Fraction(1, 1)
x - y
# => Fraction(-1, 3)
x * y
# => Fraction(2, 9)
```

分数对象也可以从浮点数字符串来创建：

```py
Fraction('.25')
# => Fraction(1, 4)
```

为了支持分数转换，浮点数对象现在有一个方法 `as_integer_ratio()`，能够产生它们的分子和分母比。

```py
(2.5).as_integer_ratio()
# => (5, 2)

Fraction(*(2.5).as_integer_ratio())
Fraction(5, 2)
```

Fraction 也有一个 `from_float()` 方法：

```py
Fraction.from_float(5, 4)
# => Fraction(5, 4)
```

## 集合

（未完待续。。。）

## REF

- [Python学习手册（第4版）][douban]，*Mark Lutz* 编著，机械工业出版社，2011年4月

[douban]: https://book.douban.com/subject/6049132/