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
