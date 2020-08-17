---
description: MDX 数据操作 - DRILLTHROUGH
title: 钻取语句 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: ee68e6cbb22bc817d478490315ab88ccb87e4ad4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88387032"
---
# <a name="mdx-data-manipulation---drillthrough"></a>MDX 数据操作 - DRILLTHROUGH


  检索用于在多维数据集中创建指定单元的基础表行。  
  
## <a name="syntax"></a>语法  
  
```  
  
DRILLTHROUGH[MAXROWSUnsigned_Integer]   
      <MDX SELECT statement>   
      [RETURNSet_of_Attributes_and_Measures   
            [,Set_of_Attributes_and_Measures ...]  
      ]  
```  
  
## <a name="arguments"></a>参数  
 *Unsigned_Integer*  
 正整数值。  
  
 *MDX SELECT 语句*  
 任何有效的多维表达式 (MDX) SELECT 语句。  
  
 *Set_of_Attributes_and_Measures*  
 以逗号分隔的维度属性和度量值列表。  
  
## <a name="remarks"></a>备注  
 钻取是一种操作，最终用户可通过该操作选择多维数据集中的一个单元，然后在该单元的源数据中检索结果集，以获取更加详细的信息。 默认情况下，钻取结果集来自表行（通过求值来计算选定的多维数据集单元的值）。 如果最终用户要执行钻取操作，则他们的客户端应用程序必须支持此功能。 在中 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ，除非查询 ROLAP 分区或维度，否则将直接从 MOLAP 存储中检索结果。  
  
> [!IMPORTANT]  
>  钻取安全性基于为多维数据集定义的常规安全选项。 如果无法用 MDX 获取一些数据，钻取也将以同样的方式限制用户。  
  
 MDX 语句指定了目标单元。 **MAXROWS**参数指定的值指示生成的行集应返回的最大行数。  
  
 默认情况下，返回的最大行数为 10000 行。 这意味着，如果未指定 **MAXROWS** ，则会收到10000行或更少的行。 如果此值对于你的方案来说太小，则可以将 **MAXROWS** 设置为更大的数字，如 `MAXROWS 20000` 。 如果此值太低，则可以通过更改 **OLAP\Query\DefaultDrillthroughMaxRows** 服务器属性来增加默认值。 有关更改此属性的详细信息，请参阅 [中的服务器属性 Analysis Services](https://docs.microsoft.com/analysis-services/server-properties/server-properties-in-analysis-services)。  
  
 除非另行指定，否则返回的列包括与指定度量值的度量值组相关的所有维度（多对多维度除外）的所有粒度属性。 多维数据集维度带有 $ 前缀，以区分维度和度量值组。 **RETURN**子句用于指定钻取查询返回的列。 以下函数可通过 **RETURN** 子句应用于单个属性或度量值。  
  
 Name(attribute_name)  
 返回指定属性成员的名称。  
  
 UniqueName(attribute_name)  
 返回指定属性成员的唯一名称。  
  
 Key(attribute_name[, N])  
 返回指定属性成员的键，其中 N 指定组合键中的列（如果有的话）。 N 的默认值为 1。  
  
 Caption(attribute_name)  
 返回指定属性成员的标题。  
  
 MemberValue(attribute_name)  
 返回指定属性成员的成员值。  
  
 CustomRollup(attribute_name)  
 返回指定属性成员的自定义汇总表达式。  
  
 CustomRollupProperties(attribute_name)  
 返回指定属性成员的自定义汇总属性。  
  
 UnaryOperator(attribute_name)  
 返回指定属性成员的一元运算符。  
  
## <a name="example"></a>示例  
 下例指定了 "July, 2007" 与 Australia 分销商销售额度量值（默认度量值）交叉的单元。 RETURN 子句指定返回此单元下各项销售的日期、产品型号名称、雇员姓名、销售额、税额和产品成本价值。  
  
```  
DRILLTHROUGH  
SELECT  
   ([Date].[Calendar].[Month].[July 2007])  
ON 0   
FROM [Adventure Works]  
WHERE [Geography].[Country].[Australia]  
RETURN   
  [$Date].[Date]  
  ,KEY([$Product].[Model Name])  
  ,NAME([$Employee].[Employee])  
  ,[Reseller Sales].[Reseller Sales Amount]  
  ,[Reseller Sales].[Reseller Tax Amount]  
  ,[Reseller Sales].[Reseller Standard Product Cost]  
```  
  
## <a name="see-also"></a>另请参阅  
 [Mdx 数据操作语句 &#40;MDX&#41;](../mdx/mdx-data-manipulation-statements-mdx.md)  
  
  
