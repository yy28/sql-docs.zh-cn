---
title: 子级（MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 0af4d7b97777002dc5683c075f82531ccc8df86e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68016806"
---
# <a name="children-mdx"></a>Children (MDX)


  返回指定成员的子成员集。  
  
## <a name="syntax"></a>语法  
  
```  
  
Member_Expression.Children  
```  
  
## <a name="arguments"></a>参数  
 *Member_Expression*  
 返回成员的有效多维表达式 (MDX)。  
  
## <a name="remarks"></a>备注  
 **子**函数返回一个自然排序集，其中包含指定成员的子级。 如果指定的成员没有子成员，则此函数返回一个空集。  
  
## <a name="example"></a>示例  
 下例将返回 Geography 维度中 Geography 层次结构的 United States 成员的子成员。  
  
```  
SELECT [Geography].[Geography].[Country].&[United States].Children ON 0  
FROM [Adventure Works]  
```  
  
 下面的示例返回列轴上的**度量值**维度中的所有成员，其中包括所有计算成员，以及来自**艾德公司**的行轴`[Product].[Model Name]`上属性层次结构的所有子级集。  
  
```  
SELECT  
    Measures.AllMembers ON COLUMNS,  
    [Product].[Model Name].Children ON ROWS  
FROM  
    [Adventure Works]  
  
```  
  
|发布|历史记录|  
|-------------|-------------|  
|[!INCLUDE[ssBOL2005_R03](../includes/ssbol2005-r03-md.md)]|**更改的内容：**<br /> -更新了语法和参数以提高清晰度。<br /><br /> -添加了更新的示例。|  
  
## <a name="see-also"></a>另请参阅  
 [Mdx 函数引用 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
