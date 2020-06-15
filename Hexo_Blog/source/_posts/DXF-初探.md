---
title: DXF 初探
date: 2020-06-03 00:29:57
tags: 
    - DXF
categories: DXF
---
## DXF™ 格式

> DXF™ 格式是 AutoCAD® 图形文件中包含的所有信息的一种**带标记数据**的表示方式。带标记数据是指文件中的每个数据元素前面都带有一个称为组码的整数。组码的值表明了随后的数据元素的类型。还指出了数据元素对于给定对象（或记录）类型的含义。实际上，图形文件中所有用户指定的信息都可以用 DXF 格式表示。
--- 
## 对象和图元

> 在 DXF 格式中，对象的定义与图元的定义不同 :对象没有图形表示，而图元有图形表示。图元称为图形对象，对象称为非图形对象。
> ***注：词典是对象不是图元。***
> 图元出现在 DXF 文件的 BLOCK 和 ENTITIES 段。组码在这两段中用法相同。定义图元的某些组码始终显示，其他组码则是可选的，仅当值与默认值不同时才显示。
--- 
## DXF文件结构

- HEADER 段
- CLASSES 段
- TABLES 段
- BLOXKS 段
- ENTITIES 段
- OBJECTS 段
- THUMBNAILIMAGE 段

## 组码值类型
[组码值类型](http://docs.autodesk.com/ACD/2011/CHS/filesDXF/WS1a9193826455f5ff18cb41610ec0a2e719-7a64.htm)

[按数字次序排列的组码](http://docs.autodesk.com/ACD/2011/CHS/filesDXF/WS1a9193826455f5ff18cb41610ec0a2e719-7a62.htm)