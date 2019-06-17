---
title: UPDATE CUBE 语句 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 878f103e236a198ff71181a64b39400c8f6ea0ca
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63187618"
---
# <a name="mdx-data-manipulation---update-cube"></a>MDX 数据操作 - UPDATE CUBE


  UPDATE CUBE 语句用于将数据写回到多维数据集中的任何单元中，该多维数据集使用 SUM 聚合而聚合到其父级。 有关详细说明和示例，请参阅这篇博客文章中的"了解分配":[生成 Analysis Services （博客） 写回应用程序](https://go.microsoft.com/fwlink/?LinkId=394977)。  
  
## <a name="syntax"></a>语法  
  
```  
  
UPDATE [ CUBE ] Cube_Name   
   SET   
            <update clause>   
           [, <update clause> ...n ]  
  
<update clause> ::=   
      Tuple_Expression[.VALUE]= New_Value  
      [   
        USE_EQUAL_ALLOCATION   
        | USE_EQUAL_INCREMENT   
        | USE_WEIGHTED_ALLOCATION [ BY Weight_Expression]   
        | USE_WEIGHTED_INCREMENT [ BY Weight_Expression]  
      ]  
```  
  
## <a name="arguments"></a>参数  
 *Cube_Name*  
 提供的多维数据集名称的有效字符串。  
  
 *Tuple_Expression*  
 返回元组的有效多维表达式 (MDX)。  
  
 *New_Value*  
 有效的数值表达式。  
  
 *Weight_Expression*  
 有效的 MDX（多维表达式）数值表达式，将返回介于 0 到 1 之间的一个十进制值。  
  
## <a name="remarks"></a>备注  
 您可以更新多维数据集中的指定叶单元或非叶单元的值，并且可以根据需要跨依赖叶单元为指定非叶单元分配值。 元组表达式指定的单元可以是多维空间中的任意有效单元（即该单元不一定是叶单元）。 但是，必须使用聚合单元格[之和](../mdx/sum-mdx.md)聚合函数并不能用于标识该单元格的元组中包含计算的成员。  
  
 它可能会有所帮助看作**更新多维数据集**语句视为子例程将自动生成的一系列个别单元格将汇总到指定总和的叶成员和非叶单元写回操作。  
  
 以下是分配方法的说明。  
  
 **USE_EQUAL_ALLOCATION:** 将基于下面的表达式具有相等值分配每个影响更新单元的叶单元格。  
  
```  
<leaf cell value> =   
<New Value> / Count(leaf cells that are contained in <tuple>)  
```  
  
 **USE_EQUAL_INCREMENT:** 将根据以下表达式更改影响更新单元的每个叶单元。  
  
```  
<leaf cell value> = <leaf cell value> +   
(<New Value > - <existing value>) /  
Count(leaf cells contained in <tuple>)  
```  
  
 **USE_WEIGHTED_ALLOCATION:** 将基于下面的表达式具有相等值分配每个影响更新单元的叶单元格。  
  
```  
<leaf cell value> = < New Value> * Weight_Expression  
```  
  
 **USE_WEIGHTED_INCREMENT:** 将根据以下表达式更改影响更新单元的每个叶单元。  
  
```  
<leaf cell value> = <leaf cell value> +   
(<New Value> - <existing value>)  * Weight_Expression  
```  
  
 如果未指定权重表达式，**更新多维数据集**语句隐式使用以下表达式。  
  
```  
Weight_Expression = <leaf cell value> / <existing value>  
```  
  
 权重表达式应表示为 0 到 1 之间的一个小数值。 此值指定希望分配到受分配影响的叶单元的分配值比率。 客户端应用程序程序员负责创建其汇总聚合值等于此表达式分配值的一系列表达式。  
  
> [!CAUTION]  
>  客户端应用程序必须同时考虑所有维度的分配，以避免可能产生的意外结果，包括不正确的汇总值或不一致的数据。  
  
 每个**更新多维数据集**分配应被视为原子用于事务性目的。 这意味着，如果任意一个分配操作由于任何原因（例如公式中出现错误或存在安全冲突）失败，则整个 UPDATE CUBE 操作都将失败。 在处理各个分配操作的计算之前，会对数据拍摄快照以确保所得到的计算是正确的。  
  
> [!CAUTION]  
>  当用于包含整数的度量值时，USE_WEIGHTED_ALLOCATION 方法可能会由于不断地进行舍入而得出不准确的结果。  
  
> [!IMPORTANT]  
>  如果更新的单元不相互重叠，则 **Update Isolation Level** 连接字符串属性可用于提高 UPDATE CUBE 的性能。  
  
## <a name="see-also"></a>请参阅  
 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A>   
 [MDX 数据操作语句&#40;MDX&#41;](../mdx/mdx-data-manipulation-statements-mdx.md)  
  
  
