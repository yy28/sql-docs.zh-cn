---
title: 合并分区 (XMLA) |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 419ebd0d67b65213fde7393430aedec14249b2ae
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63261640"
---
# <a name="merging-partitions-xmla"></a>合并分区 (XMLA)
  如果分区具有相同的聚合设计和结构，你可以通过使用合并分区[MergePartitions](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/mergepartitions-element-xmla)命令 XML for Analysis (XMLA) 中。 合并分区是将在管理分区时执行的一项重要操作，特别是那些包含按日期分区的历史数据的分区。  
  
 例如，财务多维数据集可以使用两个分区：  
  
-   一个分区表示当年的财务数据，使用实时关系 OLAP (ROLAP) 存储设置改善性能。  
  
-   另一个分区包含以往年度的财务数据，使用多维 OLAP (MOLAP) 存储设置进行存储。  
  
 这两个分区使用不同的存储设置，但使用相同的聚合设计。 而不是所有年度的历史数据的年度末处理多维数据集，则可以使用**MergePartitions**命令来合并分区当年的分区上一年。 这样将保留聚合数据，而不需要对多维数据集进行潜在耗时的完全处理。  
  
## <a name="specifying-partitions-to-merge"></a>指定要合并的分区  
 当**MergePartitions**命令运行时，存储在中指定的源分区的聚合数据[源](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/source-element-xmla)属性添加到中指定的目标分区[目标](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/target-element-xmla)属性。  
  
> [!NOTE]  
>  **源**属性可以包含多个分区对象引用。 但是，**目标**属性不能。  
  
 若要成功合并，在这种指定的分区**源**并**目标**必须包含相同的度量值组，并使用相同的聚合设计。 否则，将会出错。  
  
 中指定的分区**源**后删除**MergePartitions**命令已成功完成。  
  
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
  
## <a name="see-also"></a>请参阅  
 [在 Analysis Services 中使用 XMLA 开发](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
