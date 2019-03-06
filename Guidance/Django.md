[Home](../README.md)

# Django Guidance

## 资源和文档

[Django Homepage](https://www.djangoproject.com/)

[Django Document](https://docs.djangoproject.com/en/2.1/)

## 概览

Django 在本项目中作为程序的后端。Django 的后端渲染将不被使用。  
Django 的文件结构介绍参见 [Here](https://docs.djangoproject.com/en/2.1/intro/tutorial01/)。

## 文件结构

```
app_name/
    admin.py
    apps.py
    listeners.py
    migrations/
        __init__.py
    models.py
    services.py
    tests.py
    views.py
```


#### admin.py

Django Admin 的配置文件

#### apps.py

Django 类注册文件

#### listeners.py

与模块相关的事件触发器

#### migrations/

Django 数据库变更文件（执行 makemigrations 操作后自动生成）

#### models.py

模块数据库结构定义文件

#### services.py

事务操作文件集合

#### tests.py

单元测试

#### views.py

页面渲染文件

## 操作

### 执行数据库变更

```sh
python manage.py migrate
```

### 创建管理员账户

```sh
python manage.py createsuperuser
```

### 运行程序

```sh
python manage.py runserver 0.0.0.0:8000
```

### 增加类

```sh
python manage.py startapp app_name

# 编辑 models.py

python manage.py makemigrations
python manage.py migrate
```
### 修改类

```sh
# 编辑 models.py

python manage.py makemigrations
python manage.py migrate
```
