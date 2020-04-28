---
title: 使用 XPath 查询（SQLXML）简介
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- XPath queries [SQLXML], about XPath queries
- W3C XPath specification
- XPath queries [SQLXML], functionality
ms.assetid: 01050a8e-0ccc-4a02-a4eb-b48be5c3f4f3
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f82c330e2d18f05d0f358171a4ffeabc63ac9c3c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "75246585"
---
# <a name="introduction-to-using-xpath-queries-sqlxml-40"></a>XPath 查询使用简介 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  XML Path 语言 (XPath) 查询可以指定作为 URL 的一部分，或在模板内指定。 映射架构决定生成的此片段的结构，值从数据库中进行检索。 从概念上来说，此过程类似于使用 CREATE VIEW 语句创建视图，然后根据视图编写 SQL 查询。  
  
> [!NOTE]  
>  若要了解 SQLXML 4.0 中的 XPath 查询，必须熟悉 XML 视图和相关的概念，如模板和映射架构。 有关详细信息，请参阅[批注的 XSD 架构简介 &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml/annotated-xsd-schemas/introduction-to-annotated-xsd-schemas-sqlxml-4-0.md)和万维网联合会（W3C）定义的 XPath 标准。  
  
 XML 文档由多个节点构成，如元素节点、属性节点、文本节点等。 例如，考虑以下 XML 文档：  
  
```  
<root>  
  <Customer cid= "C1" name="Janine" city="Issaquah">  
      <Order oid="O1" date="1/20/1996" amount="3.5" />  
      <Order oid="O2" date="4/30/1997" amount="13.4">Customer was  
          very satisfied</Order>  
   </Customer>  
   <Customer cid="C2" name="Ursula" city="Oelde" >  
      <Order oid="O3" date="7/14/1999" amount="100" note="Wrap it blue white red">  
          <Urgency>Important</Urgency>  
      </Order>  
      <Order oid="O4" date="1/20/1996" amount="10000"/>  
   </Customer>  
</root>  
```  
  
 在本文档中， ** \<Customer>** 是元素节点， **cid**是属性节点， **"重要"** 是文本节点。  
  
 XPath 是图形导航语言，用于从 XML 文档中选择节点集。 每个 XPath 运算符根据前一个 XPath 运算符所选择的节点集来选择节点集。 例如，给定一组** \<Customer>** 节点，XPath 可以选择**日期**属性值为 **"7/14/1999"** 的所有** \<顺序>** 节点。 生成的节点集包含订单日期为 7/14/1999 的所有订单。  
  
 万维网联盟 (W3C) 将 XPath 语言规定为标准导航语言。 SQLXML 4.0 实现了位于的 W3C XPath 规范的子集http://www.w3.org/TR/1999/PR-xpath-19991008.html。  
  
 以下是 W3C XPath 实现与 SQLXML 4.0 实现之间的主要差异。  
  
-   **根查询**  
  
     SQLXML 4.0 不支持根查询 (/)。 每个 XPath 查询必须在该架构中的顶级** \<ElementType>** 开始。  
  
-   **报告错误**  
  
     W3C XPath 规范定义了无错误条件。 选择任意节点失败的 XPath 查询将返回空节点集。 在 SQLXML 4.0 中，查询可能返回多种类型的错误消息。  
  
-   **文档顺序**  
  
     在 SQLXML 4.0 中，文档顺序并不总是确定的。 因此，不实现使用文档顺序的数值谓词和轴（**如下所示）。**  
  
     缺少文档顺序还表示，只有在节点映射到单行中的单列时，才能计算该节点的字符串值。 包含子元素的元素或 IDREFS 或 NMTOKENS 节点无法转换为字符串。  
  
    > [!NOTE]  
    >  在某些情况下，**关系**注释中的**键字段**批注或键可能会产生确定性的文档顺序。 但是，这并不是这些批注的主要用途。有关详细信息，请参阅[使用 sql：键字段标识键列 &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/identifying-key-columns-using-sql-key-fields-sqlxml-4-0.md)并[使用 sql： relationship &#40;SQLXML 4.0&#41;指定关系](../../relational-databases/sqlxml-annotated-xsd-schemas-using/specifying-relationships-using-sql-relationship-sqlxml-4-0.md)。  
  
-   **数据类型**  
  
     SQLXML 4.0 实现 XPath**字符串**、**数字**和**布尔**数据类型的限制。 有关详细信息，请参阅[&#40;SQLXML 4.0&#41;的 XPath 数据类型](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/xpath-data-types-sqlxml-4-0.md)。  
  
-   **叉积查询**  
  
     SQLXML 4.0 不支持叉积 XPath 查询，如 `Customers[Order/@OrderDate=Order/@ShipDate]`。 此查询用于选择其任意订单的 OrderDate 等于任意订单的 ShipDate 的所有客户。  
  
     不过，SQLXML 4.0 支持诸如 `Customer[Order[@OrderDate=@ShippedDate]]` 的查询，此查询用于选择其任意订单的 OrderDate 等于其 ShipDate 的客户。  
  
-   **错误处理和安全性**  
  
     根据所用架构和 XPath 查询表达式的不同，[!INCLUDE[tsql](../../includes/tsql-md.md)] 错误可以在某些条件下向用户公开。  
  
 以下部分中的表格详细列出了 SQLXML 4.0 中的 XPath 查询实现与 W3C 规范在这些方面的不同之处。  
  
## <a name="supported-functionality"></a>支持的功能  
 下表显示了 SQLXML 4.0 中实现的 XPath 语言功能。  
  
|功能|项|示例查询链接|  
|-------------|----------|----------------------------|  
|Axes|**attribute**、 **child**、 **parent**和**self**轴|[&#40;SQLXML 4.0&#41;在 XPath 查询中指定轴](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/specifying-axes-in-xpath-queries-sqlxml-4-0.md)|  
|包含连续谓词和嵌套谓词的布尔值谓词||[&#40;SQLXML 4.0&#41;在 XPath 查询中指定算术运算符](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/specifying-arithmetic-operators-in-xpath-queries-sqlxml-4-0.md)|  
|所有关系运算符|=、！ =、<、 \<=、>、>=|[&#40;SQLXML 4.0&#41;在 XPath 查询中指定关系运算符](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/specifying-relational-operators-in-xpath-queries-sqlxml-4-0.md)|  
|算术运算符|+、-、*、div|[&#40;SQLXML 4.0&#41;在 XPath 查询中指定算术运算符](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/specifying-arithmetic-operators-in-xpath-queries-sqlxml-4-0.md)|  
|显式转换函数|**number （）**， **string （）**， **Boolean （）**|[&#40;SQLXML 4.0&#41;在 XPath 查询中指定显式转换函数](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/specifying-explicit-conversion-functions-in-xpath-queries-sqlxml-4-0.md)|  
|布尔运算符|AND、OR|[在 &#40;SQLXML 4.0&#41;的 XPath 查询中指定布尔运算符](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/specifying-boolean-operators-in-xpath-queries-sqlxml-4-0.md)|  
|布尔函数|**true （）**、 **false （）**、 **not （）**|[&#40;SQLXML 4.0&#41;在 XPath 查询中指定布尔函数](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/specifying-boolean-functions-in-xpath-queries-sqlxml-4-0.md)|  
|XPath 变量||[在 &#40;SQLXML 4.0&#41;的 XPath 查询中指定 XPath 变量](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/specifying-xpath-variables-in-xpath-queries-sqlxml-4-0.md)|  
  
## <a name="unsupported-functionality"></a>不支持的功能  
 下表显示了 SQLXML 4.0 中未实现的 XPath 语言功能。  
  
|功能|项|  
|-------------|----------|  
|Axes|**祖先**、**祖先或-self**、**子代**、**子代-或-self （//）**，**后面**是**后同辈**、**命名空间**、**前面**和**同级**|  
|数值谓词||  
|算术运算符|mod|  
|节点函数|**祖先**、**祖先或-self**、**子代**、**子代-或-self （//）**，**后面**是**后同辈**、**命名空间**、**前面**和**同级**|  
|字符串函数|**string （）**， **concat （）**，**开头为（）**，**包含（）**，**子字符串-before （）**， **substring （）**， **substring （**），**字符串长度（**），**规范化（）**，**转换（）**|  
|布尔函数|**lang （）**|  
|数值函数|**sum （）**， **floor （）**，**天花板（）**， **round （）**|  
|Union 运算符|&#124;|  
  
 在模板中指定 XPath 查询时，请注意以下行为：  
  
-   XPath 可以包含在 XML 中具有特殊含义的字符，如 < 或 &，模板是 XML 文档）。 必须使用 XML & 编码对这些字符进行转义，或在 URL 中指定 XPath。  
  
## <a name="see-also"></a>另请参阅  
 [在 SQLXML 4.0 中使用 XPath 查询](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/using-xpath-queries-in-sqlxml-4-0.md)  
  
  
