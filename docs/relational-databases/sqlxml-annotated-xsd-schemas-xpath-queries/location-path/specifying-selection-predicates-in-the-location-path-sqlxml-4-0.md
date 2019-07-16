---
title: 位置路径 (SQLXML 4.0) 中指定选择谓词 |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
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
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8f1a42cd31bce6e650fa83cec90d3552b266f0fa
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68073274"
---
# <a name="specifying-selection-predicates-in-the-location-path-sqlxml-40"></a>在位置路径中指定选择谓词 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  谓词筛选与轴有关的节点集（类似于 SELECT 语句中的 WHERE 子句）。 在方括号之间指定谓词。 对于要筛选的节点集中的每个节点，将使用该节点作为上下文节点并使用节点集中的节点数作为上下文大小来对谓词表达式求值。 如果对于该节点谓词表达式求值为 TRUE，则该节点将包含在结果节点集中。  
  
 XPath 还允许基于位置的筛选。 求值结果为数字的谓词表达式选择该序数节点。 例如，位置路径 `Customer[3]` 返回第三个客户。 不支持此类数字谓词。 只支持返回布尔值结果的谓词表达式。  
  
> [!NOTE]  
>  有关此 XPath 实现限制的信息和它与 W3C 规范之间的差异，请参阅[使用 XPath 查询简介&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/introduction-to-using-xpath-queries-sqlxml-4-0.md)。  
  
## <a name="selection-predicate-example-1"></a>选择谓词：示例 1  
 以下 XPath 表达式 （位置路径） 从所有当前上下文节点选择 **\<客户 >** 子元素具有**CustomerID**值 ALFKI 的属性：  
  
```  
/child::Customer[attribute::CustomerID="ALFKI"]  
```  
  
 在此 XPath 查询中，`child` 和 `attribute` 是轴名称。 `Customer` 是节点测试 (如果`Customer`是 **\<元素节点 >** ，这是因为 **\<元素 >** 是的主要节点类型`child`轴)。 `attribute::CustomerID="ALFKI"` 是谓词。 在谓词中，`attribute`是轴和`CustomerID`是节点测试 (如果**CustomerID**是上下文节点的属性，因为 **\<属性 >** 的主体节点类型**特性**轴)。  
  
 使用缩写语法，还可以将该 XPath 查询指定为：  
  
```  
/Customer[@CustomerID="ALFKI"]  
```  
  
## <a name="selection-predicate-example-2"></a>选择谓词：示例 2  
 以下 XPath 表达式 （位置路径） 从所有当前上下文节点选择 **\<顺序 >** 孙级**SalesOrderID**属性具有值 1:  
  
```  
/child::Customer/child::Order[attribute::SalesOrderID="1"]  
```  
  
 在此 XPath 表达式中，`child` 和 `attribute` 是轴名称。 `Customer`、`Order` 和 `SalesOrderID` 是节点测试。 `attribute::OrderID="1"` 是谓词。  
  
 使用缩写语法，还可以将该 XPath 查询指定为：  
  
```  
/Customer/Order[@SalesOrderID="1"]  
```  
  
## <a name="selection-predicate-example-3"></a>选择谓词：示例 3  
 以下 XPath 表达式 （位置路径） 从所有当前上下文节点选择 **\<客户 >** 具有一个或多个子级的 **\<ContactName >** 子级：  
  
```  
child::Customer[child::ContactName]  
```  
  
 此示例假定 **\<ContactName >** 子元素的 **\<客户 >** 元素在 XML 文档中，被称为*元素为中心的映射*在带批注的 XSD 架构。  
  
 在此 XPath 表达式中，`child` 是轴名称。 `Customer` 是节点测试 (如果`Customer`是 **\<元素 >** 节点，因为 **\<元素 >** 是的主要节点类型`child`轴)。 `child::ContactName` 是谓词。 在谓词中，`child`是轴和`ContactName`是节点测试 (如果`ContactName`是 **\<元素 >** 节点)。  
  
 此表达式仅返回 **\<客户 >** 具有的元素子级的上下文节点 **\<ContactName >** 元素子级。  
  
 使用缩写语法，还可以将该 XPath 查询指定为：  
  
```  
Customer[ContactName]  
```  
  
## <a name="selection-predicate-example-4"></a>选择谓词：示例 4  
 以下 XPath 表达式选择 **\<客户 >** 上下文节点不具有元素子级 **\<ContactName >** 元素子级：  
  
```  
child::Customer[not(child::ContactName)]  
```  
  
 此示例假定 **\<ContactName >** 子元素的 **\<客户 >** 中不需要在 XML 文档和联系人姓名字段中的元素数据库。  
  
 在本示例中，`child` 是轴。 `Customer` 是节点测试 (如果`Customer`是\<元素 > 节点)。 `not(child::ContactName)` 是谓词。 在谓词中，`child`是轴和`ContactName`是节点测试 (如果`ContactName`是\<元素 > 节点)。  
  
 使用缩写语法，还可以将该 XPath 查询指定为：  
  
```  
Customer[not(ContactName)]  
```  
  
## <a name="selection-predicate-example-5"></a>选择谓词：示例 5  
 以下 XPath 表达式选择从当前上下文节点所有 **\<客户 >** 具有子级的**CustomerID**属性：  
  
```  
child::Customer[attribute::CustomerID]  
```  
  
 在此示例中，`child`是轴和`Customer`是节点测试 (如果`Customer`是\<元素 > 节点)。 `attribute::CustomerID` 是谓词。 在谓词中，`attribute`是轴和`CustomerID`是谓词 (如果`CustomerID`是 **\<属性 >** 节点)。  
  
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
 [带批注的 XSD 架构简介&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml/annotated-xsd-schemas/introduction-to-annotated-xsd-schemas-sqlxml-4-0.md)   
 [客户端 XML 格式设置&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml/formatting/client-side-xml-formatting-sqlxml-4-0.md)  
  
  
