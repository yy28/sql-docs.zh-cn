---
title: 处理对象 (XMLA) |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 58150b6b74fd3a58fb09f44818b724214a64b8b6
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="processing-objects-xmla"></a>处理对象 (XMLA)
  在[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]、 处理是步骤或系列的指导将数据转换进行业务分析的信息。 处理因对象类型而异，但处理始终是将数据转换为信息的一个环节。  
  
 到进程[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]对象时，可以使用[过程](../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md)命令。 **过程**命令可以处理以下对象上[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]实例：  
  
-   多维数据集  
  
-   “数据库”  
  
-   维度  
  
-   度量值组  
  
-   挖掘模型  
  
-   挖掘结构  
  
-   分区  
  
 若要控制处理的对象，**过程**命令具有可以设置的各种属性。 **过程**命令具有控制属性： 将执行多少处理、 将处理哪些对象、 是否使用的外部绑定、 如何处理错误，以及如何管理写回表。  
  
## <a name="specifying-processing-options"></a>指定处理选项  
 [类型](../../analysis-services/xmla/xml-elements-properties/type-element-xmla.md)属性**过程**命令指定要处理对象时使用的处理选项。 有关处理选项的详细信息，请参阅[处理选项和设置 (Analysis Services)](../../analysis-services/multidimensional-models/processing-options-and-settings-analysis-services.md)。  
  
 下表列出的常量**类型**属性，可以使用每个常量处理的各种对象。  
  
|**类型**值|适用对象|  
|--------------------|------------------------|  
|*ProcessFull*|多维数据集、数据库、维度、度量值组、挖掘模型、挖掘结构和分区|  
|*ProcessAdd*|维度和分区|  
|*ProcessUpdate*|维度|  
|*ProcessIndexes*|维度、多维数据集、度量值组和分区|  
|*ProcessData*|维度、多维数据集、度量值组和分区|  
|*ProcessDefault*|多维数据集、数据库、维度、度量值组、挖掘模型、挖掘结构和分区|  
|*ProcessClear*|多维数据集、数据库、维度、度量值组、挖掘模型、挖掘结构和分区|  
|*ProcessStructure*|多维数据集和挖掘结构|  
|*ProcessClearStructureOnly*|挖掘结构|  
|*ProcessScriptCache*|多维数据集|  
  
 有关处理的详细信息[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]对象，请参阅[处理多维模型&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md)。  
  
## <a name="specifying-objects-to-be-processed"></a>指定要处理的对象  
 [对象](../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md)属性**过程**命令包含要处理的对象的对象标识符。 可以在指定只有一个对象**过程**命令，但处理的对象还将处理任何子对象。 例如，在处理多维数据集中的一个度量值组时会处理该度量值组的所有分区；在处理一个数据库时会处理该数据库所包含的所有对象，包括多维数据集、维度和挖掘结构。  
  
 如果你设置**ProcessAffectedObjects**属性**过程**命令为 true，任何相关还处理受处理指定的对象的对象。 例如，如果通过使用增量更新维度*ProcessUpdate*处理中的选项**过程**命令时，其聚合失效因为成员任何分区正在添加或删除由还处理[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]如果**ProcessAffectedObjects**设置为 true。 在这种情况下，单个**过程**命令可以处理多个对象上[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]实例，但[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]确定哪些对象中指定的单个对象除了**过程**此外必须处理命令。  
  
 但是，你可以通过使用多个同时处理多个对象，例如维度，**过程**内的命令**批处理**命令。 批处理操作上的对象的串行或并行处理提供更精细的控制级别[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]比使用实例**ProcessAffectedObjects**属性，并让你调整为你处理方法更大[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]数据库。 有关执行批处理操作的详细信息，请参阅[执行批处理操作&#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/performing-batch-operations-xmla.md)。  
  
## <a name="specifying-out-of-line-bindings"></a>指定外部绑定  
 如果**过程**命令不包含的**批处理**命令，可以选择指定的外部绑定中[绑定](../../analysis-services/xmla/xml-elements-properties/bindings-element-xmla.md)，[数据源](../../analysis-services/xmla/xml-elements-properties/datasource-element-xmla.md)，和[DataSourceView](../../analysis-services/xmla/xml-elements-properties/datasourceview-element-xmla.md)属性**过程**命令为要处理的对象。 外部绑定是对数据源、 数据源视图和其他绑定仅在执行过程中存在的对象的引用**过程**的命令，并且其重写与关联的任何现有绑定正在处理的对象。 如果未指定外部绑定，则使用当前与要处理的对象关联的绑定。  
  
 外部绑定用在以下情况下：  
  
-   增量处理一个分区，其中必须指定另一个事实数据表或现有事实数据表上的一个筛选器以确保不会对行进行两次计数。  
  
-   使用在数据流任务[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]在处理维度、 挖掘模型或分区时提供数据。  
  
 外部绑定属于 Analysis Services 脚本语言 (ASSL) 的一部分。 有关在 ASSL 中的外部绑定的详细信息，请参阅[数据源和绑定&#40;SSAS 多维&#41;](../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md)。  
  
### <a name="incrementally-updating-partitions"></a>增量更新分区  
 增量更新已处理的分区时通常需要外部绑定，原因在于为该分区指定的绑定会引用已在该分区中聚合的事实数据表数据。 通过使用以增量方式更新已处理的分区时**过程**命令，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]执行下列操作：  
  
-   创建一个与要增量更新的分区具有相同结构的临时分区。  
  
-   处理临时分区，使用的外部绑定中指定**过程**命令。  
  
-   将该临时分区与所选现有分区合并。  
  
 有关合并分区使用的 Analysis (XMLA) 的 XML 的详细信息，请参阅[合并分区&#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/merging-partitions-xmla.md)。  
  
## <a name="handling-processing-errors"></a>对处理错误进行处理  
 [ErrorConfiguration](../../analysis-services/xmla/xml-elements-properties/errorconfiguration-element-xmla.md)属性**过程**命令允许你指定如何处理处理的对象时遇到错误。 例如，在处理维度时，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 在键属性的键列中遇到重复的值。 因为属性键必须是唯一的，因此 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 丢弃重复的记录。 基于[KeyDuplicate](../../analysis-services/scripting/properties/keyduplicate-element-assl.md)属性**ErrorConfiguration**，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]无法：  
  
-   忽略错误并继续处理该维度。  
  
-   返回说明 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 遇到了重复键的消息并继续处理。  
  
 有许多相似条件为其**ErrorConfiguration**提供期间选项**过程**命令。  
  
## <a name="managing-writeback-tables"></a>管理写回表  
 如果**过程**命令遇到写入的分区或对于此类的分区，不已完全处理的多维数据集或度量值组、 一个写回表可能不存在为该分区。 [WritebackTableCreation](../../analysis-services/xmla/xml-elements-properties/writebacktablecreation-element-xmla.md)属性**过程**命令确定是否[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]应创建一个写回表。  
  
## <a name="examples"></a>示例  
  
### <a name="description"></a>Description  
 下面的示例对 [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] 示例 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库进行完整处理。  
  
### <a name="code"></a>代码  
  
```  
<Process xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
  <Object>  
    <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
  </Object>  
  <Type>ProcessFull</Type>  
  <WriteBackTableCreation>UseExisting</WriteBackTableCreation>  
</Process>  
```  
  
### <a name="description"></a>Description  
 下面的示例以增量方式处理**Internet_Sales_2004**分区中**Internet Sales**的度量值组**Adventure Works DW** 中的多维数据集[!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)]示例[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]数据库。 **过程**命令聚合订单日期晚于 2006 年 12 月 31 日使用添加到分区中的外部查询绑定**绑定**属性**过程**命令以检索从其生成聚合将添加到分区的事实表行。  
  
### <a name="code"></a>代码  
  
```  
<Process ProcessAffectedObjects="true" xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
  <Object>  
    <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
    <CubeID>Adventure Works DW</CubeID>  
    <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>  
    <PartitionID>Internet_Sales_2006</PartitionID>  
  </Object>  
  <Bindings>  
    <Binding>  
      <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
      <CubeID>Adventure Works DW</CubeID>  
      <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>  
      <PartitionID>Internet_Sales_2006</PartitionID>  
      <Source xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="QueryBinding">  
        <DataSourceID>Adventure Works DW</DataSourceID>  
        <QueryDefinition>  
          SELECT  
            [dbo].[FactInternetSales].[ProductKey],  
            [dbo].[FactInternetSales].[OrderDateKey],  
            [dbo].[FactInternetSales].[DueDateKey],  
            [dbo].[FactInternetSales].[ShipDateKey],   
            [dbo].[FactInternetSales].[CustomerKey],   
            [dbo].[FactInternetSales].[PromotionKey],  
            [dbo].[FactInternetSales].[CurrencyKey],  
            [dbo].[FactInternetSales].[SalesTerritoryKey],  
            [dbo].[FactInternetSales].[SalesOrderNumber],  
            [dbo].[FactInternetSales].[SalesOrderLineNumber],  
            [dbo].[FactInternetSales].[RevisionNumber],  
            [dbo].[FactInternetSales].[OrderQuantity],  
            [dbo].[FactInternetSales].[UnitPrice],  
            [dbo].[FactInternetSales].[ExtendedAmount],  
            [dbo].[FactInternetSales].[UnitPriceDiscountPct],  
            [dbo].[FactInternetSales].[DiscountAmount],  
            [dbo].[FactInternetSales].[ProductStandardCost],  
            [dbo].[FactInternetSales].[TotalProductCost],  
            [dbo].[FactInternetSales].[SalesAmount],  
            [dbo].[FactInternetSales].[TaxAmt],  
            [dbo].[FactInternetSales].[Freight],  
            [dbo].[FactInternetSales].[CarrierTrackingNumber],  
            [dbo].[FactInternetSales].[CustomerPONumber]  
          FROM [dbo].[FactInternetSales]  
          WHERE OrderDateKey > '1280'  
        </QueryDefinition>  
      </Source>  
    </Binding>  
  </Bindings>  
  <Type>ProcessAdd</Type>  
  <WriteBackTableCreation>UseExisting</WriteBackTableCreation>  
</Process>  
```  
  
  
