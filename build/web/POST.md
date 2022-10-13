# 使用Python发送POST请求
发送post请求分为表单类（x-www-form-urlencoded）和json（application/json）格式

data参数支持字典格式和字符串格式，建议使用字典格式，在使用json.dumps()方法把data转换为合法的json格式字符串，或者将data参数赋值给post方法的json参数

data以字符串格式传输需要注意的事项：

　　1、必须是json格式字符串，必须用双引号，k-v之家必须有逗号，布尔值必须是小写的true/false

　　2、不能有中文，直接传字符串不会自动编码
　　
1、传统表单post请求（x-www-form-urlencoded）
```python
import requests
url = "http://test"
data = {"key":"value"}
res = requests.post(url=url,data=data)
print(res.text)
```
2、json类型的post请求

```python
import requests
url = "http://test"
data = '{"key":"value"}'
#字符串格式
res = requests.post(url=url,data=data)
print(res.text)
```
3、使用字典格式填写参数，传递时转换为json格式
（1）json.dumps()方法转换
```python
import requests
import json
url ="http://test"
data = {"key":"value"}
res = requests.post(url=url,data=json.dumps(data))
print(res.text)
```
 （2）将字典格式的data数据赋给post方法的json参数
```python
import requests
import json
url = "http://test"
data = {"key":"value"}
res = requests.post(url=url,json=data)
print(res.text)
```
