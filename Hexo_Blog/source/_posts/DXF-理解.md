---
title: DXF-理解
date: 2020-06-14 19:47:19
tags: 
    - DXF
categories: DXF
---
## DXF™ 格式

### HEADER 段
包含图形的基本信息。它由 AutoCAD 数据库版本号和一些系统变量组成。每个参数都包含一个变量名称及其关联的值。
DXF 文件的 HEADER 段包含与图形关联的变量的设置。
每个变量由给出变量名称的组码 9 指定，其后是提供变量值的组。

```
0           HEADER段开始
SECTION 
2
HEADER
9           每个标题变量前面都要有一个
$<变量>
<组码>
<值>

0           HEADER段结束
ENDSEC
```

```
example:
    HEADER
    9
    $LASTSAVEDBY
      1
    allen
```
这一段的意思代表，Header 段中，9代表开始 $LASTSAVEDBY 代表类型'最后保存被XXX' 组码为1 内容 allen 这一段意思是 最后被 allen 保存

### CLASSES 段
包含应用程序定义的类的信息，这些类的实例出现在数据库的 BLOCKS、ENTITIES 和 OBJECTS 段中。类定义在类的层次结构中是固定不变的。

```
0
SECTION
2
CLASSES         CLASSES 段的开始

0               为每个条目重复一次
CLASS
1
<类 dxf 记录>
2
<类名>
3
<应用程序名>
90
<标志>
280
<标志>
281
<标志>

0
ENDSEC            CLASSES 段的结束

实例
CLASSES 
0                 classes 段 开始从这里开始
CLASS
 1                类 DXF 记录名；始终唯一
ACDBDICTIONARYWDFLT
 2                C++ 类名，始终唯一 
AcDbDictionaryWithDefault
 3                应用程序名。当前未加载本段列出的某个类定义时出现在“警告”框中
ObjectDBX Classes
90                代理功能标志。指示该对象作为代理时的功能
       0          不允许操作 (0)
91                自定义类的实例计数
      1
280               "是代理"标志。如果创建此 DXF 文件时未加载类，则设定为 1，否则设定为 0
   0
281               "是图元"标志。如果类从 AcDbEntity 类派生并可能位于 BLOCKS 或 ENTITIES 段中，则设定为 1。如果设定为 0，则实例可能仅出现在 OBJECTS 段中
   0
```

### TABLES 段

这里包含很多种table 表，表的次序是可以更改的，但是 LTYPE 表总是位于 LAYER 表之前。每个表都由带有 TABLE 标签的 0 组码引入。
图形中的表可以包含已删除的项目，但这些项目并不写入 DXF 文件。这样，***表标题后面的表条目可能少于 70 组码指示的数目，因此不要使用 70 组码中的计数作为索引在表中执行读取操作。***
提供此组码是为了使读取 DXF 文件的程序能够分配足以容纳其后的全部表条目的数组。

***每个表的结尾由 0 组指定，组值为 ENDTAB。***
包含以下符号表的定义：
- 符号表
- APPID（应用程序标识表）
- BLOCK_RECORD（块参照表）
- DIMSTYLE（标注样式表）
- LAYER （图层表）
- LTYPE（线型表）
- STYLE（文字样式表）
- UCS（用户坐标系表）
- VIEW（视图表）
- VPORT（视口配置表）

```
0
SECTION
2
TABLES          TABLES 段的开始

0               通用表组码；为每个条目重复一次
TABLE
2
<表类型>
5
<句柄>
100
AcDbSymbolTable
70
<最大条目数量>
0               表条目数据；为每个表记录重复一次    
<表类型>
5
<句柄>
100
AcDbSymbolTableRecord
.
. <数据>
.


0
ENDTAB           表的结束

0
ENDSEC           TABLES 段的结束
```
[Example](http://docs.autodesk.com/ACD/2011/CHS/filesDXF/WS1a9193826455f5ff18cb41610ec0a2e719-7961.htm)
[TABLES段 DOC](http://docs.autodesk.com/ACD/2011/CHS/filesDXF/WSfacf1429558a55de185c428100849a0ab7-5e1a.htm)

### BLOCKS 段
***块段***包含构成图形中每个块参照的块定义和图形图元。BLOCKS 段中的所有图元都出现在 BLOCK 和 ENDBLK 图元之间。BLOCK 和 ENDBLK 图元仅出现在 BLOCKS 段。尽管块定义可以包含插入图元，但不允许嵌套块定义（即 ***BLOCK 和 ENDBLK 图元之间不允许出现另一对 BLOCK 和 ENDBLK 图元***）。
[Example](http://docs.autodesk.com/ACD/2011/CHS/filesDXF/WS1a9193826455f5ff18cb41610ec0a2e719-795f.htm)
[BLOCKS DOC](http://docs.autodesk.com/ACD/2011/CHS/filesDXF/WSfacf1429558a55de185c428100849a0ab7-5e01.htm)

### ENTITIES 段
***图元段***包含图形中的图形对象（图元），其中包括块参照（插入图元）。
[Example](http://docs.autodesk.com/ACD/2011/CHS/filesDXF/WS1a9193826455f5ff18cb41610ec0a2e719-795d.htm)
### OBJECTS 段
包含图形中的非图形对象。除图元、符号表记录以及符号表以外的所有对象都存储在此段。OBJECTS 段中的条目样例是包含多线样式和组的词典。
[Example](http://docs.autodesk.com/ACD/2011/CHS/filesDXF/WS1a9193826455f5ff18cb41610ec0a2e719-795b.htm)
### THUMBNAILIMAGE 段
包含图形的预览图像数据。此段为可选。

---
[参考链接](http://docs.autodesk.com/ACD/2011/CHS/filesDXF/WS1a9193826455f5ff18cb41610ec0a2e719-7a6f.htm)



