---
title: 序号 (MDX) |Microsoft 文档
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 83036ec2ee0fa69c9ebb8cc2a905361eeae0aafa
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/04/2018
ms.locfileid: "34742666"
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
  
## <a name="remarks"></a>Remarks  
 **序号**函数经常与结合使用**IIF**和**CurrentMember**函数来有条件地在不同层次结构级别显示不同的值根据查询结果中的每个特定的单元格的序号位置。 例如，你可以使用**序号**函数来执行特定级别的计算和显示在其他级别的默认值为"n/A"。  
  
## <a name="example"></a>示例  
 下面的示例返回 Calendar 层次结构中的 Calendar Quarter 级别的序号。  
  
```  
WITH MEMBER Measures.x AS [Date].[Calendar].[Calendar Quarter].Ordinal  
SELECT Measures.x on 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>请参阅  
 [MDX 函数引用&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
