---
title: StrToMember (MDX) |Microsoft 文档
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- STRTOMEMBER
dev_langs:
- kbMDX
helpviewer_keywords:
- StrToMember function
ms.assetid: eb8a3dc0-5ae4-434e-b321-680a81a59e67
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: b26a0a5922f138bc13bbb13099809629ee336b02
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="strtomember-mdx"></a>StrToMember (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  返回多维表达式 (MDX) 格式的字符串指定的成员。  
  
## <a name="syntax"></a>语法  
  
```  
  
StrToMember(Member_Name [,CONSTRAINED] )   
```  
  
## <a name="arguments"></a>参数  
 *Member_Name*  
 直接或间接指定成员的有效字符串表达式。  
  
## <a name="remarks"></a>Remarks  
 **StrToMember**函数返回的字符串表达式中指定的成员。 **StrToMember**函数通常用于与用户定义的函数返回成员规范从外部函数返回到 MDX 语句，或 MDX 查询进行参数化。  
  
-   如果使用 CONSTRAINED 标志，则成员名称必须可直接解析为限定或未限定的成员名称。 此标志通过指定字符串可降低注入攻击的风险。 如果所提供的字符串无法直接解析为限定或未限定的成员名称，将出现以下错误：“违反了 STRTOMEMBER 函数中 CONSTRAINED 标志所规定的限制。”  
  
-   如果未使用 CONSTRAINED 标志，指定的成员将能直接解析为成员名称，或解析为 MDX 表达式以解析为名称。  
  
-   为了更好地理解集和成员之间的差异，请参阅“使用集表达式”和“使用成员表达式”。  
  
## <a name="examples"></a>示例  
 下面的示例返回 Bayern 成员的 Reseller Sales Amount 度量值中使用的州-省属性层次结构**StrToMember**函数。 指定字符串提供了限定的成员名称。  
  
```  
SELECT {StrToMember ('[Geography].[State-Province].[Bayern]')}  
ON 0,  
{[Measures].[Reseller Sales Amount]} ON 1  
FROM [Adventure Works]  
  
```  
  
 下面的示例返回使用 Bayern 成员的 Reseller Sales Amount 度量值**StrToMember**函数。 由于成员名称字符串仅提供了一个未限定的成员名称，因此该查询返回指定成员的第一个实例，而指定成员恰好在 Customer 维度（不与 Reseller Sales 相交）的 Customer Geography 层次结构中。 最佳做法要求指定限定名称以确保获得预期的结果。  
  
```  
SELECT {StrToMember ('[Bayern]').Parent}  
ON 0,  
{[Measures].[Reseller Sales Amount]} ON 1  
FROM [Adventure Works]  
  
```  
  
 下面的示例返回 Bayern 成员的 Reseller Sales Amount 度量值中使用的州-省属性层次结构**StrToMember**函数。 所提供的成员名称字符串解析为限定的成员名称。  
  
```  
SELECT {StrToMember('[Geography].[Geography].[Country].[Germany].FirstChild', CONSTRAINED)}  
ON 0,  
{[Measures].[Reseller Sales Amount]} ON 1  
FROM [Adventure Works]  
  
```  
  
 下面的示例返回因 CONSTRAINED 标志而引起的错误。 虽然所提供的成员名称字符串包含一个可解析为限定的成员名称的有效 MDX 成员表达式，但是 CONSTRAINED 标志要求成员名称字符串包含限定或未限定的成员名称。  
  
```  
SELECT StrToMember ('[Geography].[Geography].[Country].[Germany].FirstChild', CONSTRAINED)  
ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
