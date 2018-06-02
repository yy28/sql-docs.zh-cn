---
title: 维度 (MDX) |Microsoft 文档
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 43c105daff0d53c886df087600da99bdd1292574
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/02/2018
ms.locfileid: "34577889"
---
# <a name="dimensions-mdx"></a>Dimensions (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  返回由数值表达式或字符串表达式指定的层次结构。  
  
## <a name="syntax"></a>语法  
  
```  
  
Numeric expression syntax  
Dimensions(Hierarchy_Number)  
  
String expression syntax  
Dimensions(Hierarchy_Name)  
```  
  
## <a name="arguments"></a>参数  
 *Hierarchy_Number*  
 指定层次结构号的有效数值表达式。  
  
 *Hierarchy_Name*  
 指定层次结构名称的有效字符串表达式。  
  
## <a name="remarks"></a>Remarks  
 如果指定层次结构号，**维度**函数返回在多维数据集的从零开始的位置是层次结构指定层次结构数目。  
  
 如果指定层次结构名称，则**维度**函数将返回指定层次结构。 通常情况下，使用此字符串版本**维度**与用户定义函数的函数。  
  
> [!NOTE]  
>  **度量值**维度始终由`Dimensions(0)`。  
  
## <a name="examples"></a>示例  
 下面的示例使用**维度**函数以返回名称、 级别的计数和计数的使用数值表达式和字符串表达式指定层次结构的成员。  
  
```  
WITH MEMBER Measures.x AS Dimensions  
   ('[Product].[Product Model Lines]').Name  
SELECT Measures.x on 0  
FROM [Adventure Works]  
  
WITH MEMBER Measures.x AS Dimensions  
   ('[Product].[Product Model Lines]').Levels.Count  
SELECT Measures.x on 0  
FROM [Adventure Works]  
  
WITH MEMBER Measures.x AS Dimensions  
   ('[Product].[Product Model Lines]').Members.Count  
SELECT Measures.x on 0  
FROM [Adventure Works]  
  
WITH MEMBER Measures.x AS Dimensions(0).Name  
SELECT Measures.x on 0  
FROM [Adventure Works]  
  
WITH MEMBER Measures.x AS Dimensions(0).Levels.Count  
SELECT measures.x on 0  
FROM [Adventure Works]  
  
WITH MEMBER Measures.x AS Dimensions(0).Members.Count  
SELECT measures.x on 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>请参阅  
 [MDX 函数引用&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
