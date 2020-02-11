---
title: 序数（MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: b22cc6d5a609f8e1f585ccc1229e0e1cd67e1796
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68055646"
---
# <a name="ordinal-mdx"></a>Ordinal (MDX)


  返回与某一级别相关联的从零开始计算的序数值。  
  
## <a name="syntax"></a>语法  
  
```  
  
Level_Expression.Ordinal   
```  
  
## <a name="arguments"></a>参数  
 *Level_Expression*  
 返回级别的有效多维表达式 (MDX)。  
  
## <a name="remarks"></a>备注  
 **序数**函数经常与**IIF**和**CurrentMember**函数结合使用，根据查询结果中每个特定单元的序号位置，有条件地在不同的层次结构级别显示不同的值。 例如，可以使用**Ordinal**函数在某些级别执行计算，并在其他级别显示默认值 "N/a"。  
  
## <a name="example"></a>示例  
 下面的示例返回 Calendar 层次结构中的 Calendar Quarter 级别的序号。  
  
```  
WITH MEMBER Measures.x AS [Date].[Calendar].[Calendar Quarter].Ordinal  
SELECT Measures.x on 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另请参阅  
 [Mdx 函数引用 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
