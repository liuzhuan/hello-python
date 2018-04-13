# Django

Django 是一个 Web 框架，用更少代码开发更好的 Web 应用。

## 安装

```sh
$ pip install Django

# 查看 Django 是否安装正确
$ python -m django --version
2.4.0
```

## 入门

### 创建项目

在当前目录创建项目文件夹 `mysite`

```sh
$ django-admin startproject mysite
```

### 开发服务器

为了验证 Django 项目能否正常工作，可以运行如下命令：

```sh
$ python manage.py runserver
```

在浏览器访问 `127.0.0.1:8000` 就可以看到“恭喜”页面，这说明已经安装成功。

### 创建一个投票应用

每个 Django 应用包含一个 Python 包，它需要遵循一定的惯例。Django 自带脚手架工具，可以帮你生成应用的目录结构，你只需专心写代码就好。

（未完待续。。。）

## REF

- [The Web framework for perfectionists with deadlines | Django][django]
- [Getting started with Django | Django][start]
- [Quick install guide | Django][install]
- [Writing your first Django app, part 1][tut01]

[django]: https://www.djangoproject.com
[start]: https://www.djangoproject.com/start/
[install]: https://docs.djangoproject.com/en/2.0/intro/install/
[tut01]: https://docs.djangoproject.com/en/2.0/intro/tutorial01/