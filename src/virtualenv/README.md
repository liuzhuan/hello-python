# virtualenv

Virtualenv 是一个创建隔离 Python 环境的工具。

它解决了版本依赖的问题。如果一个应用依赖 LibFoo v1.0，另一个应用依赖 LibFoo v2.0，如何才能让两个应用共存？

Virtualenv 通过创造一个独立自主的环境，不依赖全局安装的包。

## 安装

```sh
pip install virtualenv
```

## 入门

Virtualenv 有一个基本命令：

```sh
virtualenv ENV
```

其中，`ENV` 是储存新的虚拟环境的目录。

（未完待续。。。）

## REF

- [Virtualenv][virtualenv]
- [Installation][install]
- [User Guide][guide]
- [virtualenvwrapper][wrapper]

[virtualenv]: https://virtualenv.pypa.io/en/stable/
[install]: https://virtualenv.pypa.io/en/stable/installation/
[guide]: https://virtualenv.pypa.io/en/stable/userguide/
[wrapper]: https://virtualenvwrapper.readthedocs.io/en/latest/