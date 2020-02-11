---
title: 非空（MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 45daf970f69322cad36bbe5419bf1dc8cc8009b9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68088345"
---
# <a name="nonempty-mdx"></a>NonEmpty (MDX)


  根据第一个指定集与第二个集的叉积，返回指定集中的非空元组集。  
  
## <a name="syntax"></a>语法  
  
```  
  
NONEMPTY(set_expression1 [,set_expression2])  
```  
  
## <a name="arguments"></a>参数  
 *set_expression1*  
 返回集的有效多维表达式 (MDX)。  
  
 *set_expression2*  
 返回集的有效多维表达式 (MDX)。  
  
## <a name="remarks"></a>备注  
 此函数返回位于第一个指定集中并且在对第二个集中的元组求值时不为空的元组。 非**空**函数会考虑计算并保留重复元组。 如果未提供第二个集，将在多维数据集中属性层次结构和度量值的成员的当前坐标上下文中对表达式求值。  
  
> [!NOTE]  
>  使用此函数，而不是已弃用的[NonEmptyCrossjoin &#40;MDX&#41;](../mdx/nonemptycrossjoin-mdx.md)函数。  
  
> [!IMPORTANT]  
>  非空是元组所引用的单元的特征，而不是元组本身的特征。  
  
## <a name="examples"></a>示例  
 下面的查询显示一个简单的非**空示例，返回**在7月1日2001上对 Internet 销售金额具有非 null 值的所有客户：  
  
 `SELECT [Measures].[Internet Sales Amount] ON 0,`  
  
 `NONEMPTY(`  
  
 `[Customer].[Customer].[Customer].MEMBERS`  
  
 `, {([Date].[Calendar].[Date].&[20010701], [Measures].[Internet Sales Amount])}`  
  
 `)`  
  
 `ON 1`  
  
 `FROM [Adventure Works]`  
  
 以下示例返回包含客户和采购日期的元组集，使用**筛选器**函数和非**空**函数来查找每个客户的最后一次购买日期：  
  
 `WITH SET MYROWS AS FILTER`  
  
 `(NONEMPTY`  
  
 `([Customer].[Customer Geography].[Customer].MEMBERS`  
  
 `* [Date].[Date].[Date].MEMBERS`  
  
 `, [Measures].[Internet Sales Amount]`  
  
 `) AS MYSET`  
  
 `, NOT(MYSET.CURRENT.ITEM(0)`  
  
 `IS MYSET.ITEM(RANK(MYSET.CURRENT, MYSET)).ITEM(0))`  
  
 `)`  
  
 `SELECT [Measures].[Internet Sales Amount] ON 0,`  
  
 `MYROWS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>另请参阅  
 [DefaultMember &#40;MDX&#41;](../mdx/defaultmember-mdx.md)   
 [筛选 &#40;MDX&#41;](../mdx/filter-mdx.md)   
 [IsEmpty &#40;MDX&#41;](../mdx/isempty-mdx.md)   
 [Mdx 函数引用 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)   
 [NonEmptyCrossjoin &#40;MDX&#41;](../mdx/nonemptycrossjoin-mdx.md)  
  
  
