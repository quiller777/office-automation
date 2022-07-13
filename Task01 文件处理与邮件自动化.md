# Task01 - 文件处理与邮件自动化

## 1.1	文件处理

### 1.1.1	文件与文件路径

Windows使用反斜杠“ \\\”作为路径分隔符  (一个反斜杠表示转义，所以使用两个反斜杠连接)

OS X和Linux使用正斜杠"/"作为路径分隔符

常用  ***os.path.join()*** 来创建文件名称字符串

常用指令：

- **join**	          多路径组合频接

- **getctime**	返回文件或目录创建时间

- **getatime**	返回访问时间（每读一次会刷新）
- **getmtime**   返回修改时间（每修改一次均刷新）

- **getsize**	    文件大小

- **isabs**	        判断路径是否为绝对路径，如是返回True

- **exists**	      如果路径存在，返回True；否则返回False
- **isdir**             如果路径为存在目录，返回True，否则返回False
- **isfile**            如果路径为存在文件，返回True，否则返回False

### 1.1.2	当前工作目录

- **os.getcwd()**	获取当前工作路径

- **os.chdir()**		修改当前工作路径（若文件目录没有创建好，不能进行修改）

### 1.1.3	路径操作

#### 1.1.3.1	绝对路径与相对路径

- 绝对路径	总是从根文件夹开始
- 相对路径    相对于程序的当前工作目录（单个“.”表示当前目录缩写；双个”..“表示父文件夹）

常用指令：

- **os.path.abspath(path)**    相对路径转换为绝对路径，返回参数的绝对路径字符串
-  **os.path.isabs(path)**    判断是否为绝对路径，是返回Ture,反之为False

#### 1.1.3.2	路径操作

- **os.path.relpath(path,start)**    返回从start路径到path的相对路径的字符串。如果没提供start,就使用当前工作目录作为开始路径。
- **os.path.dirname(path)**    返回当前路径的目录名称。
- **os.path.basename(path）**    返回当前路径的文件名称。
- **os.path.split()**    获取(路径,文件名称）的字符串元组
- **split(os.path.sep)**    对路径进行字符串分割

#### 1.1.3.3	路径有效性检查

为了避免路径不存在导致函数报错，提前进行路径有效性检查

- **os.path.exists(path)**    如果path参数所指的文件或文件夹存在，则返回True,否则返回False。
- **os.path.isfile(path)**      如果path参数存在，并且是一个文件，则返回True,否则返回False。
- **os.path.isdir(path)**       如果path参数存在，并且是一个文件夹，则返回True,否则返回False。

### 1.1.4	文件及文件夹操作

- **os.makedirs()**    创建新文件夹（若已存在，不会覆盖但会报错）
- **os.path.getsize(path)**    返回path参数中文件的字节数
- **os.listdir(path)**    返回文件名字符串的列标，包含path参数中每个文件

```python
#获取目录下所有文件的总字节数，使用os.path.getsize()和os.listdir()进行组合
totalSize = 0
for filename in os.listdir('D:\\Datawhale\\python办公自动化'):
    totalSize = totalSize + os.path.getsize(os.path.join('D:\\Datawhale\\python办公自动化',filename))
print(totalSize)
```

### 1.1.5	文件读写过程

读写文件3个步骤：

1.调用*open()*函数，返回一个File对象。

2.调用File对象的 *read()* 或 *write()* 方法。

3.调用File对象的 *close()* 方法，关闭该文件。

#### 1.1.5.1	用open()函数打开文件

open()完整语法：

```python
open(file,mode=r',buffering=-1,encoding=None,errors=None,newline=None,closefd=True,opener=None)
```

- 共8个参数，前4个较常用;除file以外其它均有默认值

- file    指定要打开的文件名称，应包含文件路径，若不写路径表示和当前py脚本在同一文件夹

- buffering    指定打开文件所用的缓冲方式，默认值-1表示使用系统默认缓冲机制。（目的是减少CPU操作磁盘次数）

- encoding    指定文件编码方式，如GBK、UTF-8等，默认采用UTF-8(打开乱码可能是编码方式不一致)

- mode    指定文件打开方式，基本模式r/w/a对应读/写/追加写入；附加模式b/t/+表示二进制模式/文本模式/读写模式（附加模式要与基本模式组合使用）

  注意，带w的操作需谨慎，操作时回先清空原文件;带r的文件必须先存在，否则会找不到文件报错。

#### 1.1.5.2	读取文件内容

read()	读取文件内容

readline()	只返回第一行文本

readlines()	按行读取文件内容，取得一个字符列标，每个字符串是文本中一行且以\n结束

#### 1.1.5.3	写入文件

写入时需要用“w”写模式或“a”添加模式打开文件，不能用读模式

写模式覆盖原有文件;添加模式在已有文件末尾添加文本

注意：write()需要自己添加换行符“\n”

#### 1.1.5.4	保存变量

1. shelve模块

   将Python中变量保存到二进制的shelf文件中

2. pprint.pformat()函数

### 1.1.6	文件组织

**shutil模块**

#### 1.1.6.1	复制文件和文件夹

- **shutil.copy(source,destination)**	

将路径source处文件复制到路径destination处文件夹，并返回新复制文件绝对路径字符串

destination可以是一个文件的名称，即将source文件复制为新名称的destination

destination可以是一个文件夹，即复制到文件夹中，若文件夹不存在，则自动生成该文件

- **shutil.copytree(source,destination)**	

将路径source处文件包括其包含的文件夹和文件，复制到路径destination处文件夹，并返回新复制文件绝对路径字符串

destination必须为新创建，如已存在会报错

#### 1.1.6.2	移动与改名文件和文件夹

- **shutil.move(source, destination)**	

将路径 source 处的文件/文件夹移动到路径destination，并返回新位置的绝对路径的字符串

若source与destination均为文件夹，且destination已存在，则将source下所有内容移动到至destination（移动）

若source为文件夹，destination不存在，则将source文件夹所有内容傅直到destination文件夹中，source原文件夹名称替换为destination文件夹（移动+重命名）

若source与destination均为文件，source的文件呗移动至destination处，并以destination的文件名名命（移动+重命名）

#### 1.1.6.3	永久删除文件和文件夹

- **os.unlink(path)**	删除path处文件
- **os.rmdir(path)**     删除path处文件夹（该文件夹必须为空，其中不含文件和文件夹）

- **shutil.rmtree(path)** 删除path处文件夹，包含的文件和文件夹均一起删除

注意：删除需要小心处理，第一次运行时注释掉程序，并通过printf来帮助查看是否是想要删除的文件

#### 1.1.6.3	安全删除

**send2trash** 将文件或文件夹发送至回收站，而不是永久删除

### 1.1.7	遍历目录树

**os.walk(path)**

传入一个文件夹的路径，在for循环语句中使用os.walk()函数，遍历目录树，和range()函数遍历一个范围的数字类似。

不同的是，os.walk()在循环的每次迭代中，返回三个值：

 1）、当前文件夹称的字符串。

 2）、当前文件夹中子文件夹的字符串的列表。

 3）、当前文件夹中文件的字符串的列表。

 注：当前文件夹，是指for循环当前迭代的文件夹。程序的当前工作目录，不会因为os.walk()而改变。

### 1.1.8	用zipfile模块压缩文件

#### 1.1.8.1	创建和添加到zip文件

**zipfile.ZipFile('filename.zip', 'w')** ：以写模式创建一个压缩文件

如果只希望将文件添加到原有的zip文件中，就要向*zipfile.ZipFile()*传入'a'作为第二个参数，以添加模式打开 ZIP 文件。

#### 1.1.8.2	读取zip文件

**zipfile.ZipFile(filename)**	创建一个*ZipFile*对象（注意大写字母Z和F）,filename是要读取zip文件的文件名

ZipFile对象中的两个常用方法：

namelis()方法，返回zip文件中包含的所有文件和文件夹的字符串列表。

getinfo()方法，返回一个关于特定文件的ZipInfo对象。

ZipInfo对象的两个属性：file_size和compress_size，分别表示原来文件大小和压缩后文件大小。

#### 1.1.8.3	zip文件解压缩

**extractall()**	

从zip文件中解压缩所有文件和文件夹，放到当前工作目录中

也可以向*extractall()*传递的一个文件夹名称，它将文件解压缩到那个文件夹， 而不是当前工作目录

如果传递的文件夹名称不存在，就会被创建

**extract()**

从zip文件中解压单个文件

也可以向 *extract()*传递第二个参数， 将文件解压缩到指定的文件夹， 而不是当前工作目录

如果第二个参数指定的文件夹不存在， Python 就会创建它。*extract()*的返回值是被压缩后文件的绝对路径

### 1.1.9	文件查找

- **golb**

  - glob.glob('*[0-9]*.*')    匹配当前目录下文件名中带有数字的文件。

  - glob.glob(r'G:*')       获取G盘下的所有文件和文件夹，但是它不会进一步列明文件夹下的文件。

    也就是说，其返回的文件名只包括当前目录里的文件名，不包括子文件夹里的文件

- **fnmatch**

专门用来进行文件名匹配的模块，使用它可以完成更为复杂的文件名匹配

有4个函数，分别是fnmatch、fnmatchcase、filter和translate，其中最常用的是fnmatch函数

fnmatch.fnmatch(filename,pattern)		pattern表示匹配条件，测试文件名filename是否符合匹配条件



fnmatchcase和fnmatch函数类似，只是fnmatchcase函数强制区分字母大小写

fnmatch.filter(filelist,pattern)

- **hashlib**	通过MD5来确定两个文件是不是一样的

  