---
title: "函数 （MDX 语法） |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- kbMDX
helpviewer_keywords:
- MDX [Analysis Services], functions
- Multidimensional Expressions [Analysis Services], functions
- functions [MDX]
ms.assetid: 74ca5e79-1f33-4795-9d68-98eff9c190c1
caps.latest.revision: 25
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 414a3048ec4fead73ed406914d2ee042778ee2cd
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="functions-mdx-syntax"></a>函数（MDX 语法）
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  多维表达式 (MDX) 中有几类用于执行特定操作的内部函数。 下表列出了 MDX 中可用的函数类别。  
  
> [!NOTE]  
>  有关各个函数的详细信息，请参阅[MDX 函数引用 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md).  
  
|函数类别|Description|  
|-----------------------|-----------------|  
|数组函数|提供存储过程中使用的数组。<br /><br /> 有关详细信息，请参阅[使用存储过程 &#40;MDX &#41;](../mdx/using-stored-procedures-mdx.md).|  
|维度函数|从层次结构、级别或成员返回对维度的引用。<br /><br /> 有关详细信息，请参阅[使用维度、 层次结构和级别函数](../mdx/using-dimension-hierarchy-and-level-functions.md)。|  
|层次结构函数|从级别或成员返回对层次结构的引用。<br /><br /> 有关详细信息，请参阅[使用维度、 层次结构和级别函数](../mdx/using-dimension-hierarchy-and-level-functions.md)。|  
|级别函数|从成员、维度、层次结构或字符串表达式返回对级别的引用。<br /><br /> 有关详细信息，请参阅[使用维度、 层次结构和级别函数](../mdx/using-dimension-hierarchy-and-level-functions.md)。|  
|逻辑函数|对对象和表达式执行逻辑操作和比较。<br /><br /> 有关详细信息，请参阅[使用逻辑函数](../mdx/using-logical-functions.md)。|  
|成员函数|从其他对象或从字符串表达式返回对成员的引用。<br /><br /> 有关详细信息，请参阅[使用成员函数](../mdx/using-member-functions.md)。|  
|数字函数|对对象和表达式执行数学函数和统计函数。<br /><br /> 有关详细信息，请参阅[使用数学函数](../mdx/using-mathematical-functions.md)。|  
|Set 函数|从其他对象或从字符串表达式返回对集的引用。<br /><br /> 有关详细信息，请参阅[使用 Set 函数](../mdx/using-set-functions.md)。|  
|字符串函数|从其他对象或从服务器返回字符串值。<br /><br /> 有关详细信息，请参阅[使用字符串函数](../mdx/using-string-functions.md)。|  
|元组函数|从集或从字符串表达式返回对元组的引用。<br /><br /> 有关详细信息，请参阅“使用元组函数”。|  
  
## <a name="uses-of-functions"></a>函数的使用  
 函数可用于或包含在任何 MDX 表达式中。 函数还可以嵌套（在一个函数内使用另一个函数）。  
  
## <a name="see-also"></a>另請參閱  
 [MDX 语法元素 &#40;MDX &#41;](../mdx/mdx-syntax-elements-mdx.md)  
  
  

