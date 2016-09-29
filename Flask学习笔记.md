# 1. 安装
## 1.1 安装虚拟环境

```sh
$ sudo apt-get install python-virtualenv
```

## 1.2 使用Git代码

```sh
$ git clone https://github.com/miguelgrinberg/flasky.git
$ cd flasky
$ git checkout 1a
```

## 1.3 开启虚拟环境

```sh
$ virtualenv venv
```

激活虚拟环境

```sh
$ source venv/bin/activate
(venv) $
```

退出虚拟环境

```sh
(venv) $ deactivate
```
## 1.4 使用Pip安装Python包

```sh
(venv) $ pip install flask
```

测试成功安装flask，无错误即成功

```sh
(venv) $ python
>>> import flask
>>>
```

# 2. Hello World

##2.1 Hello World代码
```git checkout 2a```

```python
from flask import Flask
app = Flask(__name__)


@app.route('/')
def index():
    return '<h1>Hello World!</h1>'


if __name__ == '__main__':
    app.run(debug=True)

```

运行

```sh
(venv) $ python hello.py
* Running on http://127.0.0.1:5000/
* Restarting with reloader
```

这时本机访问 http://127.0.0.1:5000/ 会打开HelloWorld页面!


##2.2 使用Flask-Script扩展支持命令行选项

Flask-Script 扩展使用 pip 安装：

```sh
(venv) $ pip install flask-script
```

代码中使用Flask-Script  
```git checkout 2c```

```py
from flask import Flask
from flask_script import Manager

app = Flask(__name__)

manager = Manager(app)


@app.route('/')
def index():
    return '<h1>Hello World!</h1>'


@app.route('/user/<name>')
def user(name):
    return '<h1>Hello, %s!</h1>' % name


if __name__ == '__main__':
    manager.run()

```

这时可以指定参数运行了

```sh
(venv) $ python hello.py runserver --host 0.0.0.0 --port 8080
```

这样外部机器访问其地址就可以访问了，但是必须指定端口。若要使用http默认端口80，需要root权限。


#3. 模板
## 3.1 Jinja2模板引擎
```git checkout 3a```   
两个模板文件:   
templates/index.html:   
```<h1>Hello World!</h1>```   
templates/user.html:   
```<h1>Hello, {{ name }}!</h1>```   
Flask 提供的 render_template 函数把 Jinja2 模板引擎集成到了程序中，代码为：

```py
from flask import Flask, render_template
from flask_script import Manager

app = Flask(__name__)

manager = Manager(app)


@app.route('/')
def index():
    return render_template('index.html')


@app.route('/user/<name>')
def user(name):
    return render_template('user.html', name=name)


if __name__ == '__main__':
    manager.run()
```

### 控制结构
条件控制语句:
 
 ```py
{% if user %}	Hello, {{ user }}!{% else %}	Hello, Stranger!{% endif %}
 ```

 for 循环渲染一组元素：
 
 ```html
 <ul>	{% for comment in comments %}		<li>{{ comment }}</li>
	{% endfor %}</ul>
 ```
 
 
Jinja2 还支持宏。宏类似于 Python 代码中的函数：

```py
{% macro render_comment(comment) %} 
	<li>{{ comment }}</li>{% endmacro %}<ul>	{% for comment in comments %}		{{ render_comment(comment) }}
	 {% endfor %}</ul>
```

为了重复使用宏,我们可以将其保存在单独的文件中,然后在需要使用的模板中导入:

```py
{% import 'macros.html' as macros %} 
<ul>	{% for comment in comments %}		{{ macros.render_comment(comment) }}	{% endfor %} 
</ul>`
```

需要在多处重复使用的模板代码片段可以写入单独的文件,再包含在所有模板中,以避免 重复:

```py
{% include 'common.html' %}
```

重复使用代码可以使用模板继承，比如有个base.html基模板：

```html
<html>
<head>	{% block head %}	<title>{% block title %}{% endblock %} - My Application</title> 
	{% endblock %}</head><body>	{% block body %}	{% endblock %} 
</body></html>
```

我们定义了名为 head、title 和body 的块，下面这个示例是基模板的衍生模板:

```py
{% extends "base.html" %}{% block title %}Index{% endblock %} {% block head %}	{{ super() }}	<style>	</style>{% endblock %}{% block body %} <h1>Hello, World!</h1> {% endblock %}
```
新定义的 head 块,在基模板中其内容不 是空的,所以使用 super() 获取原来的内容。

## 3.2 使用Flask-Bootstrap
安装

```sh
(venv) $ pip install flask-bootstrap
```





