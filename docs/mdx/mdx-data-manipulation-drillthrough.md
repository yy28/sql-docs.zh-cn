---
title: "钻取语句 (MDX) |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DRILLTHROUGH
dev_langs:
- kbMDX
helpviewer_keywords:
- DRILLTHROUGH statement
- retrieving data
- data retrieval [MDX]
ms.assetid: dfa22755-0ed4-4bba-9c31-7ade26d9ebdb
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 6beadd42ec1f41ccec1ce8b0df999897b50568f5
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="mdx-data-manipulation---drillthrough"></a>MDX 数据操作的钻取
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
  
## <a name="remarks"></a>注释  
 钻取是一种操作，最终用户可通过该操作选择多维数据集中的一个单元，然后在该单元的源数据中检索结果集，以获取更加详细的信息。 默认情况下，钻取结果集来自表行（通过求值来计算选定的多维数据集单元的值）。 如果最终用户要执行钻取操作，则他们的客户端应用程序必须支持此功能。 在[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]，结果是直接从存储中检索 MOLAP，除非查询 ROLAP 分区或维度。  
  
> [!IMPORTANT]  
>  钻取安全性基于为多维数据集定义的常规安全选项。 如果无法用 MDX 获取一些数据，钻取也将以同样的方式限制用户。  
  
 MDX 语句指定了目标单元。 指定的值**最大行数**参数指示的最大应生成行集返回的行数。  
  
 默认情况下，返回的最大行数为 10000 行。 这意味着，如果你离开**最大行数**未指定，将获取 10,000 行或更少。 如果此值为对于你的方案而言太低，则可以设置**最大行数**到较大的数字，如`MAXROWS 20000`。 如果它总体得太低，则可以通过更改增加默认**OLAP\Query\DefaultDrillthroughMaxRows**服务器属性。 有关更改此属性的详细信息，请参阅[Server Properties in Analysis Services](../analysis-services/server-properties/server-properties-in-analysis-services.md)。  
  
 除非另行指定，否则返回的列包括与指定度量值的度量值组相关的所有维度（多对多维度除外）的所有粒度属性。 多维数据集维度带有 $ 前缀，以区分维度和度量值组。 **返回**子句用于指定钻取查询所返回的列。 以下函数可应用于单个属性或度量值进行**返回**子句。  
  
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
 [MDX 数据操作语句 &#40;MDX &#41;](../mdx/mdx-data-manipulation-statements-mdx.md)  
  
  

