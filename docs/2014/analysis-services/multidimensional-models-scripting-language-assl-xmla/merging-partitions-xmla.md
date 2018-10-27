---
title: 合并分区 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- merging partitions [XMLA]
- XMLA, partitions
- partitions [Analysis Services], XML for Analysis
- XML for Analysis, partitions
ms.assetid: 657e1d4d-6d50-40f8-a771-7b20c9d865f8
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c459fcb3efc86566eef046df30d2d8ad9ea601b4
ms.sourcegitcommit: 7fe14c61083684dc576d88377e32e2fc315b7107
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/26/2018
ms.locfileid: "50145835"
---
# <a name="merging-partitions-xmla"></a>合并分区 (XMLA)
  如果分区具有相同的聚合设计和结构，你可以通过使用合并分区[MergePartitions](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/mergepartitions-element-xmla)命令 XML for Analysis (XMLA) 中。 合并分区是将在管理分区时执行的一项重要操作，特别是那些包含按日期分区的历史数据的分区。  
  
 例如，财务多维数据集可以使用两个分区：  
  
-   一个分区表示当年的财务数据，使用实时关系 OLAP (ROLAP) 存储设置改善性能。  
  
-   另一个分区包含以往年度的财务数据，使用多维 OLAP (MOLAP) 存储设置进行存储。  
  
 这两个分区使用不同的存储设置，但使用相同的聚合设计。 除了在年末处理所有年度的历史数据的多维数据集，还可以使用 `MergePartitions` 命令将当年的分区合并到以往年度的分区。 这样将保留聚合数据，而不需要对多维数据集进行潜在耗时的完全处理。  
  
## <a name="specifying-partitions-to-merge"></a>指定要合并的分区  
 当`MergePartitions`运行的命令中指定的源分区中存储的聚合数据[源](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/source-element-xmla)属性添加到中指定的目标分区[目标](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/target-element-xmla)属性。  
  
> [!NOTE]  
>  `Source` 属性可包含多个分区对象引用。 但是，`Target` 属性则没有此功能。  
  
 若要成功合并，在 `Source` 和 `Target` 中指定的分区必须包含在相同的度量值组，并使用相同的聚合设计。 否则，将会出错。  
  
 在 `Source` 中指定的分区将在成功执行 `MergePartitions` 命令后删除。  
  
## <a name="examples"></a>示例  
  
### <a name="description"></a>Description  
 下面的示例合并中的所有分区**Customer Counts**的度量值组**Adventure Works**多维数据集内**Adventure Works DW**示例[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]数据库分成**Customers_2004**分区。  
  
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
 [在 Analysis Services 中使用 XMLA 开发](developing-with-xmla-in-analysis-services.md)  
  
  
