---
title: 支持的 XMLA 属性 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- properties [XML for Analysis]
- XML for Analysis, properties
- XMLA, properties
ms.assetid: 5745f7b4-6b96-44d5-b77c-f2831a898e5e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7d7898c0f7263bf5355934ec072511bfd8483028
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48215917"
---
# <a name="supported-xmla-properties-xmla"></a>支持的 XMLA 属性 (XMLA)
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 支持下表中列出的属性。 使用这些列出的属性中[属性](properties-element-xmla.md)的元素[Discover](../xml-elements-methods-discover.md)并[Execute](../xml-elements-methods-execute.md)方法。  
  
|“属性”|元素|  
|----------|-------------|  
|AxisFormat|*用法*<br /> 可选的只写`String`属性<br /><br /> *说明*<br /> 确定使用的格式[MDDataSet](../xml-data-types/mddataset-data-type-xmla.md)结果设置为描述多维数据集中的轴。 此属性的值可以为下表中所列出的值。|  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|*ClusterFormat*|`MDDataSet`轴由一个或多个[CrossProduct](crossproduct-element-xmla.md)元素。|  
|*CustomFormat*|[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 使用*TupleFormat*为此设置的格式。|  
|*TupleFormat*|（默认值）`MDDataSet`轴包含一个或多个[元组](tuple-element-xmla.md)元素。|  
  
 此属性可以用于 `Execute` 方法。  
  
|“属性”|元素|  
|----------|-------------|  
|BeginRange|*用法*<br /> 可选的只写`Integer`属性<br /><br /> *说明*<br /> 包含一个与 `CellOrdinal` 属性值相对应的、从零开始的整数值。 (`CellOrdinal`属性属于[单元格](cell-element-mddataset-xmla.md)中的元素[CellData](celldata-element-xmla.md)一部分`MDDataSet`。)<br /><br /> 客户端应用程序可以综合使用 `EndRange` 属性和此属性，将命令返回的 OLAP 数据集限制在特定单元范围内。 如果指定为 -1，则将返回最大为 `EndRange` 属性所指定单元的所有单元。<br /><br /> 此属性的默认值为-1。<br /><br /> 此属性可以用于 `Execute` 方法。|  
|目录|*用法*<br /> 可选，读/写`String`属性<br /><br /> *说明*<br /> 为发送 XMLA 命令而与 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例建立会话时，此属性与 OLE DB 属性 DBPROP_INIT_CATALOG 等效。<br /><br /> 在会话期间，为更改会话的当前数据库而设置此属性时，此属性与 OLE DB 属性 DBPROP_CURRENTCATALOG 等效。<br /><br /> 此属性的默认值为空字符串。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。|  
|CatalogLocation|*用法*<br /> 可选的只读`Integer`属性<br /><br /> *说明*<br /> 此属性与 OLE DB 属性 DBPROP_CATALOGLOCATION 等效。<br /><br /> 此属性的默认值为零 (0)，与 DBPROPVAL_CL_START 等效。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。|  
|ClientProcessID|*用法*<br /> 可选，读/写`Integer`属性<br /><br /> *说明*<br /> 包含当前会话的进程线程的标识符 (ID)。<br /><br /> 此属性的默认值为零 (0)。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。|  
|CommitTimeout|*用法*<br /> 可选的只写`Integer`属性<br /><br /> *说明*<br /> 确定当前正在运行的 XMLA 命令在进行回滚前需要等待的提交阶段的时间（秒）。 提交阶段与 XMLA 命令如对应[语句](../xml-elements-commands/statement-element-xmla.md)或[进程](../xml-elements-commands/process-element-xmla.md)。<br /><br /> 零值 (0) 指示实例要无限期等待。<br /><br /> 此属性的默认值为零 (0)。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。|  
|内容|*用法*<br /> 可选的只写`String`属性<br /><br /> *说明*<br /> 确定从 `Discover` 和 `Execute` 方法返回的数据的类型。 此属性的值可以为下表中所列出的值。|  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|*无*|允许验证命令结构，但不运行命令。|  
|*架构*|返回与请求的命令相关的 XML 架构。 XML 架构指示列和其他信息。|  
|*数据*|仅返回请求的数据。|  
|*SchemaData*|（默认值）返回架构信息和数据。|  
  
 此属性可以用于 `Discover` 和 `Execute` 方法。  
  
|“属性”|元素|  
|----------|-------------|  
|多维数据集|*用法*<br /> 可选的只写`String`属性<br /><br /> *说明*<br /> 包含用于设置命令的上下文的多维数据集的名称。 如果命令本身的 FROM 子句的多维表达式 (MDX) 中包含一个多维数据集的名称，如[选择](/sql/mdx/mdx-data-manipulation-select)语句，此属性的设置将被忽略。<br /><br /> 此属性的默认值为空字符串。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。|  
|DataSourceInfo|*用法*<br /> 必需，读/写 `String` 属性<br /><br /> *说明*<br /> 包含连接到数据源要用到的信息，如实例名称。<br /><br /> 客户端应用程序不应构造要发送到实例的 `DataSourceInfo` 属性的内容。 相反，客户端应用程序应查找的提供程序通过使用支持的数据源`Discover`方法来检索[DISCOVER_DATASOURCES](../../schema-rowsets/xml/discover-datasources-rowset.md)行集。 然后，客户端应用程序将再从 DISCOVER_DATASOURCES 行集检索到的同一 `DataSourceInfo` 属性值发回。<br /><br /> 此属性无默认值。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。|  
|DbpropCatalogTerm|*用法*<br /> 可选的只读`String`属性<br /><br /> *说明*<br /> 此属性与 OLE DB 属性 DBPROP_CATALOGTERM 等效。<br /><br /> 此属性的默认值为“Database”。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。|  
|DbpropCatalogUsage|*用法*<br /> 可选的只读`Integer`属性<br /><br /> *说明*<br /> 此属性与 OLE DB 属性 DBPROP_CATALOGUSAGE 等效。<br /><br /> 此属性的默认值为零 (0)。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。|  
|DbpropColumnDefinition|*用法*<br /> 可选的只读`Integer`属性<br /><br /> *说明*<br /> 此属性与 OLE DB 属性 DBPROP_COLUMNDEFINITION 等效。<br /><br /> 此属性的默认值为零 (0)。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。|  
|DbpropConcatNullBehavior|*用法*<br /> 可选的只读`Integer`属性<br /><br /> *说明*<br /> 此属性与 OLE DB 属性 DBPROP_CONCATNULLBEHAVIOR 等效。<br /><br /> 此属性的默认值为 1，与 DBPROPVAL_CB_NULL 等效。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。|  
|DbpropDataSourceReadOnly|*用法*<br /> 可选的只读`Boolean`属性<br /><br /> *说明*<br /> 此属性与 OLE DB 属性 DBPROP_DATASOURCEREADONLY 等效。<br /><br /> 此属性的默认值是 FALSE。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。|  
|DbpropGroupBy|*用法*<br /> 可选的只读`Integer`属性<br /><br /> *说明*<br /> 此属性与 OLE DB 属性 DBPROP_GROUPBY 等效。<br /><br /> 此属性的默认值为 2，与 DBPROPVAL_GB_EQUALS_SELECT 等效。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。|  
|DbpropHeterogeneousTables|*用法*<br /> 可选的只读`Integer`属性<br /><br /> *说明*<br /> 此属性与 OLE DB 属性 DBPROP_HETEROGENEOUSTABLES 等效。<br /><br /> 此属性的默认值为零 (0)。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。|  
|DbpropIdentifierCase|*用法*<br /> 可选的只读`Integer`属性<br /><br /> *说明*<br /> 此属性与 OLE DB 属性 DBPROP_IDENTIFIERCASE 等效。<br /><br /> 此属性的默认值为 8，与 DBPROPVAL_IC_MIXED 等效。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。|  
|DbpropInitMode|*用法*<br /> 可选，读/写`Integer`属性<br /><br /> *说明*<br /> 此属性与 OLE DB 属性 DBPROP_INIT_MODE 等效。<br /><br /> 此属性仅支持值 DB_MODE_READWRITE 和 DB_MODE_READ。<br /><br /> 此属性无默认值。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。|  
|DbpropMaxIndexSize|*用法*<br /> 可选的只读`Integer`属性<br /><br /> *说明*<br /> 此属性与 OLE DB 属性 DBPROP_MAXINDEXSIZE 等效。<br /><br /> 此属性的默认值为零 (0)。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。|  
|DbpropMaxOpenChapters|*用法*<br /> 可选的只读`Integer`属性<br /><br /> *说明*<br /> 此属性与 OLE DB 属性 DBPROP_MAXOPENCHAPTERS 等效。<br /><br /> 此属性的默认值为零 (0)。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。|  
|DbpropMaxRowSize|*用法*<br /> 可选的只读`Integer`属性<br /><br /> *说明*<br /> 此属性与 OLE DB 属性 DBPROP_MAXROWSIZE 等效。<br /><br /> 此属性的默认值为零 (0)。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。|  
|DbpropMaxRowSizeIncludeBlob|*用法*<br /> 可选，只读 `Boolean` 属性<br /><br /> *说明*<br /> 此属性与 OLE DB 属性 DBPROP_MAXROWSIZEINCLUDESBLOB 等效。<br /><br /> 此属性的默认值为 TRUE。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。|  
|DbpropMaxTablesInSelect|*用法*<br /> 可选的只读`Integer`属性<br /><br /> *说明*<br /> 此属性与 OLE DB 属性 DBPROP_MAXTABLESINSELECT 等效。<br /><br /> 此属性的默认值为 1。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。|  
|DbpropMsmdAutoexists|*用法*<br /> 可选，读/写`Integer`属性<br /><br /> *说明*<br /> 确定 autoexists 的行为。 此属性的值可以为下表中所列出的值。|  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|*0*|默认值，与 1 相同。|  
|*1*|对查询轴和命名集应用深度 autoexists。 包括 WHERE 子句和嵌套 select。|  
|*2*|对查询轴应用深度 autoexists，从 autoexists 中排除命名集。 包括 WHERE 子句和嵌套 select。|  
|*3*|对带 WHERE 子句的命名集不应用 autoexists。 对带 WHERE 子句的查询轴应用浅表 autoexists。 对带嵌套 select 的查询轴和带嵌套 select 的命名集应用深度 autoexists。|  
  
 此属性的默认值为零或空。 这是一个会话属性，仅在创建会话时可以设置。  
  
|“属性”|元素|  
|----------|-------------|  
|DbpropMsmdCacheMode|*用法*<br /> 可选，读/写`Integer`属性<br /><br /> *说明*<br /> 保留供将来使用。<br /><br /> 此属性无默认值。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。|  
|DbpropMsmdCachePolicy|*用法*<br /> 可选，读/写`Integer`属性<br /><br /> *说明*<br /> 保留供将来使用。<br /><br /> 此属性无默认值。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。|  
|DbpropMsmdCacheRatio|*用法*<br /> 可选，读/写`Integer`属性<br /><br /> *说明*<br /> 保留供将来使用。<br /><br /> 此属性无默认值。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。|  
|DbpropMsmdCacheRatio2|*用法*<br /> 可选，读/写`Double`属性<br /><br /> *说明*<br /> 保留供将来使用。<br /><br /> 此属性无默认值。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。|  
|DbpropMsmdCompareCaseNotSensitiveStringFlags|*用法*<br /> 可选，读/写 `Integer` 属性<br /><br /> *说明*<br /> 确定区分大小写的字符串的比较和排序功能。 此属性可以控制不支持大写字符和小写字符的字符集中的比较方式，如对于日语的片假名和印地语。 此属性的值在进程线程第一个连接中设置，会影响该进程线程中的所有后续连接。<br /><br /> 使用下表可以确定要使用的标志。|  
  
|“属性”|ReplTest1|Description|  
|----------|-----------|-----------------|  
|NORM_IGNORECASE|*0x00000001*|忽略大小写。|  
|不适用|*0x00000002*|二进制比较。 在字符集中，字符是按照其基础值进行比较的，而不是按照其特定的字符顺序进行比较。|  
|NORM_IGNORENONSPACE|*0x00000010*|忽略非空格字符。|  
|NORM_IGNORESYMBOLS|*0x00000100*|忽略符号。|  
|NORM_IGNOREKANATYPE|*0x00001000*|不区分平假名字符和片假名字符。 比较时，相应的平假名和片假名字符视为等效。|  
|NORM_IGNOREWIDTH|*0x00010000*|不区分同一字符的单字节格式和双字节格式。|  
|SORT_STRINGSORT|*0x00100000*|标点与符号同等对待。|  
  
 有关 OLE DB 中字符串比较的详细信息，请在 MSDN Library 的 Platform SDK 部分中对“CompareString”进行搜索。  
  
 此属性无默认值。  
  
 此属性可以用于 `Discover` 和 `Execute` 方法。  
  
|“属性”|元素|  
|----------|-------------|  
|DbpropMsmdCompareCaseSensitiveStringFlags|*用法*<br /> 可选，读/写`Integer`属性<br /><br /> *说明*<br /> 确定不区分大小写的字符串的比较和排序功能。 此属性可以控制不支持大写字符和小写字符的字符集中的比较方式，如对于日语的片假名和印地语。 此属性的值在进程线程第一个连接中设置，会影响该进程线程中的所有后续连接。<br /><br /> 使用下表可以确定要使用的标志。|  
  
|“属性”|ReplTest1|Description|  
|----------|-----------|-----------------|  
|NORM_IGNORECASE|*0x00000001*|忽略大小写。|  
|不适用|*0x00000002*|二进制比较。 在字符集中，字符是按照其基础值进行比较的，而不是按照其特定的字符顺序进行比较。|  
|NORM_IGNORENONSPACE|*0x00000010*|忽略非空格字符。|  
|NORM_IGNORESYMBOLS|*0x00000100*|忽略符号。|  
|NORM_IGNOREKANATYPE|*0x00001000*|不区分平假名字符和片假名字符。 比较时，相应的平假名和片假名字符视为等效。|  
|NORM_IGNOREWIDTH|*0x00010000*|不区分同一字符的单字节格式和双字节格式。|  
|SORT_STRINGSORT|*0x00100000*|标点与符号同等对待。|  
  
 有关 OLE DB 中字符串比较的详细信息，请在 MSDN Library 的 Platform SDK 部分中对“CompareString”进行搜索。  
  
 此属性无默认值。  
  
 此属性可以用于 `Discover` 和 `Execute` 方法。  
  
|“属性”|元素|  
|----------|-------------|  
|DbpropMsmdDebugMode|*用法*<br /> 可选，读/写`String`属性<br /><br /> *说明*<br /> 保留供将来使用。<br /><br /> 此属性无默认值。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。|  
|DbpropMsmdDynamicDebugLimit|*用法*<br /> 可选，读/写`Integer`属性<br /><br /> *说明*<br /> 保留供将来使用。<br /><br /> 此属性无默认值。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。|  
|DbpropMsmdFlattened2|*用法*<br /> 可选，读/写`Boolean`属性<br /><br /> *说明*<br /> 除非轴 0 上需要父子层次结构，否则在简化结果中输出单个表列中父子层次结构的所有成员。 不使用输出列的级别模板。<br /><br /> 此属性的默认值是 FALSE。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。|  
|DbpropMsmdMDXCompatibility|*用法*<br /> 可选，读/写`Integer`属性<br /><br /> *说明*<br /> 确定如何处理不规则或不对称层次结构中的占位符成员。 此属性的值可以为下表中所列出的值。|  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|*0*|为了与 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 的早期版本相兼容，此值与 1 等效。|  
|*1*|角色扮演维度中的层次结构可以接收包含维度名称和层次结构名称的标题。 该标题的格式如下；<br /><br /> [Dimension].[Hierarchy]<br /><br /> 公开占位符成员。|  
|*2*|角色扮演维度中的层次结构可以接收包含维度名称和层次结构名称的标题，该标题的格式如下：<br /><br /> [Dimension].[Hierarchy]<br /><br /> 不公开占位符成员。|  
|*3*|（默认值）不公开占位符成员。|  
  
 此属性可以用于 `Discover` 和 `Execute` 方法。  
  
|“属性”|元素|  
|----------|-------------|  
|DbpropMsmdMDXUniqueNameStyle|*用法*<br /> 可选，读/写`Integer`属性<br /><br /> *说明*<br /> 确定用于在维度中生成成员的唯一名称的算法。 此属性的值可以为下表中所列出的值。<br /><br /> 此属性的默认值为 6。|  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|*0*|为了与 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 的早期版本相兼容，此值与 2 等效。|  
|*1*|使用项路径算法：<br /><br /> [dim].&[key1].&[key2]|  
|*2*|使用名称路径算法：<br /><br /> [dim].[name1].&[name2]|  
|*3*|使用可长期保证稳定的唯一名称。|  
  
 此属性可以用于 `Discover` 和 `Execute` 方法。  
  
|“属性”|元素|  
|----------|-------------|  
|DbpropMsmdSQLCompatibility|*用法*<br /> 可选，读/写`Integer`属性<br /><br /> *说明*<br /> 保留供将来使用。<br /><br /> 此属性的默认值为零 (0)。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。|  
|DbpropMsmdSubQueries|*用法*<br /> 可选，读/写`Integer`属性<br /><br /> *说明*<br /> 确定子查询行为的位掩码。 此属性的值可以为下表中所列出的值。|  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|*0*|默认值，与 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 的早期版本兼容。<br /><br /> 计算成员或计算集不允许在嵌套 select 语句或子多维数据集中使用。|  
|*1*|计算成员或计算集允许在嵌套 select 语句或子多维数据集中使用。 计算成员的祖先不包括在嵌套 select 语句或子多维数据集的空间中。|  
|*2*|计算成员或计算集允许在嵌套 select 语句或子多维数据集中使用。 计算成员的祖先包括在嵌套 select 语句或子多维数据集的空间中。|  
  
 此属性的默认值为零或空。  
  
 这是一个会话属性，仅在创建会话时可以设置。  
  
 请参阅[中嵌套 select 语句和子多维数据集的计算成员](../../multidimensional-models/mdx/calculated-members-in-subselects-and-subcubes.md)计算的成员或计算的集的嵌套 select 语句和子多维数据集的行为的详细说明。  
  
|“属性”|元素|  
|----------|-------------|  
|DbpropMsmdUseFormulaCache|*用法*<br /> 可选，读/写`String`属性<br /><br /> *说明*<br /> 保留供将来使用。<br /><br /> 此属性无默认值。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。|  
|DbpropMultiTableUpdate|*用法*<br /> 可选的只读`Boolean`属性<br /><br /> *说明*<br /> 此属性与 OLE DB 属性 DBPROP_MULTITABLEUPDATE 等效。<br /><br /> 此属性的默认值是 FALSE。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。|  
|DbpropNullCollation|*用法*<br /> 可选的只读`Integer`属性<br /><br /> *说明*<br /> 此属性与 OLE DB 属性 DBPROP_NULLCOLLATION 等效。<br /><br /> 此属性的默认值为 4，与 DBPROPVAL_NC_LOW 等效。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。|  
|DbpropOrderByColumnsInSelect|*用法*<br /> 可选的只读`Boolean`属性<br /><br /> *说明*<br /> 此属性与 OLE DB 属性 DBPROP_ORDERBYCOLUMNSINSELECT 等效。<br /><br /> 此属性的默认值是 FALSE。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。|  
|DbpropOutputParameterAvailable|*用法*<br /> 可选的只读`Integer`属性<br /><br /> *说明*<br /> 此属性与 OLE DB 属性 DBPROP_OUTPUTPARAMETERAVAILABILITY 等效。<br /><br /> 此属性的默认值为 1，与 DBPROPVAL_OA_NOTSUPPORTED 等效。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。|  
|DbpropPersistentIdType|*用法*<br /> 可选的只读`Integer`属性<br /><br /> *说明*<br /> 此属性与 OLE DB 属性 DBPROP_PERSISTENTIDTYPE 等效。<br /><br /> 此属性的默认值为 4，与 DBPROPVAL_PT_NAME 等效。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。|  
|DbpropPrepareAbortBehavior|*用法*<br /> 可选的只读`Integer`属性<br /><br /> *说明*<br /> 此属性与 OLE DB 属性 DBPROP_PREPAREABORTBEHAVIOR 等效。<br /><br /> 此属性的默认值为 1，与 DBPROPVAL_CB_DELETE 等效。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。|  
|DbpropPrepareCommitBehavior|*用法*<br /> 可选的只读`Integer`属性<br /><br /> *说明*<br /> 此属性与 OLE DB 属性 DBPROP_PREPARECOMMITBEHAVIOR 等效。<br /><br /> 此属性的默认值为 1，与 DBPROPVAL_CB_DELETE 等效。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。|  
|DbpropProcedureTerm|*用法*<br /> 可选的只读`String`属性<br /><br /> *说明*<br /> 此属性与 OLE DB 属性 DBPROP_PROCEDURETERM 等效。<br /><br /> 此属性的默认值为“Calculated member”。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。|  
|DbpropQuotedIdentifierCase|*用法*<br /> 可选，只读 `Integer` 属性<br /><br /> *说明*<br /> 此属性与 OLE DB 属性 DBPROP_QUOTEDIDENTIFIERCASE 等效。<br /><br /> 此属性的默认值为 8，与 DBPROPVAL_IC_MIXED 等效。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。|  
|DbpropSchemaUsage|*用法*<br /> 可选的只读`Integer`属性<br /><br /> *说明*<br /> 此属性与 OLE DB 属性 DBPROP_SCHEMAUSAGE 等效。<br /><br /> 此属性的默认值为零 (0)。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。|  
|DbpropSqlSupport|*用法*<br /> 可选的只读`Integer`属性<br /><br /> *说明*<br /> 此属性与 OLE DB 属性 DBPROP_SQLSUPPORT 等效。<br /><br /> 此属性的默认值为 512，与 DBPROPVAL_SQL_SUBMINIMUM 等效。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。|  
|DbpropSubqueries|*用法*<br /> 可选的只读`Integer`属性<br /><br /> *说明*<br /> 此属性与 OLE DB 属性 DBPROP_SUBQUERIES 等效。<br /><br /> **注意！** 数据挖掘扩展插件 (DMX) 支持子查询，而此属性引用 SQL 中的子查询支持。<br /><br /> 此属性的默认值为零 (0)。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。|  
|DbpropSupportedTxnDdl|*用法*<br /> 可选的只读`Integer`属性<br /><br /> *说明*<br /> 此属性与 OLE DB 属性 DBPROP_SUPPORTEDTXNDDL 等效。<br /><br /> 此属性的默认值为零 (0)，与 DBPROPVAL_TC_NONE 等效。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。|  
|DbpropSupportedTxnIsoLevels|*用法*<br /> 可选的只读`Integer`属性<br /><br /> *说明*<br /> 此属性与 OLE DB 属性 DBPROP_SUPPORTEDTXNISOLEVELS 等效。<br /><br /> 此属性的默认值为 4096，与 DBPROPVAL_TI_READCOMMITTED 等效。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。|  
|DbpropSupportedTxnIsoRetain|*用法*<br /> 可选的只读`Integer`属性<br /><br /> *说明*<br /> 此属性与 OLE DB 属性 DBPROP_SUPPORTEDTXNISORETAIN 等效。<br /><br /> 此属性的默认值为 292，与 DBPROPVAL_TR_ABORT_NO、DBPROPVAL_TR_COMMIT_NO 和 DBPROPVAL_TR_NONE 的组合等效。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。|  
|DbpropTableTerm|*用法*<br /> 可选的只读`String`属性<br /><br /> *说明*<br /> 此属性与 OLE DB 属性 DBPROP_TABLETERM 等效。<br /><br /> 此属性的默认值为“Cube”。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。|  
|Dialect|*用法*<br /> 可选，读/写`String`属性<br /><br /> *说明*<br /> 建立以下情况下使用的方言：<br /><br /> -提供程序将使用第一个的方言时间提供程序尝试运行查询。<br />-用于作为查询失败的结果而返回的执行错误的方言。<br /><br /> 如果您期望多数查询均优先使用一种特定的方言，则可以使用 `Dialect` 属性。<br /><br /> 对于语言方言，查询语法可以是相似的，如 DMX 和 SQL。 由于语法可以是相似的，所以 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 可能会无法从查询语法推断方言。 如果查询不在一种方言中运行，则 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例可能会尝试在其他方言中再次运行该查询。<br /><br /> 如果设置 `Dialect` 属性，则 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 将返回具有优先权的方言中的执行错误，即使提供程序尝试在另一种方言中再次运行查询也是如此。 例如，将 `Dialect` 属性设置为 MDGUID_DM。 提供程序第一次会尝试将该查询作为数据挖掘查询运行，但此查询会失败。 然后，提供程序将该查询重新提交为 SQL 查询。 同样此 SQL 查询也会失败。 原因是 `Dialect` 属性的值为 MDGUID_DM，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 会返回数据挖掘错误消息，而不是 SQL 错误消息。<br /><br /> 如果不设置 `Dialect` 属性，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 将返回最后使用的方言中的查询执行错误。 例如，如果不设置 `Dialect` 属性，数据挖掘查询将会失败。 提供程序然后重新提交查询，为 SQL。 该 SQL 查询同样也会失败。 原因是没有设置 `Dialect` 属性，提供程序返回的是 SQL 错误消息，而不是数据挖掘错误消息。<br /><br /> 此属性无默认值。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。<br /><br /> 下表列出了此属性可用的方言。|  
  
|“属性”|ReplTest1|Description|  
|----------|-----------|-----------------|  
|DBGUID_SQL|*C8B522D7-5CF3-11CE-ADE5-00AA0044773D*|SQL 分析器具有优先权。|  
|MDGUID_DM|*62C58FED-CCA5-44F1-83B6-7B45682B3904*|DMX 分析器具有优先权。|  
|MDGUID_MDX|*A07CCCD0-8148-11D0-87BB-00C04FC33942*|MDX 分析器具有优先权。|  
  
|“属性”|元素|  
|----------|-------------|  
|Disable Prefetch Facts|*用法*<br /> 可选，读/写`Boolean`属性，<br /><br /> *说明*<br /> 设置为 True 时，该引擎停止尝试预提取会话长度的值。<br /><br /> 此属性的默认值是`False`。|  
|EffectiveRoles|*用法*<br /> 可选的只写`String`属性<br /><br /> *说明*<br /> 保留供将来使用。<br /><br /> 此属性无默认值。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。|  
|EffectiveUserName|*用法*<br /> 可选的只写`String`属性<br /><br /> *说明*<br /> 指定连接到 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例时，用于覆盖用户名的帐户的名称。 属性的值不会加以规范，该 MDX[用户名](/sql/mdx/username-mdx)函数返回文本值，如果使用此属性。 只有服务器管理员才可以使用此属性。<br /><br /> 此属性支持以下 SID 类型：User、Group、Alias、WellKnownGroup、Computer。<br /><br /> 此属性无默认值。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。|  
|EndRange|*用法*<br /> 可选的只写`Integer`属性<br /><br /> *说明*<br /> 指定一个与 `CellOrdinal` 属性值相对应的、从零开始的整数值。 （`CellOrdinal` 属性是 `Cell` 的 `CellData` 部分中的 `MDDataSet` 元素的一部分。）<br /><br /> 客户端应用程序可以综合使用 `BeginRange` 属性和此属性，将命令返回的 OLAP 数据集限制在特定单元范围内。 如果指定为 -1，则将返回从 `BeginRange` 属性所指定的单元开始的所有单元。<br /><br /> 此属性的默认值为-1。<br /><br /> 此属性可以用于 `Execute` 方法。|  
|ExecutionMode|*用法*<br /> 可选的只写`String`属性<br /><br /> *说明*<br /> 保留供将来使用。<br /><br /> 此属性的默认值是*Execute*。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。|  
|ForceCommitTimeout|*用法*<br /> 可选的只写`Integer`属性<br /><br /> *说明*<br /> 确定当前正在运行的 XMLA 命令在强制要求先前发出的命令进行回滚前，需要等待的提交阶段的时间（秒）。 提交阶段与 XMLA 命令对应，如 `Statement` 或 `Process`。<br /><br /> 零值 (0) 指示实例要无限期等待。<br /><br /> 此属性的默认值为零 (0)。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。|  
|“格式”|*用法*<br /> 可选的只写`String`属性<br /><br /> *说明*<br /> 确定从 `Discover` 和 `Execute` 方法返回的结果集的类型。 此属性的值可以为下表中所列出的值。|  
  
 此属性的默认值是*本机*。  
  
 此属性可以用于 `Discover` 和 `Execute` 方法。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|*表格*|返回一个结果集，使用[行集](../xml-data-types/rowset-data-type-xmla.md)数据类型。|  
|*多维*|返回行集使用[MDDataSet](../xml-data-types/mddataset-data-type-xmla.md)数据类型。|  
|*本机*|不显示指定格式。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 会为命令返回相应的格式。 实际结果类型由结果的命名空间识别。|  
  
|“属性”|元素|  
|----------|-------------|  
|ImpactAnalysis|*用法*<br /> 可选的只写`Boolean`属性<br /><br /> *说明*<br /> 保留供将来使用。<br /><br /> 此属性的默认值为零 (0)。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。|  
|LocaleIdentifier|*用法*<br /> 可选，读/写`Integer`属性<br /><br /> *说明*<br /> 读取或设置 `Discover` 或 `Execute` 方法使用的区域设置标识符 (LCID)。 有关完整的语言标识符的十六进制列表，请在 MSDN Library 中查找“Language Identifiers”。<br /><br /> 此属性无默认值。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。|  
|MaximumRows|*用法*<br /> 可选的只写`Integer`属性<br /><br /> *说明*<br /> 保留供将来使用。<br /><br /> 此属性无默认值。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。|  
|MdpropAggregateCellUpdate|*用法*<br /> 可选的只读`Integer`属性<br /><br /> *说明*<br /> 此属性与 OLE DB 属性 MDPROP_AGGREGATECELL_UPDATE 等效。<br /><br /> 此属性的默认值为 4，与 MDPROPVAL_AU_SUPPORTED 等效。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。|  
|MdpropAxes|*用法*<br /> 可选的只读`Integer`属性<br /><br /> *说明*<br /> 此属性与 OLE DB 属性 MDPROP_AXES 等效。<br /><br /> 此属性的默认值为 2147483647。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。|  
|MdpropDrillFunctions|*用法*<br /> 可选的只读`Integer`属性<br /><br /> *说明*<br /> 确定针对服务器的钻取功能的支持级别。 下面的值用于生成有效的位掩码：<br /><br /> MDPROPVAL_MDF_BASIC (0x01)<br /><br /> MDPROPVAL_MDF_ASYMMETRIC (0x02)<br /><br /> MDPROPVAL_MDF_CALC_MEMBERS (0x04)<br /><br /> 默认值为：<br /><br /> 对于 SQL Server 2008 为 3<br /><br /> 对于 SQL Server 2008 R2 和 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 为 7<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。|  
|MdpropFlatteningSupport|*用法*<br /> 可选的只读`Integer`属性<br /><br /> *说明*<br /> 此属性与 OLE DB 属性 MDPROP_FLATTENING_SUPPORT 等效。<br /><br /> 此属性的默认值为 1，与 MDPROPVAL_FS_FULL_SUPPORT 等效。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。|  
|MdpropMdxCaseSupport|*用法*<br /> 可选的只读`Integer`属性<br /><br /> *说明*<br /> 此属性与 OLE DB 属性 MDPROP_MDX_CASESUPPORT 等效。<br /><br /> 此属性的默认值为零 (0)。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。|  
|MdpropMdxDescFlags|*用法*<br /> 可选的只读`Integer`属性<br /><br /> *说明*<br /> 此属性与 OLE DB 属性 MDPROP_MDX_DESCFLAGS 等效。<br /><br /> 此属性的默认值为 7，与 MDPROPVAL_MD_BEFORE、MDPROPVAL_MD_AFTER 和 MDPROPVAL_MD_SELF 等效。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。|  
|MdpropMdxFormulas|*用法*<br /> 可选的只读`Integer`属性<br /><br /> *说明*<br /> 此属性与 OLE DB 属性 MDPROP_MDX_FORMULAS 等效。<br /><br /> 此属性的默认值为 63，与 MDPROPVAL_MF_WITH_CALCMEMBERS、MDPROPVAL_MF_WITH_NAMEDSETS、MDPROPVAL_MF_CREATE_CALCMEMBERS、MDPROPVAL_MF_CREATE_NAMEDSETS、MDPROPVAL_MF_SCOPE_SESSION 和 MDPROPVAL_MF_SCOPE_GLOBAL 的组合等效。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。|  
|MdpropMdxJoinCubes|*用法*<br /> 可选的只读`Integer`属性<br /><br /> *说明*<br /> 此属性与 OLE DB 属性 MDPROP_MDX_JOINCUBES 等效。<br /><br /> 此属性的默认值为 1，与 MDPROPVAL_MJC_SINGLECUBE 等效。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。|  
|MdpropMdxMemberFunctions|*用法*<br /> 可选的只读`Integer`属性<br /><br /> *说明*<br /> 此属性与 OLE DB 属性 MDPROP_MDX_MEMBER_FUNCTIONS 等效。<br /><br /> 此属性的默认值为 15，与所有可用的 OLE DB 值的组合等效。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。|  
|MdpropMdxNamedSets|*用法*<br /> 可选的只读`Integer`属性<br /><br /> *说明*<br /> 位掩码，可能为下表中所列的值。|  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|*0x01*|MDPROPVAL_MNS_BASIC。|  
|*0x02*|MDPROPVAL_MNS_DYNAMIC。|  
|*0x04*|MDPROPVAL_MNS_DISPLAYFOLDER。|  
|*0x08*|MDPROPVAL_MNS_CAPTION。|  
  
 此属性的默认值为 15。  
  
|“属性”|元素|  
|----------|-------------|  
|MdpropMdxNonMeasureExpressions|*用法*<br /> 可选的只读`Integer`属性<br /><br /> *说明*<br /> 此属性与 OLE DB 属性 MDPROP_MDX_NONMEASURE_EXPRESSIONS 等效。<br /><br /> 此属性的默认值为零 (0)，与 MDPROPVAL_NME_ALLDIMENSIONS 等效。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。|  
|MdpropMdxNumericFunctions|*用法*<br /> 可选的只读`Integer`属性<br /><br /> *说明*<br /> 此属性与 OLE DB 属性 MDPROP_MDX_NUMERIC_FUNCTIONS 等效。<br /><br /> 此属性的默认值为 2047，与 MDPROPVAL_MNF_MEDIAN, MDPROPVAL_MNF_VAR、MDPROPVAL_MNF_STDDEV、MDPROPVAL_MNF_RANK、MDPROPVAL_MNF_AGGREGATE、MDPROPVAL_MNF_COVARIANCE、MDPROPVAL_MNF_CORRELATION、MDPROPVAL_MNF_LINREGSLOPE、MDPROPVAL_MNF_LINREGVARIANCE、MDPROPVAL_MNF_LINREG2 和 MDPROPVAL_MNF_LINREGPOINT 的组合等效。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。|  
|MdpropMdxObjQualification|*用法*<br /> 可选的只读`Integer`属性<br /><br /> *说明*<br /> 此属性与 OLE DB 属性 MDPROP_MDX_OBJQUALIFICATION 等效。<br /><br /> 此属性的默认值为 496，与 MDPROPVAL_MOQ_DIM_HIER、MDPROPVAL_MOQ_DIMHIER_LEVEL、MDPROPVAL_MOQ_DIMHIER_MEMBER、MDPROPVAL_MOQ_LEVEL_MEMBER 和 MDPROPVAL_MOQ_MEMBER_MEMBER 的组合等效。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。|  
|MdpropMdxOuterReference|*用法*<br /> 可选的只读`Integer`属性<br /><br /> *说明*<br /> 此属性与 OLE DB 属性 MDPROP_MDX_OUTERREFERENCE 等效。<br /><br /> 此属性的默认值为零 (0)。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。|  
|MdpropMdxQueryByProperty|*用法*<br /> 可选的只读`Boolean`属性<br /><br /> *说明*<br /> 此属性与 OLE DB 属性 MDPROP_MDX_QUERYBYPROPERTY 等效。<br /><br /> 此属性的默认值为 TRUE。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。|  
|MdpropMdxRangeRowset|*用法*<br /> 可选的只读`Integer`属性<br /><br /> *说明*<br /> 此属性与 OLE DB 属性 MDPROP_MDX_RANGEROWSET 等效。<br /><br /> 此属性的默认值为 4，与 MDPROPVAL_RR_UPDATE 等效。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。|  
|MdpropMdxSetFunctions|*用法*<br /> 可选的只读`Integer`属性<br /><br /> *说明*<br /> 此属性与 OLE DB 属性 MDPROP_MDX_SET_FUNCTIONS 等效。<br /><br /> 此属性的默认值为 524287，与 MDPROPVAL_MSF_TOPPERCENT、MDPROPVAL_MSF_BOTTOMPERCENT、MDPROPVAL_MSF_TOPSUM、MDPROPVAL_MSF_BOTTOMSUM、MDPROPVAL_MSF_PERIODSTODATE、MDPROPVAL_MSF_LASTPERIODS、MDPROPVAL_MSF_YTD、MDPROPVAL_MSF_QTD、MDPROPVAL_MSF_MTD、MDPROPVAL_MSF_WTD、MDPROPVAL_MSF_DRILLDOWNMEMBER、MDPROPVAL_MSF_DRILLDOWNLEVEL、MDPROPVAL_MSF_DRILLDOWNMEMBERTOP、MDPROPVAL_MSF_DRILLDOWNMEMBERBOTTOM、MDPROPVAL_MSF_DRILLDOWNLEVEL、MDPROPVAL_MSF_DRILLDOWNLEVELTOP、MDPROPVAL_MSF_DRILLDOWNLEVELBOTTOM、MDPROPVAL_MSF_DRILLUPMEMBER、MDPROPVAL_MSF_DRILLUPLEVEL 和 MDPROPVAL_MSF_TOGGLEDRILLSTATE 的组合等效。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。|  
|MdpropMdxSlicer|*用法*<br /> 可选的只读`Integer`属性<br /><br /> *说明*<br /> 此属性与 OLE DB 属性 MDPROP_MDX_SLICER 等效。<br /><br /> 此属性的默认值为 2，与 MDPROPVAL_MS_SINGLETUPLE 等效。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。|  
|MdpropMdxStringCompop|*用法*<br /> 可选的只读`Integer`属性<br /><br /> *说明*<br /> 此属性与 OLE DB 属性 MDPROP_MDX_STRING_COMPOP 等效。<br /><br /> 此属性的默认值为 15，与 MDPROPVAL_MSC_LESSTHAN、MDPROPVAL_MSC_GREATERTHAN、MDPROPVAL_MSC_LESSTHANEQUAL 和 MDPROPVAL_MSC_GREATERTHANEQUAL 的组合等效。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。|  
|MdpropMdxSubQueries|*用法*<br /> 可选的只读`Integer`属性<br /><br /> *说明*<br /> 值 63 是此属性在 SQL Server 2014 中的默认值。<br /><br /> 值 31 是此属性在 SQL Server 2008 R2 和 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 中的默认值<br /><br /> 值 15 是此属性在 SQL Server 2008 中的默认值<br /><br /> 指示对 MDX 中子查询的支持级别。 位掩码，可能为下表中所列的值。|  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|*0x01*|MDPROPVAL_MSQ_BASIC。|  
|*0x02*|MDPROPVAL_MSQ_ARBITRARYSHAPE。|  
|*0x04*|MDPROPVAL_MSQ_NONVISUAL。|  
|*0x08*|MDPROPVAL_MSQ_CALCMEMBERS。|  
  
|||  
|-|-|  
|*0x10*|MDPROPVAL_MSQ_CALCMEMBERS2|  
  
|“属性”|元素|  
|----------|-------------|  
|MdpropNamedLevels|*用法*<br /> 可选的只读`Integer`属性<br /><br /> *说明*<br /> 此属性与 OLE DB 属性 MDPROP_NAMED_LEVELS 等效。<br /><br /> 此属性的默认值为 3，与 MDPROPVAL_NL_NAMEDLEVELS 和 MDPROPVAL_NL_NUMBEREDLEVELS 的组合等效。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。|  
|MdxMissingMemberMode|*用法*<br /> 可选的只写`String`属性<br /><br /> *说明*<br /> 指示是否在 MDX 语句中忽略缺少的成员。<br /><br /> 此属性与 OLE DB 属性 DBPROP_MDX_MISSING_MEMBER_MODE 等效。<br /><br /> 此属性的默认值是*默认*。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。<br /><br /> 此属性的值可以为下表中所列出的值。|  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|*默认*|使用 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例生成的值。|  
|*错误*|生成一个错误。|  
|*忽略*|始终忽略缺少的成员。|  
  
|“属性”|元素|  
|----------|-------------|  
|MDXSupport|*用法*<br /> 可选的只读`String`属性<br /><br /> *说明*<br /> 指定一个说明 MDX 支持的程度的枚举。<br /><br /> `Value` = *核心*支持所有 MDX 选项。<br /><br /> 目前，该枚举包含唯一值是*Core*。 但在未来的版本中，会为此枚举定义其他值。<br /><br /> 此属性的默认值是*Core*。<br /><br /> 此属性可以用于 `Discover` 方法。|  
|NonEmptyThreshold|*用法*<br /> 可选，读/写 `Integer` 属性<br /><br /> *说明*<br /> 保留供将来使用。<br /><br /> 此属性无默认值。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。|  
|Password|**不再支持此属性。**<br /><br /> *用法*<br /> 可选，只写 `String` 属性<br /><br /> *说明*<br /> 为了后向兼容，当将此属性用于 `Execute` 或 `Discover` 方法时，将忽略此属性，不会生成错误。|  
|ProviderName|*用法*<br /> 可选的只读`String`属性<br /><br /> *说明*<br /> 此属性与 OLE DB 属性 DBPROP_DBMSNAME 等效。<br /><br /> 此属性的默认值为“OLAP Server”。<br /><br /> 此属性可以用于 `Discover` 方法。|  
|ProviderType|*用法*<br /> 可选的只读`Integer`属性<br /><br /> *说明*<br /> 此属性与 OLE DB 属性 DBPROP_DATASOURCE_TYPE 等效。<br /><br /> 此属性的默认值为 6。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。|  
|ProviderVersion|*用法*<br /> 可选的只读`String`属性<br /><br /> *说明*<br /> 此属性与 OLE DB 属性 DBPROP_DBMSVER 等效。<br /><br /> 此属性的默认值为 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例的版本。<br /><br /> 此属性可以用于 `Discover` 方法。|  
|ReadOnlySession|*用法*<br /> 可选，读/写`Integer`属性<br /><br /> *说明*<br /> 保留供将来使用。<br /><br /> 此属性无默认值。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。|  
|RealTimeOlap|*用法*<br /> 可选，读/写`Boolean`属性<br /><br /> *说明*<br /> 设置为 TRUE 时，指示所有侦听表通知的分区都将实时查询，跳过缓存操作。 此属性与 OLE DB 属性 DBPROP_MSMD_REAL_TIME_OLAP 等效。<br /><br /> 此属性的默认值是 FALSE。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。|  
|ReturnCellProperties|*用法*<br /> 可选，读/写`Boolean`属性<br /><br /> *说明*<br /> 此属性的默认值是 FALSE。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。|  
|角色|*用法*<br /> 可选，读/写`String`属性<br /><br /> *说明*<br /> 指定一个以逗号分隔的、客户端应用程序用以连接到 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例的角色名称字符串。 此属性允许用户使用其当前所用角色以外的角色进行连接。 例如，服务器管理员可能会为了测试授予给角色的权限，而希望以角色成员连接到多维数据集。 这种情况下，该用户就必须为使用此属性进行连接而指定的角色的成员。<br /><br /> 此属性无默认值。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。<br /><br /> **注意！** 角色名称区分大小写。 **不要使用**以逗号分隔的角色名称之间的空格。 否则，为了保护单元集，查询可能会返回错误和意外结果。|  
|SafetyOptions|*用法*<br /> 可选，读/写`Integer`属性<br /><br /> *说明*<br /> 确定客户端应用程序是否可以注册和加载不安全的库。<br /><br /> 此属性的值还可以确定本地多维数据集中是否允许 PASSTHROUGH 关键字。 下列情况下可能会发生错误：<br /><br /> -如果客户端应用程序尝试使用 INSERT INTO 语句包含 PASSTHROUGH 关键字创建本地多维数据集。<br />-如果客户端应用程序尝试更新包含 INSERT INTO 语句使用 PASSTHROUGH 关键字的本地多维数据集。<br /><br /> 此属性无默认值。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。<br /><br /> 此属性的值可以为下表中所列出的值。|  
  
|“属性”|ReplTest1|Description|  
|----------|-----------|-----------------|  
|DBPROPVAL_MSMD_SAFETY_OPTIONS_DEFAULT|*0*|此值将被视为 DBPROPVAL_MSMD_SAFETY_OPTIONS_ALLOW_SAFE。<br /><br /> 对于到本地多维数据集的连接，此值取决于是否使用 CREATECUBE 连接字符串属性。 如果使用 CREATECUBE 连接字符串属性，则此属性将与 DBPROPVAL_MSMD_SAFETY_OPTIONS_ALLOW_ALL 相同。 否则，此属性与 DBPROPVAL_MSMD_SAFETY_OPTIONS_ALLOW_SAFE 相同。|  
|DBPROPVAL_MSMD_SAFETY_OPTIONS_ALLOW_ALL|*1*|此值可启用所有用户定义的功能库，且不用验证对于初始化和脚本编写，这些功能库是否是安全的。 对于到本地多维数据集的连接，此属性可帮助实现使用存储过程和在 INSERT INTO 语句中使用 PASSTHROUGH 关键字。<br /><br /> **我们不建议使用此选项**。|  
|DBPROPVAL_MSMD_SAFETY_OPTIONS_ALLOW_SAFE|*2*|此值可确保对用户定义的特定功能库的所有类进行检查，以确保它们对于初始化和编写脚本是安全的。 对于到本地多维数据集的连接，此值不但可以阻止在 INSERT INTO 语句中使用 PASSTHROUGH 关键字，还可以阻止使用其 PermissionSet 属性未设置为“Safe”的 PASSTHROUGH。<br /><br /> 此值还会删除中的操作[MDSCHEMA_ACTIONS](../../schema-rowsets/ole-db-olap/mdschema-actions-rowset.md) ACTION_TYPE 列中具有值为 HTML 或命令或在内容列不具有 ACTION_TYPE 列中的 URL 的值和的值的架构行集以"http://"或"https://"开头。|  
|DBPROPVAL_MSMD_SAFETY_OPTIONS_ALLOW_NONE|*3*|此值可阻止在会话期间使用用户定义的功能。 对于到本地多维数据集的连接，此属性可阻止使用所有存储过程和在 INSERT INTO 语句中使用 PASSTHROUGH 关键字。<br /><br /> 此属性还可删除 MDSCHEMA_ACTIONS 架构集中的所有操作。|  
  
|“属性”|元素|  
|----------|-------------|  
|SecuredCellValue|*用法*<br /> 可选，读/写`Integer`属性<br /><br /> *说明*<br /> 指定当尝试访问受保护的单元时，要返回的`Value` 和 `Formatted Value` 单元属性的错误代码和值。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。<br /><br /> 此属性的值可以为下表中所列出的值。|  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|*0*|（默认值）为了与早期版本兼容，此值是与相同*1*。 此默认值的含义在将来版本中可能会发生变化。|  
|*1*|返回：HRESULT = NO_ERROR<br /><br /> 单元的 `Value` 属性包含作为变量数据类型。 返回字符串“#N/A”到 `Formatted Value` 属性中。|  
|*2*|返回一个作为 HRESULT 的值的错误。|  
|*3*|返回 NULL 到 `Value` 和 `Formatted Value` 属性中。|  
|*4*|返回数字零 (0) 到 `Value` 属性中，返回格式零到 `Formatted Value` 属性中。 例如，返回 0.00 到其 `Formatted Value` 属性为“#.##”的单元的 `Format` 属性中。|  
|*5*|返回字符串“#SEC”到 `Value` 和 `Formatted Value` 属性中。|  
  
|“属性”|元素|  
|----------|-------------|  
|ServerName|*用法*<br /> 可选的只读`String`属性<br /><br /> *说明*<br /> 此属性与 OLE DB 属性 DBPROP_SERVERNAME 等效。<br /><br /> 此属性的默认值为 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例的名称。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。|  
|ShowHiddenCubes|*用法*<br /> 可选，读/写`Boolean`属性<br /><br /> *说明*<br /> 保留供将来使用。<br /><br /> 此属性的默认值是 FALSE。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。|  
|SQLQueryMode|*用法*<br /> 可选，读/写`String`属性<br /><br /> *说明*<br /> 确定是否在 SQL 查询中包含计算。<br /><br /> 此属性的默认值是*计算*。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。<br /><br /> 此属性的值可以为下表中所列出的值。|  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|*数据*|不包含任何计算。|  
|*计算*|返回计算。|  
|*IncludeEmpty*|返回计算和空行。|  
  
|“属性”|元素|  
|----------|-------------|  
|SQLSupport|*用法*<br /> 可选的只读`Integer`属性<br /><br /> *说明*<br /> 此属性的默认值为 512。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。|  
|SspropInitAppName|*用法*<br /> 可选，读/写`String`属性<br /><br /> *说明*<br /> 包含客户端应用程序的名称。<br /><br /> 此属性无默认值。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。|  
|SspropInitPacketsize|*用法*<br /> 可选，读/写`Integer`属性<br /><br /> *说明*<br /> 包含客户端应用程序的 ID。<br /><br /> 此属性无默认值。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。|  
|SspropInitWsid|*用法*<br /> 可选，读/写`String`属性<br /><br /> *说明*<br /> 包含客户端工作站的 ID。<br /><br /> 此属性无默认值。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。|  
|StateSupport|*用法*<br /> 可选的只读`String`属性<br /><br /> *说明*<br /> 指定对状态的支持程度。<br /><br /> *无* = <br />                        不支持状态。<br /><br /> *会话*= 通过会话支持提供状态。<br /><br /> 有关状态和会话支持的详细信息，请参阅[管理连接和会话&#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md)。<br /><br /> 此属性的默认值是*会话*。<br /><br /> 此属性可以用于 `Discover` 方法。|  
|超时|*用法*<br /> 可选，读/写`Integer`属性<br /><br /> *说明*<br /> 指定 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例在返回错误前，应等待请求的最长时间（以秒为单位）。 此属性还可确定实例在返回错误前，应等待更新成功回写表的最长时间，与连接字符串属性 Writeback Timeout 等效。<br /><br /> 此属性的默认值为零 (0)。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。|  
|TransactionDDL|*用法*<br /> 可选的只读`Integer`属性<br /><br /> *说明*<br /> 保留供将来使用。<br /><br /> 此属性的默认值为 0。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。|  
|UserName|不再支持此属性。<br /><br /> *用法*<br /> 可选的只读`String`属性<br /><br /> *说明*<br /> 指定一个字符串，该字符串可返回 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例用以关联命令的用户名称。 为了后向兼容，当将此属性用于 `Execute` 或 `Discover` 方法时，将忽略此属性，不会生成错误。 此属性与 OLE DB 属性 DBPROP_USERNAME 等效。<br /><br /> 此属性的默认值为打开当前会话或连接的用户名称。<br /><br /> 此属性可以用于 `Execute` 方法。|  
|VisualMode|*用法*<br /> 可选的只写`Integer`属性<br /><br /> *说明*<br /> 此属性与 OLE DB 属性 MDPROP_VISUALMODE 等效。<br /><br /> 此属性的默认值为零 (0)，与 DBPROPVAL_VISUAL_MODE_DEFAULT 等效。<br /><br /> 此属性可以用于 `Discover` 和 `Execute` 方法。|  
  
## <a name="see-also"></a>请参阅  
 [PropertyList 元素&#40;XMLA&#41;](propertylist-element-xmla.md)  
  
  
