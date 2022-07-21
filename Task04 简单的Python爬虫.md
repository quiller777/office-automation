# Task04	简单的Python爬虫

## 4.1	Requests (http请求库)

**常规指令**

- **re.status_code** 	响应的HTTP状态码 (可以判断请求是否成功)
- **re.text**                   响应内容的字符串形式
- **rs.content**            响应内容的二进制形式
- **rs.encoding**          响应内容的编码 （常见编码有ASCII / GBK / UTF-8 )

**下载文本/图片**

- **re.text**                   用于文本内容的获取、下载

- **re.content**           用于图片、视频、音频等内容的获取、下载



## 4.2	BeautifulSoup 库 (解析网页)

```python
from bs4 import BeautifulSoup 		# 导入BeautifulSoup库
BeautifulSoup(res.text, 'lxmlr’) 	# 将网页源代码的字符串形式解析成了 BeautifulSoup 对象
```

解析后的 BeautifulSoup 对象可以方便的提取信息

- **find()** 					返回符合条件的**首个**数据
- **find_all()**               返回符合条件的**所有**数据

标签定位

```python
# 定位div开头 同时id为'doubanapp-tip的标签
soup.find('div', id='doubanapp-tip')
# 定位a抬头 同时class为rating_nums的标签
soup.find_all('span', class_='rating_nums')
#class是python中定义类的关键字，因此用class_表示HTML中的class
```

### 定位方式

- **直接定位**

```HTML
<body>

<table>

<td>apple</td>

<td>banana</td>

</table>

</body>
```

```python
label_loc = bs.body.table.td
```

- **通过 标签名 定位**

  ```html
  <table>
  
  <td>apple</td>
      
  <td>banana</td>
  
  </table>
  ```

  ```python
  bs.find("td") 返回第一个<td></td>
  
  bs.findAll("td") 返回所有<td></td>**通过 标签名 定位**
  ```

<table>

- **通过 标签署性 定位**

```html
<table>

<td name="fruit">apple</td>

<td name="fruit">apple</td>

</table>
```

```python
bs.find("td",{"name":"fruit"}) 返回第一个<td></td>

bs.findAll("td",{"name":"fruit"}) 返回所有<td></td>
```

**注意：**

**find(name="fruit") 与  find("td",{"name":"fruit"})  区别： 后者由<td>的限制条件**



- **通过 text 定位**

  ```html
  <table>
  
  <td>apple</td>
  
  <td>banana</td>
  
  </table>
  ```

  ```python
  find(text="apple") 返回<td></td>
  ```

注意：

text匹配必须完全相同，而且应在同一标签内。上面例子中 find(text="app") 返回None

想要只匹配部分文本，应使用正则表达式，接下来介绍。

- **通过 正则表达式与以上方式结合 定位**

```html
<table>

<td name="fruit">apple</td>

<td name="fruit">apple</td>

</table>
```

```python
find(text=re.compile("app")) 返回含有app的标签

bs.find("td",{"name":re.compile("fruit")})
```

