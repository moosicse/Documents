# Code Style and Standards

> 代码风格和规范

## General

### 代码换行规则

代码应从 { 或者 ( 处换行。代码要么都在一行，要么都分开。每行代码最好不超过80个字符。

### 代码行数

每次提交的代码最好不要超过 200 行（大量前端除外）。如果有超过，请根据具体情况进行拆分或者详细说明。  
函数代码数量不要超过 80 行。如果超过，请拆分或者写好完整的注释。

## Python

### 命名

Python 变量应使用蛇形命名法，类名使用大驼峰命名法。例如

```python
class UserSong:
    def __init__(self):
        pass


this_song = UserSong()
```

如果是某个对象的 id 属性，或是某个对象的 id 列表，应以如下形式展现：

```python
object_id = 1
object_ids = [1, 2, 3]
```

```python
# 只在文件内部使用的函数，需要以下划线开头
_get_something() 

# 函数名要简洁，可以指明应传入什么参数
get_object_by_user(user)
```

### Import

在导入包时，应先导入以 *from* 开头的导入项目，再导入以 *import* 开头的导入项目。相同开头的导入项目尽量以开头字母顺序进行导入。  
导入包之间可添加一个空行用作区别。导入包部分和下文要两个空行进行区别。
例如

```python
from collections import OrderedDict
from django.db import models

import arrow

import datetime
import os


class Class1:
    pass
```

### 空行

在每个类开始之前，必须有两个空行。
在每个函数开始之间，必须有一个空行。
整段代码中不应该出现大于两行的空行。

### if-else 简化

假设以下情况

```python
if condition:
    // 一大段代码
else:
    return xx
```

应简化为

```python
if not condition:
    return xx

// 一大段代码
```

## JavaScript

### 命名

JavaScript 变量应使用小驼峰命名法，类名使用大驼峰命名法。例如

```javascript
class UserSong {
    doSomething = () => {
        // Do something
    };
}

export default new UserSong();

const newSong = UserSong();
```

### React

对于每个功能(app)，请使用components和containers两个文件夹分别归类*展示组件*和*容器组件*

### Console

提交的代码中不要包含 console.log/warning/error, alert 之类的存在输出的代码。如果特殊情况需要使用，请带上注释。

### 箭头函数

尽量使用箭头函数。即如下函数

```javascript
function a () {
  //do something...
}
// 以上函数应改为
a = () => {
  //do something...
};
```

### 分号

请完整并正确地使用分号。如果分号没有处理清楚，可能被 JS 语法分析错误地处理。
