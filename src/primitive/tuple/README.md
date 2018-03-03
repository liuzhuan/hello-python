# 元组

## 排序

如果想对元组排序，通常先得将它转换为列表并使其成为一个可变对象，才能获得使用排序方法调用的权限，或使用 `sorted` 内置方法，它接受任何序列对象：

```py
>>> T = ('cc', 'aa', 'dd', 'bb')
>>> tmp = list(T)
>>> tmp.sort()
>>> tmp
['aa', 'bb', 'cc', 'dd']
>>> T = tuple(tmp)
>>> T
('aa', 'bb', 'cc', 'dd')

>>> T = ('cc', 'aa', 'dd', 'bb')
>>> sorted(T)
['aa', 'bb', 'cc', 'dd']
```