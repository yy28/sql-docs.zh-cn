---
title: "AllMembers (MDX) |Microsoft 文档"
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
- ALLMEMBERS
dev_langs:
- kbMDX
helpviewer_keywords:
- AllMembers function
ms.assetid: 202e81d4-d2ee-4ec1-a019-4835eb19f446
caps.latest.revision: 44
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 8c677d421c70b6e05273db6ec437e7fe9667d638
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="allmembers-mdx"></a>AllMembers (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
  
## <a name="remarks"></a>備註  
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
  
## <a name="see-also"></a>另请参阅  
 [AddCalculatedMembers &#40;MDX &#41;](../mdx/addcalculatedmembers-mdx.md)   
 [子级 &#40;MDX &#41;](../mdx/children-mdx.md)   
 [MDX 函数引用 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

