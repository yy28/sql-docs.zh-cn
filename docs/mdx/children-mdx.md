---
title: "子级 (MDX) |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: CHILDREN
dev_langs: kbMDX
helpviewer_keywords: Children function
ms.assetid: ce2c3069-914c-44a3-8a4c-5cbd4fb71e4c
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 8a818777528583214a948a5fefd7d9c78896fc79
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2017
---
# <a name="children-mdx"></a>Children (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  返回指定成员的子成员集。  
  
## <a name="syntax"></a>语法  
  
```  
  
Member_Expression.Children  
```  
  
## <a name="arguments"></a>参数  
 *Member_Expression*  
 返回成员的有效多维表达式 (MDX)。  
  
## <a name="remarks"></a>注释  
 **子级**函数将返回包含指定成员的子级的自然排序的集。 如果指定的成员没有子成员，则此函数返回一个空集。  
  
## <a name="example"></a>示例  
 下例将返回 Geography 维度中 Geography 层次结构的 United States 成员的子成员。  
  
```  
SELECT [Geography].[Geography].[Country].&[United States].Children ON 0  
FROM [Adventure Works]  
```  
  
 下面的示例返回中的所有成员**度量值**维度列在轴上，这包括所有计算的成员、 和的一组的所有子级`[Product].[Model Name]`属性从在行轴上的层次结构**Adventure Works**多维数据集。  
  
```  
SELECT  
    Measures.AllMembers ON COLUMNS,  
    [Product].[Model Name].Children ON ROWS  
FROM  
    [Adventure Works]  
  
```  
  
|发行版本|历史记录|  
|-------------|-------------|  
|[!INCLUDE[ssBOL2005_R03](../includes/ssbol2005-r03-md.md)]|**内容已更改：**<br /> -更新语法和参数以提高清晰度。<br /><br /> -添加更新的示例。|  
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
