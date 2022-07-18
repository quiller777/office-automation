# Task3.1	Python与Word

通过 **python-docx** 库实现相关功能

Word文档（**Document**) 由不同段落（**Paragraph**) 和文字块 (**Run**) 组成

- 每个**`Document`**包含许多个代表“段落”的**`Paragraph`**对象，存放在**`document.paragraphs`**中。
- 每个**`Paragraph`**都有许多个代表"行内元素"的**`Run`**对象，存放在**`paragraph.runs`**中。

`run`**是最基本的单位，每个**`run`**对象内的文本样式都是一致的**

**`Paragraph`**格式	paragraph_format 进行设置

**`Run`**格式				字号、颜色等

### 3.1.1	字体设置

font.name的设置为全局变量，如果需要进行多种字体设置，可以设置成不同的style_font进行调用 或者 定义字体设置函数（font_setting)

style_font可以对同一行的不同文字进行设置，而font_setting只能针对段落

### 3.1.2	插入图片与表格

```python
#新增图片
doc_1.add_picture('周杰伦.jpg',width=Inches(1.0), height=Inches(1.0))
```

```python
# 创建3行1列表格
table1 = doc_1.add_table(rows=2, cols=1)
table1.style='Medium Grid 1 Accent 1'  #表格样式很多种，如，Light Shading Accent 1等
```

### 3.1.3	设置页眉页脚

对文档中 节(section) 中的 页眉(header) 和 页脚 (footer) 对象

### 3.1.4	相关格式设置

```python
'''对齐设置'''
from docx.enum.text import WD_ALIGN_PARAGRAPH
#LEFT: 左对齐
#CENTER: 文字居中
#RIGHT: 右对齐
#JUSTIFY: 文本两端对齐

'''设置段落行距'''
from docx.shared import Length
# SINGLE :单倍行距（默认）
#ONE_POINT_FIVE : 1.5倍行距
# DOUBLE2 : 倍行距
#AT_LEAST : 最小值
#EXACTLY:固定值
# MULTIPLE : 多倍行距

paragraph.line_spacing_rule = WD_LINE_SPACING.EXACTLY #固定值
paragraph_format.line_spacing = Pt(18) # 固定值18磅
paragraph.line_spacing_rule = WD_LINE_SPACING.MULTIPLE #多倍行距
paragraph_format.line_spacing = 1.75 # 1.75倍行间距

'''设置字体属性'''
from docx.shared import RGBColor,Pt
#all_caps:全部大写字母
#bold:加粗
#color:字体颜色

#double_strike:双删除线
#hidden : 隐藏
#imprint : 印记
#italic : 斜体
#name  :字体
#shadow  :阴影
#strike  :  删除线
#subscript  :下标	
#superscript  :上标
#underline  :下划线
```



# Task3.2	Python与PDF

相关功能使用库文件 **PyPDF2**  和 **pdfplumber**

 **PyPDF2**	更好的读取、写入、分割、合并PDF文件

**pdfplumber**	更好的读取 PDF 文件中内容和提取 PDF 中的表格

#### 3.2.1	批量拆分

将完整PDF拆分成不同页数PDF。大致过程为：

- 读取 PDF 的整体信息、总页数等
- 遍历每一页内容，以每个 step 为间隔将 PDF 存成每一个小的文件块
- 将小的文件块重新保存为新的 PDF 文件

拆分的过程中，可以手动设置间隔，例如：每5页保存成一个小的 PDF 文件

#### 3.2.2	批量合并

过程思路：

- 确定要合并的 **文件顺序**
- 循环追加到一个文件块中
- 保存成一个新的文件

#### 3.2.3	提取文字内容

通过使用 **pdfplumber** 库的 **extract_text** 函数进行实现

#### 3.2.5	提取表格内容

通过使用 **pdfplumber** 库的 **extract_table** 函数进行实现

注：多个表格改为使用 **extract_tables**

#### 3.2.6	提取图片内容

这里讨论主要是提取PDF中的图片，不是讲PDF转存为图片

该功能需要使用 **PyMuPDF** 模块中的 **fitz**，大致思路如下：

- 使用 fitz 打开文档，获取文档详细数据
- 遍历每一个元素，通过正则找到图片的索引位置
- 使用 Pixmap 将索引对应的元素生成图片
- 通过 size 函数过滤较小的图片

#### 3.2.7	PDF转换为图片

使用  **pdf2image**  库的相关功能

#### 3.2.8	添加水印

在现有的水印PDF文件基础上，依次通过 mergePage 讲每一页PDF合并到水印文件上，最后将每一页待水印的PDF合并成一个文件



