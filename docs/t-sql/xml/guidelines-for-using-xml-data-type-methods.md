---
title: "使用 xml 数据类型方法的指导原则 |Microsoft 文档"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|xml
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- xml data type [SQL Server], methods
- methods [XML in SQL Server]
ms.assetid: 1a483aa1-42de-4c88-a4b8-c518def3d496
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 79f10b22ba88d6dd860c608c9468e20a27615650
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="guidelines-for-using-xml-data-type-methods"></a>xml 数据类型方法的使用准则
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  本主题介绍使用指南**xml**数据类型方法。  
  
## <a name="the-print-statement"></a>PRINT 语句  
 **Xml**数据类型方法不能用在打印语句中，如下面的示例中所示。 **Xml**数据类型方法将被视为子查询，而 PRINT 语句中不允许使用子查询。 因此，下面的示例将返回一个错误：  
  
```  
DECLARE @x xml  
SET @x = '<root>Hello</root>'  
PRINT @x.value('/root[1]', 'varchar(20)') -- will not work because this is treated as a subquery (select top 1 col from table)   
```  
  
 解决方案是首次分配的结果**value （)**给变量的方法**xml**键入，然后在查询中指定的变量。  
  
```  
DECLARE @x xml  
DECLARE @c varchar(max)  
SET @x = '<root>Hello</root>'  
SET @c = @x.value('/root[1]', 'varchar(11)')  
PRINT @c                                                        
```  
  
## <a name="the-group-by-clause"></a>组 BY 子句  
 **Xml**数据类型方法内部视为子查询。 因为 GROUP BY 需要一个标量，但不允许聚合和子查询，不能指定**xml** GROUP BY 子句中的数据类型方法。 另一种解决方案是调用用户定义函数，然后在其内部使用 XML 方法。  
  
## <a name="reporting-errors"></a>报告错误  
 时报告错误， **xml**数据类型方法引发的单个错误采用以下格式：  
  
```  
Msg errorNumber, Level levelNumber, State stateNumber:  
XQuery [database.table.method]: description_of_error  
```  
  
 例如：  
  
```  
Msg 2396, Level 16, State 1:  
XQuery [xmldb_test.xmlcol.query()]: Attribute may not appear outside of an element  
```  
  
## <a name="singleton-checks"></a>单一性检查  
 如果编译器无法确定在运行时能否确保单一性，则具有单一性要求的位置步骤、函数参数和运算符将返回错误。 此问题经常出现在非类型化数据上。 例如，查找属性时就需要使用单一的父元素。 通过一个用来选择单个父节点的序号即可满足此要求。 评估**node （)**-**value （)**进行组合，以提取属性值可能不需要的序号规范。 如下例所示。  
  
### <a name="example-known-singleton"></a>示例：已知单一性  
 在此示例中， **nodes （)**方法生成每个单独的一行 <`book`> 元素。 **Value （)**计算的方法 <`book`> 节点将的值提取@genre和属性，是单一实例。  
  
```  
SELECT nref.value('@genre', 'varchar(max)') LastName  
FROM   T CROSS APPLY xCol.nodes('//book') AS R(nref)  
```  
  
 XML 架构用于对类型化的 XML 进行类型检查。 如果将某个节点指定为 XML 架构中单一的节点，则编译器将使用该信息，并且不会发生任何错误。 否则，需要使用一个用来选择单个节点的序号。 具体而言，使用后代或自助轴 (/ /) 轴，例如/簿 / / 标题、 失去的单一实例基数推理\<标题 > 元素中，即使 XML 架构已指定，则要这样。 因此，您应该将其重写为 (/book//title)[1]。  
  
 对于类型检查，务必注意 //first-name[1] 和 (//first-name)[1] 之间的差异。 前者返回的序列\<第一个名称 > 节点中的每个节点是最左边\<第一个名称 > 同级节点。 后者返回的第一个 singleton\<第一个名称 > 节点在 XML 实例中的文档顺序排列。  
  
### <a name="example-using-value"></a>示例：使用 value()  
 非类型化的 XML 列中的以下查询会导致静态的编译错误。这是因为**value （)**需要单一实例节点，如第一个参数，编译器无法确定是否只有一个\<最后名称 > 节点将出现在运行时：  
  
```  
SELECT xCol.value('//author/last-name', 'nvarchar(50)') LastName  
FROM   T  
```  
  
 可以考虑下面的解决办法：  
  
```  
SELECT xCol.value('//author/last-name[1]', 'nvarchar(50)') LastName  
FROM   T  
```  
  
 但是，该解决办法不解决错误，因为在每个 XML 实例中可能会有多个 <`author`> 节点。 采用下面的重写代码可以解决问题：  
  
```  
SELECT xCol.value('(//author/last-name/text())[1]', 'nvarchar(50)') LastName  
FROM   T  
```  
  
 此查询返回每个 XML 实例中第一个 `<last-name>` 元素的值。  
  
## <a name="see-also"></a>另请参阅  
 [xml 数据类型方法](../../t-sql/xml/xml-data-type-methods.md)  
  
  
