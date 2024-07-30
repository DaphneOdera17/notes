settings.py
```python
# MySQL 配置  
DATABASES = {  
    "default": {  
        "ENGINE": "django.db.backends.mysql",  
        "NAME": "kgllm",  
        "USER": "root",  
        "PASSWORD": "root",  
        "HOST": '127.0.0.1',  
        "PORT": 3306,  
    }  
}
```
models.py
```python
from django.db import models  
  
# MySQL 表  
class UserInfo(models.Model):  
    name = models.CharField(max_length=32)  
    password = models.CharField(max_length=64)
```
终端输入:
```shell
py manage.py makemigrations
py manage.py migrate
```

在表中新增列，新增列需要指定默认数据，例如：
```python
class UserInfo(models.Model):  
    name = models.CharField(max_length=32)  
    password = models.CharField(max_length=64)  
    email = models.EmailField(default="") # 新增列
```
或者允许为空
```python
email = models.EmailField(null=True, blank=True) # 新增列
```
