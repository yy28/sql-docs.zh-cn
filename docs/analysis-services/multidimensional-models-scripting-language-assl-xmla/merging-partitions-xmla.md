---
title: "合并分区 (XMLA) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- merging partitions [XMLA]
- XMLA, partitions
- partitions [Analysis Services], XML for Analysis
- XML for Analysis, partitions
ms.assetid: 657e1d4d-6d50-40f8-a771-7b20c9d865f8
caps.latest.revision: "14"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 90d92549184a5dc3a93123a86870d3905f38791a
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="merging-partitions-xmla"></a>合并分区 (XMLA)
  如果分区具有相同的聚合设计和结构，你可以通过使用合并分区[MergePartitions](../../analysis-services/xmla/xml-elements-commands/mergepartitions-element-xmla.md) XML Analysis (XMLA) 命令。 合并分区是将在管理分区时执行的一项重要操作，特别是那些包含按日期分区的历史数据的分区。  
  
 例如，财务多维数据集可以使用两个分区：  
  
-   一个分区表示当年的财务数据，使用实时关系 OLAP (ROLAP) 存储设置改善性能。  
  
-   另一个分区包含以往年度的财务数据，使用多维 OLAP (MOLAP) 存储设置进行存储。  
  
 这两个分区使用不同的存储设置，但使用相同的聚合设计。 而不是处理多维数据集分布年的历史数据年份的末尾，则可以使用**MergePartitions**命令来合并分区为当前的年分区上一年。 这样将保留聚合数据，而不需要对多维数据集进行潜在耗时的完全处理。  
  
## <a name="specifying-partitions-to-merge"></a>指定要合并的分区  
 当**MergePartitions**命令运行时，存储在中指定的源分区的聚合数据[源](../../analysis-services/xmla/xml-elements-properties/source-element-xmla.md)属性添加到目标分区中指定[目标](../../analysis-services/xmla/xml-elements-properties/target-element-xmla.md)属性。  
  
> [!NOTE]  
>  **源**属性可以包含多个分区对象引用。 但是，**目标**属性不能。  
  
 要成功合并中同时, 指定分区**源**和**目标**必须包含相同的度量值组和使用相同的聚合设计。 否则，将会出错。  
  
 在指定的分区**源**后删除**MergePartitions**命令成功完成。  
  
## <a name="examples"></a>示例  
  
### <a name="description"></a>Description  
 下面的示例合并中的所有分区**客户计数**的度量值组**Adventure Works**多维数据集内**Adventure Works DW**示例[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]数据库分成**Customers_2004**分区。  
  
### <a name="code"></a>代码  
  
```  
<MergePartitions xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
  <Sources>  
    <Source>  
      <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
      <CubeID>Adventure Works DW</CubeID>  
      <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>  
      <PartitionID>Internet_Sales_2001</PartitionID>  
    </Source>  
    <Source>  
      <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
      <CubeID>Adventure Works DW</CubeID>  
      <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>  
      <PartitionID>Internet_Sales_2002</PartitionID>  
    </Source>  
    <Source>  
      <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
      <CubeID>Adventure Works DW</CubeID>  
      <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>  
      <PartitionID>Internet_Sales_2003</PartitionID>  
    </Source>  
  </Sources>  
  <Target>  
    <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
    <CubeID>Adventure Works DW</CubeID>  
    <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>  
    <PartitionID>Internet_Sales_2004</PartitionID>  
  </Target>  
</MergePartitions>  
```  
  
## <a name="see-also"></a>另请参阅  
 [在 Analysis Services 中使用 XMLA 开发](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
