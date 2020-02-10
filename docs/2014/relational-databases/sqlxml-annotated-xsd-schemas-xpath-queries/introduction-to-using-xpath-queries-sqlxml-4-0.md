---
title: XPath 查询使用简介（SQLXML 4.0） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: 4ada9351eca0b068838b38e59c8e0833d5a9af61
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66012713"
---
# <a name="introduction-to-using-xpath-queries-sqlxml-40"></a>XPath 查询使用简介 (SQLXML 4.0)
  XML Path 语言 (XPath) 查询可以指定作为 URL 的一部分，或在模板内指定。 映射架构决定生成的此片段的结构，值从数据库中进行检索。 从概念上来说，此过程类似于使用 CREATE VIEW 语句创建视图，然后根据视图编写 SQL 查询。  
  
> [!NOTE]  
>  若要了解 SQLXML 4.0 中的 XPath 查询，必须熟悉 XML 视图和相关的概念，如模板和映射架构。 有关详细信息，请参阅[批注的 XSD 架构简介 &#40;SQLXML 4.0&#41;](../sqlxml/annotated-xsd-schemas/introduction-to-annotated-xsd-schemas-sqlxml-4-0.md)和万维网联合会（W3C）定义的 XPath 标准。  
  
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
  
     在 SQLXML 4.0 中，文档顺序并不总是确定的。 因此，无法实现使用文档顺序（如 `following`）的数值谓词和轴。  
  
     缺少文档顺序还表示，只有在节点映射到单行中的单列时，才能计算该节点的字符串值。 包含子元素的元素或 IDREFS 或 NMTOKENS 节点无法转换为字符串。  
  
    > [!NOTE]  
    >  在某些情况下，`key-fields` 批注或 `relationship` 批注中的关键字可以生成确定的文档顺序。 但是，这并不是这些批注的主要用途。有关详细信息，请参阅[使用 sql：键字段标识键列 &#40;SQLXML 4.0&#41;](../sqlxml-annotated-xsd-schemas-using/identifying-key-columns-using-sql-key-fields-sqlxml-4-0.md)并[使用 sql： relationship &#40;SQLXML 4.0&#41;指定关系](../sqlxml-annotated-xsd-schemas-using/specifying-relationships-using-sql-relationship-sqlxml-4-0.md)。  
  
-   **数据类型**  
  
     SQLXML 4.0 在实现 XPath `string`、`number` 和 `boolean` 数据类型时存在局限性。 有关详细信息，请参阅[&#40;SQLXML 4.0&#41;的 XPath 数据类型](xpath-data-types-sqlxml-4-0.md)。  
  
-   **叉积查询**  
  
     SQLXML 4.0 不支持叉积 XPath 查询，如 `Customers[Order/@OrderDate=Order/@ShipDate]`。 此查询用于选择其任意订单的 OrderDate 等于任意订单的 ShipDate 的所有客户。  
  
     不过，SQLXML 4.0 支持诸如 `Customer[Order[@OrderDate=@ShippedDate]]` 的查询，此查询用于选择其任意订单的 OrderDate 等于其 ShipDate 的客户。  
  
-   **错误处理和安全性**  
  
     根据所用架构和 XPath 查询表达式的不同，[!INCLUDE[tsql](../../includes/tsql-md.md)] 错误可以在某些条件下向用户公开。  
  
 以下部分中的表格详细列出了 SQLXML 4.0 中的 XPath 查询实现与 W3C 规范在这些方面的不同之处。  
  
## <a name="supported-functionality"></a>支持的功能  
 下表显示了 SQLXML 4.0 中实现的 XPath 语言功能。  
  
|Feature|Item|示例查询链接|  
|-------------|----------|----------------------------|  
|Axes|
  `attribute`、`child`、`parent` 和 `self` 轴|[&#40;SQLXML 4.0&#41;在 XPath 查询中指定轴](samples/specifying-axes-in-xpath-queries-sqlxml-4-0.md)|  
|包含连续谓词和嵌套谓词的布尔值谓词||[&#40;SQLXML 4.0&#41;在 XPath 查询中指定算术运算符](samples/specifying-arithmetic-operators-in-xpath-queries-sqlxml-4-0.md)|  
|所有关系运算符|=、！ =、<、 \<=、>、>=|[&#40;SQLXML 4.0&#41;在 XPath 查询中指定关系运算符](samples/specifying-relational-operators-in-xpath-queries-sqlxml-4-0.md)|  
|算术运算符|+、-、*、div|[&#40;SQLXML 4.0&#41;在 XPath 查询中指定算术运算符](samples/specifying-arithmetic-operators-in-xpath-queries-sqlxml-4-0.md)|  
|显式转换函数|`number()`, `string()`, `Boolean()`|[&#40;SQLXML 4.0&#41;在 XPath 查询中指定显式转换函数](samples/specifying-explicit-conversion-functions-in-xpath-queries-sqlxml-4-0.md)|  
|布尔运算符|AND、OR|[在 &#40;SQLXML 4.0&#41;的 XPath 查询中指定布尔运算符](samples/specifying-boolean-operators-in-xpath-queries-sqlxml-4-0.md)|  
|布尔函数|`true()`, `false()`, `not()`|[&#40;SQLXML 4.0&#41;在 XPath 查询中指定布尔函数](samples/specifying-boolean-functions-in-xpath-queries-sqlxml-4-0.md)|  
|XPath 变量||[在 &#40;SQLXML 4.0&#41;的 XPath 查询中指定 XPath 变量](samples/specifying-xpath-variables-in-xpath-queries-sqlxml-4-0.md)|  
  
## <a name="unsupported-functionality"></a>不支持的功能  
 下表显示了 SQLXML 4.0 中未实现的 XPath 语言功能。  
  
|Feature|Item|  
|-------------|----------|  
|Axes|`ancestor`, `ancestor-or-self`, `descendant`, `descendant-or-self (//)`, `following`, `following-sibling`, `namespace`, `preceding`, `preceding-sibling`|  
|数值谓词||  
|算术运算符|mod|  
|节点函数|`ancestor`, `ancestor-or-self`, `descendant`, `descendant-or-self (//)`, `following`, `following-sibling`, `namespace`, `preceding`, `preceding-sibling`|  
|字符串函数|`string()`, `concat()`, `starts-with()`, `contains()`, `substring-before()`, `substring-after()`, `substring()`, `string-length()`, `normalize()`, `translate()`|  
|布尔函数|`lang()`|  
|数值函数|`sum()`, `floor()`, `ceiling()`, `round()`|  
|Union 运算符|&#124;|  
  
 在模板中指定 XPath 查询时，请注意以下行为：  
  
-   XPath 可以包含在 XML 中具有特殊含义的字符，如 < 或 &，模板是 XML 文档）。 必须使用 XML & 编码对这些字符进行转义，或在 URL 中指定 XPath。  
  
## <a name="see-also"></a>另请参阅  
 [在 SQLXML 4.0 中使用 XPath 查询](using-xpath-queries-in-sqlxml-4-0.md)  
  
  
