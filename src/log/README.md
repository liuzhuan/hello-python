# 日志记录

使用标准库的 `logging` 模块。基本用法很简单：

```python
import logging

logging.basicConfig(level=logging.INFO, filename='mylog.log')
logging.info('Starting game')
logging.info('Trying to divide 1 by 0')
print 1/0
logging.info('The division succeeded')
logging.info('The game is over')
```

运行这个程序，会出现日志文件（`mylog.log`），其内容如下：

```
INFO:root:Starting game
INFO:root:Trying to divide 1 by 0
```