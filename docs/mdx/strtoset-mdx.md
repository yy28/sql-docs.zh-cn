---
title: StrToSet (MDX) |Microsoft 文档
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7184dc872624f6589ec6e93911b39c9f8b4e4aa3
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/04/2018
ms.locfileid: "34742976"
---
# <a name="strtoset-mdx"></a>StrToSet (MDX)


  返回多维表达式 (MDX) 格式的字符串指定的集。  
  
## <a name="syntax"></a>语法  
  
```  
  
StrToSet(Set_Specification [,CONSTRAINED] )   
```  
  
## <a name="arguments"></a>参数  
 *Set_Specification*  
 直接或间接指定某个集的有效字符串表达式。  
  
## <a name="remarks"></a>Remarks  
 **StrToSet**函数返回的字符串表达式中指定的集合。 **StrToSet**函数通常用于与用户定义的函数返回一组规范从外部函数返回到 MDX 语句，或 MDX 查询进行参数化。  
  
-   当使用约束的标志时，限定或非限定成员名称或一组元组包含限定或非限定的成员名称括在大括号必须包含集规范{}。 此标志通过指定字符串可降低注入攻击的风险。 如果提供的字符串不能直接解析为限定或非限定的成员名称，则会出现下列出错信息：“违反了 STRTOSET 函数中 CONSTRAINED 标志所规定的限制。”  
  
-   如果未使用 CONSTRAINED 标志，则指定的集规范可以解析为返回一个集的有效多维表达式 (MDX)。  
  
-   为了更好地理解集和成员之间的差异，请参阅“使用集表达式”和“使用成员表达式”。  
  
## <a name="examples"></a>示例  
 下面的示例返回州-省属性层次结构使用的成员组成的集**StrToSet**函数。 该集规范提供一个有效的 MDX 集表达式。  
  
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
 [MDX 函数引用&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
