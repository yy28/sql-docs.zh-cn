---
description: DataMember (MDX)
title: DataMember (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 7291a8d2c57d4a996893146e8e855df234ed0139
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88413133"
---
# <a name="datamember-mdx"></a>DataMember (MDX)


  返回系统生成的、与某个维度的非叶成员相关联的数据成员。  
  
## <a name="syntax"></a>语法  
  
```  
  
Member_Expression.DataMember  
```  
  
## <a name="arguments"></a>参数  
 *Member_Expression*  
 返回成员的有效多维表达式 (MDX)。  
  
## <a name="remarks"></a>备注  
 此函数对任何层次结构中的非叶成员进行操作，并且可由 [UPDATE CUBE 语句 (MDX) ](../mdx/mdx-data-manipulation-update-cube.md) 命令用于直接将数据写回非叶成员（而不是叶成员的后代）。  
  
> [!NOTE]  
>  如果指定的成员为叶成员，或者如果非叶成员没有关联的数据成员，则返回指定的成员。  
  
## <a name="example"></a>示例  
 下面的示例在计算度量值中使用 **DataMember** 函数显示每个雇员的销售配额：  
  
```  
WITH MEMBER measures.InvidualQuota AS   
([Employee].[Employees].currentmember.datamember, [Measures].[Sales Amount Quota])  
,FORMAT_STRING='Currency'  
SELECT {[Measures].[Sales Amount Quota],[Measures].InvidualQuota} ON COLUMNS,  
[Employee].[Employees].MEMBERS ON ROWS  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另请参阅  
 [Mdx 函数引用 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)   
 [MDX 中的重要概念 (Analysis Services)](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services)  
  
  
