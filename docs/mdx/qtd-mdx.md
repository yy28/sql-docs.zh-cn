---
title: Qtd （MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 7a8856b28d8eec76d2bc262c4209b007c0a7fa04
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "68020646"
---
# <a name="qtd-mdx"></a>Qtd (MDX)


  从与给定成员相同的级别返回一组同级成员，从第一个同级成员开始，到给定成员的末尾，由时间维度中的*季度*级别进行约束。  
  
## <a name="syntax"></a>语法  
  
```  
  
Qtd( [ Member_Expression ] )  
```  
  
## <a name="arguments"></a>参数  
 *Member_Expression*  
 返回成员的有效多维表达式 (MDX)。  
  
## <a name="remarks"></a>备注  
 如果未指定成员 expressionis，则默认值为第一个层次结构的当前成员，该层次结构的第一个层次结构的第一个维度中的第一个维度*的类型为*该度量值组中的*Time* 。  
  
 **Qtd**函数是[PeriodsToDate &#40;MDX&#41;](../mdx/periodstodate-mdx.md)函数的快捷函数，其 level expression 参数设置为 "*季度*"。 也就是说，`Qtd(Member_Expression)` 的功能与 `PeriodsToDate(Quarter_Level_Expression, Member_Expression)` 相同。  
  
## <a name="example"></a>示例  
 下面的示例将返回从`Measures.[Order Quantity]` **艾德工作**多维数据集中包含在该`Date`维度中的第三季度第三2003季度的第三个月的成员的总和。  
  
```  
WITH MEMBER [Date].[Calendar].[First2MonthsSecondSemester2003] AS  
    Aggregate(  
        QTD([Date].[Calendar].[Month].[August 2003])  
    )  
SELECT   
    [Date].[Calendar].[First2MonthsSecondSemester2003] ON COLUMNS,  
    [Product].[Category].Children ON ROWS  
FROM  
    [Adventure Works]  
WHERE  
    [Measures].[Order Quantity]  
```  
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
