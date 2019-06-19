---
title: AllMembers (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 92cde0acf07f62d0678da6dd96efa707dedc1a1f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63066245"
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
 **AllMembers**函数将返回一组包含所有成员，其中包括计算的成员中指定的层次结构或级别。 **AllMembers**函数返回计算的成员，即使指定的层次结构或级别不包含任何可见的成员。  
  
> [!IMPORTANT]  
>  如果维度仅包含单个可见层次结构，由于在此情况下维度名称将解析为其唯一可见的层次结构，所以既可以通过维度名称也可以通过层次结构名称来引用该层次。 例如，`Measures.AllMembers` 是一个有效的 MDX 表达式，这是因为它会解析为 Measures 维度中唯一的层次结构。  
  
> [!NOTE]  
>  **AllMembers**函数在语义上类似于[AddCalculatedMembers (MDX)](../mdx/addcalculatedmembers-mdx.md)函数。  
  
## <a name="examples"></a>示例  
 下面的示例返回中的所有成员 [`Date].[Calendar Year]`列轴上的属性层次结构，这包括计算的成员、 和的所有子级集`[Product].[Model Name]`属性层次结构从在行轴上的**Adventure工作原理**多维数据集。  
  
```  
SELECT  
   [Date].[Calendar Year].AllMembers ON COLUMNS,  
   [Product].[Model Name].Children ON ROWS  
FROM  
   [Adventure Works]  
```  
  
 下面的示例返回中的所有成员**度量值**维度在列轴上这包括所有计算的成员、 和的所有子级集`[Product].[Model Name]`属性层次结构行轴上的，从**Adventure Works**多维数据集。  
  
```  
SELECT  
    Measures.AllMembers ON COLUMNS,  
    [Product].[Model Name].Children ON ROWS  
FROM  
    [Adventure Works]  
```  
  
## <a name="see-also"></a>请参阅  
 [AddCalculatedMembers (MDX)](../mdx/addcalculatedmembers-mdx.md)   
 [Children (MDX)](../mdx/children-mdx.md)   
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
