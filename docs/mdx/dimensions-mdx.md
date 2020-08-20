---
description: Dimensions (MDX)
title: " (MDX) 的维度 |Microsoft Docs"
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: c98167516f9e01525ecd351389c885c48626636e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88491414"
---
# <a name="dimensions-mdx"></a>Dimensions (MDX)


  返回由数值表达式或字符串表达式指定的层次结构。  
  
## <a name="syntax"></a>语法  
  
```  
  
Numeric expression syntax  
Dimensions(Hierarchy_Number)  
  
String expression syntax  
Dimensions(Hierarchy_Name)  
```  
  
## <a name="arguments"></a>参数  
 *Hierarchy_Number*  
 指定层次结构号的有效数值表达式。  
  
 *Hierarchy_Name*  
 指定层次结构名称的有效字符串表达式。  
  
## <a name="remarks"></a>备注  
 如果指定了层次结构编号，则 **维度** 函数将返回一个层次结构，其在多维数据集中从零开始的位置是指定的层次结构编号。  
  
 如果指定了层次结构名称，则 **维度** 函数返回指定的层次结构。 通常，对用户定义函数使用 **维度** 函数的这一字符串版本。  
  
> [!NOTE]  
>  **度量值**维度始终由表示 `Dimensions(0)` 。  
  
## <a name="examples"></a>示例  
 下面的示例使用 **维度** 函数返回指定层次结构的名称、级别计数和成员计数，同时使用数值表达式和字符串表达式。  
  
```  
WITH MEMBER Measures.x AS Dimensions  
   ('[Product].[Product Model Lines]').Name  
SELECT Measures.x on 0  
FROM [Adventure Works]  
  
WITH MEMBER Measures.x AS Dimensions  
   ('[Product].[Product Model Lines]').Levels.Count  
SELECT Measures.x on 0  
FROM [Adventure Works]  
  
WITH MEMBER Measures.x AS Dimensions  
   ('[Product].[Product Model Lines]').Members.Count  
SELECT Measures.x on 0  
FROM [Adventure Works]  
  
WITH MEMBER Measures.x AS Dimensions(0).Name  
SELECT Measures.x on 0  
FROM [Adventure Works]  
  
WITH MEMBER Measures.x AS Dimensions(0).Levels.Count  
SELECT measures.x on 0  
FROM [Adventure Works]  
  
WITH MEMBER Measures.x AS Dimensions(0).Members.Count  
SELECT measures.x on 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
