---
title: AllMembers （MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 770d66941af9b42be3c7b26f7e04a60d2a95cac2
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "68017149"
---
# <a name="allmembers-mdx"></a>AllMembers (MDX)


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
  
## <a name="remarks"></a>备注  
 **AllMembers**函数返回一个集，该集包含指定层次结构或级别中的所有成员，包括计算成员。 即使指定的层次结构或级别不包含可见成员， **AllMembers**函数也会返回计算成员。  
  
> [!IMPORTANT]  
>  如果维度仅包含单个可见层次结构，由于在此情况下维度名称将解析为其唯一可见的层次结构，所以既可以通过维度名称也可以通过层次结构名称来引用该层次。 例如，`Measures.AllMembers` 是一个有效的 MDX 表达式，这是因为它会解析为 Measures 维度中唯一的层次结构。  
  
> [!NOTE]  
>  **AllMembers**函数在语义上类似于[AddCalculatedMembers （MDX）](../mdx/addcalculatedmembers-mdx.md)函数。  
  
## <a name="examples"></a>示例  
 下面的示例返回列轴上 [`Date].[Calendar Year]`属性层次结构中的所有成员，这包括计算成员，以及来自**艾德工作**多维数据集的`[Product].[Model Name]`行轴上属性层次结构的所有子级的集合。  
  
```  
SELECT  
   [Date].[Calendar Year].AllMembers ON COLUMNS,  
   [Product].[Model Name].Children ON ROWS  
FROM  
   [Adventure Works]  
```  
  
 下面的示例返回列轴上的**度量值**维度中的所有成员，其中包括所有计算成员，以及来自**艾德公司**的行轴`[Product].[Model Name]`上属性层次结构的所有子级集。  
  
```  
SELECT  
    Measures.AllMembers ON COLUMNS,  
    [Product].[Model Name].Children ON ROWS  
FROM  
    [Adventure Works]  
```  
  
## <a name="see-also"></a>另请参阅  
 [AddCalculatedMembers &#40;MDX&#41;](../mdx/addcalculatedmembers-mdx.md)   
 [子 &#40;MDX&#41;](../mdx/children-mdx.md)   
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
