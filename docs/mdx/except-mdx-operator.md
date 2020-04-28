---
title: '- 只有（MDX） |Microsoft Docs'
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: cf0121d1be3cd2943a801f3c72ca4952b70ec681
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "68139084"
---
# <a name="except-mdx-operator"></a>Except （MDX）运算符


  执行一个集运算，以返回两个集之间的不同项并删除重复成员。  
  
## <a name="syntax"></a>语法  
  
```  
  
Set_Expression - Set_Expression  
```  
  
#### <a name="parameters"></a>参数  
 *Set_Expression*  
 返回集的有效多维表达式 (MDX)。  
  
## <a name="return-value"></a>返回值  
 由两个指定集的非共享成员组成的集。  
  
## <a name="remarks"></a>备注  
 **-（Except）** 运算符在功能上等效于[Except](../mdx/except-mdx-function.md)函数。  
  
## <a name="examples"></a>示例  
 以下示例演示此运算符的用法：  
  
```  
// This query shows the quantity of orders for all product categories  
// with the exception of Components.  
SELECT   
   [Measures].[Order Quantity] ON COLUMNS,  
   [Product].[Product Categories].[All].Children   
   - [Product].[Product Categories].[Components] ON ROWS  
FROM  
    [Adventure Works]  
```  
  
## <a name="see-also"></a>另请参阅  
 [Mdx 运算符引用 &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
