---
title: 此 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: a2486f23170ec19f16dca31672696c09815a2e83
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68036637"
---
# <a name="this-mdx"></a>This (MDX)


  返回用于多维表达式 (MDX) 脚本中的分配的当前子多维数据集。  
  
## <a name="syntax"></a>语法  
  
```  
  
This   
```  
  
## <a name="remarks"></a>备注  
 **这**函数可以使用到位置的任何子多维数据集表达式，以提供 MDX 计算脚本中的当前作用域内当前子多维数据集。 **这**函数必须使用作为赋值的左侧。  
  
## <a name="examples"></a>示例  
 以下 MDX 脚本片段说明如何将 This 关键字用于 SCOPE 语句来为子多维数据集进行分配：  
  
 `Scope`  
  
 `(`  
  
 `[Date].[Fiscal Year].&[2005],`  
  
 `[Date].[Fiscal].[Fiscal Quarter].Members,`  
  
 `[Measures].[Sales Amount Quota]`  
  
 `) ;`  
  
 `This = ParallelPeriod`  
  
 `(`  
  
 `[Date].[Fiscal].[Fiscal Year], 1,`  
  
 `[Date].[Fiscal].CurrentMember`  
  
 `) * 1.35 ;`  
  
 `/*-- Allocate equally to months in FY 2002 -----------------------------*/`  
  
 `Scope`  
  
 `(`  
  
 `[Date].[Fiscal Year].&[2002],`  
  
 `[Date].[Fiscal].[Month].Members`  
  
 `) ;`  
  
 `This = [Date].[Fiscal].CurrentMember.Parent / 3 ;`  
  
 `End Scope ;`  
  
 `End Scope;`  
  
## <a name="see-also"></a>请参阅  
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)   
 [计算](../analysis-services/multidimensional-models-olap-logical-cube-objects/calculations.md)  
  
  
