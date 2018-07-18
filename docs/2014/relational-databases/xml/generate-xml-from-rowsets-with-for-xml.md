---
title: 使用 FOR XML 从行集生成 XML | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- FOR XML clause, generating XML from rowsets
ms.assetid: d061c0f1-3de9-4ad1-bbca-ce45d064b6c8
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 75446ba8c61f03c46c4000793d7ca75f1dc8cb85
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37201107"
---
# <a name="generate-xml-from-rowsets-with-for-xml"></a>使用 FOR XML 从行集生成 XML
  您可以生成`xml`通过使用带有新的 FOR XML 行集的数据类型实例**类型**指令。  
  
 可以将结果赋给`xml`数据类型列、 变量或参数。 同样，可以嵌套 FOR XML 以生成任意层次结构。 这使嵌套的 FOR XML 在编写上比 FOR XML EXPLICIT 更为方便，但是对于深层次的结构，它的执行效果不如后者。 FOR XML 还引入了新的 PATH 模式。 这个新模式指定某个列的值在 XML 树中的路径。  
  
 可以使用新的 **FOR XML TYPE** 指令，采用 SQL 语法来定义关系数据上的只读 XML 视图。 可以使用 SQL 语句和嵌入式 XQuery 查询该视图，如下面的示例所示。 另外，您还可以在存储过程中引用这些 SQL 视图。  
  
## <a name="example-sql-view-returning-generated-xml-data-type"></a>示例：返回生成的 xml 数据类型的 SQL 视图  
 以下 SQL 视图定义对关系列 pk 和从 XML 列中检索到的书作者创建 XML 视图：  
  
```  
CREATE VIEW V (xmlVal) AS  
SELECT pk, xCol.query('/book/author')  
FROM   T  
FOR XML AUTO, TYPE  
```  
  
 V 视图只包含 XML 类型的单个行与单一 columnxmlVal`.`其能够与普通查询`xml`数据类型实例。 例如，下面的查询返回名字为“David”的作者：  
  
```  
SELECT xmlVal.query('//author[first-name = "David"]')  
FROM   V  
```  
  
 SQL 视图定义与使用带批注的架构创建的 XML 视图有些相似。 但二者之间存在重要的差异。 SQL 视图定义是只读的，且必须使用嵌入式 XQuery 来操作。 XML 视图是通过使用带批注的架构创建的。 此外，SQL 视图在应用 XQuery 表达式之前具体化 XML 结果，而对 XML 视图的 XPath 查询是对基础表计算 SQL 查询。  
  
## <a name="see-also"></a>请参阅  
 [FOR XML (SQL Server)](for-xml-sql-server.md)  
  
  
