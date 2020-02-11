---
title: 在位置路径中设置选择谓词（SQLXML）
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
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 84a3eade8a706e95b3ddba72d96e37d8fabf1fd3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "75256001"
---
# <a name="specifying-selection-predicates-in-the-location-path-sqlxml-40"></a>在位置路径中指定选择谓词 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  谓词筛选与轴有关的节点集（类似于 SELECT 语句中的 WHERE 子句）。 在方括号之间指定谓词。 对于要筛选的节点集中的每个节点，将使用该节点作为上下文节点并使用节点集中的节点数作为上下文大小来对谓词表达式求值。 如果对于该节点谓词表达式求值为 TRUE，则该节点将包含在结果节点集中。  
  
 XPath 还允许基于位置的筛选。 求值结果为数字的谓词表达式选择该序数节点。 例如，位置路径 `Customer[3]` 返回第三个客户。 不支持此类数字谓词。 只支持返回布尔值结果的谓词表达式。  
  
> [!NOTE]  
>  有关 XPath 的 xpath 实现的限制以及它与 W3C 规范之间的差异的信息，请参阅[&#40;SQLXML 4.0&#41;使用 Xpath 查询简介](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/introduction-to-using-xpath-queries-sqlxml-4-0.md)。  
  
## <a name="selection-predicate-example-1"></a>选择谓词：示例1  
 以下 XPath 表达式（位置路径）从当前上下文节点中选择所有** \<Customer>** 元素子级，其**CustomerID**属性值为 ALFKI：  
  
```  
/child::Customer[attribute::CustomerID="ALFKI"]  
```  
  
 在此 XPath 查询中，`child` 和 `attribute` 是轴名称。 `Customer``Customer`是节点测试（如果是** \<元素节点>**，则为 TRUE，因为** \<元素>** 是`child`轴的主要节点类型）。 
  `attribute::CustomerID="ALFKI"` 是谓词。 在谓词中， `attribute` `CustomerID`是轴，是节点测试（如果**CustomerID**是上下文节点的属性，则为 TRUE，因为** \<属性>** 是**属性**轴的主要节点类型）。  
  
 使用缩写语法，还可以将该 XPath 查询指定为：  
  
```  
/Customer[@CustomerID="ALFKI"]  
```  
  
## <a name="selection-predicate-example-2"></a>选择谓词：示例2  
 以下 XPath 表达式（位置路径）从当前上下文节点选择具有值1的孙级的**SalesOrderID**属性的所有** \<订单>** ：  
  
```  
/child::Customer/child::Order[attribute::SalesOrderID="1"]  
```  
  
 在此 XPath 表达式中，`child` 和 `attribute` 是轴名称。 
  `Customer`、`Order` 和 `SalesOrderID` 是节点测试。 
  `attribute::OrderID="1"` 是谓词。  
  
 使用缩写语法，还可以将该 XPath 查询指定为：  
  
```  
/Customer/Order[@SalesOrderID="1"]  
```  
  
## <a name="selection-predicate-example-3"></a>选择谓词：示例3  
 以下 XPath 表达式（位置路径）从当前上下文节点选择所有** \<客户>** 具有一个或多个** \<联系人姓名>** 儿童的孩子：  
  
```  
child::Customer[child::ContactName]  
```  
  
 此示例假设 " ** \<联系人姓名">** 是 XML 文档中** \<Customer>** 元素的子元素，在带批注的 XSD 架构中称为以*元素为中心的映射*。  
  
 在此 XPath 表达式中，`child` 是轴名称。 `Customer``Customer`是节点测试（如果是** \<元素>** 节点，则为 TRUE，因为** \<元素>** 是`child`轴的主要节点类型）。 
  `child::ContactName` 是谓词。 在谓词中， `child`是轴， `ContactName`是节点测试（如果`ContactName`是** \<元素>** "节点），则为 TRUE。  
  
 此表达式仅返回具有** \<"联系人">** 元素子级的上下文节点的** \<Customer>** 元素子级。  
  
 使用缩写语法，还可以将该 XPath 查询指定为：  
  
```  
Customer[ContactName]  
```  
  
## <a name="selection-predicate-example-4"></a>选择谓词：示例4  
 下面的 XPath 表达式选择** \<** 不具有** \<"联系人">** 元素子级的上下文节点的 Customer>元素子级：  
  
```  
child::Customer[not(child::ContactName)]  
```  
  
 此示例假设 " ** \<联系人姓名">** 是 XML 文档中** \<Customer>** 元素的子元素，并且数据库中不需要 "联系人姓名" 字段。  
  
 在本示例中，`child` 是轴。 `Customer`是节点测试（如果`Customer`是\<元素> 节点），则为 TRUE。 
  `not(child::ContactName)` 是谓词。 在谓词中， `child`是轴， `ContactName`是节点测试（如果`ContactName`是\<元素> "节点），则为 TRUE。  
  
 使用缩写语法，还可以将该 XPath 查询指定为：  
  
```  
Customer[not(ContactName)]  
```  
  
## <a name="selection-predicate-example-5"></a>选择谓词：示例5  
 以下 XPath 表达式从当前上下文节点选择具有**CustomerID**属性的所有** \<客户>** 子项：  
  
```  
child::Customer[attribute::CustomerID]  
```  
  
 在此示例中`child` ，是轴， `Customer`是节点测试（如果`Customer`是> 节点\<的元素，则为 TRUE）。 
  `attribute::CustomerID` 是谓词。 在谓词中， `attribute`是轴， `CustomerID`是谓词（如果`CustomerID`是>节点的** \<属性**，则为 TRUE）。  
  
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
 [&#40;SQLXML 4.0&#41;的批注 XSD 架构简介](../../../relational-databases/sqlxml/annotated-xsd-schemas/introduction-to-annotated-xsd-schemas-sqlxml-4-0.md)   
 [&#40;SQLXML 4.0&#41;的客户端 XML 格式](../../../relational-databases/sqlxml/formatting/client-side-xml-formatting-sqlxml-4-0.md)  
  
  
