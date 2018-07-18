# face_login
利用facenet实现检测图片中的人脸，将识别到的人脸向量存入数据库，此外利用post提交一个新图片（也可以提交一个图片地址，参考face_recognition_api.py文件中get_url_imgae函数自行修改），返回数据库中相似的人脸的信息
算法主要分为2个步骤<br/>
1.**提取图片中的人脸 ，并保存到临时目录中**<br/>
2.**将人脸图片转换为128维的向量 ，便于后续求人脸相似度**<br/>

项目主要分为3个步骤<br/>
1.**提交post请求，将uid ugroup pic提交，进行人脸信息保存操作**<br/>
2.**收到请求后将pic进行处理解析为128维向量保存，并跟uid和ugroup保存入库 ，返回数据库插入成功的id**<br/>
3.**提交post请求，将ugroup pic提交人脸查询请求，意思为再ugroup中查看与图片pic相似的人脸**<br/>
4.**收到请求后，处理图片解析图片中所有的人脸，进行按库查询，然后与该图片中所有人脸相似的uid和距离（相似度距离）**<br/>

## 安装准备
#### 安装python包 
下列包全部安装即可
如下
`tensorflow`
`scipy`
`scikit-learn`
`opencv-python`
`h5py`
`matplotlib`
`Pillow`
`requests`
`psutil`
`mysql-connector`
`Werkzeug`
`Flask`
`Flask-HTTPAuth`


## 提前建立数据库 
建表语句再database.sql 
（需要提前建立数据库，名字自己定义，本项目数据库名为face）
数据库配置在face_mysql.py文件中 
（第12行 配置数据库用户名、密码、地址、数据库地址 本案例配置如下
```python
db = mysql.connector.connect(user='root', password='root', host='127.0.0.1', database='face')
```
）

## 模型准备
本项目是根据[facenet](https://github.com/davidsandberg/facenet)中提取关键的代码，将其进行封装使用
所以需要提交下载facenect提供的模型，现在保存在[百度网盘](http://pan.baidu.com/s/1i4YhAdB)中  密码：avbl
下载下来后按照models\facenet\20170512-110547  这个目录结构存放即可

## 如何使用？
首先在服务器上 执行 
``` bash
python  face_recognition_api.py  
```

访问地址是XXXXXX:8080  这个可以配置 （文件face_recognition_api.py 最后代码中有注释）
# 页面
## 注册
<img src="https://github.com/xvshu/face_login/blob/master/doc/face_insert.jpg" ></img>

## 登陆
<img src="https://github.com/xvshu/face_login/blob/master/doc/face_query.jpg" ></img>
