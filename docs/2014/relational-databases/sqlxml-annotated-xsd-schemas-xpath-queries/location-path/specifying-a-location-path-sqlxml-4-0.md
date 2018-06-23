---
title: 指定的位置路径 (SQLXML 4.0) |Microsoft 文档
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
- absolute location path
- node-set [SQLXML]
- XPath queries [SQLXML], location paths
- relative location path [SQLXML]
- location path for XPath query
ms.assetid: a23a2b75-bc69-49f0-99db-05e14dc15bc0
caps.latest.revision: 23
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 4cade66ce5778440a59ddae209ff515670748f3d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36128729"
---
# <a name="specifying-a-location-path-sqlxml-40"></a>指定位置路径 (SQLXML 4.0)
  XPath 查询以表达式形式指定。 具有各种各样的表达式。 一个位置路径是一个表达式，它选择相对于上下文节点的一组节点。 对位置路径进行求值的结果为节点集。  
  
## <a name="types-of-location-paths"></a>位置路径的类型  
 位置路径可能采用以下任一形式：  
  
-   **绝对位置路径**  
  
     绝对位置路径以文档的根节点为起点。 它包含斜杠标记 (/)，后面可选包括相对位置路径。 斜杠标记 (/) 选择文档的根节点。  
  
-   **相对位置路径**  
  
     相对位置路径以文档中的上下文节点为起点。 位置路径由包含一个或多个位置步骤的序列组成，位置步骤间以斜杠标记 (/) 分隔。 每个步骤选择相对于上下文节点的一组节点。 初始步骤序列选择相对于某个上下文节点的一组节点。 该组节点中的每个节点都用作下一个步骤的上下文节点。 由该步骤表示的节点集将联接起来。 例如， **child::Order/child::OrderDetail**选择 **\<OrderDetail >** 元素的子级**\<顺序 >** 元素上下文节点的子级。  
  
    > [!NOTE]  
    >  在 XPath 的 SQLXML 4.0 实现中，每个 XPath 查询都从根上下文开始，即使 XPath 并非显式绝对路径也不例外。 例如，以“Customer”开始的 XPath 查询被视为“/Customer”。 在 XPath 查询中**客户 [顺序]**，客户开始根上下文中，但顺序开始客户上下文。 有关详细信息，请参阅[使用 XPath 查询简介&#40;SQLXML 4.0&#41;](../introduction-to-using-xpath-queries-sqlxml-4-0.md)。  
  
## <a name="location-steps"></a>位置步骤  
 位置路径（绝对或相对）由位置步骤组成，而位置步骤包含三个部分：  
  
-   **Axis**  
  
     轴指定根据位置步骤和上下文节点选择的节点之间的树关系。 支持 `parent`、`child`、`attribute` 和 `self` 轴。 如果在位置路径中指定 `child` 轴，则由查询选择的所有节点均为上下文节点的子级。 如果指定 `parent` 轴，则所选节点为上下文节点的父节点。 如果指定 `attribute` 轴，则所选节点为上下文节点的属性。  
  
-   **节点测试**  
  
     节点测试指定根据位置步骤选择的节点类型。 每个轴（`child`、`parent`、`attribute` 和 `self`）都具有主要节点类型。 有关`attribute`轴，主体数据库节点类型是**\<属性 >**。 有关`parent`， `child`，和`self`轴，主体数据库节点类型是**\<元素 >**。  
  
     例如，如果指定的位置路径**child::Customer**、 **\<客户 >** 选定元素的上下文节点的子级。 因为`child`轴具有**\<元素 >** 作为其主体数据库节点类型，节点测试，客户，则为 TRUE，如果客户为**\<元素 >** 节点。  
  
-   **选择谓词 （零个或多个）**  
  
     谓词针对轴筛选节点集。 在 XPath 表达式中指定选择谓词类似于在 SELECT 语句中指定 WHERE 子句。 在方括号之间指定谓词。 应用在选择谓词中指定的测试可以筛选由节点测试返回的节点。 对于要筛选的节点集中的每个节点，将使用该节点作为上下文节点并使用节点集中的节点数作为上下文大小来对谓词表达式求值。 如果对于该节点谓词表达式求值为 TRUE，则该节点将包含在结果节点集中。  
  
     位置步骤的语法为轴名称和节点测试（用双冒号 (::) 分隔），后跟零或多个表达式，每个表达式都位于方括号中。 例如，XPath 表达式 （位置路径） **child::Customer [@CustomerID= ALFKI]** 选择所有**\<客户 >** 元素的上下文节点的子级。 然后，在谓词中的测试应用于的节点集，仅返回**\<客户 >** 元素节点具有属性值 ALFKI 其**CustomerID**属性。  
  
## <a name="in-this-section"></a>本节内容  
 [指定轴&#40;SQLXML 4.0&#41;](specifying-an-axis-sqlxml-4-0.md)  
 提供用于指定轴的示例。  
  
 [指定的位置路径中的节点测试&#40;SQLXML 4.0&#41;](specifying-a-node-test-in-the-location-path-sqlxml-4-0.md)  
 提供用于指定节点测试的示例。  
  
 [中的位置路径指定选择谓词&#40;SQLXML 4.0&#41;](specifying-selection-predicates-in-the-location-path-sqlxml-4-0.md)  
 提供用于指定选择谓词的示例。  
  
  