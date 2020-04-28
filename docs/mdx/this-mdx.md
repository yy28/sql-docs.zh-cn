---
title: 此（MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 12455c82fe7a885a3530b6c0db216b9996a5eda6
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "68893562"
---
# <a name="this-mdx"></a>This (MDX)


  返回用于多维表达式 (MDX) 脚本中的分配的当前子多维数据集。  
  
## <a name="syntax"></a>语法  
  
```  
  
This   
```  
  
## <a name="remarks"></a>备注  
 **此**函数可用于在任何子多维数据集表达式的位置提供当前范围内的当前子多维数据集。 必须在赋值的左侧使用**此**函数。  
  
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
  
## <a name="see-also"></a>另请参阅  
 [Mdx 函数引用 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)   
 [“新建命名集”](https://docs.microsoft.com/analysis-services/multidimensional-models-olap-logical-cube-objects/calculations)  
  
  
