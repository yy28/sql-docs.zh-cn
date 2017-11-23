---
title: "LookupCube (MDX) |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: LOOKUPCUBE
dev_langs: kbMDX
helpviewer_keywords: LookupCube function
ms.assetid: 243fa101-328a-4016-86e0-d8b5977e15a9
caps.latest.revision: "32"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: ecd1810908dfda4d3e9f4e8c36d4c35ba6e37185
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="lookupcube-mdx"></a>LookupCube (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
  
## <a name="remarks"></a>注释  
 如果指定数值表达式，则**LookupCube**函数中指定的多维数据集的指定数值表达式的计算结果并返回生成的数字值。  
  
 如果指定的字符串表达式，则**LookupCube**函数中指定的多维数据集的指定的字符串表达式的计算结果并返回结果的字符串值。  
  
 **LookupCube**函数工作方式的同一数据库中的多维数据集，因为在其 MDX 查询的源多维数据集包含**LookupCube**运行函数。  
  
> [!IMPORTANT]  
>  因为当前查询的上下文不会延续到将要查询的多维数据集，所以必须在数值或字符串表达式内提供任何必要的当前成员。  
  
 任何计算使用**LookupCube**函数是可能遇到中的性能不佳。 请考虑重新设计您的解决方案，而不是使用此函数，以便在一个多维数据集中提供您所需的所有数据。  
  
## <a name="examples"></a>示例  
 以下查询演示 LookupCube 的用法：  
  
 `WITH MEMBER MEASURES.LOOKUPCUBEDEMO AS`  
  
 `LOOKUPCUBE("Adventure Works", "[Measures].[In" + "ternet Sales Amount]")`  
  
 `SELECT MEASURES.LOOKUPCUBEDEMO  ON 0`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
