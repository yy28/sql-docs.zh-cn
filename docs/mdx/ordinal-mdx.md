---
title: "序号 (MDX) |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: Ordinal
dev_langs: kbMDX
helpviewer_keywords: Ordinal function
ms.assetid: 9d416c39-da4a-4f0d-8d85-a76af5df0a87
caps.latest.revision: "28"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 2cf441cb5eaaba8ec7b0e14adb1f770464006abb
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2017
---
# <a name="ordinal-mdx"></a>Ordinal (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  返回与某一级别相关联的从零开始计算的序数值。  
  
## <a name="syntax"></a>语法  
  
```  
  
Level_Expression.Ordinal   
```  
  
## <a name="arguments"></a>参数  
 *Level_Expression*  
 返回级别的有效多维表达式 (MDX)。  
  
## <a name="remarks"></a>注释  
 **序号**函数经常与结合使用**IIF**和**CurrentMember**函数来有条件地在不同层次结构级别显示不同的值根据查询结果中的每个特定的单元格的序号位置。 例如，你可以使用**序号**函数来执行特定级别的计算和显示在其他级别的默认值为"n/A"。  
  
## <a name="example"></a>示例  
 下面的示例返回 Calendar 层次结构中的 Calendar Quarter 级别的序号。  
  
```  
WITH MEMBER Measures.x AS [Date].[Calendar].[Calendar Quarter].Ordinal  
SELECT Measures.x on 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
