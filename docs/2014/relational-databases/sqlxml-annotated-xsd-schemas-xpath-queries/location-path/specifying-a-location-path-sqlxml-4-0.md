---
title: 指定位置路径（SQLXML 4.0） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- absolute location path
- node-set [SQLXML]
- XPath queries [SQLXML], location paths
- relative location path [SQLXML]
- location path for XPath query
ms.assetid: a23a2b75-bc69-49f0-99db-05e14dc15bc0
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: d769bbb8c1d3890f80c89c32e7ddfc913dd517a8
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/01/2020
ms.locfileid: "82703115"
---
# <a name="specifying-a-location-path-sqlxml-40"></a>指定位置路径 (SQLXML 4.0)
  XPath 查询以表达式形式指定。 具有各种各样的表达式。 一个位置路径是一个表达式，它选择相对于上下文节点的一组节点。 对位置路径进行求值的结果为节点集。  
  
## <a name="types-of-location-paths"></a>位置路径的类型  
 位置路径可能采用以下任一形式：  
  
-   **绝对位置路径**  
  
     绝对位置路径以文档的根节点为起点。 它包含斜杠标记 (/)，后面可选包括相对位置路径。 斜杠标记 (/) 选择文档的根节点。  
  
-   **相对位置路径**  
  
     相对位置路径以文档中的上下文节点为起点。 位置路径由包含一个或多个位置步骤的序列组成，位置步骤间以斜杠标记 (/) 分隔。 每个步骤选择相对于上下文节点的一组节点。 初始步骤序列选择相对于某个上下文节点的一组节点。 该组节点中的每个节点都用作下一个步骤的上下文节点。 由该步骤表示的节点集将联接起来。 例如， **child：： Order/child：： OrderDetail**选择上下文节点的** \< Order>** 元素子级的 Order ** \<>** 元素子级。  
  
    > [!NOTE]  
    >  在 XPath 的 SQLXML 4.0 实现中，每个 XPath 查询都从根上下文开始，即使 XPath 并非显式绝对路径也不例外。 例如，以“Customer”开始的 XPath 查询被视为“/Customer”。 在 XPath 查询**customer [订单]** 中，客户从根上下文开始，但从客户上下文开始排序。 有关详细信息，请参阅[&#40;SQLXML 4.0&#41;使用 XPath 查询简介](../introduction-to-using-xpath-queries-sqlxml-4-0.md)。  
  
## <a name="location-steps"></a>位置步骤  
 位置路径（绝对或相对）由位置步骤组成，而位置步骤包含三个部分：  
  
-   **轴**  
  
     轴指定根据位置步骤和上下文节点选择的节点之间的树关系。 支持 `parent`、`child`、`attribute` 和 `self` 轴。 如果在位置路径中指定 `child` 轴，则由查询选择的所有节点均为上下文节点的子级。 如果指定 `parent` 轴，则所选节点为上下文节点的父节点。 如果指定 `attribute` 轴，则所选节点为上下文节点的属性。  
  
-   **节点测试**  
  
     节点测试指定根据位置步骤选择的节点类型。 每个轴（`child`、`parent`、`attribute` 和 `self`）都具有主要节点类型。 对于 `attribute` 轴，主体节点类型为** \< attribute>**。 对于 `parent` 、 `child` 和 `self` 轴，主体节点类型为** \< 元素>**。  
  
     例如，如果 location 路径指定了**child：： customer**，则会选择该上下文节点的** \< Customer>** 元素子级。 由于 `child` 轴的** \< 元素>** 为其主体节点类型，因此，如果 Customer 是>节点的** \< 元素**，则节点测试，Customer 为 TRUE。  
  
-   **选择谓词（零个或多个）**  
  
     谓词针对轴筛选节点集。 在 XPath 表达式中指定选择谓词类似于在 SELECT 语句中指定 WHERE 子句。 在方括号之间指定谓词。 应用在选择谓词中指定的测试可以筛选由节点测试返回的节点。 对于要筛选的节点集中的每个节点，将使用该节点作为上下文节点并使用节点集中的节点数作为上下文大小来对谓词表达式求值。 如果对于该节点谓词表达式求值为 TRUE，则该节点将包含在结果节点集中。  
  
     位置步骤的语法为轴名称和节点测试（用双冒号 (::) 分隔），后跟零或多个表达式，每个表达式都位于方括号中。 例如，XPath 表达式（位置路径） **child：： Customer [ @CustomerID = ' ALFKI ']** 选择上下文节点的所有** \< Customer>** 元素子级。 然后，谓词中的测试应用于节点集，该节点集仅返回** \< 客户>** 元素节点的属性值为 "ALFKI" 的**CustomerID**属性。  
  
## <a name="in-this-section"></a>本节内容  
 [&#40;SQLXML 4.0&#41;指定轴](specifying-an-axis-sqlxml-4-0.md)  
 提供用于指定轴的示例。  
  
 [在位置路径中指定节点测试 &#40;SQLXML 4.0&#41;](specifying-a-node-test-in-the-location-path-sqlxml-4-0.md)  
 提供用于指定节点测试的示例。  
  
 [在位置路径中指定选择谓词 &#40;SQLXML 4.0&#41;](specifying-selection-predicates-in-the-location-path-sqlxml-4-0.md)  
 提供用于指定选择谓词的示例。  
  
  
