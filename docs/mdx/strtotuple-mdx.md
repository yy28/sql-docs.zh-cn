---
title: "StrToTuple (MDX) |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STRTOTUPLE
dev_langs:
- kbMDX
helpviewer_keywords:
- StrToTuple function
ms.assetid: e162cc01-cddd-4654-baab-d73abdc33b80
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: e2ca9d105bf04c91fd2c65bea74f92a0d0ef1edd
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="strtotuple-mdx"></a>StrToTuple (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回多维表达式 (MDX) 格式的字符串指定的元组。  
  
## <a name="syntax"></a>語法  
  
```  
  
StrToTuple(Tuple_Specification [,CONSTRAINED] )   
```  
  
## <a name="arguments"></a>参数  
 *Tuple_Specification*  
 直接或间接指定元组的有效字符串表达式。  
  
## <a name="remarks"></a>注释  
 **StrToTuple**函数返回指定的集。 **StrToTuple**函数通常用于与用户定义的函数返回元组规范函数的外部函数从回 MDX 语句。  
  
-   如果使用 CONSTRAINED 标志，则元组规范必须包含限定或未限定的成员名称。 此标志通过指定字符串可降低注入攻击的风险。 如果所提供的字符串无法直接解析为限定或未限定的成员名称，将出现以下错误：“违反了 STRTOTUPLE 函数中 CONSTRAINED 标志所规定的限制。”  
  
-   如果未使用 CONSTRAINED 标志，则指定的元组可以解析为有效的 MDX 表达式以返回元组。  
  
## <a name="examples"></a>示例  
 下面的示例返回 Bayern 成员在日历年度 2004 的 Reseller Sales Amount 度量值。 提供的元组规范包含有效的 MDX 元组表达式。  
  
```  
SELECT StrToTuple ('([Geography].[State-Province].[Bayern],[Date].[Calendar Year].[CY 2004], [Measures].[Reseller Sales Amount])')  
ON 0  
FROM [Adventure Works]  
  
```  
  
 下面的示例返回 Bayern 成员在日历年度 2004 的 Reseller Sales Amount 度量值。 提供的元组规范包含了 CONSTRAINED 标志所需的限定成员名称。  
  
```  
SELECT StrToTuple ('([Geography].[State-Province].[Bayern],[Date].[Calendar Year].[CY 2004], [Measures].[Reseller Sales Amount])', CONSTRAINED)  
ON 0  
FROM [Adventure Works]  
  
```  
  
 下面的示例返回 Bayern 成员在日历年度 2004 的 Reseller Sales Amount 度量值。 提供的元组规范包含有效的 MDX 元组表达式。  
  
```  
SELECT StrToTuple ('([Geography].[State-Province].[Bayern],[Date].[Calendar Year].&[2003].NEXTMEMBER, [Measures].[Reseller Sales Amount])')  
ON 0  
FROM [Adventure Works]  
  
```  
  
 下面的示例返回因 CONSTRAINED 标志而引起的错误。 虽然所提供的元组规范包含有效的 MDX 元组表达式，但是 CONSTRAINED 标志要求元组规范包含限定或未限定的成员名称。  
  
```  
SELECT StrToTuple ('([Geography].[State-Province].[Bayern],[Date].[Calendar Year].&[2003].NEXTMEMBER, [Measures].[Reseller Sales Amount])', CONSTRAINED)  
ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

