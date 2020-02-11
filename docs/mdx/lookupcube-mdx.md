---
title: LookupCube （MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: ec18b600c369de872df5f6eadf06ef6c30c88efa
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68098516"
---
# <a name="lookupcube-mdx"></a>LookupCube (MDX)


  返回用多维表达式 (MDX) 对同一数据库中的另一个指定多维数据集求得的值。  
  
## <a name="syntax"></a>语法  
  
```  
  
Numeric expression syntax  
LookupCube(Cube_Name, Numeric_Expression )  
  
String expression syntax  
LookupCube(Cube_Name, String_Expression )  
```  
  
## <a name="arguments"></a>参数  
 *Cube_Name*  
 指定多维数据集名称的有效字符串表达式。  
  
 *Numeric_Expression*  
 返回数字的有效数值表达式，通常为单元坐标的多维表达式 (MDX)。  
  
 *String_Expression*  
 一个有效的字符串表达式，通常为返回一个字符串的单元坐标的有效多维表达式 (MDX)。  
  
## <a name="remarks"></a>备注  
 如果指定了数值表达式，则**LookupCube**函数将在指定的多维数据集中计算指定的数值表达式，并返回生成的数值。  
  
 如果指定了字符串表达式，则**LookupCube**函数将在指定的多维数据集中计算指定的字符串表达式，并返回生成的字符串值。  
  
 **LookupCube**函数适用于源多维数据集所在的数据库中的多维数据集，其中包含**LOOKUPCUBE**函数的 MDX 查询正在运行。  
  
> [!IMPORTANT]  
>  因为当前查询的上下文不会延续到将要查询的多维数据集，所以必须在数值或字符串表达式内提供任何必要的当前成员。  
  
 使用**LookupCube**函数的任何计算都可能会导致性能不佳。 请考虑重新设计您的解决方案，而不是使用此函数，以便在一个多维数据集中提供您所需的所有数据。  
  
## <a name="examples"></a>示例  
 以下查询演示 LookupCube 的用法：  
  
 `WITH MEMBER MEASURES.LOOKUPCUBEDEMO AS`  
  
 `LOOKUPCUBE("Adventure Works", "[Measures].[In" + "ternet Sales Amount]")`  
  
 `SELECT MEASURES.LOOKUPCUBEDEMO  ON 0`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>另请参阅  
 [Mdx 函数引用 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
