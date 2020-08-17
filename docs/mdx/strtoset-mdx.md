---
description: StrToSet (MDX)
title: StrToSet (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 882ab646af51d4b1edbe0a1240eaaed7cbfa5422
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88386773"
---
# <a name="strtoset-mdx"></a>StrToSet (MDX)


  返回由 MDX) 格式字符串 (多维表达式指定的集。  
  
## <a name="syntax"></a>语法  
  
```  
  
StrToSet(Set_Specification [,CONSTRAINED] )   
```  
  
## <a name="arguments"></a>参数  
 *Set_Specification*  
 直接或间接指定某个集的有效字符串表达式。  
  
## <a name="remarks"></a>备注  
 **StrToSet**函数返回字符串表达式中指定的集。 **StrToSet**函数通常与用户定义函数一起使用，以将外部函数中的 set 规范返回到 mdx 语句，或在参数化 mdx 查询时返回。  
  
-   使用受约束的标志时，设置规范必须包含限定或非限定的成员名称或包含括在大括号中的限定或非限定成员名称的元组集 {} 。 此标志通过指定字符串可降低注入攻击的风险。 如果提供的字符串不能直接解析为限定或非限定的成员名称，则会出现下列出错信息：“违反了 STRTOSET 函数中 CONSTRAINED 标志所规定的限制。”  
  
-   如果未使用 CONSTRAINED 标志，则指定的集规范可以解析为返回一个集的有效多维表达式 (MDX)。  
  
-   为了更好地理解集和成员之间的差异，请参阅“使用集表达式”和“使用成员表达式”。  
  
## <a name="examples"></a>示例  
 下面的示例使用 **StrToSet** 函数返回省/市/自治区属性层次结构的成员集。 该集规范提供一个有效的 MDX 集表达式。  
  
```  
SELECT StrToSet ('[Geography].[State-Province].Members')  
ON 0  
FROM [Adventure Works]  
  
```  
  
 下面的示例返回因 CONSTRAINED 标志而引起的错误。 如果集规范提供一个有效的 MDX 集表达式，则 CONSTRAINED 标志在集规范中需要限定或非限定的成员名称。  
  
```  
SELECT StrToSet ('[Geography].[State-Province].Members', CONSTRAINED)  
ON 0  
FROM [Adventure Works]  
  
```  
  
 下例返回德国和加拿大的“分销商销售额”度量值。 指定字符串中提供的集规范包含了 CONSTRAINED 标志所需的限定成员名称。  
  
```  
SELECT StrToSet ('{[Geography].[Geography].[Country].[Germany],[Geography].[Geography].[Country].[Canada]}', CONSTRAINED)  
ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
