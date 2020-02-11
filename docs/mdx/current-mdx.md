---
title: 当前（MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 821d517419b90df44b7943a1e0edde12ef667b6e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68047119"
---
# <a name="current-mdx"></a>Current (MDX)


  返回迭代过程中集内的当前元组。  
  
## <a name="syntax"></a>语法  
  
```  
  
Set_Expression.Current   
```  
  
## <a name="arguments"></a>参数  
 *Set_Expression*  
 返回集的有效多维表达式 (MDX)。  
  
## <a name="remarks"></a>备注  
 迭代过程的每一步中所操作的元组就是当前元组。 **当前**函数返回该元组。 该函数仅在对集执行迭代的过程中有效。  
  
 遍历集的 MDX 函数包括[生成](../mdx/generate-mdx.md)函数。  
  
> [!NOTE]  
>  该函数只能使用已命名的集（使用集别名或定义命名集）。  
  
## <a name="examples"></a>示例  
 下面的示例演示如何在**生成**中使用**当前**函数：  
  
 `WITH`  
  
 `//Creates a set of tuples consisting of all Calendar Years crossjoined with`  
  
 `//all Product Categories`  
  
 `SET MyTuples AS CROSSJOIN(`  
  
 `[Date].[Calendar Year].[Calendar Year].MEMBERS,`  
  
 `[Product].[Category].[Category].MEMBERS)`  
  
 `//Iterates through each tuple in the set and returns the name of the Calendar`  
  
 `//Year in each tuple`  
  
 `MEMBER MEASURES.CURRENTDEMO AS`  
  
 `GENERATE(MyTuples, MyTuples.CURRENT.ITEM(0).NAME, ", ")`  
  
 `SELECT MEASURES.CURRENTDEMO ON 0`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>另请参阅  
 [Mdx 函数引用 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
