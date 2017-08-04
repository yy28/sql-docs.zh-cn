---
title: "使用维度、 层次结构和级别函数 |Microsoft 文档"
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
- dimensions [Analysis Services], functions
- level functions [MDX]
- hierarchy functions [MDX]
ms.assetid: e730f65a-1798-4094-9acf-2739e2505d52
caps.latest.revision: 25
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 10996fe3bec61356308a59ef78e52ecfeacca95a
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="using-dimension-hierarchy-and-level-functions"></a>使用维度函数、层次结构函数和级别函数
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  维度函数、层次结构函数和级别函数对遍历 Analysis Services 中的多维结构非常有用。 通常将此类函数和其他函数一起使用，以获得有关维度、层次结构或级别的成员信息。  
  
 下面的示例演示如何使用**。维度**， **。层次结构**，和**。级别**函数：  
  
 `WITH`  
  
 `MEMBER MEASURES.DIMENSIONNAME AS [Date].[Calendar].CURRENTMEMBER.DIMENSION.NAME`  
  
 `MEMBER MEASURES.HIERARCHYNAME AS [Date].[Calendar].CURRENTMEMBER.HIERARCHY.NAME`  
  
 `MEMBER MEASURES.LEVELNAME AS [Date].[Calendar].LEVEL.NAME`  
  
 `SELECT`  
  
 `{MEASURES.DIMENSIONNAME, MEASURES.HIERARCHYNAME, MEASURES.LEVELNAME}`  
  
 `ON Columns,`  
  
 `[Date].[Calendar].MEMBERS`  
  
 `ON Rows`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>另请参阅  
 [维度 &#40;MDX &#41;](../mdx/dimension-mdx.md)   
 [函数 &#40;MDX 语法 &#41;](../mdx/functions-mdx-syntax.md)   
 [层次结构 &#40;MDX &#41;](../mdx/hierarchy-mdx.md)   
 [级别 &#40;MDX &#41;](../mdx/level-mdx.md)  
  
  

