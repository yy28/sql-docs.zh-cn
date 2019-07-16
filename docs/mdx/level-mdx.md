---
title: 级别 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: b419cbb05aa616f163f5878bda83c9d68203575d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67905663"
---
# <a name="level-mdx"></a>Level (MDX)


  返回成员的级别。  
  
## <a name="syntax"></a>语法  
  
```  
  
Member_Expression.Level  
```  
  
## <a name="arguments"></a>参数  
 *Member_Expression*  
 一个有效多维表达式 (MDX) 返回成员。  
  
### <a name="examples"></a>示例  
 下面的示例使用**级别**函数返回 Adventure Works 多维数据集中的所有月份。  
  
```  
SELECT[Date].[Fiscal].[Month].[February 2002].Level.Members ON 0,  
[Measures].[Internet Sales Amount] ON 1  
FROM [Adventure Works]  
```  
  
 下面的示例使用**级别**函数为 All-Purpose Bike Stand Adventure Works 多维数据集中型号名称属性层次结构中返回的级别名称。  
  
```  
WITH MEMBER Measures.x AS   
   [Product].[Model Name].[All-Purpose Bike Stand].Level.Name  
SELECT Measures.x ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>请参阅  
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
