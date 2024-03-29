# 教务管理系统

本项目为东北林业大学教务管理系统，分为管理员端，学生端，教师端，实现了根据学工号登录、登录验证、信息管理、选课管理、成绩管理等功能。

仅供交流学习使用！

## 技术栈

采用BS架构，前后端分离。

- 前端：vue3.x

- 后端：[Django3.x](https://docs.djangoproject.com/zh-hans/3.2/)

- 页面: [Element-UI](https://element.eleme.cn/#/zh-CN)

## 运行方法

### 1. 下载文件
### 2. 运行后端

进入MyWeb文件夹

```
cd MyWeb
```
#### 安装依赖

```
pip install -r requirements.txt
```
#### 数据库

这里默认使用django自带的sqlite数据库，使用mysql数据库请看下面[配置mysql数据库](#anchor)

- 数据库迁移

  执行以下数据库迁移命令，会自动创建好在Model/models.py 文件中已定义的表。

  ```shell
  python manage.py makemigrations
  python manage.py migrate
  ```


- 数据库初始化

  ```shell
  python DBSettings.py
  ```


#### 运行后端

```
py manage.py runserver 8001
```
> 此处的端口8001需要与前端一致


#### 查看API

[文档地址](https://documenter.getpostman.com/view/14310338/TzXwGeZ5)


### 3. 运行前端

**确保本地已经有node.js环境**

返回项目文件夹

#### 安装依赖
```
npm install
```

#### 前端运行
```
npm run serve
```

#### 账号说明

- 管理员账号：
    - user_id : 9001
    - password: admin123

- 教师账号：
    - user_id : 1001
    - password: 12345678

- 学生账号：
    - user_id : 18122801
    - password: 12345678

## 其他

### 配置mysql数据库

<span id = "anchor"></span>

默认使用的是自带的sqlite数据库，使用mysql数据库需要重新配置一下。

进入后端文件夹：`./MyWeb/MyWeb/`

找到DBSetings.py文件，将数据库配置修改一下:

```python
mysql = "mysql+pymysql://root:Forget,88@123.60.31.182:3306/schoolnew" #1
DBSettings = mysql #2
DATABASES_mysql = {  
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'schoolnew',  # 数据库名称，需要实现建好 3
        'USER': 'root',  # 数据库用户名 4
        'PASSWORD': 'Forget,88',  # 数据库密码 5 
        'HOST': '123.60.31.182',  # 数据库所在主机地址，如果是本机的话，用localhost 6
        'PORT': '3306',  # 数据库端口 7
        'OPTIONS': {
            'init_command': 'SET foreign_key_checks = 0;',  # 初始化外键检查为0
            'charset': 'utf8mb4'
        }
    }
}
DATABASES_settings = DATABASES_mysql #8 
```

以上标数字的变量都需要修改。

> 注意初始化文件只能运行一次，不然数据库里面的数据会重复。
>
> 如果配置出错，**把下面这两个文件删除**，**重建一个数据库**，**修改上面提到的数据库配置**，从数据库迁移这一步再来一遍。

### 文件说明

```
├─.gitignore----------------------------------git忽略文件
├─.prettierrc---------------------------------配置文件
├─babel.config.js-----------------------------配置文件
├─package-lock.json---------------------------配置文件
├─package.json--------------------------------配置文件
├─postcss.config.js---------------------------配置文件
├─README.md-----------------------------------说明文档
├─vue.config.js-------------------------------配置文件
├─images--------------------------------------效果截图
├─src-----------------------------------------前端主要项目文件
|  ├─App.vue----------------------------------项目全局配置文件
|  ├─main.js----------------------------------项目入口文件
|  ├─router.js--------------------------------设置路由
|  ├─plugins----------------------------------UI文件
|  |    └element.js---------------------------引入UI组件
|  ├─components-------------------------------前端页面文件
|  |     ├─Login.vue--------------------------登录页面 管理员、教师、学生共享页面
|  |     |-admin------------------------------管理员页面文件夹
|  |     |-student----------------------------学生页面文件夹
|  |     |-teacher----------------------------教师页面文件夹
|  └─assets-----------------------------------资源文件，存放图片等
├─MyWeb---------------------------------------后端文件
|        ├─db.sqlite3-------------------------本地数据库
|        ├─manage.py--------------------------主程序入口
|        ├─requirements.txt-------------------依赖文件
|        └─MyWeb------------------------------项目主文件
└─public--------------------------------------公共资源文件
````
### 测试工具

postman

下载连接：https://www.postman.com/

## 参考资料

1. [Django 官方中文文档](https://docs.djangoproject.com/zh-hans/3.2/)

2. [Django REST framework 中文文档](https://q1mi.github.io/Django-REST-framework-documentation/)

3. [Django Rest Framework 自动生成接口文档的方法](https://cloud.tencent.com/developer/article/1632466)

4. [后台系统参考](http://gl.timemeetyou.com/#/login)



