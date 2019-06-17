---
title: 序号 (MDX) |Microsoft Docs
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
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63278118"
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
 **序号**函数经常与结合使用**IIF**并**CurrentMember**函数来有条件地在不同显示不同的值层次结构级别，根据查询结果中的每个特定的单元格的序号位置。 例如，可以使用**序号**函数来执行某些级别的计算，并在其他级别上显示的默认值为"n/A"。  
  
## <a name="example"></a>示例  
 下面的示例返回 Calendar 层次结构中的 Calendar Quarter 级别的序号。  
  
```  
WITH MEMBER Measures.x AS [Date].[Calendar].[Calendar Quarter].Ordinal  
SELECT Measures.x on 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>请参阅  
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
