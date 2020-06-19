---
title: 在位置路径中指定选择谓词（SQLXML 4.0） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- XPath queries [SQLXML], predicates
- predicates [SQLXML]
- position-based filtering [SQLXML]
- XPath queries [SQLXML], location paths
- filtering [SQLXML]
- location path for XPath query
ms.assetid: dbef4cf4-a89b-4d7e-b72b-4062f7b29a80
author: rothja
ms.author: jroth
ms.openlocfilehash: 3ea3f5d7662a4893e45ed10235c3b9114ab55841
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85062941"
---
# <a name="specifying-selection-predicates-in-the-location-path-sqlxml-40"></a>在位置路径中指定选择谓词 (SQLXML 4.0)
  谓词筛选与轴有关的节点集（类似于 SELECT 语句中的 WHERE 子句）。 在方括号之间指定谓词。 对于要筛选的节点集中的每个节点，将使用该节点作为上下文节点并使用节点集中的节点数作为上下文大小来对谓词表达式求值。 如果对于该节点谓词表达式求值为 TRUE，则该节点将包含在结果节点集中。  
  
 XPath 还允许基于位置的筛选。 求值结果为数字的谓词表达式选择该序数节点。 例如，位置路径 `Customer[3]` 返回第三个客户。 不支持此类数字谓词。 只支持返回布尔值结果的谓词表达式。  
  
> [!NOTE]  
>  有关 XPath 的 xpath 实现的限制以及它与 W3C 规范之间的差异的信息，请参阅[&#40;SQLXML 4.0&#41;使用 Xpath 查询简介](../introduction-to-using-xpath-queries-sqlxml-4-0.md)。  
  
## <a name="selection-predicate-example-1"></a>选择谓词：示例1  
 以下 XPath 表达式（位置路径）从当前上下文节点选择 **\<Customer>** 具有**CustomerID**属性值为 ALFKI 的所有元素子级：  
  
```  
/child::Customer[attribute::CustomerID="ALFKI"]  
```  
  
 在此 XPath 查询中，`child` 和 `attribute` 是轴名称。 `Customer`是节点测试（如果是，则为 TRUE `Customer` **\<element node>** ，因为 **\<element>** 是轴的主要节点类型 `child` ）。 `attribute::CustomerID="ALFKI"` 是谓词。 在谓词中， `attribute` 是轴， `CustomerID` 是节点测试（如果**CustomerID**是上下文节点的属性，则为 TRUE，因为 **\<attribute>** 是轴的主要节点类型 `attribute` ）。  
  
 使用缩写语法，还可以将该 XPath 查询指定为：  
  
```  
/Customer[@CustomerID="ALFKI"]  
```  
  
## <a name="selection-predicate-example-2"></a>选择谓词：示例2  
 以下 XPath 表达式（位置路径）从当前上下文节点选择 **\<Order>** 具有值1的**SalesOrderID**属性的所有孙级：  
  
```  
/child::Customer/child::Order[attribute::SalesOrderID="1"]  
```  
  
 在此 XPath 表达式中，`child` 和 `attribute` 是轴名称。 `Customer`、`Order` 和 `SalesOrderID` 是节点测试。 `attribute::OrderID="1"` 是谓词。  
  
 使用缩写语法，还可以将该 XPath 查询指定为：  
  
```  
/Customer/Order[@SalesOrderID="1"]  
```  
  
## <a name="selection-predicate-example-3"></a>选择谓词：示例3  
 以下 XPath 表达式（位置路径）从当前上下文节点选择 **\<Customer>** 具有一个或多个子级的所有子级 **\<ContactName>** ：  
  
```  
child::Customer[child::ContactName]  
```  
  
 此示例假定 **\<ContactName>** 是 **\<Customer>** XML 文档中元素的子元素，该元素在带批注的 XSD 架构中称为以*元素为中心的映射*。  
  
 在此 XPath 表达式中，`child` 是轴名称。 `Customer`是节点测试（如果 `Customer` 是节点，则为 TRUE **\<element>** ，因为 **\<element>** 是轴的主要节点类型 `child` ）。 `child::ContactName` 是谓词。 在谓词中， `child` 是轴， `ContactName` 是节点测试（如果是节点，则为 TRUE `ContactName` **\<element>** ）。  
  
 此表达式仅返回 **\<Customer>** 具有元素子级的上下文节点的子元素 **\<ContactName>** 。  
  
 使用缩写语法，还可以将该 XPath 查询指定为：  
  
```  
Customer[ContactName]  
```  
  
## <a name="selection-predicate-example-4"></a>选择谓词：示例4  
 下面的 XPath 表达式选择 **\<Customer>** 不具有元素子级的上下文节点的子元素 **\<ContactName>** ：  
  
```  
child::Customer[not(child::ContactName)]  
```  
  
 此示例假定 **\<ContactName>** 是 **\<Customer>** XML 文档中元素的子元素，并且数据库中不需要 "联系人姓名" 字段。  
  
 在本示例中，`child` 是轴。 `Customer`节点测试（如果 `Customer` 是节点，则为 TRUE \<element> ）。 `not(child::ContactName)` 是谓词。 在谓词中， `child` 是轴， `ContactName` 是节点测试（如果是节点，则为 TRUE `ContactName` \<element> ）。  
  
 使用缩写语法，还可以将该 XPath 查询指定为：  
  
```  
Customer[not(ContactName)]  
```  
  
## <a name="selection-predicate-example-5"></a>选择谓词：示例5  
 下面的 XPath 表达式从当前上下文节点选择 **\<Customer>** 具有**CustomerID**属性的所有子级：  
  
```  
child::Customer[attribute::CustomerID]  
```  
  
 在此示例中， `child` 是轴， `Customer` 是节点测试（如果是节点，则为 TRUE `Customer` \<element> ）。 `attribute::CustomerID` 是谓词。 在谓词中， `attribute` 是轴， `CustomerID` 是谓词（如果是节点，则为 TRUE `CustomerID` **\<attribute>** ）。  
  
 使用缩写语法，还可以将该 XPath 查询指定为：  
  
```  
Customer[@CustomerID]  
```  
  
## <a name="selection-predicate-example-6"></a>选择谓词：示例 6  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLXML 4.0 可以支持谓词中包含叉积的 XPath 查询，如以下示例中所示：  
  
```  
Customer[Order/@OrderDate=Order/@ShipDate]  
```  
  
 此查询选择具有以下 `Order` 的所有客户：其 `OrderDate` 等于任意 `ShipDate` 的 `Order`。  
  
## <a name="see-also"></a>另请参阅  
 [&#40;SQLXML 4.0&#41;的批注 XSD 架构简介](../../sqlxml/annotated-xsd-schemas/introduction-to-annotated-xsd-schemas-sqlxml-4-0.md)   
 [&#40;SQLXML 4.0&#41;的客户端 XML 格式](../../sqlxml/formatting/client-side-xml-formatting-sqlxml-4-0.md)  
  
  
