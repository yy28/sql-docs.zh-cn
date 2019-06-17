---
title: StrToSet (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ee1e0cbeaa4e33be223e1b777ff243b5c3ef2d01
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63150190"
---
# <a name="strtoset-mdx"></a>StrToSet (MDX)


  返回多维表达式 MDX 格式的字符串指定的集。  
  
## <a name="syntax"></a>语法  
  
```  
  
StrToSet(Set_Specification [,CONSTRAINED] )   
```  
  
## <a name="arguments"></a>参数  
 *Set_Specification*  
 直接或间接指定某个集的有效字符串表达式。  
  
## <a name="remarks"></a>备注  
 **StrToSet**函数返回字符串表达式中指定的集。 **StrToSet**函数通常用于用户定义的函数以从外部函数向 MDX 语句，或在参数化 MDX 查询时返回集规范。  
  
-   使用 CONSTRAINED 的标志时，该集规范必须包含限定或非限定成员名称或一组元组包含限定或非限定成员名称括在大括号{}。 此标志通过指定字符串可降低注入攻击的风险。 如果提供一个字符串，不是直接解析为限定或非限定成员名称将显示以下错误："CONSTRAINED 所规定的限制违反了 STRTOSET 函数中的标志。"  
  
-   如果未使用 CONSTRAINED 标志，则指定的集规范可以解析为返回一个集的有效多维表达式 (MDX)。  
  
-   为了更好地理解集和成员之间的差异，请参阅“使用集表达式”和“使用成员表达式”。  
  
## <a name="examples"></a>示例  
 下面的示例返回 State-province 属性层次结构使用的成员的一套**StrToSet**函数。 该集规范提供一个有效的 MDX 集表达式。  
  
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
  
## <a name="see-also"></a>请参阅  
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
