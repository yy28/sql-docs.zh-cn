---
title: 使用 Dimension、层次结构和 Level 函数 |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 8fa374ef93f56f8cddaed81bc9e3872d1eb206c7
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "68097178"
---
# <a name="using-dimension-hierarchy-and-level-functions"></a>使用维度函数、层次结构函数和级别函数


  维度函数、层次结构函数和级别函数对遍历 Analysis Services 中的多维结构非常有用。 通常将此类函数和其他函数一起使用，以获得有关维度、层次结构或级别的成员信息。  
  
 下面的示例演示如何使用 **。Dimension** **。层次结构**和 **。级别**函数：  
  
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
 [维度 &#40;MDX&#41;](../mdx/dimension-mdx.md)   
 [函数 &#40;MDX 语法&#41;](../mdx/functions-mdx-syntax.md)   
 [&#40;MDX&#41;的层次结构](../mdx/hierarchy-mdx.md)   
 [级别 &#40;MDX&#41;](../mdx/level-mdx.md)  
  
  
