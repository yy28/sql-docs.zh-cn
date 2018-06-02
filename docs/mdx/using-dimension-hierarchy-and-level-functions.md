---
title: 使用维度、 层次结构和级别函数 |Microsoft 文档
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 96315c01133f3a25e5853ba076d2b28e5ba81a35
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/02/2018
ms.locfileid: "34581489"
---
# <a name="using-dimension-hierarchy-and-level-functions"></a>使用维度函数、层次结构函数和级别函数
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  维度函数、层次结构函数和级别函数对遍历 Analysis Services 中的多维结构非常有用。 通常将此类函数和其他函数一起使用，以获得有关维度、层次结构或级别的成员信息。  
  
 下面的示例演示如何使用 **。维度**， **。层次结构**，和 **。级别**函数：  
  
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
  
## <a name="see-also"></a>请参阅  
 [维度&#40;MDX&#41;](../mdx/dimension-mdx.md)   
 [函数&#40;MDX 语法&#41;](../mdx/functions-mdx-syntax.md)   
 [层次结构&#40;MDX&#41;](../mdx/hierarchy-mdx.md)   
 [级别&#40;MDX&#41;](../mdx/level-mdx.md)  
  
  
