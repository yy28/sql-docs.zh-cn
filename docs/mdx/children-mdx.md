---
title: 子级 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 03c96a1c90f7ca0a18bd49c371a2ec90582b38f1
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2018
ms.locfileid: "52533411"
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
 **子级**函数将返回包含指定成员的子级的自然排序的集。 如果指定的成员没有子成员，则此函数返回一个空集。  
  
## <a name="example"></a>示例  
 下例将返回 Geography 维度中 Geography 层次结构的 United States 成员的子成员。  
  
```  
SELECT [Geography].[Geography].[Country].&[United States].Children ON 0  
FROM [Adventure Works]  
```  
  
 下面的示例返回中的所有成员**度量值**维度在列轴上这包括所有计算的成员、 和的所有子级集`[Product].[Model Name]`属性层次结构行轴上的，从**Adventure Works**多维数据集。  
  
```  
SELECT  
    Measures.AllMembers ON COLUMNS,  
    [Product].[Model Name].Children ON ROWS  
FROM  
    [Adventure Works]  
  
```  
  
|发行版本|历史记录|  
|-------------|-------------|  
|[!INCLUDE[ssBOL2005_R03](../includes/ssbol2005-r03-md.md)]|**更改的内容：**<br /> -更新语法和参数以提高清晰度。<br /><br /> -添加了更新的示例。|  
  
## <a name="see-also"></a>请参阅  
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
