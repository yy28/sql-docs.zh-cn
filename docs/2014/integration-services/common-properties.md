---
title: 通用属性 |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- external metadata column properties [Integration Services]
- output properties [Integration Services]
- data types [Integration Services], properties
- input properties [Integration Services]
- component properties [Integration Services]
ms.assetid: 51973502-5cc6-4125-9fce-e60fa1b7b796
caps.latest.revision: 45
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 3cf48911196d3bb96fa54a6d912fbf5a5646516f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36028425"
---
# <a name="common-properties"></a>通用属性
  [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 对象模型中的数据流对象在组件级、输入和输出级以及输入列和输出列级具有通用属性和自定义属性。 其中许多属性的值是只读的，由数据流引擎在运行时分配。  
  
 本主题列出并描述了数据流对象的通用属性。  
  
-   [组件](#components)  
  
-   [输入](#inputs)  
  
-   [Input columns](#inputcolumns)  
  
-   [输出](#outputs)  
  
-   [输出列](#outputcolumns)  
  
 有关客户属性的信息，请参阅下面的主题  
  
-   [ADO NET 自定义属性](data-flow/ado-net-custom-properties.md)  
  
-   [CDC 控制任务自定义属性](control-flow/cdc-control-task-custom-properties.md)  
  
-   [CDC 源自定义属性](data-flow/cdc-source-custom-properties.md)  
  
-   [数据挖掘模型定型目标自定义属性](data-flow/data-mining-model-training-destination-custom-properties.md)  
  
-   [DataReader 目标自定义属性](data-flow/datareader-destination-custom-properties.md)  
  
-   [维度处理目标自定义属性](data-flow/dimension-processing-destination-custom-properies.md)  
  
-   [Excel 自定义属性](data-flow/excel-custom-properties.md)  
  
-   [平面文件自定义属性](data-flow/flat-file-custom-properties.md)  
  
-   [ODBC 目标自定义属性](data-flow/odbc-destination-custom-properties.md)  
  
-   [ODBC 源自定义属性](data-flow/odbc-source-custom-properties.md)  
  
-   [OLE DB Custom Properties](data-flow/ole-db-custom-properties.md)OLE DB 自定义属性  
  
-   [分区处理目标自定义属性](data-flow/partition-processing-destination-custom-properties.md)  
  
-   [原始文件自定义属性](data-flow/raw-file-custom-properties.md)  
  
-   [记录集目标自定义属性](data-flow/recordset-destination-custom-properties.md)  
  
-   [SQL Server Compact Edition 目标自定义属性](data-flow/sql-server-compact-edition-destination-custom-properties.md)  
  
-   [SQL Server 目标自定义属性](data-flow/sql-server-destination-custom-properties.md)  
  
-   [转换自定义属性](data-flow/transformations/transformation-custom-properties.md)  
  
-   [XML 源自定义属性](data-flow/xml-source-custom-properties.md)  
  
##  <a name="components"></a> 组件属性  
 在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 对象模型中，数据流中的组件实现 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> 接口。  
  
 下表介绍了数据流中的组件的属性。 其中某些属性的值是只读的，由数据流引擎在运行时分配。  
  
|“属性”|数据类型|Description|  
|--------------|---------------|-----------------|  
|ComponentClassID|String|组件的 CLSID。|  
|ContactInfo|String|组件开发人员的联系信息。|  
|Description|String|对数据流组件的说明。 此属性的默认值是数据流组件的名称。|  
|ID|Integer|唯一标识此组件实例的值。|  
|IdentificationString|String|标识组件。|  
|IsDefaultLocale|Boolean|指示组件是否使用其所属的数据流任务的区域设置。|  
|LocaleID|Integer|包运行时数据流组件使用的区域设置。 数据流组件可以使用所有 Windows 区域设置。|  
|“属性”|String|数据流组件的名称。|  
|PipelineVersion|Integer|将某组件设计为要在其中执行的数据流任务的版本。|  
|UsesDispositions|Boolean|指示组件是否有错误输出。|  
|ValidateExternalMetadata|Boolean|指示外部列的元数据是否经过验证。 此属性的默认值是`True`。|  
|版本|Integer|组件的版本。|  
  
##  <a name="inputs"></a> 输入的属性  
 在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 对象模型中，转换和目标都具有输入。 数据流中的组件的输入实现了 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSInput100> 接口。  
  
 下表描述了数据流中的组件的输入属性。 其中某些属性的值是只读的，由数据流引擎在运行时分配。  
  
|“属性”|数据类型|Description|  
|--------------|---------------|-----------------|  
|Description|String|输入的说明。|  
|ErrorOrTruncationOperation|String|一个可选字符串，它指定处理行时可以发生的错误或截断的类型。|  
|ErrorRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|用于指定错误的处理方式的值。 值是`Fail component`， `Ignore failure`，和`Redirect row`。|  
|HasSideEffects|Boolean|指示它未附加到下游组件和时，是否可以从数据流的执行计划中删除该组件`RunInOptimizedMode`是`true`。|  
|ID|Integer|用于唯一标识输入的值。|  
|IdentificationString|String|用于标识输入的字符串。|  
|IsSorted|Boolean|指示输入中的数据是否已排序。|  
|“属性”|String|输入的名称。|  
|SourceLocale|Integer|输入数据的区域设置 ID (LCID)。|  
|TruncationRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|用于确定组件如何处理在处理行时发生的截断的值。 实例时都提供 SQL Server 登录名。 值是`Fail component`， `Ignore failure`，和`Redirect row`。|  
  
 目标以及某些转换不支持错误输出，这些组件的 ErrorRowDisposition 和 TruncationRowDisposition 属性是只读的。  
  
###  <a name="inputcolumns"></a> 输入的列属性  
 在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 对象模型中，输入包含输入列集合。 数据流中的组件的输入列实现了 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSInputColumn100> 接口。  
  
 下表描述了数据流中的组件的输入列属性。 其中某些属性的值是只读的，由数据流引擎在运行时分配。  
  
|“属性”|数据类型|Description|  
|--------------|---------------|-----------------|  
|ComparisonFlags|Integer|一组标志，用于指定数据类型为 character 的列的比较方式。 有关详细信息，请参阅 [Comparing String Data](data-flow/comparing-string-data.md)。|  
|Description|String|对输入列的说明。|  
|ErrorOrTruncationOperation|String|一个可选字符串，它指定处理行时可以发生的错误或截断的类型。|  
|ErrorRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|用于指定错误的处理方式的值。 值是`Fail component`， `Ignore failure`，和`Redirect row`。|  
|ExternalMetadataColumnID|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSExternalMetadataColumn100>|分配给输入列的外部元数据列的 ID。|  
|ID|Integer|用于唯一标识输入列的值。|  
|IdentificationString|String|用于标识输入列的字符串。|  
|LineageID|Integer|上游列的 ID。|  
|“属性”|String|输入列的名称。|  
|SortKeyPosition|Integer|用于指示单个列是否已排序、其排序顺序以及多个列的排序顺序的值。 如何值为 **0** ，则表示未对该列进行排序。  有关详细信息，请参阅 [为合并转换和合并联接转换排序数据](data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)。|  
|TruncationRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|用于确定组件如何处理在处理行时发生的截断的值。 值是`Fail component`， `Ignore failure`，和`Redirect row`。|  
|UpstreamComponentName|String|上游组件的名称。|  
|UsageType|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSUsageType>|用于确定组件如何使用输入列的值。|  
  
 输入列还具有“数据类型属性”下描述的数据类型属性。  
  
##  <a name="outputs"></a> 输出属性  
 在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 对象模型中，源和转换具有输出。 数据流中的组件的输出实现了 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100> 接口。  
  
 下表描述了数据流中的组件的输出属性。 其中某些属性的值是只读的，由数据流引擎在运行时分配。  
  
|“属性”|数据类型|Description|  
|--------------|---------------|-----------------|  
|DeleteOutputOnPathDetached|Boolean|用于确定当输出与路径分离时数据流引擎是否将其删除的值。|  
|Description|String|对输出的说明。|  
|ErrorOrTruncationOperation|String|一个可选字符串，它指定处理行时可以发生的错误或截断的类型。|  
|ErrorRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|用于指定错误的处理方式的值。 值是`Fail component`， `Ignore failure`，和`Redirect row`。|  
|ExclusionGroup|Integer|用于标识一组互斥输出的值。|  
|HasSideEffects|Boolean|用于指示当组件没有附加到上游组件并且 `RunInOptimizedMode` 为 `true` 时是否可以从数据流的执行计划中删除该组件的值。|  
|ID|Integer|用于唯一标识输出的值。|  
|IdentificationString|String|用于标识输出的字符串。|  
|IsErrorOut|Boolean|指示输出是否为错误输出。|  
|IsSorted|Boolean|指示输出是否已排序。 默认值是 `False`。<br /><br /> **\*\* 重要\* \*** 的值设置`IsSorted`属性`True`数据不排序。 此属性仅向下游组件提示数据之前已经过排序。 有关详细信息，请参阅 [为合并转换和合并联接转换排序数据](data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)。|  
|“属性”|String|输出的名称。|  
|SynchronousInputID|Integer|与输出同步的输入的 ID。|  
|TruncationRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|用于确定组件如何处理在处理行时发生的截断的值。 值是`Fail component`， `Ignore failure`，和`Redirect row`。|  
  
###  <a name="outputcolumns"></a> 输出列属性  
 在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 对象模型中，输出包含输出列集合。 数据流中的组件的输出列实现了 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputColumn100> 接口。  
  
 下表描述了数据流中的组件的输出列属性。 其中某些属性的值是只读的，由数据流引擎在运行时分配。  
  
|“属性”|数据类型|Description|  
|--------------|---------------|-----------------|  
|ComparisonFlags|Integer|一组标志，用于指定数据类型为 character 的列的比较方式。 有关详细信息，请参阅 [Comparing String Data](data-flow/comparing-string-data.md)。|  
|Description|String|对输出列的说明。|  
|ErrorOrTruncationOperation|String|一个可选字符串，它指定处理行时可以发生的错误或截断的类型。|  
|ErrorRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|用于指定错误的处理方式的值。 值是`Fail component`， `Ignore failure`，和`Redirect row`。 默认值是 `Fail component`。|  
|ExternalMetadataColumnID|Integer|分配给输入列的外部元数据列的 ID。|  
|ID|Integer|用于唯一标识输出列的值。|  
|IdentificationString|String|用于标识输出列的字符串。|  
|LineageID|Integer|输出列的 ID。 下游组件使用此值引用列。|  
|“属性”|String|输出列的名称。|  
|SortKeyPosition|Integer|用于指示单个列是否已排序、其排序顺序以及多个列的排序顺序的值。 如何值为 **0** ，则表示未对该列进行排序。 有关详细信息，请参阅 [为合并转换和合并联接转换排序数据](data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)。|  
|SpecialFlags|Integer|包含输出列的特殊标志的值。|  
|TruncationRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|用于确定组件如何处理在处理行时发生的截断的值。 值是`Fail component`， `Ignore failure`，和`Redirect row`。 默认值是 `Fail component`。|  
  
 输出列还包括一组数据类型属性。  
  
## <a name="external-metadata-column-properties"></a>外部元数据列属性  
 在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 对象模型中，输入和输出可以包含一组外部元数据列。 数据流中的组件的外部元数据列实现了 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSExternalMetadataColumn100> 接口。  
  
 下表描述了数据流中的组件的外部元数据列属性。 其中某些属性的值是只读的，由数据流引擎在运行时分配。  
  
|“属性”|数据类型|Description|  
|--------------|---------------|-----------------|  
|Description|String|对外部列的说明。|  
|ID|Integer|用于唯一标识列的值。|  
|IdentificationString|String|用于标识列的字符串。|  
|“属性”|String|外部列的名称。|  
  
 外部元数据列还包括一组数据类型属性。  
  
## <a name="data-type-properties"></a>数据类型属性  
 输出列和外部元数据列还包括一组数据类型属性。 这些属性可能为读/写属性或只读属性，具体取决于列的数据类型。  
  
 下表描述了输出列和外部元数据列的数据类型属性。  
  
|“属性”|数据类型|Description|  
|--------------|---------------|-----------------|  
|CodePage|Integer|指定非 Unicode 字符串数据的代码页。|  
|DataType|Integer（枚举）|列的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 数据类型。 有关详细信息，请参阅 [Integration Services 数据类型](data-flow/integration-services-data-types.md)。|  
|长度|Integer|以字符计的列的长度。|  
|精度|Integer|数字列的精度。|  
|小数位数|Integer|数字列的小数位数。|  
  
## <a name="see-also"></a>请参阅  
 [数据流](data-flow/data-flow.md)   
 [转换自定义属性](data-flow/transformations/transformation-custom-properties.md)   
 [路径属性](../../2014/integration-services/path-properties.md)   
 [可以使用表达式设置的数据流属性](../../2014/integration-services/data-flow-properties-that-can-be-set-by-using-expressions.md)  
  
  