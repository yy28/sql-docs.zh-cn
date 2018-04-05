---
title: 更新多维数据集语句 (MDX) |Microsoft 文档
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- Cube
- UPDATE CUBE
- UPDATE_CUBE
- UPDATE
dev_langs:
- kbMDX
helpviewer_keywords:
- updating cubes
- cubes [Analysis Services], modifying
- modifying cubes
- UPDATE CUBE statement
ms.assetid: 6c8f23bb-401b-49de-843a-5324ac977239
caps.latest.revision: 43
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 77ca2c4e3a63db80ff21a91309f5fc531e5ba3ca
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="mdx-data-manipulation---update-cube"></a>MDX 数据操作的更新多维数据集
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  UPDATE CUBE 语句用于将数据写回到多维数据集中的任何单元中，该多维数据集使用 SUM 聚合而聚合到其父级。 详细说明和示例，请参阅"了解分配"在此博客文章：[使用 Analysis Services （博客） 生成写回](http://go.microsoft.com/fwlink/?LinkId=394977)。  
  
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
 一个提供多维数据集的名称的有效字符串。  
  
 *Tuple_Expression*  
 返回元组的有效多维表达式 (MDX)。  
  
 *New_Value*  
 有效的数值表达式。  
  
 *Weight_Expression*  
 有效的 MDX（多维表达式）数值表达式，将返回介于 0 到 1 之间的一个十进制值。  
  
## <a name="remarks"></a>Remarks  
 您可以更新多维数据集中的指定叶单元或非叶单元的值，并且可以根据需要跨依赖叶单元为指定非叶单元分配值。 元组表达式指定的单元可以是多维空间中的任意有效单元（即该单元不一定是叶单元）。 但是，必须使用聚合单元格[总和](../mdx/sum-mdx.md)聚合函数和不能包含计算的成员的元组中用于标识该单元格。  
  
 可能需要考虑**更新多维数据集**作为将自动生成一系列到叶和非叶单元格将汇总到指定的和的各个单元格写回操作子例程的语句。  
  
 下面是分配的方法的说明。  
  
 **USE_EQUAL_ALLOCATION:**分配给已更新的单元格每个叶单元格将分配基于下面的表达式的相等值。  
  
```  
<leaf cell value> =   
<New Value> / Count(leaf cells that are contained in <tuple>)  
```  
  
 **USE_EQUAL_INCREMENT:**分配给已更新的单元格每个叶单元格将根据下面的表达式会更改。  
  
```  
<leaf cell value> = <leaf cell value> +   
(<New Value > - <existing value>) /  
Count(leaf cells contained in <tuple>)  
```  
  
 **USE_WEIGHTED_ALLOCATION:**分配给已更新的单元格每个叶单元格将分配一个相等的值，基于下面的表达式。  
  
```  
<leaf cell value> = < New Value> * Weight_Expression  
```  
  
 **USE_WEIGHTED_INCREMENT:**分配给已更新的单元格每个叶单元格将根据下面的表达式会更改。  
  
```  
<leaf cell value> = <leaf cell value> +   
(<New Value> - <existing value>)  * Weight_Expression  
```  
  
 如果未指定权重表达式，**更新多维数据集**语句隐式使用下面的表达式。  
  
```  
Weight_Expression = <leaf cell value> / <existing value>  
```  
  
 权重表达式应表示为 0 到 1 之间的一个小数值。 此值指定希望分配到受分配影响的叶单元的分配值比率。 客户端应用程序程序员负责创建其汇总聚合值等于此表达式分配值的一系列表达式。  
  
> [!CAUTION]  
>  客户端应用程序必须同时考虑所有维度的分配，以避免可能产生的意外结果，包括不正确的汇总值或不一致的数据。  
  
 每个**更新多维数据集**分配应被视为原子事务供。 这意味着，如果任意一个分配操作由于任何原因（例如公式中出现错误或存在安全冲突）失败，则整个 UPDATE CUBE 操作都将失败。 在处理各个分配操作的计算之前，会对数据拍摄快照以确保所得到的计算是正确的。  
  
> [!CAUTION]  
>  当用于包含整数的度量值时，USE_WEIGHTED_ALLOCATION 方法可能会由于不断地进行舍入而得出不准确的结果。  
  
> [!IMPORTANT]  
>  如果更新的单元不相互重叠，则 **Update Isolation Level** 连接字符串属性可用于提高 UPDATE CUBE 的性能。  
  
## <a name="see-also"></a>另请参阅  
 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A>   
 [MDX 数据操作语句 &#40;MDX &#41;](../mdx/mdx-data-manipulation-statements-mdx.md)  
  
  
