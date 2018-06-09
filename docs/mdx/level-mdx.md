---
title: 级别 (MDX) |Microsoft 文档
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8406d02e167258901c3a6ce9ed3a1d7de935df54
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/04/2018
ms.locfileid: "34741746"
---
# <a name="level-mdx"></a>Level (MDX)


  返回成员的级别。  
  
## <a name="syntax"></a>语法  
  
```  
  
Member_Expression.Level  
```  
  
## <a name="arguments"></a>参数  
 *Member_Expression*  
 有效多维表达式 (MDX)，返回的成员。  
  
### <a name="examples"></a>示例  
 下面的示例使用**级别**函数返回的 Adventure Works 多维数据集中的所有月份。  
  
```  
SELECT[Date].[Fiscal].[Month].[February 2002].Level.Members ON 0,  
[Measures].[Internet Sales Amount] ON 1  
FROM [Adventure Works]  
```  
  
 下面的示例使用**级别**函数返回通用 Bike Stand Adventure Works 多维数据集中的模型名称属性层次结构中的级别的名称。  
  
```  
WITH MEMBER Measures.x AS   
   [Product].[Model Name].[All-Purpose Bike Stand].Level.Name  
SELECT Measures.x ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>请参阅  
 [MDX 函数引用&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
