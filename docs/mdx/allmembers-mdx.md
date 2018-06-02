---
title: AllMembers (MDX) |Microsoft 文档
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a5720c3e82fdb341635c23d13a9c6bf4346a1cc0
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/02/2018
ms.locfileid: "34577169"
---
# <a name="allmembers-mdx"></a>AllMembers (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  计算层次结构或级别表达式，并返回一个包含指定层次结构或级别的所有成员的集，该集包含层次结构或级别的所有计算成员。  
  
## <a name="syntax"></a>语法  
  
```  
  
Hierarchy syntax  
Hierarchy_Expression.AllMembers  
  
Level syntax  
Level_Expression.AllMembers  
```  
  
## <a name="arguments"></a>参数  
 *Hierarchy_Expression*  
 返回层次结构的有效多维表达式 (MDX)。  
  
 *Level_Expression*  
 返回级别的有效多维表达式 (MDX)。  
  
## <a name="remarks"></a>Remarks  
 **AllMembers**函数将返回一组包含所有的成员，其中包括计算的成员、 指定层次结构或级别。 **AllMembers**函数返回计算的成员，即使指定层次结构或级别不包含任何可见的成员。  
  
> [!IMPORTANT]  
>  如果维度仅包含单个可见层次结构，由于在此情况下维度名称将解析为其唯一可见的层次结构，所以既可以通过维度名称也可以通过层次结构名称来引用该层次。 例如，`Measures.AllMembers` 是一个有效的 MDX 表达式，这是因为它会解析为 Measures 维度中唯一的层次结构。  
  
> [!NOTE]  
>  **AllMembers**函数在语义上等同于[AddCalculatedMembers (MDX)](../mdx/addcalculatedmembers-mdx.md)函数。  
  
## <a name="examples"></a>示例  
 下面的示例返回中的所有成员 [`Date].[Calendar Year]`列轴上的属性层次结构，这包括计算的成员、 和的所有子级集`[Product].[Model Name]`属性从在行轴上的层次结构**Adventure Works**多维数据集。  
  
```  
SELECT  
   [Date].[Calendar Year].AllMembers ON COLUMNS,  
   [Product].[Model Name].Children ON ROWS  
FROM  
   [Adventure Works]  
```  
  
 下面的示例返回中的所有成员**度量值**维度列在轴上，这包括所有计算的成员、 和的一组的所有子级`[Product].[Model Name]`属性从在行轴上的层次结构**Adventure Works**多维数据集。  
  
```  
SELECT  
    Measures.AllMembers ON COLUMNS,  
    [Product].[Model Name].Children ON ROWS  
FROM  
    [Adventure Works]  
```  
  
## <a name="see-also"></a>请参阅  
 [AddCalculatedMembers &#40;MDX&#41;](../mdx/addcalculatedmembers-mdx.md)   
 [子级&#40;MDX&#41;](../mdx/children-mdx.md)   
 [MDX 函数引用&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
