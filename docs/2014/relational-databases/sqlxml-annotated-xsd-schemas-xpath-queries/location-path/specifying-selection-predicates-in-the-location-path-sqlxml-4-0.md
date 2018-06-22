---
title: 指定选择谓词中的位置路径 (SQLXML 4.0) |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- XPath queries [SQLXML], predicates
- predicates [SQLXML]
- position-based filtering [SQLXML]
- XPath queries [SQLXML], location paths
- filtering [SQLXML]
- location path for XPath query
ms.assetid: dbef4cf4-a89b-4d7e-b72b-4062f7b29a80
caps.latest.revision: 27
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 80090288026a8b0e2728b1322efe68bea6d960be
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36017279"
---
# <a name="specifying-selection-predicates-in-the-location-path-sqlxml-40"></a>在位置路径中指定选择谓词 (SQLXML 4.0)
  谓词筛选与轴有关的节点集（类似于 SELECT 语句中的 WHERE 子句）。 在方括号之间指定谓词。 对于要筛选的节点集中的每个节点，将使用该节点作为上下文节点并使用节点集中的节点数作为上下文大小来对谓词表达式求值。 如果对于该节点谓词表达式求值为 TRUE，则该节点将包含在结果节点集中。  
  
 XPath 还允许基于位置的筛选。 求值结果为数字的谓词表达式选择该序数节点。 例如，位置路径 `Customer[3]` 返回第三个客户。 不支持此类数字谓词。 只支持返回布尔值结果的谓词表达式。  
  
> [!NOTE]  
>  有关 XPath 的该 XPath 实现的限制信息和与 W3C 规范之间的差异，请参阅[使用 XPath 查询简介&#40;SQLXML 4.0&#41;](../introduction-to-using-xpath-queries-sqlxml-4-0.md)。  
  
## <a name="selection-predicate-example-1"></a>选定谓词： 示例 1  
 下面的 XPath 表达式 （位置路径） 选择从当前上下文节点所有**\<客户 >** 元素子级具有**CustomerID**值为 ALFKI 的属性：  
  
```  
/child::Customer[attribute::CustomerID="ALFKI"]  
```  
  
 在此 XPath 查询中，`child` 和 `attribute` 是轴名称。 `Customer` 是节点的测试 (true`Customer`是**\<元素节点 >**，这是因为**\<元素 >** 是的主体数据库节点类型`child`轴)。 `attribute::CustomerID="ALFKI"` 是谓词。 在谓词中，`attribute`是轴和`CustomerID`是节点的测试 (true **CustomerID**是上下文节点的属性，因为**\<属性 >** 的主体节点类型`attribute`轴)。  
  
 使用缩写语法，还可以将该 XPath 查询指定为：  
  
```  
/Customer[@CustomerID="ALFKI"]  
```  
  
## <a name="selection-predicate-example-2"></a>选定谓词： 示例 2  
 下面的 XPath 表达式 （位置路径） 选择从当前上下文节点所有**\<顺序 >** 孙级具有**SalesOrderID**具有值 1 属性：  
  
```  
/child::Customer/child::Order[attribute::SalesOrderID="1"]  
```  
  
 在此 XPath 表达式中，`child` 和 `attribute` 是轴名称。 `Customer`、`Order` 和 `SalesOrderID` 是节点测试。 `attribute::OrderID="1"` 是谓词。  
  
 使用缩写语法，还可以将该 XPath 查询指定为：  
  
```  
/Customer/Order[@SalesOrderID="1"]  
```  
  
## <a name="selection-predicate-example-3"></a>选定谓词： 示例 3  
 下面的 XPath 表达式 （位置路径） 选择从当前上下文节点所有**\<客户 >** 包含一个或多个子级 **\<ContactName >** 子级：  
  
```  
child::Customer[child::ContactName]  
```  
  
 此示例假定 **\<ContactName >** 是的子元素**\<客户 >** 元素在 XML 文档中，称为*元素为中心的映射*带批注的 XSD 架构中。  
  
 在此 XPath 表达式中，`child` 是轴名称。 `Customer` 是节点的测试 (true`Customer`是**\<元素 >** 节点，因为**\<元素 >** 是的主体数据库节点类型`child`轴)。 `child::ContactName` 是谓词。 在谓词中，`child`是轴和`ContactName`是节点的测试 (true`ContactName`是**\<元素 >** 节点)。  
  
 此表达式仅返回**\<客户 >** 的上下文节点的具有元素子级，  **\<ContactName >** 元素子级。  
  
 使用缩写语法，还可以将该 XPath 查询指定为：  
  
```  
Customer[ContactName]  
```  
  
## <a name="selection-predicate-example-4"></a>选定谓词： 示例 4  
 下面的 XPath 表达式选择**\<客户 >** 的上下文节点的元素子级，而没有 **\<ContactName >** 元素子级：  
  
```  
child::Customer[not(child::ContactName)]  
```  
  
 此示例假定 **\<ContactName >** 是的子元素**\<客户 >** 中不需要在 XML 文档中和联系人姓名字段中的元素数据库。  
  
 在本示例中，`child` 是轴。 `Customer` 是节点的测试 (true`Customer`是\<元素 > 节点)。 `not(child::ContactName)` 是谓词。 在谓词中，`child`是轴和`ContactName`是节点的测试 (true`ContactName`是\<元素 > 节点)。  
  
 使用缩写语法，还可以将该 XPath 查询指定为：  
  
```  
Customer[not(ContactName)]  
```  
  
## <a name="selection-predicate-example-5"></a>选定谓词： 示例 5  
 下面的 XPath 表达式选择从当前上下文节点所有**\<客户 >** 具有的子级**CustomerID**属性：  
  
```  
child::Customer[attribute::CustomerID]  
```  
  
 在此示例中，`child`是轴和`Customer`是节点测试 (true`Customer`是\<元素 > 节点)。 `attribute::CustomerID` 是谓词。 在谓词中，`attribute`是轴和`CustomerID`是谓词 (true`CustomerID`是**\<属性 >** 节点)。  
  
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
  
## <a name="see-also"></a>请参阅  
 [批注的 XSD 架构简介&#40;SQLXML 4.0&#41;](../../sqlxml/annotated-xsd-schemas/introduction-to-annotated-xsd-schemas-sqlxml-4-0.md)   
 [客户端的 XML 格式&#40;SQLXML 4.0&#41;](../../sqlxml/formatting/client-side-xml-formatting-sqlxml-4-0.md)  
  
  