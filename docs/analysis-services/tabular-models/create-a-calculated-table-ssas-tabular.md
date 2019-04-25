---
title: 在 Analysis Services 表格模型中创建计算的表 |Microsoft Docs
ms.date: 12/19/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 199096efcdf9212e19e1055f1276079eddfb1a75
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62469364"
---
# <a name="create-a-calculated-table"></a>创建计算的表 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  *计算表* 是一个基于 DAX 查询或表达式的计算对象，派生自相同模型中的所有或部分其他表。  
  
 计算表可以解决的常见设计问题是在特定的上下文中显示角色扮演维度，以便将其作为查询结构在客户端应用程序中公开。  你可能还记得，角色扮演维度只是出现在多个上下文中的一个表 -- 一个典型示例是 Date 表，可表示为 OrderDate、ShipDate 或 DueDate，具体取决于外键关系。 通过为 ShipDate 显式创建计算表，你可以获取一个可用于查询的独立表，该表和任何其他表一样完全可操作。 另一个用途包括配置的筛选行集、 子集或来自其他现有的表的列的超集。 这样可在保持原始表不变的同时创建该表的变体以支持特定场景。  
  
 要充分利用计算表，你至少需要知道几个 DAX 表达式。 表达式与工作表时，它可能有助于知道计算的表包含单个分区 daxsource 其中，表达式是 DAX 表达式。  
该表达式返回的每个列均有一个 CalculatedTableColumn，其中 SourceColumn 是返回的列的名称（类似于非计算表中的 DataColumn） 

可以创建计算的表之前，必须已存在至少一个表。 如果要创建计算的表作为一个单独的计算的表对象，可以从文件数据源 （csv、 xls、 xml） 导入首先创建一个表。 从导入该文件可以具有单个列和单个值。 然后，您可以隐藏该表。 
  
## <a name="how-to-create-a-calculated-table"></a>如何创建计算表  
  
1.  首先，验证表格模型具有兼容级别为 1200年或更高版本。 你可以在 SSDT 中检查模型的 **兼容性级别** 属性。  
  
2.  切换到数据视图。 不能在关系图视图中创建计算表。  
  
3.  选择“表” > “新建计算表”。  
  
4.  键入或粘贴一个 DAX 表达式（请参见以下内容获取一些想法）。  
  
5.  命名此表。  
  
6.  创建与模型中其他表之间的关系。 请参阅[创建表之间的关系两个](../../analysis-services/tabular-models/create-a-relationship-between-two-tables-ssas-tabular.md)如果需要此步骤的帮助。  
  
7.  在模型的计算或表达式中引用此表，或者在专项数据浏览中使用 **在 Excel 中分析** 。  
  
### <a name="replicate-a-role-playing-dimension"></a>复制角色扮演维度  
 在公式栏中输入 DAX 公式获取另一个表的副本。 填充计算表之后，为其提供一个描述性名称，然后设置使用特定于角色的外键的关系。 例如，在 Adventure Works 数据库中，你可以为 Due Date 创建计算表，并将 DueDateKey 用作与事实数据表的关系的基础。  
  
```  
=DimDate  
```  
  
### <a name="summarized-or-filtered-dataset"></a>已汇总或筛选的数据集  
 在公式栏中输入一个 DAX 表达式，该表达式用于筛选、汇总数据集，或者操作数据集以包含所需的行。 该示例按销售、颜色和货币进行分组。  
  
```  
=SUMMARIZECOLUMNS(DimProduct[Color]  
, DimCurrency[CurrencyName]   
, "Sales" , SUM(FactInternetSales[SalesAmount])  
)  
```  
  
### <a name="superset-using-columns-from-multiple-tables"></a>使用多个表中的列的超集  
 在公式栏中输入将来自多个表的列组合在一起的 DAX 表达式。 在此情况下，查询输出将列出每个货币的产品类别。  
  
```  
=CROSSJOIN(DimProductCategory, DimCurrency)  
```  
  
## <a name="see-also"></a>另请参阅  
 [兼容性级别](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)   
 [Analysis Services 中的数据分析表达式 (DAX)](http://msdn.microsoft.com/library/abb336c9-3346-4cab-b91b-90f93f4575e5)   
 [了解表格模型中的 DAX](../../analysis-services/tabular-models/understanding-dax-in-tabular-models-ssas-tabular.md)  
  
  
