---
title: 构建在 MDX 中的度量值 |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: mdx
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d06bd5f67ae36434a2ce09e3cfd324bcbf20bdc2
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="mdx-building-measures"></a>MDX 生成度量值
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  在多维表达式 (MDX) 中，度量值是名为 DAX 的表达式，通过计算该表达式来解析它以返回表格模型中的值。 这种泛泛的定义所包括的范围十分惊人。 由于能在 MDX 查询中构造和使用度量值，使得人们能够更有力地驾驭表格数据。  
  
> [!WARNING]  
>  只能在表格模型中定义度量值；如果在多维模式下设置数据库，创建度量值将导致错误。  
  
 若要创建一个度量值，该度量值被定义为 MDX 查询的一部分并且其作用域因此被限制在该查询内，请使用 WITH 关键字。 然后，就可以在 MDX SELECT 语句中使用该度量值。 通过这种方法，更改用 WITH 关键字创建的计算成员时就不会打乱 SELECT 语句。 但是，在 MDX 中您引用度量值的方式不用于在 DAX 表达式中引用它的方式；为了引用度量值，您将它命名为 [度量值] 维度的成员，请参阅以下 MDX 示例：  
  
```  
with measure  'Sales Territory'[Total Sales Amount] = SUM('Internet Sales'[Sales Amount]) + SUM('Reseller Sales'[Sales Amount])  
select measures.[Total Sales Amount] on columns  
     ,NON EMPTY [Date].[Calendar Year].children on rows  
from [Model]  
  
```  
  
 执行时将返回以下数据：  
  
||总销售额||  
|-|------------------------|-|  
|2001|11331808.96||  
|2002|30674773.18||  
|2003|41993729.72||  
|2004|25808962.34||  
  
## <a name="see-also"></a>另请参阅  
 [创建成员语句 & #40;MDX & #41;](../../../mdx/mdx-data-definition-create-member.md)   
 [MDX 函数引用 & #40;MDX & #41;](../../../mdx/mdx-function-reference-mdx.md)   
 [SELECT 语句 & #40;MDX & #41;](../../../mdx/mdx-data-manipulation-select.md)  
  
  
