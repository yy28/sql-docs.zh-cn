---
title: "支持 XMLA 属性 (XMLA) |Microsoft 文档"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: xmla
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apitype: Schema
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- properties [XML for Analysis]
- XML for Analysis, properties
- XMLA, properties
ms.assetid: 5745f7b4-6b96-44d5-b77c-f2831a898e5e
caps.latest.revision: 27
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: bc63db6c3f61de7e77ea41e3c5a24acd4d3b275e
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="propertylist-element---supported-xmla-properties"></a>PropertyList 元素-支持 XMLA 属性
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]支持下表中列出的属性。 使用这些列出的属性中[属性](../../../analysis-services/xmla/xml-elements-properties/properties-element-xmla.md)元素[发现](../../../analysis-services/xmla/xml-elements-methods-discover.md)和[执行](../../../analysis-services/xmla/xml-elements-methods-execute.md)方法。  
  
|Name|Description|类型|值|  
|----------|-----------------|----------|------------|  
|AxisFormat|确定在中使用的格式[MDDataSet](../../../analysis-services/xmla/xml-data-types/mddataset-data-type-xmla.md)结果集来描述轴的多维数据集。 此属性的值可以为下表中所列出的值。<br /><br /> 此属性可与**执行**方法。|可选的只写**字符串**属性|*ClusterFormat*: **MDDataSet**轴由一个或多个组成[CrossProduct](../../../analysis-services/xmla/xml-elements-properties/crossproduct-element-xmla.md)元素。<br /><br /> *CustomFormat*: <br />                          [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]使用*TupleFormat*此设置格式。<br /><br /> *TupleFormat*默认。 **MDDataSet**轴包含一个或多个[元组](../../../analysis-services/xmla/xml-elements-properties/tuple-element-xmla.md)元素。|  
|BeginRange|包含一个从零开始的整数值对应于**CellOrdinal**属性值。 ( **CellOrdinal**属性是的一部分[单元格](../../../analysis-services/xmla/xml-elements-properties/cell-element-mddataset-xmla.md)中的元素[CellData](../../../analysis-services/xmla/xml-elements-properties/celldata-element-xmla.md)部分**MDDataSet**。)<br /><br /> 此属性的默认值为-1。<br /><br /> 此属性可与**执行**方法。<br /><br /> 一起使用**EndRange**属性，客户端应用程序可以使用此属性来限制由命令返回到特定范围的单元格的 OLAP 数据集。 如果指定-1，则所有单元格到指定的单元格**EndRange**属性返回。|可选的只写**整数**属性||  
|目录|为发送 XMLA 命令而与 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例建立会话时，此属性与 OLE DB 属性 DBPROP_INIT_CATALOG 等效。<br /><br /> 在会话期间，为更改会话的当前数据库而设置此属性时，此属性与 OLE DB 属性 DBPROP_CURRENTCATALOG 等效。<br /><br /> 此属性的默认值为空字符串。<br /><br /> 此属性可与**发现**和**执行**方法。|可选的读/写**字符串**属性||  
|CatalogLocation|此属性与 OLE DB 属性 DBPROP_CATALOGLOCATION 等效。<br /><br /> 此属性的默认值为零 (0)，与 DBPROPVAL_CL_START 等效。<br /><br /> 此属性可与**发现**和**执行**方法。|可选的只读**整数**属性||  
|ClientProcessID|包含当前会话的进程线程的标识符 (ID)。<br /><br /> 此属性的默认值为零 (0)。<br /><br /> 此属性可与**发现**和**执行**方法。|可选的读/写**整数**属性||  
|CommitTimeout|确定等待多长时间，以毫秒为单位，当前正在运行的 XMLA 命令提交阶段之前回滚。 如果大于 0，则覆盖服务器配置中对应 CommitTimeout 属性的值。 提交阶段对应于 XMLA 命令如[语句](../../../analysis-services/xmla/xml-elements-commands/statement-element-xmla.md)或[过程](../../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md)。<br /><br /> 零值 (0) 指示实例要无限期等待。<br /><br /> 此属性的默认值为零 (0)。<br /><br /> 此属性可与**发现**和**执行**方法。|可选的只写**整数**属性||  
|内容|确定返回的数据的类型**发现**和**执行**方法。<br /><br /> 此属性可与**发现**和**执行**方法。|可选的只写**字符串**属性|*SchemaData*： 默认值。 返回的架构信息和数据。<br /><br /> *无*： 允许通过验证，但不是运行的命令结构。<br /><br /> *架构*： 返回与请求的命令相关的 XML 架构。 XML 架构指示列和其他信息。<br /><br /> *数据*： 返回所请求数据。|  
|多维数据集|包含用于设置命令的上下文的多维数据集的名称。 如果命令本身中包含的多维数据集名称，例如，在 FROM 子句的多维表达式 (MDX) 中[选择](../../../mdx/mdx-data-manipulation-select.md)语句，此属性的设置将被忽略。<br /><br /> 此属性的默认值为空字符串。<br /><br /> 此属性可与**发现**和**执行**方法。|可选的只写**字符串**属性||  
|DataSourceInfo|包含连接到数据源要用到的信息，如实例名称。<br /><br /> 客户端应用程序不应构造的内容**DataSourceInfo**属性将发送到实例。 相反，客户端应用程序应会发现提供程序通过使用支持的数据源**发现**方法来检索[DISCOVER_DATASOURCES](../../../analysis-services/schema-rowsets/xml/discover-datasources-rowset.md)行集。 然后，客户端应用程序发送回相同的值**DataSourceInfo**从 DISCOVER_DATASOURCES 行集检索客户端的属性。<br /><br /> 此属性无默认值。<br /><br /> 此属性可与**发现**和**执行**方法。|所需，读/写**字符串**属性||  
|DbpropCatalogTerm|此属性与 OLE DB 属性 DBPROP_CATALOGTERM 等效。<br /><br /> 此属性的默认值为“Database”。<br /><br /> 此属性可与**发现**和**执行**方法。|可选的只读**字符串**属性||  
|DbpropCatalogUsage|此属性与 OLE DB 属性 DBPROP_CATALOGUSAGE 等效。<br /><br /> 此属性的默认值为零 (0)。<br /><br /> 此属性可与**发现**和**执行**方法。|可选的只读**整数**属性||  
|DbpropColumnDefinition|此属性与 OLE DB 属性 DBPROP_COLUMNDEFINITION 等效。<br /><br /> 此属性的默认值为零 (0)。<br /><br /> 此属性可与**发现**和**执行**方法。|可选的只读**整数**属性||  
|DbpropConcatNullBehavior|此属性与 OLE DB 属性 DBPROP_CONCATNULLBEHAVIOR 等效。<br /><br /> 此属性的默认值为 1，与 DBPROPVAL_CB_NULL 等效。<br /><br /> 此属性可与**发现**和**执行**方法。|可选的只读**整数**属性||  
|DbpropDataSourceReadOnly|此属性与 OLE DB 属性 DBPROP_DATASOURCEREADONLY 等效。<br /><br /> 此属性的默认值是 FALSE。<br /><br /> 此属性可与**发现**和**执行**方法。|可选的只读**布尔**属性||  
|DbpropGroupBy|此属性与 OLE DB 属性 DBPROP_GROUPBY 等效。<br /><br /> 此属性的默认值为 2，与 DBPROPVAL_GB_EQUALS_SELECT 等效。<br /><br /> 此属性可与**发现**和**执行**方法。|可选的只读**整数**属性||  
|DbpropHeterogeneousTables|此属性与 OLE DB 属性 DBPROP_HETEROGENEOUSTABLES 等效。<br /><br /> 此属性的默认值为零 (0)。<br /><br /> 此属性可与**发现**和**执行**方法。|可选的只读**整数**属性||  
|DbpropIdentifierCase|此属性与 OLE DB 属性 DBPROP_IDENTIFIERCASE 等效。<br /><br /> 此属性的默认值为 8，与 DBPROPVAL_IC_MIXED 等效。<br /><br /> 此属性可与**发现**和**执行**方法。|可选的只读**整数**属性||  
|DbpropInitMode|此属性与 OLE DB 属性 DBPROP_INIT_MODE 等效。<br /><br /> 此属性仅支持值 DB_MODE_READWRITE 和 DB_MODE_READ。<br /><br /> 此属性无默认值。<br /><br /> 此属性可与**发现**和**执行**方法。|可选的读/写**整数**属性||  
|DbpropMaxIndexSize|此属性与 OLE DB 属性 DBPROP_MAXINDEXSIZE 等效。<br /><br /> 此属性的默认值为零 (0)。<br /><br /> 此属性可与**发现**和**执行**方法。|可选的只读**整数**属性||  
|DbpropMaxOpenChapters|此属性与 OLE DB 属性 DBPROP_MAXOPENCHAPTERS 等效。<br /><br /> 此属性的默认值为零 (0)。<br /><br /> 此属性可与**发现**和**执行**方法。|可选的只读**整数**属性||  
|DbpropMaxRowSize|此属性与 OLE DB 属性 DBPROP_MAXROWSIZE 等效。<br /><br /> 此属性的默认值为零 (0)。<br /><br /> 此属性可与**发现**和**执行**方法。|可选的只读**整数**属性||  
|DbpropMaxRowSizeIncludeBlob|此属性与 OLE DB 属性 DBPROP_MAXROWSIZEINCLUDESBLOB 等效。<br /><br /> 此属性的默认值为 TRUE。<br /><br /> 此属性可与**发现**和**执行**方法。|可选只读**布尔**属性||  
|DbpropMaxTablesInSelect|此属性与 OLE DB 属性 DBPROP_MAXTABLESINSELECT 等效。<br /><br /> 此属性的默认值为 1。<br /><br /> 此属性可与**发现**和**执行**方法。|可选的只读**整数**属性||  
|DbpropMsmdAutoexists|确定 autoexists 的行为。 此属性的值可以为下表中所列出的值。<br /><br /> 此属性的默认值为零或空。<br /><br /> 这是一个会话属性，仅在创建会话时可以设置。|可选的读/写**整数**属性|*0*： 默认值 1 相同。<br /><br /> *1*： 应用的查询轴的深度 autoexists 和命名集。 包括 WHERE 子句和嵌套 select。<br /><br /> *2*： 应用的查询轴的深度 autoexists 以及 autoexists 中排除的命名的集。 包括 WHERE 子句和嵌套 select。<br /><br /> *3*： 应用中用 WHERE 子句的命名集没有 autoexists。 对带 WHERE 子句的查询轴应用浅表 autoexists。 对带嵌套 select 的查询轴和带嵌套 select 的命名集应用深度 autoexists。|  
|DbpropMsmdCacheMode|保留供将来使用。<br /><br /> 此属性无默认值。<br /><br /> 此属性可与**发现**和**执行**方法。|可选的读/写**整数**属性||  
|DbpropMsmdCachePolicy|保留供将来使用。<br /><br /> 此属性无默认值。<br /><br /> 此属性可与**发现**和**执行**方法。|可选的读/写**整数**属性||  
|DbpropMsmdCacheRatio|保留供将来使用。<br /><br /> 此属性无默认值。<br /><br /> 此属性可与**发现**和**执行**方法。|可选的读/写**整数**属性||  
|DbpropMsmdCacheRatio2|保留供将来使用。<br /><br /> 此属性无默认值。<br /><br /> 此属性可与**发现**和**执行**方法。|可选的读/写**Double**属性||  
|DbpropMsmdCompareCaseNotSensitiveStringFlags|确定区分大小写的字符串的比较和排序功能。 此属性可以控制不支持大写字符和小写字符的字符集中的比较方式，如对于日语的片假名和印地语。 此属性的值在进程线程第一个连接中设置，会影响该进程线程中的所有后续连接。<br /><br /> 有关 OLE DB 中字符串比较的详细信息，请在 MSDN Library 的 Platform SDK 部分中对“CompareString”进行搜索。<br /><br /> 此属性无默认值。<br /><br /> 此属性可与**发现**和**执行**方法。|可选的读/写**整数**属性|使用以下**名称**:**值**对以确定用于使用的标志：<br /><br /> **NORM_IGNORECASE**: *0x00000001*。 忽略大小写。<br /><br /> 不适用： *0x00000002*。二进制比较。 在字符集中，字符是按照其基础值进行比较的，而不是按照其特定的字符顺序进行比较。<br /><br /> **NORM_IGNORENONSPACE**: *0x00000010*。 忽略非空格字符。<br /><br /> **NORM_IGNORESYMBOLS**: *0x00000100*。 忽略符号。<br /><br /> **NORM_IGNOREKANATYPE**: *0x00001000*。 不区分平假名字符和片假名字符。 比较时，相应的平假名和片假名字符视为等效。<br /><br /> **NORM_IGNOREWIDTH**: *0x00010000*。 不区分同一字符的单字节格式和双字节格式。<br /><br /> **SORT_STRINGSORT**: *0x00100000*。 标点与符号同等对待。|  
|DbpropMsmdCompareCaseSensitiveStringFlags|确定不区分大小写的字符串的比较和排序功能。 此属性可以控制不支持大写字符和小写字符的字符集中的比较方式，如对于日语的片假名和印地语。 此属性的值在进程线程第一个连接中设置，会影响该进程线程中的所有后续连接。<br /><br /> 有关 OLE DB 中字符串比较的详细信息，请在 MSDN Library 的 Platform SDK 部分中对“CompareString”进行搜索。<br /><br /> 此属性无默认值。<br /><br /> 此属性可与**发现**和**执行**方法。|可选的读/写**整数**属性|使用以下**名称**:**值**对以确定用于使用的标志：<br /><br /> **NORM_IGNORECASE**: *0x00000001*。 忽略大小写。<br /><br /> 不适用： <br />                          *0x00000002*。 二进制比较。 在字符集中，字符是按照其基础值进行比较的，而不是按照其特定的字符顺序进行比较。<br /><br /> **NORM_IGNORENONSPACE**: <br />                          *0x00000010*。 忽略非空格字符。<br /><br /> **NORM_IGNORESYMBOLS**: <br />                          *0x00000100*。 忽略符号。<br /><br /> **NORM_IGNOREKANATYPE**: <br />                          *0x00001000*。 <br />                        不区分平假名字符和片假名字符。 比较时，相应的平假名和片假名字符视为等效。<br /><br /> **NORM_IGNOREWIDTH**: <br />                          *0x00010000*。 <br />                        不区分同一字符的单字节格式和双字节格式。<br /><br /> **SORT_STRINGSORT**: <br />                          *0x00100000*。<br />                        标点与符号同等对待。|  
|DbpropMsmdDebugMode|*用法*<br /> 可选的读/写**字符串**属性<br /><br /> *说明*<br /> 保留供将来使用。<br /><br /> 此属性无默认值。<br /><br /> 此属性可与**发现**和**执行**方法。|||  
|DbpropMsmdDynamicDebugLimit|*用法*<br /> 可选的读/写**整数**属性<br /><br /> *说明*<br /> 保留供将来使用。<br /><br /> 此属性无默认值。<br /><br /> 此属性可与**发现**和**执行**方法。|||  
|DbpropMsmdFlattened2|*用法*<br /> 可选的读/写**布尔**属性<br /><br /> *说明*<br /> 除非轴 0 上需要父子层次结构，否则在简化结果中输出单个表列中父子层次结构的所有成员。 不使用输出列的级别模板。<br /><br /> 此属性的默认值是 FALSE。<br /><br /> 此属性可与**发现**和**执行**方法。|||  
|DbpropMsmdMDXCompatibility|*用法*<br /> 可选的读/写**整数**属性<br /><br /> *说明*<br /> 确定如何处理不规则或不对称层次结构中的占位符成员。 此属性可以有下列值：<br /><br /> ***0***<br /><br /> 为了与 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 的早期版本相兼容，此值与 1 等效。<br /><br /> ***1***<br /><br /> 角色扮演维度中的层次结构可以接收包含维度名称和层次结构名称的标题。 标题采用以下格式：`{Dimension].[Hierarchy]`占位符成员公开。<br /><br /> ***2***<br /><br /> 角色扮演维度中的层次结构可以接收包含维度名称和层次结构名称的标题，该标题的格式如下：<br /><br /> [Dimension].[Hierarchy]<br /><br /> 不公开占位符成员。<br /><br /> *3*<br /><br /> （默认值）不公开占位符成员。<br /><br /> 此属性可与**发现**和**执行**方法。|||  
|DbpropMsmdMDXUniqueNameStyle|*用法*<br /> 可选的读/写**整数**属性<br /><br /> *说明*<br /> 确定用于在维度中生成成员的唯一名称的算法。 此属性的值可以为下表中所列出的值。<br /><br /> ***0***<br /><br /> 为了与 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 的早期版本相兼容，此值与 2 等效。<br /><br /> ***1***<br /><br /> 使用注册表项路径算法：`[dim].&[key1].&[key2]`<br /><br /> ***2***<br /><br /> 使用名称路径算法：`[dim].[name1].&[name2]`<br /><br /> ***3***<br /><br /> 使用可长期保证稳定的唯一名称。<br /><br /> 此属性的默认值为 6。<br /><br /> 此属性可与**发现**和**执行**方法。|||  
|DbpropMsmdSQLCompatibility|保留供将来使用。<br /><br /> 此属性的默认值为零 (0)。<br /><br /> 此属性可与**发现**和**执行**方法。|可选的读/写**整数**属性||  
|DbpropMsmdSubQueries|确定子查询行为的位掩码。<br /><br /> 此属性的默认值为零或空。<br /><br /> 这是一个会话属性，仅在创建会话时可以设置。<br /><br /> 请参阅[中嵌套 select 语句和子多维数据集的计算成员](../../../analysis-services/multidimensional-models/mdx/calculated-members-in-subselects-and-subcubes.md)计算的成员或在嵌套 select 语句和子多维数据集的计算的集的行为的详细说明。|可选的读/写**整数**属性|此属性可以具有下列值之一：<br /><br /> *0*： 默认值，与早期版本的兼容[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。 在嵌套 select 或子多维数据集不允许计算的成员或计算的集...<br /><br /> *1*： 计算成员或计算的集允许在嵌套 select 或子多维数据集。 计算成员的祖先不包括在嵌套 select 语句或子多维数据集的空间中。<br /><br /> *2*： 计算成员或计算的集允许在嵌套 select 或子多维数据集。 计算成员的祖先包括在嵌套 select 语句或子多维数据集的空间中。|  
|DbpropMsmdUseFormulaCache|*用法*<br /> *说明*<br /> 保留供将来使用。<br /><br /> 此属性无默认值。<br /><br /> 此属性可与**发现**和**执行**方法。|||  
|DbpropMultiTableUpdate|*用法*<br /> 可选的只读**布尔**属性<br /><br /> *说明*<br /> 此属性与 OLE DB 属性 DBPROP_MULTITABLEUPDATE 等效。<br /><br /> 此属性的默认值是 FALSE。<br /><br /> 此属性可与**发现**和**执行**方法。|||  
|DbpropNullCollation|*用法*<br /> 可选的只读**整数**属性<br /><br /> *说明*<br /> 此属性与 OLE DB 属性 DBPROP_NULLCOLLATION 等效。<br /><br /> 此属性的默认值为 4，与 DBPROPVAL_NC_LOW 等效。<br /><br /> 此属性可与**发现**和**执行**方法。|||  
|DbpropOrderByColumnsInSelect|此属性与 OLE DB 属性 DBPROP_ORDERBYCOLUMNSINSELECT 等效。<br /><br /> 此属性的默认值是 FALSE。<br /><br /> 此属性可与**发现**和**执行**方法。|可选的只读**布尔**属性||  
|DbpropOutputParameterAvailable|此属性与 OLE DB 属性 DBPROP_OUTPUTPARAMETERAVAILABILITY 等效。<br /><br /> 此属性的默认值为 1，与 DBPROPVAL_OA_NOTSUPPORTED 等效。<br /><br /> 此属性可与**发现**和**执行**方法。|可选的只读**整数**属性||  
|DbpropPersistentIdType|此属性与 OLE DB 属性 DBPROP_PERSISTENTIDTYPE 等效。<br /><br /> 此属性的默认值为 4，与 DBPROPVAL_PT_NAME 等效。<br /><br /> 此属性可与**发现**和**执行**方法。|可选的只读**整数**属性||  
|DbpropPrepareAbortBehavior|此属性与 OLE DB 属性 DBPROP_PREPAREABORTBEHAVIOR 等效。<br /><br /> 此属性的默认值为 1，与 DBPROPVAL_CB_DELETE 等效。<br /><br /> 此属性可与**发现**和**执行**方法。|可选的只读**整数**属性||  
|DbpropPrepareCommitBehavior|此属性与 OLE DB 属性 DBPROP_PREPARECOMMITBEHAVIOR 等效。<br /><br /> 此属性的默认值为 1，与 DBPROPVAL_CB_DELETE 等效。<br /><br /> 此属性可与**发现**和**执行**方法。|可选的只读**整数**属性||  
|DbpropProcedureTerm|此属性与 OLE DB 属性 DBPROP_PROCEDURETERM 等效。<br /><br /> 此属性的默认值为“Calculated member”。<br /><br /> 此属性可与**发现**和**执行**方法。|可选的只读**字符串**属性||  
|DbpropQuotedIdentifierCase|此属性与 OLE DB 属性 DBPROP_QUOTEDIDENTIFIERCASE 等效。<br /><br /> 此属性的默认值为 8，与 DBPROPVAL_IC_MIXED 等效。<br /><br /> 此属性可与**发现**和**执行**方法。|可选只读**整数**属性||  
|DbpropSchemaUsage|此属性与 OLE DB 属性 DBPROP_SCHEMAUSAGE 等效。<br /><br /> 此属性的默认值为零 (0)。<br /><br /> 此属性可与**发现**和**执行**方法。|可选的只读**整数**属性||  
|DbpropSqlSupport|此属性与 OLE DB 属性 DBPROP_SQLSUPPORT 等效。<br /><br /> 此属性的默认值为 512，与 DBPROPVAL_SQL_SUBMINIMUM 等效。<br /><br /> 此属性可与**发现**和**执行**方法。|可选的只读**整数**属性||  
|DbpropSubqueries|此属性与 OLE DB 属性 DBPROP_SUBQUERIES 等效。<br /><br /> 注意： 尽管数据挖掘扩展插件 (DMX) 支持子查询，此属性是指在 SQL 中的子查询支持。<br /><br /> 此属性的默认值为零 (0)。<br /><br /> 此属性可与**发现**和**执行**方法。|可选的只读**整数**属性||  
|DbpropSupportedTxnDdl|此属性与 OLE DB 属性 DBPROP_SUPPORTEDTXNDDL 等效。<br /><br /> 此属性的默认值为零 (0)，与 DBPROPVAL_TC_NONE 等效。<br /><br /> 此属性可与**发现**和**执行**方法。|可选的只读**整数**属性||  
|DbpropSupportedTxnIsoLevels|此属性与 OLE DB 属性 DBPROP_SUPPORTEDTXNISOLEVELS 等效。<br /><br /> 此属性的默认值为 4096，与 DBPROPVAL_TI_READCOMMITTED 等效。<br /><br /> 此属性可与**发现**和**执行**方法。|可选的只读**整数**属性||  
|DbpropSupportedTxnIsoRetain|此属性与 OLE DB 属性 DBPROP_SUPPORTEDTXNISORETAIN 等效。<br /><br /> 此属性的默认值为 292，与 DBPROPVAL_TR_ABORT_NO、DBPROPVAL_TR_COMMIT_NO 和 DBPROPVAL_TR_NONE 的组合等效。<br /><br /> 此属性可与**发现**和**执行**方法。|可选的只读**整数**属性||  
|DbpropTableTerm|*用法*<br /> 可选的只读**字符串**属性<br /><br /> *说明*<br /> 此属性与 OLE DB 属性 DBPROP_TABLETERM 等效。<br /><br /> 此属性的默认值为“Cube”。<br /><br /> 此属性可与**发现**和**执行**方法。|||  
|Dialect|你可以使用**方言**属性时希望大部分查询，将通过任何其他使用一个特定的方言。<br /><br /> 对于语言方言，查询语法可以是相似的，如 DMX 和 SQL。 由于语法可以是相似的，所以 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 可能会无法从查询语法推断方言。 如果查询不在一种方言中运行，则 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例可能会尝试在其他方言中再次运行该查询。<br /><br /> 如果**方言**设置属性，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]返回查询中的优先级的方言的执行错误，即使该提供程序尝试在另一个方言中再次运行查询。 例如，**方言**属性设置为 MDGUID_DM。 提供程序第一次会尝试将该查询作为数据挖掘查询运行，但此查询会失败。 然后，提供程序将该查询重新提交为 SQL 查询。 同样此 SQL 查询也会失败。 因为的值**方言**属性是 MDGUID_DM，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]返回数据挖掘错误消息，不 SQL 错误消息。<br /><br /> 如果**方言**未设置属性，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]返回查询在上一次使用的方言执行错误。 例如，**方言**未设置属性，并在数据挖掘查询失败。 提供程序然后会查询为 SQL 重新提交。 该 SQL 查询同样也会失败。 因为**方言**未设置属性，该提供程序返回 SQL 错误消息而不是数据挖掘错误消息。<br /><br /> 此属性可与**发现**和**执行**方法。<br /><br /> 此属性无默认值。 建立以下情况下使用的方言：<br /><br /> -提供程序将使用第一个的方言时间提供程序尝试运行查询。<br /><br /> 的用于返回作为查询失败的结果执行错误方言。|可选的读/写**字符串**属性|以下**名称**:**值**对是方言可用于此属性：<br /><br /> **DBGUID_SQL**: <br />                          *C8B522D7-5CF3-11CE-ADE5-00AA0044773D*。 SQL 分析器具有优先权。<br /><br /> **MDGUID_DM**: <br />                          *62C58FED-CCA5-44F1-83B6-7B45682B3904*。 DMX 分析器具有优先权。<br /><br /> **MDGUID_MDX**: <br />                          *A07CCCD0-8148-11D0-87BB-00C04FC33942*。 MDX 分析器具有优先权。|  
|Disable Prefetch Facts|设置为 True 时，该引擎停止尝试预提取会话长度的值。<br /><br /> 此属性的默认值为 **False**。|可选的读/写**布尔**属性，||  
|EffectiveRoles|保留供将来使用。<br /><br /> 此属性无默认值。<br /><br /> 此属性可与**发现**和**执行**方法。|可选的只写**字符串**属性||  
|EffectiveUserName|指定连接到 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例时，用于覆盖用户名的帐户的名称。 属性的值是否不被规范化中的 MDX[用户名](../../../mdx/username-mdx.md)函数返回文本值，如果使用此属性。 只有服务器管理员才可以使用此属性。<br /><br /> 此属性支持以下 SID 类型：User、Group、Alias、WellKnownGroup、Computer。<br /><br /> 此属性无默认值。<br /><br /> 此属性可与**发现**和**执行**方法。|可选的只写**字符串**属性||  
|EndRange|指定一个从零开始的整数值对应于**CellOrdinal**属性值。 ( **CellOrdinal**属性是的一部分**单元格**中的元素**CellData**部分**MDDataSet**)。<br /><br /> 一起使用**BeginRange**属性，客户端应用程序可以使用此属性来限制由命令返回到特定范围的单元格的 OLAP 数据集。 如果指定-1，则所有单元格从指定的单元格**BeginRange**属性返回。<br /><br /> 此属性的默认值为-1。<br /><br /> 此属性可与**执行**方法。|可选的只写**整数**属性||  
|ExecutionMode|保留供将来使用。<br /><br /> 此属性的默认值是*执行*。<br /><br /> 此属性可与**发现**和**执行**方法。|可选的只写**字符串**属性||  
|ForceCommitTimeout|确定当前正在运行的 XMLA 命令在强制要求先前发出的命令进行回滚前，需要等待的提交阶段的时间（秒）。 提交阶段对应于 XMLA 命令如**语句**或**过程**。<br /><br /> 零值 (0) 指示实例要无限期等待。<br /><br /> 此属性的默认值为零 (0)。<br /><br /> 此属性可与**发现**和**执行**方法。|可选的只写**整数**属性||  
|格式|确定从返回的结果集的类型**发现**和**执行**方法。<br /><br /> 此属性的默认值是*本机*。<br /><br /> 此属性可与**发现**和**执行**方法。|可选的只写**字符串**属性|此属性可以有下列值：<br /><br /> *表格*： 返回的结果集使用[行集](../../../analysis-services/xmla/xml-data-types/rowset-data-type-xmla.md)数据类型。<br /><br /> *多维*： 返回行集使用[MDDataSet](../../../analysis-services/xmla/xml-data-types/mddataset-data-type-xmla.md)数据类型。<br /><br /> *本机*： 显式指定无格式。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 会为命令返回相应的格式。 实际结果类型由结果的命名空间识别。|  
|ImpactAnalysis|保留供将来使用。<br /><br /> 此属性的默认值为零 (0)。<br /><br /> 此属性可与**发现**和**执行**方法。|可选的只写**布尔**属性||  
|LocaleIdentifier|读取或设置使用的区域设置标识符 (LCID)**发现**或**执行**方法。 有关完整的语言标识符的十六进制列表，请在 MSDN Library 中查找“Language Identifiers”。<br /><br /> 此属性无默认值。<br /><br /> 此属性可与**发现**和**执行**方法。|可选的读/写**整数**属性||  
|MaximumRows|保留供将来使用。<br /><br /> 此属性无默认值。<br /><br /> 此属性可与**发现**和**执行**方法。|可选的只写**整数**属性||  
|MdpropAggregateCellUpdate|此属性与 OLE DB 属性 MDPROP_AGGREGATECELL_UPDATE 等效。<br /><br /> 此属性的默认值为 4，与 MDPROPVAL_AU_SUPPORTED 等效。<br /><br /> 此属性可与**发现**和**执行**方法。|可选的只读**整数**属性||  
|MdpropAxes|此属性与 OLE DB 属性 MDPROP_AXES 等效。<br /><br /> 此属性的默认值是 2147483647。<br /><br /> 此属性可与**发现**和**执行**方法。|可选的只读**整数**属性||  
|MdpropDrillFunctions|确定针对服务器的钻取功能的支持级别。<br /><br /> 此属性可与**发现**和**执行**方法。|可选的只读**整数**属性|下面的值用于生成有效的位掩码：<br /><br /> **MDPROPVAL_MDF_BASIC** (0x01)<br /><br /> **MDPROPVAL_MDF_ASYMMETRIC** (0x02)<br /><br /> **MDPROPVAL_MDF_CALC_MEMBERS** (0x04)<br /><br /> 默认值为：<br /><br /> 对于 SQL Server 2008 为 3<br /><br /> 对于 SQL Server 2008 R2 和 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 为 7|  
|MdpropFlatteningSupport|此属性与 OLE DB 属性 MDPROP_FLATTENING_SUPPORT 等效。<br /><br /> 此属性的默认值为 1，与 MDPROPVAL_FS_FULL_SUPPORT 等效。<br /><br /> 此属性可与**发现**和**执行**方法。|可选的只读**整数**属性||  
|MdpropMdxCaseSupport|此属性与 OLE DB 属性 MDPROP_MDX_CASESUPPORT 等效。<br /><br /> 此属性的默认值为零 (0)。<br /><br /> 此属性可与**发现**和**执行**方法。|可选的只读**整数**属性||  
|MdpropMdxDescFlags|此属性与 OLE DB 属性 MDPROP_MDX_DESCFLAGS 等效。<br /><br /> 此属性的默认值为 7，与 MDPROPVAL_MD_BEFORE、MDPROPVAL_MD_AFTER 和 MDPROPVAL_MD_SELF 等效。<br /><br /> 此属性可与**发现**和**执行**方法。|可选的只读**整数**属性||  
|MdpropMdxFormulas|此属性与 OLE DB 属性 MDPROP_MDX_FORMULAS 等效。<br /><br /> 此属性的默认值为 63，与 MDPROPVAL_MF_WITH_CALCMEMBERS、MDPROPVAL_MF_WITH_NAMEDSETS、MDPROPVAL_MF_CREATE_CALCMEMBERS、MDPROPVAL_MF_CREATE_NAMEDSETS、MDPROPVAL_MF_SCOPE_SESSION 和 MDPROPVAL_MF_SCOPE_GLOBAL 的组合等效。<br /><br /> 此属性可与**发现**和**执行**方法。|可选的只读**整数**属性||  
|MdpropMdxJoinCubes|此属性与 OLE DB 属性 MDPROP_MDX_JOINCUBES 等效。<br /><br /> 此属性的默认值为 1，与 MDPROPVAL_MJC_SINGLECUBE 等效。<br /><br /> 此属性可与**发现**和**执行**方法。|可选的只读**整数**属性||  
|MdpropMdxMemberFunctions|此属性与 OLE DB 属性 MDPROP_MDX_MEMBER_FUNCTIONS 等效。<br /><br /> 此属性的默认值为 15，与所有可用的 OLE DB 值的组合等效。<br /><br /> 此属性可与**发现**和**执行**方法。|可选的只读**整数**属性||  
|MdpropMdxNamedSets|此属性可用于创建命名集。|可选的只读**整数**属性|位掩码，可能为下表中所列的值。<br /><br /> ***0x01***<br /><br /> MDPROPVAL_MNS_BASIC。<br /><br /> ***0x02***<br /><br /> MDPROPVAL_MNS_DYNAMIC。<br /><br /> ***0x04，则***<br /><br /> MDPROPVAL_MNS_DISPLAYFOLDER。<br /><br /> ***0x08***<br /><br /> MDPROPVAL_MNS_CAPTION。<br /><br /> 此属性的默认值为 15。|  
|MdpropMdxNonMeasureExpressions|此属性与 OLE DB 属性 MDPROP_MDX_NONMEASURE_EXPRESSIONS 等效。<br /><br /> 此属性的默认值为零 (0)，与 MDPROPVAL_NME_ALLDIMENSIONS 等效。<br /><br /> 此属性可与**发现**和**执行**方法。|可选的只读**整数**属性||  
|MdpropMdxNumericFunctions|此属性与 OLE DB 属性 MDPROP_MDX_NUMERIC_FUNCTIONS 等效。<br /><br /> 此属性的默认值为 2047，与 MDPROPVAL_MNF_MEDIAN, MDPROPVAL_MNF_VAR、MDPROPVAL_MNF_STDDEV、MDPROPVAL_MNF_RANK、MDPROPVAL_MNF_AGGREGATE、MDPROPVAL_MNF_COVARIANCE、MDPROPVAL_MNF_CORRELATION、MDPROPVAL_MNF_LINREGSLOPE、MDPROPVAL_MNF_LINREGVARIANCE、MDPROPVAL_MNF_LINREG2 和 MDPROPVAL_MNF_LINREGPOINT 的组合等效。<br /><br /> 此属性可与**发现**和**执行**方法。|可选的只读**整数**属性||  
|MdpropMdxObjQualification|此属性与 OLE DB 属性 MDPROP_MDX_OBJQUALIFICATION 等效。<br /><br /> 此属性的默认值为 496，与 MDPROPVAL_MOQ_DIM_HIER、MDPROPVAL_MOQ_DIMHIER_LEVEL、MDPROPVAL_MOQ_DIMHIER_MEMBER、MDPROPVAL_MOQ_LEVEL_MEMBER 和 MDPROPVAL_MOQ_MEMBER_MEMBER 的组合等效。<br /><br /> 此属性可与**发现**和**执行**方法。|可选的只读**整数**属性||  
|MdpropMdxOuterReference|此属性与 OLE DB 属性 MDPROP_MDX_OUTERREFERENCE 等效。<br /><br /> 此属性的默认值为零 (0)。<br /><br /> 此属性可与**发现**和**执行**方法。|可选的只读**整数**属性||  
|MdpropMdxQueryByProperty|此属性与 OLE DB 属性 MDPROP_MDX_QUERYBYPROPERTY 等效。<br /><br /> 此属性的默认值为 TRUE。<br /><br /> 此属性可与**发现**和**执行**方法。|可选的只读**布尔**属性||  
|MdpropMdxRangeRowset|此属性与 OLE DB 属性 MDPROP_MDX_RANGEROWSET 等效。<br /><br /> 此属性的默认值为 4，与 MDPROPVAL_RR_UPDATE 等效。<br /><br /> 此属性可与**发现**和**执行**方法。|可选的只读**整数**属性||  
|MdpropMdxSetFunctions|此属性与 OLE DB 属性 MDPROP_MDX_SET_FUNCTIONS 等效。<br /><br /> 此属性的默认值为 524287，与 MDPROPVAL_MSF_TOPPERCENT、MDPROPVAL_MSF_BOTTOMPERCENT、MDPROPVAL_MSF_TOPSUM、MDPROPVAL_MSF_BOTTOMSUM、MDPROPVAL_MSF_PERIODSTODATE、MDPROPVAL_MSF_LASTPERIODS、MDPROPVAL_MSF_YTD、MDPROPVAL_MSF_QTD、MDPROPVAL_MSF_MTD、MDPROPVAL_MSF_WTD、MDPROPVAL_MSF_DRILLDOWNMEMBER、MDPROPVAL_MSF_DRILLDOWNLEVEL、MDPROPVAL_MSF_DRILLDOWNMEMBERTOP、MDPROPVAL_MSF_DRILLDOWNMEMBERBOTTOM、MDPROPVAL_MSF_DRILLDOWNLEVEL、MDPROPVAL_MSF_DRILLDOWNLEVELTOP、MDPROPVAL_MSF_DRILLDOWNLEVELBOTTOM、MDPROPVAL_MSF_DRILLUPMEMBER、MDPROPVAL_MSF_DRILLUPLEVEL 和 MDPROPVAL_MSF_TOGGLEDRILLSTATE 的组合等效。<br /><br /> 此属性可与**发现**和**执行**方法。|可选的只读**整数**属性||  
|MdpropMdxSlicer|此属性与 OLE DB 属性 MDPROP_MDX_SLICER 等效。<br /><br /> 此属性的默认值为 2，与 MDPROPVAL_MS_SINGLETUPLE 等效。<br /><br /> 此属性可与**发现**和**执行**方法。|可选的只读**整数**属性||  
|MdpropMdxStringCompop|此属性与 OLE DB 属性 MDPROP_MDX_STRING_COMPOP 等效。<br /><br /> 此属性的默认值为 15，与 MDPROPVAL_MSC_LESSTHAN、MDPROPVAL_MSC_GREATERTHAN、MDPROPVAL_MSC_LESSTHANEQUAL 和 MDPROPVAL_MSC_GREATERTHANEQUAL 的组合等效。<br /><br /> 此属性可与**发现**和**执行**方法。|可选的只读**整数**属性||  
|MdpropMdxSubQueries|指示对 MDX 中子查询的支持级别。<br /><br /> 值 63 是此属性在 SQL Server 2014 中的默认值。<br /><br /> 值 31 是此属性在 SQL Server 2008 R2 和 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 中的默认值<br /><br /> 值 15 是此属性在 SQL Server 2008 中的默认值<br /><br /> 值 3 是在此属性的默认值[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。|可选的只读**整数**属性|此属性的有效值是一个位屏蔽，由以下值：<br /><br /> *0x01*: **MDPROPVAL_MSQ_BASIC**<br /><br /> *0x02*: **MDPROPVAL_MSQ_ARBITRARYSHAPE**<br /><br /> *0x04，则*: **MDPROPVAL_MSQ_NONVISUAL**<br /><br /> *0x08*: **MDPROPVAL_MSQ_CALCMEMBERS**<br /><br /> *0x10*: **MDPROPVAL_MSQ_CALCMEMBERS2**|  
|MdpropNamedLevels|此属性与 OLE DB 属性 MDPROP_NAMED_LEVELS 等效。<br /><br /> 此属性的默认值为 3，与 MDPROPVAL_NL_NAMEDLEVELS 和 MDPROPVAL_NL_NUMBEREDLEVELS 的组合等效。<br /><br /> 此属性可与**发现**和**执行**方法。|可选的只读**整数**属性||  
|MdxMissingMemberMode|指示是否在 MDX 语句中忽略缺少的成员。<br /><br /> 此属性与 OLE DB 属性 DBPROP_MDX_MISSING_MEMBER_MODE 等效。<br /><br /> 此属性的默认值是*默认*。<br /><br /> 此属性可与**发现**和**执行**方法。|可选的只写**字符串**属性|此属性可以具有下列值之一：<br /><br /> *默认*： 使用生成的值[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]实例。<br /><br /> *错误*： 生成错误。<br /><br /> *忽略*： 始终忽略缺少的成员。|  
|MDXSupport|指定一个说明 MDX 支持的程度的枚举。<br /><br /> 此属性的默认值是*核心*。<br /><br /> 此属性可与**发现**方法。<br /><br /> 请注意，目前，唯一有效的值为此枚举是*核心*。 其他值可能为将来的此枚举定义。|可选的只读**字符串**属性|此属性可以具有以下值：<br /><br /> *核心*： 支持所有 MDX 选项。|  
|NonEmptyThreshold|保留供将来使用。<br /><br /> 此属性无默认值。<br /><br /> 此属性可与**发现**和**执行**方法。|可选的读/写**整数**属性||  
|密码|不再支持此属性。<br /><br /> 为了向后兼容，而不会生成错误一起使用时将忽略了此属性**执行**或**发现**方法。|只写的可选**字符串**属性||  
|ProviderName|此属性与 OLE DB 属性 DBPROP_DBMSNAME 等效。<br /><br /> 此属性的默认值为“OLAP Server”。<br /><br /> 此属性可与**发现**方法。|可选的只读**字符串**属性||  
|ProviderType|此属性与 OLE DB 属性 DBPROP_DATASOURCE_TYPE 等效。<br /><br /> 此属性的默认值为 6。<br /><br /> 此属性可与**发现**和**执行**方法。|可选的只读**整数**属性||  
|ProviderVersion|此属性与 OLE DB 属性 DBPROP_DBMSVER 等效。<br /><br /> 此属性的默认值为 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例的版本。<br /><br /> 此属性可与**发现**方法。|可选的只读**字符串**属性||  
|ReadOnlySession|保留供将来使用。<br /><br /> 此属性无默认值。<br /><br /> 此属性可与**发现**和**执行**方法。|可选的读/写**整数**属性||  
|RealTimeOlap|设置为 TRUE 时，指示所有侦听表通知的分区都将实时查询，跳过缓存操作。 此属性与 OLE DB 属性 DBPROP_MSMD_REAL_TIME_OLAP 等效。<br /><br /> 此属性的默认值是 FALSE。<br /><br /> 此属性可与**发现**和**执行**方法。|可选的读/写**布尔**属性||  
|ReturnCellProperties|指定是否将返回单元属性。<br /><br /> 此属性的默认值是 FALSE。<br /><br /> 此属性可与**发现**和**执行**方法。|可选的读/写**布尔**属性||  
|角色|指定一个以逗号分隔的、客户端应用程序用以连接到 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例的角色名称字符串。 此属性允许用户使用其当前所用角色以外的角色进行连接。 例如，服务器管理员可能会为了测试授予给角色的权限，而希望以角色成员连接到多维数据集。 这种情况下，该用户就必须为使用此属性进行连接而指定的角色的成员。<br /><br /> **\*\*重要\* \*** 角色名称区分大小写，并且不应使用以逗号分隔的角色名称之间的空格。 否则，为了保护单元集，查询可能会返回错误和意外结果。<br /><br /> 此属性无默认值。<br /><br /> 此属性可与**发现**和**执行**方法。|可选的读/写**字符串**属性||  
|SafetyOptions|确定客户端应用程序是否可以注册和加载不安全的库。<br /><br /> 此属性的值还可以确定本地多维数据集中是否允许 PASSTHROUGH 关键字。 下列情况下可能会发生错误：<br /><br /> -如果客户端应用程序尝试使用 INSERT INTO 语句，其中包含传递关键字创建本地多维数据集。<br /><br /> -如果客户端应用程序尝试更新本地多维数据集包含使用传递关键字的 INSERT INTO 语句。<br /><br /> 此属性无默认值。<br /><br /> 此属性可与**发现**和**执行**方法。|可选的读/写**整数**属性|此属性可以具有以下所列的值之一**名称**:**值**对：<br /><br /> **DBPROPVAL_MSMD_SAFETY_OPTIONS_DEFAULT**: <br />                          *0*。此值将被视为 DBPROPVAL_MSMD_SAFETY_OPTIONS_ALLOW_SAFE。对于连接到本地多维数据集，此值取决于是否使用 CREATECUBE 连接字符串属性。 如果使用 CREATECUBE 连接字符串属性，则此属性将与 DBPROPVAL_MSMD_SAFETY_OPTIONS_ALLOW_ALL 相同。 否则，此属性与 DBPROPVAL_MSMD_SAFETY_OPTIONS_ALLOW_SAFE 相同。<br /><br /> **DBPROPVAL_MSMD_SAFETY_OPTIONS_ALLOW_ALL**: <br />                          *1*。此值可启用所有用户定义的功能库，且不用验证对于初始化和脚本编写，这些功能库是否是安全的。 对于到本地多维数据集的连接，此属性可帮助实现使用存储过程和在 INSERT INTO 语句中使用 PASSTHROUGH 关键字。 **\*\*安全说明\* \*** ： 不建议使用此选项。<br /><br /> **DBPROPVAL_MSMD_SAFETY_OPTIONS_ALLOW_SAFE**: <br />                          *2*。此值可确保对用户定义的特定功能库的所有类进行检查，以确保它们对于初始化和编写脚本是安全的。 对于到本地多维数据集的连接，此值不但可以阻止在 INSERT INTO 语句中使用 PASSTHROUGH 关键字，还可以阻止使用其 PermissionSet 属性未设置为“Safe”的 PASSTHROUGH。 此值还会删除中的操作[MDSCHEMA_ACTIONS](../../../analysis-services/schema-rowsets/ole-db-olap/mdschema-actions-rowset.md) ACTION_TYPE 列中具有值为 HTML 或命令或在内容列不具有 ACTION_TYPE 列中的 URL 的值和值的架构行集以"http://"或"https://"开头。<br /><br /> **DBPROPVAL_MSMD_SAFETY_OPTIONS_ALLOW_NONE**: <br />                          *3*： 此值可以防止用户定义函数在会话期间使用。 对于到本地多维数据集的连接，此属性可阻止使用所有存储过程和在 INSERT INTO 语句中使用 PASSTHROUGH 关键字。 此属性还可删除 MDSCHEMA_ACTIONS 架构集中的所有操作。|  
|SecuredCellValue|指定的错误代码和的值**值**和**格式值**单元格它尝试访问的受保护的单元格时要返回的属性。<br /><br /> 此属性可与**发现**和**执行**方法。|可选的读/写**整数**属性|此属性可以具有下列值之一：<br /><br /> *0*： 默认值。 为了与早期版本兼容，此值等同于*1*。 此默认值的含义在将来版本中可能会发生变化。<br /><br /> *1*： 返回的 HRESULT = NO_ERROR。 **值**单元格的属性包含为 variant 数据类型的结果。 在中返回字符串"# n/A"**格式值**属性。<br /><br /> *2*： 作为 HRESULT 的值将返回错误。<br /><br /> *3*： 中都返回 NULL**值**和**格式值**属性。<br /><br /> *4*： 返回数字零 (0) 中**值**属性，并返回格式化的零**格式值**属性。 例如，在返回 0.00**格式值**属性的单元格其**格式**属性是"#。 # #"。<br /><br /> *5*： 在这两返回字符串"#SEC"**值**和**格式值**属性。|  
|ServerName|此属性与 OLE DB 属性 DBPROP_SERVERNAME 等效。<br /><br /> 此属性的默认值为 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例的名称。<br /><br /> 此属性可与**发现**和**执行**方法。|可选的只读**字符串**属性||  
|ShowHiddenCubes|保留供将来使用。<br /><br /> 此属性的默认值是 FALSE。<br /><br /> 此属性可与**发现**和**执行**方法。|可选的读/写**布尔**属性||  
|SQLQueryMode|确定是否在 SQL 查询中包含计算。<br /><br /> 此属性的默认值是*计算*。<br /><br /> 此属性可与**发现**和**执行**方法。|可选的读/写**字符串**属性|此属性可以具有下列值之一：<br /><br /> *数据*： 没有计算是包含。<br /><br /> *计算*： 返回计算。<br /><br /> *IncludeEmpty*： 返回计算和为空的行。|  
|SQLSupport|指定提供程序上可用的 SQL 支持的类型。<br /><br /> 此属性的默认值为 512。<br /><br /> 此属性可与**发现**和**执行**方法。|可选的只读**整数**属性||  
|SspropInitAppName|包含客户端应用程序的名称。<br /><br /> 此属性无默认值。<br /><br /> 此属性可与**发现**和**执行**方法。|可选的读/写**字符串**属性||  
|SspropInitPacketsize|包含客户端应用程序的 ID。<br /><br /> 此属性无默认值。<br /><br /> 此属性可与**发现**和**执行**方法。|可选的读/写**整数**属性||  
|SspropInitWsid|包含客户端工作站的 ID。<br /><br /> 此属性无默认值。<br /><br /> 此属性可与**发现**和**执行**方法。|可选的读/写**字符串**属性||  
|StateSupport|指定对状态的支持程度。<br /><br /> 有关 statefulness 和会话支持的详细信息，请参阅[管理连接和会话 &#40;XMLA &#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md).<br /><br /> 此属性的默认值是*会话*。<br /><br /> 此属性可与**发现**方法。|可选的只读**字符串**属性|此属性可以具有下列值之一：<br /><br /> *无*: Statefulness 不支持。<br /><br /> *会话*: Statefulness 提供通过会话支持。|  
|超时|指定 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例在返回错误前，应等待请求的最长时间（以秒为单位）。 此属性还可确定实例在返回错误前，应等待更新成功回写表的最长时间，与连接字符串属性 Writeback Timeout 等效。<br /><br /> 此属性的默认值为零 (0)。<br /><br /> 此属性可与**发现**和**执行**方法。|可选的读/写**整数**属性||  
|TransactionDDL|保留供将来使用。<br /><br /> 此属性的默认值为 0。<br /><br /> 此属性可与**发现**和**执行**方法。|可选的只读**整数**属性||  
|UserName|不再支持此属性。<br /><br /> 指定一个字符串，该字符串可返回 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例用以关联命令的用户名称。 为了向后兼容，而不会生成错误一起使用时将忽略了此属性**执行**或**发现**方法。 此属性与 OLE DB 属性 DBPROP_USERNAME 等效。<br /><br /> 此属性的默认值为打开当前会话或连接的用户名称。<br /><br /> 此属性可与**执行**方法。|可选的只读**字符串**属性||  
|VisualMode|此属性与 OLE DB 属性 MDPROP_VISUALMODE 等效。<br /><br /> 此属性的默认值为零 (0)，与 DBPROPVAL_VISUAL_MODE_DEFAULT 等效。<br /><br /> 此属性可与**发现**和**执行**方法。|可选的只写**整数**属性||  
  
## <a name="see-also"></a>另请参阅  
 [PropertyList 元素 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/propertylist-element-xmla.md)  
  
  

