---
title: 示例：指定 XMLTEXT 指令 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- XMLTEXT directive
ms.assetid: e78008ec-51e8-4fd1-b86f-1058a781de17
caps.latest.revision: 10
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 7d53197ef75615141a2f25f326e3dcdd0f0d0ba2
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36129837"
---
# <a name="example-specifying-the-xmltext-directive"></a>示例：指定 XMLTEXT 指令
  此示例演示了如何通过使用解决溢出列中的数据`XMLTEXT`指令`SELECT`使用 EXPLICIT 模式的语句。  
  
 请考虑一下 `Person` 表。 此表含有存储 XML 文档的未使用部分的 `Overflow` 列。  
  
```  
USE tempdb;  
GO  
CREATE TABLE Person(PersonID varchar(5), PersonName varchar(20), Overflow nvarchar(200));  
GO  
INSERT INTO Person VALUES   
    ('P1','Joe',N'<SomeTag attr1="data">content</SomeTag>')  
   ,('P2','Joe',N'<SomeTag attr2="data"/>')  
   ,('P3','Joe',N'<SomeTag attr3="data" PersonID="P">content</SomeTag>');  
```  
  
 此查询从 `Person` 表中检索列。 对于 `Overflow` 列，没有指定 *AttributeName* ，但是在提供通用表列名的过程中，已将 *directive* 设置为 `XMLTEXT` 。  
  
```  
SELECT 1 as Tag, NULL as parent,  
       PersonID as [Parent!1!PersonID],  
       PersonName as [Parent!1!PersonName],  
       Overflow as [Parent!1!!XMLTEST] -- No AttributeName; XMLTEXT directive  
FROM Person  
FOR XML EXPLICIT;  
```  
  
 在所得到的 XML 文档中：  
  
-   因为 `Overflow` 列没有指定 *AttributeName*，但却指定了 `xmltext` 指令，所以 <`overflow`> 元素中的属性被追加到封闭的 <`Parent`> 元素的属性列表中。  
  
-   因为 <`xmltext`> 元素中的 `PersonID` 属性与相同元素级上检索到的 `PersonID` 属性冲突，所以忽略 <`xmltext`> 元素中的此属性，即使 `PersonID` 为 NULL 也是如此。 通常情况下，属性将覆盖溢出中具有相同名称的属性。  
  
 结果如下：  
  
 `<Parent PersonID="P1" PersonName="Joe" attr1="data">content</Parent>`  
  
 `<Parent PersonID="P2" PersonName="Joe" attr2="data"></Parent>`  
  
 `<Parent PersonID="P3" PersonName="Joe" attr3="data">content</Parent>`  
  
 如果溢出数据包含子元素且指定了相同的查询，则 `Overflow` 列中的子元素将作为包含它的 <`Parent`> 元素的子元素添加。  
  
 例如，更改 `Person` 表中的数据以使 `Overflow` 列此时包含子元素。  
  
```  
USE tempdb;  
GO  
TRUNCATE TABLE Person;  
GO  
INSERT INTO Person VALUES   
    ('P1','Joe',N'<SomeTag attr1="data">content</SomeTag>')  
   ,('P2','Joe',N'<SomeTag attr2="data"/>')  
    ,('P3','Joe',N'<SomeTag attr3="data" PersonID="P"><name>PersonName</name></SomeTag>');  
```  
  
 如果执行相同的查询，则 <`xmltext`> 元素中的子元素将作为包含它的 <`Parent`> 元素的子元素添加。  
  
```  
SELECT 1 as Tag, NULL as parent,  
       PersonID as [Parent!1!PersonID],  
       PersonName as [Parent!1!PersonName],  
       Overflow as [Parent!1!!XMLTEXT] -- no AttributeName, XMLTEXT directive  
FROM Person  
FOR XML EXPLICIT;  
```  
  
 结果如下：  
  
 `<Parent PersonID="P1" PersonName="Joe" attr1="data">content</Parent>`  
  
 `<Parent PersonID="P2" PersonName="Joe" attr2="data"></Parent>`  
  
 `<Parent PersonID="P3" PersonName="Joe" attr3="data">`  
  
 `<name>PersonName</name>`  
  
 `</Parent>`  
  
 如果使用 `xmltext` 指令指定了 *AttributeName*，则 <`overflow`> 元素的属性将作为封闭的 <`Parent`> 元素的子元素属性添加。 为 *AttributeName* 指定的名称将成为子元素的名称。  
  
 在此查询中，将 *AttributeName* <`overflow`> 与 `xmltext` 指令一起指定 *：*  
  
```  
SELECT 1 as Tag, NULL as parent,  
       PersonID as [Parent!1!PersonID],  
       PersonName as [Parent!1!PersonName],  
       Overflow as [Parent!1!overflow!XMLTEXT] -- Overflow is AttributeName  
                      -- XMLTEXT is a directive  
FROM Person  
FOR XML EXPLICIT  
```  
  
 结果如下：  
  
 `<Parent PersonID="P1" PersonName="Joe">`  
  
 `<overflow attr1="data">content</overflow>`  
  
 `</Parent>`  
  
 `<Parent PersonID="P2" PersonName="Joe">`  
  
 `<overflow attr2="data" />`  
  
 `</Parent>`  
  
 `<Parent PersonID="P3" PersonName="Joe">`  
  
 `<overflow attr3="data" PersonID="P">`  
  
 `<name>PersonName</name>`  
  
 `</overflow>`  
  
 `</Parent>`  
  
 在此查询元素中，为 *指令一起指定* 属性指定了 `PersonName` 。 这将导致 `PersonName` 作为包含它的 <`Parent`> 元素的子元素添加。 <`xmltext`> 的属性仍将追加到包含它的 <`Parent`> 元素中。 <`overflow`> 元素、子元素的内容将放置到包含它们的 <`Parent`> 元素的其他子元素之前。  
  
```  
SELECT 1      AS Tag, NULL as parent,  
       PersonID   AS [Parent!1!PersonID],  
       PersonName AS [Parent!1!PersonName!element], -- element directive  
       Overflow   AS [Parent!1!!XMLTEXT]  
FROM Person  
FOR XML EXPLICIT;  
```  
  
 结果如下：  
  
 `<Parent PersonID="P1" attr1="data">content<PersonName>Joe</PersonName>`  
  
 `</Parent>`  
  
 `<Parent PersonID="P2" attr2="data">`  
  
 `<PersonName>Joe</PersonName>`  
  
 `</Parent>`  
  
 `<Parent PersonID="P3" attr3="data">`  
  
 `<name>PersonName</name>`  
  
 `<PersonName>Joe</PersonName>`  
  
 `</Parent>`  
  
 如果 `XMLTEXT` 列数据包含根元素的属性，这些属性将不显示在 XML 数据架构中，并且 MSXML 分析器不会验证所得到的 XML 文档片段。 例如：  
  
```  
SELECT 1 AS Tag,  
       0 ASParent,  
       N'<overflow a="1"/>' AS 'overflow!1!!xmltext'  
FOR XML EXPLICIT, xmldata;  
```  
  
 结果如下： 请注意，在返回的架构中缺少溢出属性 `a` ：  
  
 `<Schema name="Schema2"`  
  
 `xmlns="urn:schemas-microsoft-com:xml-data"`  
  
 `xmlns:dt="urn:schemas-microsoft-com:datatypes">`  
  
 `<ElementType name="overflow" content="mixed" model="open">`  
  
 `</ElementType>`  
  
 `</Schema>`  
  
 `<overflow xmlns="x-schema:#Schema2" a="1">`  
  
 `</overflow>`  
  
## <a name="see-also"></a>请参阅  
 [将 EXPLICIT 模式与 FOR XML 一起使用](use-explicit-mode-with-for-xml.md)  
  
  