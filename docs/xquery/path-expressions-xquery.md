---
title: 路径表达式 (XQuery) |Microsoft 文档
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: sql
ms.component: xquery
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
dev_langs:
- XML
helpviewer_keywords:
- axis step [XQuery]
- path expressions [XQuery]
- expressions [XQuery], path
ms.assetid: b93fa36c-bf69-46b9-b137-f597d66fd0c0
caps.latest.revision: 27
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: b964a11fe7e726abf1e5342641171aa11f583cb7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "33077774"
---
# <a name="path-expressions-xquery"></a>路径表达式 (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  XQuery 路径表达式用于定位文档中的节点，如元素节点、属性节点和文本节点。 路径表达式的结果始终以文档顺序显示，结果序列中不会出现重复的节点。 指定路径时，可以使用全文拼写的语法，也可以使用缩写语法。 以下信息主要介绍了全文拼写的语法。 缩写语法将在本主题的后面进行介绍。  
  
> [!NOTE]  
>  因为针对指定的本主题中的示例查询**xml**类型列， **CatalogDescription**和**说明**中**ProductModel**表，你应该熟悉的内容和存储这些列中的 XML 文档的结构。  
  
 路径表达式可以是相对的，也可以是绝对的。 这两种表达式的说明如下：  
  
-   相对路径表达式由一个或多个步骤组成，步骤间以单斜杠或双斜杠（/ 或 //）分隔。 例如，`child::Features` 是相对路径表达式，其中 `Child` 仅指上下文节点的子节点， 即当前正在处理的节点。 表达式将检索\<功能 > 元素节点的上下文节点的子级。  
  
-   绝对路径表达式以单斜杠或双斜杠（/ 或 //）开头，后面跟有可选的相对路径。 例如，表达式 `/child::ProductDescription` 中的起始斜杠表示它是一个绝对路径表达式。 因为斜杠标记表达式的开头返回的上下文节点的文档根节点，该表达式将返回所有\<ProductDescription > 元素的文档根节点子级。  
  
     如果绝对路径以单斜杠开头，则它后面未必跟有相对路径。 如果仅指定单斜杠，则表达式将返回上下文节点的根节点。 对于 XML 数据类型，根节点为其文档节点。  
  
 典型路径表达式由几个步骤组成。 例如，绝对路径表达式， `/child::ProductDescription/child::Summary`，包含由斜杠分隔的两个步骤。  
  
-   第一步检索\<ProductDescription > 元素的文档根节点子级。  
  
-   第二步检索\<摘要 > 检索每个元素节点子级\<ProductDescription > 元素节点，后者反过来变成上下文节点。  
  
 路径表达式中的步骤可以是轴步骤，也可以是一般步骤。  
  
## <a name="axis-step"></a>轴步骤  
 路径表达式中的轴步骤分为下列几个部分。  
  
 [轴](../xquery/path-expressions-specifying-axis.md)  
 定义移动的方向。 路径表达式中的轴步骤从上下文节点开始，导航到在轴指定的方向上可访问的那些节点。  
  
 [节点测试](../xquery/path-expressions-specifying-node-test.md)  
 指定要选择的节点类型或节点名称。  
  
 零个或多个可选谓词  
 通过选择一些节点和放弃其他节点来筛选节点。  
  
 下面的示例使用**axisstep**路径表达式中：  
  
-   绝对路径表达式 `/child::ProductDescription` 只包含一个步骤。 它指定了一个轴 (`child`) 和一个节点测试 (`ProductDescription`)。  
  
-   相对路径表达式 `child::ProductDescription/child::Features` 包含两个步骤，步骤间以单斜杠分隔。 两个步骤指定了一个轴 child。 ProductDescription 和 Features 为节点测试。  
  
-   相对路径表达式， `child::root/child::Location[attribute::LocationID=10]`，包含由斜杠分隔的两个步骤。 第一步指定了一个轴 (`child`) 和一个节点测试 (`root`)。 第二步指定了轴步骤的所有三个组件：轴 (child)、节点测试 (`Location`) 和谓词 (`[attribute::LocationID=10]`)。  
  
 有关组件轴步骤的详细信息，请参阅[在路径表达式步骤中指定的轴](../xquery/path-expressions-specifying-axis.md)，[在路径表达式步骤中指定节点测试](../xquery/path-expressions-specifying-node-test.md)，和[指定谓词中路径表达式步骤](../xquery/path-expressions-specifying-predicates.md)。  
  
## <a name="general-step"></a>一般步骤  
 一般步骤是一个必须为节点序列的表达式。  
  
 SQL Server 中的 XQuery 实现支持一般步骤作为路径表达式中的第一步。 下面是使用一般步骤的路径表达式的示例。  
  
```  
(/a, /b)/c  
id(/a/b)  
```  
  
 Id 函数，请参阅有关详细信息[id 函数&#40;XQuery&#41;](../xquery/functions-on-sequences-id.md)。  
  
## <a name="in-this-section"></a>本節內容  
 [在路径表达式步骤中指定轴](../xquery/path-expressions-specifying-axis.md)  
 说明如何使用路径表达式中的轴步骤。  
  
 [在路径表达式步骤中指定节点测试](../xquery/path-expressions-specifying-node-test.md)  
 说明如何使用路径表达式中的节点测试。  
  
 [在路径表达式步骤中指定的谓词](../xquery/path-expressions-specifying-predicates.md)  
 说明如何使用路径表达式中的谓词。  
  
 [在路径表达式中使用缩写的语法](../xquery/path-expressions-using-abbreviated-syntax.md)  
 说明如何使用路径表达式中的缩写语法。  
  
  
