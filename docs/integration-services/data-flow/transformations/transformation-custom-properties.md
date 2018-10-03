---
title: 转换自定义属性 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Aggregate transformation [Integration Services]
- Slowly Changing Dimension transformation
- Import Column transformation [Integration Services]
- Sort transformation
- Unpivot transformation
- Merge Join transformation
- Data Mining Query transformation
- Fuzzy Grouping transformation
- Data Conversion transformation
- Fuzzy Lookup transformation
- Term Extraction transformation
- Row Count transformation custom properties [Integration Services]
- transformations [Integration Services], properties
- Pivot transformation
- Lookup transformation
- Percentage Sampling transformation
- Export Column transformation [Integration Services]
- Row Sampling transformation
- Conditional Split transformation custom properties [Integration Services]
- custom properties [Integration Services]
- Audit transformation
- Term Lookup transformation
- Script Component transformation custom properties [Integration Services]
- Derived Column transformation
- OLE DB Command transformation
- Copy Column transformation custom properties [Integration Services]
- Character Map transformation custom properties [Integration Services]
ms.assetid: 56f5df6a-56f6-43df-bca9-08476a3bd931
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: cee76028cbc0e416b320a8042eaf577dfeb621ec
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47722935"
---
# <a name="transformation-custom-properties"></a>Transformation Custom Properties
  在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 对象模型中，除了对大多数数据流对象通用的属性以外，许多数据流对象还具有特定于该对象的自定义属性。 这些自定义属性仅在运行时可用，并未记录在 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 托管编程参考文档中。  
  
 本主题列出并描述了各种数据流转换的自定义属性。 有关对大多数数据流对象都通用的属性的信息，请参阅 [Common Properties](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)。  
  
 某些转换属性可以使用属性表达式进行设置。 有关详细信息，请参阅 [可以使用表达式设置的数据流属性](http://msdn.microsoft.com/library/cd0e171a-08be-45d6-81dc-ed94f37698b8)。  
  
## <a name="transformations-with-custom-properties"></a>包含自定义属性的转换  
  
||||  
|-|-|-|  
|[Aggregate](#aggregate)|[导出列](#extract)|[行计数](#rowcount)|  
|[审核](#audit)|[模糊分组](#fgroup)|[行抽样](#rowsamp)|  
|[缓存转换](#cachetransform)|[模糊查找](#flookup)|[脚本组件](#script)|  
|[字符映射](#charmap)|[导入列](#insert)|[渐变维度](#scd)|  
|[有条件拆分](#condsplit)|[查找](#lookup)|[排序](#sort)|  
|[复制列](#copymap)|[合并联接](#mjoin)|[字词提取](#textract)|  
|[数据转换](#dataconv)|[OLE DB 命令](#oledbcmd)|[字词查找](#tlookup)|  
|[数据挖掘查询](#dmquery)|[百分比抽样](#percent)|[逆透视](#unpivot)|  
|[派生列](#derived)|[透视](#pivot)||  
  
### <a name="transformations-without-custom-properties"></a>不包含自定义属性的转换  
 以下转换不包含组件级、输入级或输出级自定义属性： [Merge Transformation](../../../integration-services/data-flow/transformations/merge-transformation.md)、 [Multicast Transformation](../../../integration-services/data-flow/transformations/multicast-transformation.md)和 [Union All Transformation](../../../integration-services/data-flow/transformations/union-all-transformation.md)。 这些转换仅使用对所有数据流组件均通用的属性。  
  
##  <a name="aggregate"></a> 聚合转换自定义属性  
 聚合转换既包含自定义属性，又包含对所有数据流组件通用的属性。  
  
 下表介绍聚合转换的自定义属性。 所有属性均可读/写。  
  
|“属性”|数据类型|描述|  
|--------------|---------------|-----------------|  
|AutoExtendFactor|Integer|一个介于 1 和 100 之间的值，用于指定在聚合过程中内存可扩展的百分比。 此属性的默认值为 **25**。|  
|CountDistinctKeys|Integer|该值用于指定聚合可以写入的非重复值的精确数目。 如果指定了 CountDistinctScale 值，则 CountDistinctKeys 中的值优先。|  
|CountDistinctScale|Integer（枚举）|该值用于说明聚合可以计数的列中非重复值的大致数目。 此属性可以具有下列值之一：<br /><br /> **低** (1) — 指示最多 500,000 个键值<br /><br /> **中** (2) — 指示最多 500 万个键值<br /><br /> **高** (3) — 指示超过 2500 万个键值。<br /><br /> **未指定** (0) — 指示未使用 CountDistinctScale 值。 使用“未指定”(0) 选项可能会影响大型数据集的性能。|  
|键|Integer|该值用于指定聚合写入的分组依据键的精确数目。 如果指定了 KeyScale 值，则 Keys 中的值优先。|  
|KeyScale|Integer（枚举）|该值用于说明聚合可以写入的分组依据键值的大致数目。 此属性可以具有下列值之一：<br /><br /> **低** (1) — 指示最多 500,000 个键值。<br /><br /> **中** (2) — 指示最多 500 万个键值。<br /><br /> **高** (3) — 指示超过 2500 万个键值。<br /><br /> **未指定** (0) — 指示未使用 KeyScale 值。|  
  
 下表介绍聚合转换的输出的自定义属性。 所有属性均可读/写。  
  
|“属性”|数据类型|描述|  
|--------------|---------------|-----------------|  
|键|Integer|该值用于指定聚合可以写入的分组依据键的精确数目。 如果指定了 KeyScale 值，则 Keys 中的值优先。|  
|KeyScale|Integer（枚举）|该值用于说明聚合可以写入的分组依据键值的大致数目。 此属性可以具有下列值之一：<br /><br /> **低** (1) — 指示最多 500,000 个键值，<br /><br /> **中** (2) — 指示最多 500 万个键值，<br /><br /> **高** (3) — 指示超过 2500 万个键值。<br /><br /> **未指定** (0) — 指示未使用 KeyScale 值。|  
  
 下表介绍聚合转换的输出列的自定义属性。 所有属性均可读/写。  
  
|“属性”|数据类型|描述|  
|--------------|---------------|-----------------|  
|AggregationColumnId|Integer|参与 GROUP BY 或聚合函数的列的 **LineageID** 。|  
|AggregationComparisonFlags|Integer|该值用于指定聚合转换如何比较列中的字符串数据。 有关详细信息，请参阅 [Comparing String Data](../../../integration-services/data-flow/comparing-string-data.md)。|  
|AggregationType|Integer（枚举）|该值用于指定要对列执行的聚合操作。 此属性可以具有下列值之一：<br /><br /> **Group by** (0)<br /><br /> **Count** (1)<br /><br /> **Count all** (2)<br /><br /> **Countdistinct** (3)<br /><br /> **Sum** (4)<br /><br /> **Average** (5)<br /><br /> **Maximum** (7)<br /><br /> **Minimum** (6)|  
|CountDistinctKeys|Integer|该值用于指定聚合类型为 **Count distinct**时聚合可以写入的键的精确数目。 如果指定了 CountDistinctScale 值，则 CountDistinctKeys 中的值优先。|  
|CountDistinctScale|Integer（枚举）|该值用于指定聚合类型为 **Count distinct**时聚合可以写入的键值的大致数目。 此属性可以具有下列值之一：<br /><br /> **低** (1) — 指示最多 500,000 个键值，<br /><br /> **中** (2) — 指示最多 500 万个键值，<br /><br /> **高** (3) — 指示超过 2500 万个键值。<br /><br /> **未指定** (0) — 指示未使用 CountDistinctScale 值。|  
|IsBig|Boolean|该值用于指示列是包含大于 40 亿的值还是精度超过双精度浮点值的值。 该值可以是 0 或 1。 0 指示 IsBig 为 **False** 并且该列不包含大值或精确值。 此属性的默认值为 1。|  
  
 聚合转换的输入和输入列不包含自定义属性。  
  
 有关详细信息，请参阅 [Aggregate Transformation](../../../integration-services/data-flow/transformations/aggregate-transformation.md)。  
  
##  <a name="audit"></a> 审核转换自定义属性  
 审核转换仅包含在组件级别对所有数据流组件通用的属性。  
  
 下表介绍审核转换的输出列的自定义属性。 所有属性均可读/写。  
  
|属性名称|数据类型|描述|  
|-------------------|---------------|-----------------|  
|LineageItemSelected|Integer（枚举）|针对输出选定的审核项。 此属性可以具有下列值之一：<br /><br /> **执行实例 GUID** (0)<br /><br /> **执行开始时间** (4)<br /><br /> **计算机名称** (5)<br /><br /> **包 ID** (1)<br /><br /> **包名称** (2)<br /><br /> **任务 ID** (8)<br /><br /> **任务名称** (7)<br /><br /> **用户名** (6)<br /><br /> **版本 ID** (3)|  
  
 审核转换的输入、输入列和输出都不包含自定义属性。  
  
 有关详细信息，请参阅 [Audit Transformation](../../../integration-services/data-flow/transformations/audit-transformation.md)。  
  
##  <a name="cachetransform"></a> “缓存转换”转换自定义属性  
 “缓存转换”转换既包含自定义属性，也包含对所有数据流组件通用的属性。  
  
 下表介绍“缓存转换”转换的属性。 所有属性均可读/写。  
  
|“属性”|数据类型|描述|  
|--------------|---------------|-----------------|  
|Connectionmanager|String|指定连接管理器的名称。|  
|ValidateExternalMetadata|Boolean|指示在设计时是否已使用外部数据源对缓存转换进行了验证。 如果将该属性设置为 **False**，则会在运行时针对外部数据源进行验证。<br /><br /> 默认值为 **True**。|  
|AvailableInputColumns|String|可用输入列的列表。|  
|InputColumns|String|选定输入列的列表。|  
|CacheColumnName|String|指定映射到选定输入列的列名称。<br /><br /> CacheColumnName 属性中的列名称必须与“缓存连接管理器编辑器”的“列”页中列出的对应列的名称相匹配。<br /><br /> 有关详细信息，请参阅 [Cache Connection Manager Editor](../../../integration-services/data-flow/transformations/cache-connection-manager-editor.md)|  
  
##  <a name="charmap"></a> 字符映射转换自定义属性  
 字符映射转换仅包含在组件级别对所有数据流组件通用的属性。  
  
 下表介绍字符映射转换的输出列的自定义属性。 所有属性均可读/写。  
  
|“属性”|数据类型|描述|  
|--------------|---------------|-----------------|  
|InputColumnLineageId|Integer|该值用于指定作为输出列的源的输入列的 **LineageID** 。|  
|MapFlags|Integer（枚举）|该值用于指定字符映射转换对列执行的字符串操作。 此属性可以具有下列值之一：<br /><br /> **字节反转** (2)<br /><br /> **全角** (6)<br /><br /> **半角** (5)<br /><br /> **平假名** (3)<br /><br /> **片假名** (4)<br /><br /> **语言中的大小写** (7)<br /><br /> **小写** (0)<br /><br /> **简体中文** (8)<br /><br /> **繁体中文**(9)<br /><br /> **大写** (1)|  
  
 字符映射转换的输入、输入列和输出都不包含自定义属性。  
  
 有关详细信息，请参阅 [Character Map Transformation](../../../integration-services/data-flow/transformations/character-map-transformation.md)。  
  
##  <a name="condsplit"></a> 有条件拆分转换自定义属性  
 有条件拆分转换仅包含在组件级别对所有数据流组件通用的属性。  
  
 下表介绍有条件拆分转换的输出的自定义属性。 所有属性均可读/写。  
  
|“属性”|数据类型|描述|  
|--------------|---------------|-----------------|  
|EvaluationOrder|Integer|该值用于指定有条件拆分转换所计算的条件列表中与某个输出关联的条件的位置。 条件按值从低到高的顺序进行计算。|  
|表达式|String|表示有条件拆分转换所计算的条件的表达式。 列由沿袭标识符表示。|  
|FriendlyExpression|String|表示有条件拆分转换所计算的条件的表达式。 列由列名称表示。<br /><br /> 此属性的值可以使用属性表达式来指定。|  
|IsDefaultOut|Boolean|该值用于指示输出是否为默认输出。|  
  
 有条件拆分转换的输入、输入列和输出列不包含自定义属性。  
  
 有关详细信息，请参阅 [Conditional Split Transformation](../../../integration-services/data-flow/transformations/conditional-split-transformation.md)。  
  
##  <a name="copymap"></a> 复制列转换自定义属性  
 复制列转换仅包含在组件级别对所有数据流组件通用的属性。  
  
 下表介绍复制列转换的输出列的自定义属性。 所有属性均可读/写。  
  
|属性名称|数据类型|描述|  
|-------------------|---------------|-----------------|  
|copyColumnId|Integer|从中复制输出列的输入列的 **LineageID** 。|  
  
 复制列转换的输入、输入列和输出不包含自定义属性。  
  
 有关详细信息，请参阅 [Copy Column Transformation](../../../integration-services/data-flow/transformations/copy-column-transformation.md)。  
  
##  <a name="dataconv"></a> 数据转换自定义属性  
 数据转换仅包含在组件级别对所有数据流组件通用的属性。  
  
 下表介绍数据转换的输出列的自定义属性。 所有属性均可读/写。  
  
|“属性”|数据类型|描述|  
|--------------|---------------|-----------------|  
|FastParse|Boolean|该值用于指示列是使用 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 提供的不区分区域设置的较快分析例程，还是使用标准的区分区域设置的分析例程。 此属性的默认值为 **False**。 有关详细信息，请参阅 [Fast Parse](http://msdn.microsoft.com/library/6688707d-3c5b-404e-aa2f-e13092ac8d95) 和 [Standard Parse](http://msdn.microsoft.com/library/dfe835b1-ea52-4e18-a23a-5188c5b6f013)。 实例时都提供 SQL Server 登录名。<br /><br /> 注意：此属性在“数据转换编辑器” 中不可用，但可通过“高级编辑器” 进行设置。|  
|SourceInputColumnLineageId|Integer|作为输出列的源的输入列的 **LineageID** 。|  
  
 数据转换的输入、输入列和输出不包含自定义属性。  
  
 有关详细信息，请参阅 [Data Conversion Transformation](../../../integration-services/data-flow/transformations/data-conversion-transformation.md)。  
  
##  <a name="dmquery"></a> 数据挖掘查询转换自定义属性  
 数据挖掘查询转换既包含自定义属性，也包含对所有数据流组件通用的属性。  
  
 下表介绍数据挖掘查询转换的自定义属性。 所有属性均可读/写。  
  
|“属性”|数据类型|描述|  
|--------------|---------------|-----------------|  
|ASConnectionId|String|连接对象的唯一标识符。|  
|ASConnectionString|String|某个 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 项目或 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 数据库的连接字符串。|  
|CatalogName|String|[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 数据库的名称。|  
|ModelName|String|数据挖掘模型的名称。|  
|ModelStructureName|String|挖掘结构的名称。|  
|ObjectRef|String|标识转换使用的数据挖掘结构的 XML 标记。|  
|QueryText|String|转换所使用的预测查询语句。|  
  
 数据挖掘查询转换的输入、输入列、输出和输出列不包含自定义属性。  
  
 有关详细信息，请参阅 [Data Mining Query Transformation](../../../integration-services/data-flow/transformations/data-mining-query-transformation.md)。  
  
##  <a name="derived"></a> 派生列转换自定义属性  
 派生列转换仅包含在组件级别对所有数据流组件通用的属性。  
  
 下表介绍派生列转换的输入列和输出列的自定义属性。 如果选择将派生列添加为新列，则这些自定义属性将应用到新的输出列；如果选择将现有输入列的内容替换为派生结果，则这些自定义属性将应用到现有输入列。 所有属性均可读/写。  
  
|“属性”|数据类型|描述|  
|--------------|---------------|-----------------|  
|表达式|String|表示有条件拆分转换所计算的条件的表达式。 列由列的 **LineageID** 属性表示。|  
|FriendlyExpression|String|表示有条件拆分转换所计算的条件的表达式。 列由列名称表示。<br /><br /> 此属性的值可以使用属性表达式来指定。|  
  
 派生列转换的输入和输出不包含自定义属性。  
  
 有关详细信息，请参阅 [Derived Column Transformation](../../../integration-services/data-flow/transformations/derived-column-transformation.md)。  
  
##  <a name="extract"></a> 导出列转换自定义属性  
 导出列转换仅包含在组件级别对所有数据流组件通用的属性。  
  
 下表介绍导出列转换的输入列的自定义属性。 所有属性均可读/写。  
  
|“属性”|数据类型|描述|  
|--------------|---------------|-----------------|  
|AllowAppend|Boolean|该值用于指定转换是否向现有文件追加数据。 此属性的默认值为 **False**。|  
|ForceTruncate|Boolean|该值用于指定转换是否在写入数据之前截断现有文件。 此属性的默认值为 **False**。|  
|FileDataColumnID|Integer|该值用于标识包含转换插入到文件中的数据的列。 在“提取列”上，该属性的值为 **0**；在“文件路径列”上，该属性包含提取列的 **LineageID** 。|  
|WriteBOM|Boolean|该值用于指定是否将字节顺序标记 (BOM) 写入文件中。|  
  
 导出列转换的输入、输出和输出列不包含自定义属性。  
  
 有关详细信息，请参阅 [Export Column Transformation](../../../integration-services/data-flow/transformations/export-column-transformation.md)。  
  
##  <a name="insert"></a> 导入列转换自定义属性  
 导入列转换仅包含在组件级别对所有数据流组件通用的属性。  
  
 下表介绍导入列转换的输入列的自定义属性。 所有属性均可读/写。  
  
|“属性”|数据类型|描述|  
|--------------|---------------|-----------------|  
|ExpectBOM|Boolean|该值用于指定导入列转换是否需要使用字节顺序标记 (BOM)。 仅当数据为 DT_NTEXT 数据类型时才需要 BOM。|  
|FileDataColumnID|Integer|该值用于标识包含转换插入到数据流中的数据的列。 在要插入的数据列上，此属性的值为 0；在包含源文件路径的列上，此属性包含要插入的数据列的 **LineageID** 。|  
  
 导入列转换的输入、输出和输出列不包含自定义属性。  
  
 有关详细信息，请参阅 [Import Column Transformation](../../../integration-services/data-flow/transformations/import-column-transformation.md)。  
  
##  <a name="fgroup"></a> 模糊分组转换自定义属性  
 模糊分组转换既包含自定义属性，也包含对所有数据流组件通用的属性。  
  
 下表介绍模糊分组转换的自定义属性。 所有属性均可读/写。  
  
|“属性”|数据类型|描述|  
|--------------|---------------|-----------------|  
|Delimiters|String|转换所使用的标记分隔符。 默认分隔符包括以下字符：空格 ( )、逗号 (,)、句点 (.)、分号 (;)、冒号 (:)、连字符 (-)、双直引号 (")、单直引号 (')、与号 (&)、斜杠 (/)、反斜杠 (\\)、at 符号 (@)、感叹号 (!)、问号 (?)、左括号 (()、右括号 ())、小于号 (\<)、大于号 (>)、左方括号 ([)、右方括号 (])、左大括号 ({)、右大括号 (})、竖线 (&#124;)、数字符号 (#)、星号 (*)、脱字号 (^) 和百分号 (%)。|  
|Exhaustive|Boolean|该值用于指定是否将每个输入记录与所有其他输入记录进行比较。 值 **True** 主要用于调试目的。 此属性的默认值为 **False**。<br /><br /> 注意：此属性在“模糊分组转换编辑器” 中不可用，但可通过“高级编辑器” 进行设置。|  
|MaxMemoryUsage|Integer|转换所使用的最大内存量。 此属性的默认值为 **0**，该值将启用动态内存使用。<br /><br /> 此属性的值可以使用属性表达式来指定。<br /><br /> 注意：此属性在“模糊分组转换编辑器” 中不可用，但可通过“高级编辑器” 进行设置。|  
|MinSimilarity|双精度|转换用来标识重复值的相似性阈值，以 0 和 1 之间的值表示。  此属性的默认值为 0.8。|  
  
 下表介绍模糊分组转换的输入列的自定义属性。 所有属性均可读/写。  
  
|“属性”|数据类型|描述|  
|--------------|---------------|-----------------|  
|ExactFuzzy|Integer（枚举）|该值用于指定转换是执行模糊匹配还是完全匹配。 有效值是 **Exact** 和 **Fuzzy**。 此属性的默认值为 **Fuzzy**。|  
|FuzzyComparisonFlags|Integer（枚举）|该值用于指定转换如何比较列中的字符串数据。 此属性可以具有下列值之一：<br /><br /> **FullySensitive**<br /><br /> **IgnoreCase**<br /><br /> **IgnoreKanaType**<br /><br /> **IgnoreNonSpace**<br /><br /> **IgnoreSymbols**<br /><br /> **IgnoreWidth**<br /><br /> <br /><br /> 有关详细信息，请参阅 [Comparing String Data](../../../integration-services/data-flow/comparing-string-data.md)。|  
|LeadingTrailingNumeralsSignificant|Integer（枚举）|该值用于指定数字的重要性。 此属性可以具有下列值之一：<br /><br /> **NumeralsNotSpecial** (0) — 如果数字不重要则使用。<br /><br /> **LeadingNumeralsSignificant** (1) — 如果前导数字重要则使用。<br /><br /> **TrailingNumeralsSignificant** (2) — 如果尾随数字重要则使用。<br /><br /> **LeadingAndTrailingNumeralsSignificant** (3) — 如果前导数字和尾随数字都重要则使用。|  
|MinSimilarity|双精度|用于列上的联接的相似性阈值，指定为 0 和 1 之间的值。 只有大于阈值的行才能作为匹配值。|  
|ToBeCleaned|Boolean|该值用于指定是否使用列来标识重复值，即：是否存在要分组的列。 此属性的默认值为 **False**。|  
  
 下表介绍模糊分组转换的输出列的自定义属性。 所有属性均可读/写。  
  
|属性名称|数据类型|描述|  
|-------------------|---------------|-----------------|  
|ColumnType|Integer（枚举）|该值用于标识输出列的类型。 此属性可以具有下列值之一：<br /><br /> **未定义** (0)<br /><br /> **KeyIn** (1)<br /><br /> **KeyOut** (2)<br /><br /> **Similarity** (3)<br /><br /> **ColumnSimilarity** (4)<br /><br /> **PassThru** (5)<br /><br /> **Canonica**l (6)|  
|InputID|Integer|对应输入列的 **LineageID** 。|  
  
 模糊分组转换的输入和输出不包含自定义属性。  
  
 有关详细信息，请参阅 [Fuzzy Grouping Transformation](../../../integration-services/data-flow/transformations/fuzzy-grouping-transformation.md)。  
  
##  <a name="flookup"></a> 模糊查找转换自定义属性  
 模糊查找转换既包含自定义属性，也包含对所有数据流组件通用的属性。  
  
 下表介绍模糊查找转换的自定义属性。 除 **ReferenceMetadataXML** 以外的所有属性均可读/写。  
  
|“属性”|数据类型|描述|  
|--------------|---------------|-----------------|  
|CopyReferenceTable|Boolean|指定是否应为模糊查找索引结构和后续查找生成引用表副本。 此属性的默认值为 **True**。|  
|Delimiters|String|转换用来标记列值的分隔符。 默认分隔符包括以下字符：空格 ( )、逗号 (,)、句点 (.)、分号 (;)、冒号 (:)、连字符 (-)、双直引号 (")、单直引号 (')、与号 (&)、斜杠 (/)、反斜杠 (\\)、at 符号 (@)、感叹号 (!)、问号 (?)、左小括号 (()、右小括号 ())、小于号 (\<)、大于号 (>)、左方括号 ([)、右方括号 (])、左大括号 ({)、右大括号 (})、竖线 (&#124;)。 数字符号 (#)、星号 (*)、插入符号 (^) 和百分号 (%)。|  
|DropExistingMatchIndex|Boolean|一个值，用于指定当 MatchIndexOptions 未设置为 ReuseExistingIndex 时是否删除 MatchIndexName 中指定的匹配索引。 此属性的默认值为 **True**。|  
|Exhaustive|Boolean|该值用于指定是否将每个输入记录与所有其他输入记录进行比较。 值 **True** 主要用于调试目的。 此属性的默认值为 **False**。<br /><br /> 注意：此属性在“模糊查找转换编辑器” 中不可用，但可通过“高级编辑器” 进行设置。|  
|MatchIndexName|String|匹配索引的名称。 匹配索引是转换在其中创建和保存所使用的索引的表。 如果重复使用匹配索引，MatchIndexName 将指定要重复使用的索引。 MatchIndexName 必须是有效的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 标识符名称。 例如，如果名称包含空格，则必须用方括号将名称括起来。|  
|MatchIndexOptions|Integer（枚举）|该值用于指定转换如何管理匹配索引。 此属性可以具有下列值之一：<br /><br /> **ReuseExistingIndex** (0)<br /><br /> **GenerateNewIndex** (1)<br /><br /> **GenerateAndPersistNewIndex** (2)<br /><br /> **GenerateAndMaintainNewIndex** (3)|  
|MaxMemoryUsage|Integer|查找表的最大缓存大小。 此属性的默认值为 **0**，表示缓存没有大小限制。<br /><br /> 此属性的值可以使用属性表达式来指定。<br /><br /> 注意：此属性在“模糊查找转换编辑器” 中不可用，但可通过“高级编辑器” 进行设置。|  
|MaxOutputMatchesPerInput|Integer|转换可以为每个输入行返回的最大匹配数。 此属性的默认值为 **1**。<br /><br /> 注意：大于 100 的值只能使用“高级编辑器” 进行指定。|  
|MinSimilarity|Integer|转换在组件级别使用的相似性阈值，指定为 0 和 1 之间的值。 只有大于阈值的行才能作为匹配值。|  
|ReferenceMetadataXML|String|[!INCLUDE[ssInternalOnly](../../../includes/ssinternalonly-md.md)]|  
|ReferenceTableName|String|查找表的名称。 该名称必须是有效的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 标识符名称。 例如，如果名称包含空格，则必须用方括号将名称括起来。|  
|WarmCaches|Boolean|如果该值为 True，则查找在执行开始之前会将索引和引用表部分加载到内存中。 这样可以提高性能。|  
  
 下表介绍模糊查找转换的输入列的自定义属性。 所有属性均可读/写。  
  
|“属性”|数据类型|描述|  
|--------------|---------------|-----------------|  
|FuzzyComparisonFlags|Integer|该值用于指定转换如何比较列中的字符串数据。 有关详细信息，请参阅 [Comparing String Data](../../../integration-services/data-flow/comparing-string-data.md)。|  
|FuzzyComparisonFlagsEx|Integer（枚举）|该值用于指定转换所使用的扩展比较标志。 其值包括 **MapExpandLigatures、MapFoldCZone**、 **MapFoldDigits**、 **MapPrecomposed**和 **NoMapping**。 **NoMapping** 不能与其他标志一起使用。|  
|JoinToReferenceColumn|String|该值用于指定列所联接的引用表中的列的名称。|  
|JoinType|Integer|该值用于指定转换是执行模糊匹配还是完全匹配。 此属性的默认值为 **Fuzzy**。 完全联接类型的整数值为 **1** ，而模糊联接类型的值为 **2**。|  
|MinSimilarity|双精度|转换在列级别使用的相似性阈值，指定为 0 到 1 之间的值。 只有大于阈值的行才能作为匹配值。|  
  
 下表介绍模糊查找转换的输出列的自定义属性。 所有属性均可读/写。  
  
> [!NOTE]  
>  对于包含来自对应输入列的传递值的输出列，CopyFromReferenceColumn 为空，SourceInputColumnLineageID 包含对应输入列的 **LineageID** 。 对于包含查找结果的输出列，CopyFromReferenceColumn 包含查找列的名称，SourceInputColumnLineageID 为空。  
  
|“属性”|数据类型|描述|  
|--------------|---------------|-----------------|  
|ColumnType|整数（枚举）|该值用于标识转换添加到输出的列的输出列的类型。 此属性可以具有下列值之一：<br /><br /> **未定义** (0)<br /><br /> **Similarity** (1)<br /><br /> **Confidence** (2)<br /><br /> **ColumnSimilarity** (3)|  
|CopyFromReferenceColumn|String|该值用于指定引用表中提供输出列中的值的列名称。|  
|SourceInputColumnLineageId|Integer|该值用于标识向此输出列提供值的输入列。|  
  
 模糊查找转换的输入和输出不包含自定义属性。  
  
 有关详细信息，请参阅 [Fuzzy Lookup Transformation](../../../integration-services/data-flow/transformations/fuzzy-lookup-transformation.md)。  
  
##  <a name="lookup"></a> 查找转换自定义属性  
 查找转换既包含自定义属性，也包含对所有数据流组件通用的属性。  
  
 下表介绍查找转换的自定义属性。 除 **ReferenceMetadataXML** 以外的所有属性均可读/写。  
  
|“属性”|数据类型|描述|  
|--------------|---------------|-----------------|  
|CacheType|Integer（枚举）|查找表的缓存类型。 其值包括：“完全”(0)、“部分”(1) 和“无”(2)。 此属性的默认值为 **Full**。|  
|DefaultCodePage|Integer|当无法从数据源使用代码页信息时所使用的默认代码页。|  
|MaxMemoryUsage|Integer|查找表的最大缓存大小。 此属性的默认值为 **25**，表示缓存没有大小限制。|  
|MaxMemoryUsage64|Integer|64 位计算机上的查找表的最大缓存大小。|  
|NoMatchBehavior|Integer（枚举）|该值用于指定是否将引用数据集中不包含匹配项的行视为错误。<br /><br /> 如果将该属性设置为“将没有匹配项的行视为错误”(0)，则不包含匹配项的行将被视为错误。 使用 **“查找转换编辑器”** 对话框的 **“错误输出”** 页可以指定当发生此类错误时会发生什么情况。 有关详细信息，请参阅[查找转换编辑器（“错误输出”页）](../../../integration-services/data-flow/transformations/lookup-transformation-editor-error-output-page.md)。<br /><br /> 如果将该属性设置为“将没有匹配项的行发送至无匹配输出”(1)，则不会将行视为错误。<br /><br /> 默认值为“将没有匹配项的行视为错误”(0)。|  
|ParameterMap|String|以分号分隔的沿袭 ID 列表，这些 ID 映射到 **SqlCommand** 语句中所使用的参数。|  
|ReferenceMetadataXML|String|转换复制到其输出的查找表中的列的元数据。|  
|SqlCommand|String|用于填充查找表的 SELECT 语句。|  
|SqlCommandParam|String|用于填充查找表的参数化 SQL 语句。|  
  
 下表介绍查找转换的输入列的自定义属性。 所有属性均可读/写。  
  
|“属性”|数据类型|描述|  
|--------------|---------------|-----------------|  
|CopyFromReferenceColumn|String|从中复制列的引用表中的列的名称。|  
|JoinToReferenceColumns|String|源列所联接的引用表中的列的名称。|  
  
 下表介绍查找转换输出列的自定义属性。 所有属性均可读/写。  
  
|属性名称|数据类型|描述|  
|-------------------|---------------|-----------------|  
|CopyFromReferenceColumn|String|从中复制列的引用表中的列的名称。|  
  
 查找转换的输入和输出不包含自定义属性。  
  
 有关详细信息，请参阅 [Lookup Transformation](../../../integration-services/data-flow/transformations/lookup-transformation.md)。  
  
##  <a name="mjoin"></a> 合并联接转换自定义属性  
 合并联接转换既包含自定义属性，也包含对所有数据流组件通用的属性。  
  
 下表介绍合并联接转换的自定义属性。  
  
|“属性”|数据类型|描述|  
|--------------|---------------|-----------------|  
|JoinType|Integer（枚举）|指定联接是内部联接 (2)、左外部联接 (1) 还是完整联接 (0)。|  
|MaxBuffersPerInput|Integer|您不再必须配置 **MaxBuffersPerInput** 属性的值，因为 Microsoft 已进行了更改，减少了合并联接转换将占用过多内存的风险。 在合并联接的多个输入以不相等速率生成数据时，有时候可能会发生此问题。|  
|NumKeyColumns|Integer|联接所使用的列数。|  
|TreatNullsAsEqual|Boolean|该值用于指定转换是否将 null 值处理为相等的值。 此属性的默认值为 **True**。 如果属性值为 **False**，则转换处理 null 值的方式与 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的处理方式相同。|  
  
 下表介绍合并联接转换的输出列的自定义属性。 所有属性均可读/写。  
  
|属性名称|数据类型|描述|  
|-------------------|---------------|-----------------|  
|InputColumnID|Integer|从中将数据复制到此输出列的输入列的 **LineageID** 。|  
  
 合并联接转换的输入、输入列和输出不包含自定义属性。  
  
 有关详细信息，请参阅 [Merge Join Transformation](../../../integration-services/data-flow/transformations/merge-join-transformation.md)。  
  
##  <a name="oledbcmd"></a> OLE DB 命令转换自定义属性  
 OLE DB 命令转换既包含自定义属性，也包含对所有数据流组件通用的属性。  
  
 下表介绍 OLE DB 命令转换的自定义属性。  
  
|属性名称|数据类型|描述|  
|-------------------|---------------|-----------------|  
|CommandTimeout|Integer|SQL 命令在超时前可以运行的最大秒数。值 **0** 表示不限制时间。 此属性的默认值为 **0**。|  
|DefaultCodePage|Integer|当无法从数据源使用代码页信息时所使用的代码页。|  
|SqlCommand|String|转换针对数据流中的每一行运行的 Transact-SQL 语句。<br /><br /> 此属性的值可以使用属性表达式来指定。|  
  
 下表介绍 OLE DB 命令转换的外部列的自定义属性。 所有属性均可读/写。  
  
|属性名称|数据类型|描述|  
|-------------------|---------------|-----------------|  
|DBParamInfoFlag|Integer（位掩码）|一组描述参数特征的标志。 有关详细信息，请参阅 MSDN 库的 OLE DB 文档中的 DBPARAMFLAGSENUM。|  
  
 OLE DB 命令转换的输入、输入列、输出和输出列不包含自定义属性。  
  
 有关详细信息，请参阅 [OLE DB Command Transformation](../../../integration-services/data-flow/transformations/ole-db-command-transformation.md)。  
  
##  <a name="percent"></a> 百分比抽样转换自定义属性  
 百分比抽样转换既包含自定义属性，也包含对所有数据流组件通用的属性。  
  
 下表介绍百分比抽样转换的自定义属性。  
  
|“属性”|数据类型|描述|  
|--------------|---------------|-----------------|  
|SamplingSeed|Integer|随机数生成器所使用的种子。 此属性的默认值为 **0**，指示转换使用时钟周期数。|  
|SamplingValue|Integer|以与源的百分比表示的样本大小。<br /><br /> 此属性的值可以使用属性表达式来指定。|  
  
 下表介绍百分比抽样转换的输出的自定义属性。 所有属性均可读/写。  
  
|属性名称|数据类型|描述|  
|-------------------|---------------|-----------------|  
|所选|Boolean|指定已抽样的行定向到的输出。 在选定的输出中，Selected 设置为 **True**；在未选定的输出中，Selected 设置为 **False**。|  
  
 百分比抽样转换的输入、输入列和输出列不包含自定义属性。  
  
 有关详细信息，请参阅 [Percentage Sampling Transformation](../../../integration-services/data-flow/transformations/percentage-sampling-transformation.md)。  
  
##  <a name="pivot"></a> 透视转换自定义属性  
 下表介绍透视转换的自定义组件属性。  
  
|“属性”|数据类型|描述|  
|--------------|---------------|-----------------|  
|**PassThroughUnmatchedPivotKeyts**|Boolean|设置为 **True** ，以将透视转换配置为在运行包时忽略包含“透视键”列中无法识别的值的行并将所有透视键值输出到日志消息。|  
  
 下表介绍透视转换的输入列的自定义属性。 所有属性均可读/写。  
  
|“属性”|数据类型|描述|  
|--------------|---------------|-----------------|  
|PivotUsage|Integer（枚举）|该值用于指定透视数据集时列的角色。<br /><br /> **0**：<br />                      此列未经透视，列值将传递到转换输出。<br /><br /> **1**：<br />                      此列为设置键的一部分，该设置键将一行或多行标识为一个集的组成部分。 将所有具有同一设置键的输入行组合到一个输出行。<br /><br /> **2**：<br />                      列为透视列。 从每个列值至少创建一列。<br /><br /> **3**：<br />                      将此列的值放入作为透视结果创建的列中。|  
  
 下表介绍透视转换的输出列的自定义属性。 所有属性均可读/写。  
  
|“属性”|数据类型|描述|  
|--------------|---------------|-----------------|  
|PivotKeyValue|String|列中由其 PivotUsage 属性的值标记为透视键的可能值之一。<br /><br /> 此属性的值可以使用属性表达式来指定。|  
|SourceColumn|Integer|包含透视值或 -1 的输入列的 **LineageID** 。 值 -1 表示透视操作中未使用该列。|  
  
 有关详细信息，请参阅 [Pivot Transformation](../../../integration-services/data-flow/transformations/pivot-transformation.md)。  
  
##  <a name="rowcount"></a> 行计数转换自定义属性  
 行计数转换既包含自定义属性，也包含对所有数据流组件通用的属性。  
  
 下表介绍行计数转换的自定义属性。 所有属性均可读/写。  
  
|属性名称|数据类型|描述|  
|-------------------|---------------|-----------------|  
|VariableName|String|保存行计数的变量的名称。|  
  
 行计数转换的输入、输入列、输出和输出列不包含自定义属性。  
  
 有关详细信息，请参阅 [Row Count Transformation](../../../integration-services/data-flow/transformations/row-count-transformation.md)。  
  
##  <a name="rowsamp"></a> 行抽样转换自定义属性  
 行抽样转换既包含自定义属性，也包含对所有数据流组件通用的属性。  
  
 下表介绍行抽样转换的自定义属性。 所有属性均可读/写。  
  
|“属性”|数据类型|描述|  
|--------------|---------------|-----------------|  
|SamplingSeed|Integer|随机数生成器所使用的种子。 此属性的默认值为 **0**，指示转换使用时钟周期数。|  
|SamplingValue|Integer|样本的行计数。<br /><br /> 此属性的值可以使用属性表达式来指定。|  
  
 下表介绍行抽样转换的输出的自定义属性。 所有属性均可读/写。  
  
|属性名称|数据类型|描述|  
|-------------------|---------------|-----------------|  
|所选|Boolean|指定已抽样的行定向到的输出。 在选定的输出中，Selected 设置为 **True**；在未选定的输出中，Selected 设置为 **False**。|  
  
 下表介绍行抽样转换的输出列的自定义属性。 所有属性均可读/写。  
  
|“属性”|数据类型|描述|  
|--------------|---------------|-----------------|  
|InputColumnLineageId|Integer|该值用于指定作为输出列的源的输入列的 **LineageID** 。|  
  
 行抽样转换的输入和输入列不包含自定义属性。  
  
 有关详细信息，请参阅 [Row Sampling Transformation](../../../integration-services/data-flow/transformations/row-sampling-transformation.md)。  
  
##  <a name="script"></a> 脚本组件自定义属性  
 脚本组件既包含自定义属性，也包含对所有数据流组件通用的属性。 无论脚本组件用作源、转换，还是用作目标，都具有相同的自定义属性。  
  
 下表介绍脚本组件的自定义属性。 所有属性均可读/写。  
  
|属性名称|数据类型|描述|  
|-------------------|---------------|-----------------|  
|ReadOnlyVariables|String|以逗号分隔的、可供脚本组件进行只读访问的变量列表。|  
|ReadWriteVariables|String|以逗号分隔的、可供脚本组件进行读/写访问的变量列表。|  
  
 脚本组件的输入、输入列、输出和输出列不包含自定义属性，除非脚本开发人员为它们创建自定义属性。  
  
 有关详细信息，请参阅 [Script Component](../../../integration-services/data-flow/transformations/script-component.md)。  
  
##  <a name="scd"></a> 渐变维度转换自定义属性  
 渐变维度转换既包含自定义属性，也包含对所有数据流组件通用的属性。  
  
 下表介绍渐变维度转换的自定义属性。 所有属性均可读/写。  
  
|“属性”|数据类型|描述|  
|--------------|---------------|-----------------|  
|CurrentRowWhere|String|SELECT 语句中的 WHERE 子句，用于在具有相同业务键的行中选择当前行。|  
|EnableInferredMember|Boolean|该值用于指定是否检测推断成员更新。 此属性的默认值为 **True**。|  
|FailOnFixedAttributeChange|Boolean|该值用于指定当具有固定属性的行列包含更改或维度表中的查找失败时，转换是否失败。 如果期望传入的行包含新记录，请将该值设置为 **True** ，使转换在查找失败后继续，因为转换将使用该失败来标识新记录。 此属性的默认值为 **False**。|  
|FailOnLookupFailure|Boolean|该值用于指定当查找现有记录失败时转换是否失败。 此属性的默认值为 **False**。|  
|IncomingRowChangeType|Integer|该值用于指定是否所有传入的行均为新行，或者转换是否应检测更改类型。|  
|InferredMemberIndicator|String|推断成员的列名称。|  
|SqlCommand|String|用于创建架构行集的 SQL 语句。|  
|UpdateChangingAttributeHistory|Boolean|该值用于指示是否将历史属性更新定向到转换输出，以用于更改属性更新。|  
  
 下表介绍渐变维度转换的输入列的自定义属性。 所有属性均可读/写。  
  
|“属性”|数据类型|描述|  
|--------------|---------------|-----------------|  
|ColumnType|Integer（枚举）|列的更新类型。 其值包括：“变化的属性”(2)、“固定的属性”(4)、“历史属性”(3)、“键”(1) 和“其他”(0)。|  
  
 渐变维度转换的输入、输出和输出列不包含自定义属性。  
  
 有关详细信息，请参阅 [Slowly Changing Dimension Transformation](../../../integration-services/data-flow/transformations/slowly-changing-dimension-transformation.md)。  
  
##  <a name="sort"></a> 排序转换自定义属性  
 排序转换既包含自定义属性，也包含对所有数据流组件通用的属性。  
  
 下表介绍排序转换的自定义属性。 所有属性均可读/写。  
  
|“属性”|数据类型|描述|  
|--------------|---------------|-----------------|  
|EliminateDuplicates|Boolean|指定转换是否删除转换输出中的重复行。 此属性的默认值为 **False**。|  
|MaximumThreads|Integer|包含转换可用于排序的最大线程数。 如果值为 **0** ，则表示不限制线程数。 此属性的默认值为 **0**。<br /><br /> 此属性的值可以使用属性表达式来指定。|  
  
 下表介绍排序转换的输入列的自定义属性。 所有属性均可读/写。  
  
|“属性”|数据类型|描述|  
|--------------|---------------|-----------------|  
|NewComparisonFlags|Integer（位掩码）|该值用于指定转换如何比较列中的字符串数据。 有关详细信息，请参阅 [Comparing String Data](../../../integration-services/data-flow/comparing-string-data.md)。|  
|NewSortKeyPosition|Integer|该值用于指定列的排序顺序。 如果值为 0，则表示不对该列上的数据进行排序。|  
  
 下表介绍排序转换的输出列的自定义属性。 所有属性均可读/写。  
  
|“属性”|数据类型|描述|  
|--------------|---------------|-----------------|  
|SortColumnID|Integer|排序列的 **LineageID** 。|  
  
 排序转换的输入和输出不包含自定义属性。  
  
 有关详细信息，请参阅 [Sort Transformation](../../../integration-services/data-flow/transformations/sort-transformation.md)。  
  
##  <a name="textract"></a> 字词提取转换自定义属性  
 字词提取转换既包含自定义属性，也包含对所有数据流组件通用的属性。  
  
 下表介绍字词提取转换的自定义属性。 所有属性均可读/写。  
  
|“属性”|数据类型|描述|  
|--------------|--------------|-----------------|  
|FrequencyThreshold|Integer|该数值指示提取某个字词之前，该字词必须出现的次数。 此属性的默认值为 **2**。|  
|IsCaseSensitive|Boolean|该值指定提取名词和名词短语时是否区分大小写。 此属性的默认值为 **False**。|  
|MaxLengthOfTerm|Integer|该数值指示某个字词的最大长度。 此属性只适用于短语。 此属性的默认值为 **12**。|  
|NeedRefenceData|Boolean|该值用于指定转换是否使用引用表中存储的排除字词列表。 此属性的默认值为 **False**。|  
|OutTermColumn|String|包含排除字词的列的名称。|  
|OutTermTable|String|包含具有排除字词的列的表的名称。|  
|ScoreType|Integer|该值用于指定与字词关联的计分类型。 有效值为 0 和 1：0 表示频率，1 表示 TFIDF 分数。 TFIDF 分数是字词频率和文档频率倒数的乘积，其定义如下：TFIDF of a Term T = (frequency of T) \* log( (#rows in Input) / (#rows having T) )。 此属性的默认值为 **0**。|  
|WordOrPhrase|Integer|该值用于指定字词类型。 有效值包括 0、1 和 2：0 表示仅词；1 表示仅名词短语；2 表示词和名称短语。 此属性的默认值为 **0**。|  
  
 字词提取转换的输入、输入列、输出和输出列不包含自定义属性。  
  
 有关详细信息，请参阅 [Term Extraction Transformation](../../../integration-services/data-flow/transformations/term-extraction-transformation.md)。  
  
##  <a name="tlookup"></a> 字词查找转换自定义属性  
 字词查找转换既包含自定义属性，也包含对所有数据流组件通用的属性。  
  
 下表介绍字词查找转换的自定义属性。 所有属性均可读/写。  
  
|“属性”|数据类型|描述|  
|--------------|---------------|-----------------|  
|IsCaseSensitive|Boolean|该值用于指定是否将大小写区分比较应用于输入列文本与查找字词的匹配。 此属性的默认值为 **False**。|  
|RefTermColumn|String|包含查找字词的列的名称。|  
|RefTermTable|String|包含具有查找字词的列的表名称。|  
  
 下表介绍字词查找转换的输入列的自定义属性。 所有属性均可读/写。  
  
|“属性”|数据类型|描述|  
|--------------|---------------|-----------------|  
|InputColumnType|Integer|该值用于指定列的使用。 有效值包括 0、1 和 2：0 表示传递列；1 表示查找列；2 表示既是传递列又是查找列的列。|  
  
 下表介绍字词查找转换的输出列的自定义属性。 所有属性均可读/写。  
  
|属性名称|数据类型|描述|  
|-------------------|---------------|-----------------|  
|CustomLineageID|Integer|当该列的 **LineageID** 为 0 或 2 时，对应的输入列的 **InputColumnType** 。|  
  
 字词查找转换的输入和输出不包含自定义属性。  
  
 有关详细信息，请参阅 [Term Lookup Transformation](../../../integration-services/data-flow/transformations/term-lookup-transformation.md)。  
  
##  <a name="unpivot"></a> 逆透视转换自定义属性  
 逆透视转换仅包含在组件级别对所有数据流组件通用的属性。  
  
> [!NOTE]  
>  本节围绕 [逆透视转换](../../../integration-services/data-flow/transformations/unpivot-transformation.md) 中所述的逆透视应用场景，举例说明此处介绍的各选项的用法。  
  
 下表介绍逆透视转换的输入列的自定义属性。 所有属性均可读/写。  
  
|“属性”|数据类型|描述|  
|--------------|---------------|-----------------|  
|DestinationColumn|Integer|输入列映射到的输出列的 **LineageID** 。 如果值为 -1，则表示输入列未映射到输出列。|  
|PivotKeyValue|String|复制到转换输出列的值。<br /><br /> 此属性的值可以使用属性表达式来指定。<br /><br /> 在 [Unpivot Transformation](../../../integration-services/data-flow/transformations/unpivot-transformation.md)中所述的逆透视应用场景中，透视值为以下文本值：Ham、Coke、Milk、Beer 和 Chips。 这些值在由 **“透视键值列名”** 选项指定的新 Product 列中显示为文本值。|  
  
 下表介绍逆透视转换的输出列的自定义属性。 所有属性均可读/写。  
  
|属性名称|数据类型|描述|  
|-------------------|---------------|-----------------|  
|PivotKey|Boolean|指示是否将输入列的 **PivotKeyValue** 属性中的值写入此输出列。<br /><br /> 在 [Unpivot Transformation](../../../integration-services/data-flow/transformations/unpivot-transformation.md)中所述的逆透视应用场景中，透视值列名称为 **Product** ，并指定了将 Ham、Coke、Milk、Beer 和 Chips 列逆透视到其中的新的 **Product** 列。|  
  
 逆透视转换的输入和输出不包含自定义属性。  
  
 有关详细信息，请参阅 [Unpivot Transformation](../../../integration-services/data-flow/transformations/unpivot-transformation.md)。  
  
## <a name="see-also"></a>另请参阅  
 [Integration Services 转换](../../../integration-services/data-flow/transformations/integration-services-transformations.md)   
 [通用属性](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)   
 [路径属性](http://msdn.microsoft.com/library/89b1e347-9579-4f6b-af74-c6519ea08eea)   
 [可以使用表达式设置的数据流属性](http://msdn.microsoft.com/library/cd0e171a-08be-45d6-81dc-ed94f37698b8)  
  
  
