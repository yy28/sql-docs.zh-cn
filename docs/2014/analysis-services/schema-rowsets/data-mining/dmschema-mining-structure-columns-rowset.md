---
title: DMSCHEMA_MINING_STRUCTURE_COLUMNS 行集 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- DMSCHEMA_MINING_STRUCTURE_COLUMNS
topic_type:
- apiref
helpviewer_keywords:
- DMSCHEMA_MINING_STRUCTURE_COLUMNS rowset
ms.assetid: 81f25502-ac90-42f1-8ddf-7b0f9752ebfd
caps.latest.revision: 34
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3c98da6f1e843b08fac4b91baabec79ab0d9c341
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37171578"
---
# <a name="dmschemaminingstructurecolumns-rowset"></a>DMSCHEMA_MINING_STRUCTURE_COLUMNS 行集
  描述部署在正在运行的服务器上的所有挖掘结构的各个列[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
## <a name="rowset-columns"></a>行集列  
 `DMSCHEMA_MINING_STRUCTURE_COLUMNS`行集包含以下列。  
  
|列名|类型指示符|长度|Description|  
|-----------------|--------------------|------------|-----------------|  
|`STRUCTURE_CATALOG`|`DBTYPE_WSTR`||目录名称。|  
|`STRUCTURE_SCHEMA`|`DBTYPE_WSTR`||非限定的架构名称。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 不支持架构，因此该列始终为 `NULL`。|  
|`STRUCTURE_NAME`|`DBTYPE_WSTR`||结构名称。 此列不能包含`NULL`。|  
|`COLUMN_NAME`|`DBTYPE_WSTR`||列的名称。 只保证在共享同一种模式的列之间具有唯一性。 例如，如果两个嵌套列属于同一结构中的两个不同嵌套表，则它们可能同名。|  
|`COLUMN_GUID`|`DBTYPE_GUID`||列 GUID。 不使用 GUID 来标识列的访问接口应在此列中返回 `NULL`。|  
|`COLUMN_PROPID`|`DBTYPE_UI4`||列属性 ID。 不能将属性 ID 与列关联的访问接口应在此列中返回 `NULL`。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 返回`NULL`此列。|  
|`ORDINAL_POSITION`|`DBTYPE_UI4`||列的序号。 列从 1 开始编号。 如果该列没有固定的序号值，则为 `NULL`。|  
|`COLUMN_HASDEFAULT`|`DBTYPE_BOOL`||指示此列是否有默认值的布尔值。<br /><br /> 如果该列有默认值，则为 `TRUE`。<br /><br /> 如果该列没有默认值，或未知该列是否有默认值，则为 `FALSE`。|  
|`COLUMN_DEFAULT`|`DBTYPE_WSTR`||列的默认值。 访问接口可能会在 `DBCOLUMN_DEFAULTVALUE` 返回的行集中公开 `DBCOLUMN_HASDEFAULT`，但不公开 `IColumnsRowset::GetColumnsRowset`（用于 ISO 表）。<br /><br /> 如果默认值为 `NULL`，则 `COLUMN_HASDEFAULT` 为 `TRUE`，并且 `COLUMN_DEFAULT` 列是一个 `NULL` 值。|  
|`COLUMN_FLAGS`|`DBTYPE_UI4`||的描述列特征位掩码。 `DBCOLUMNFLAGS` 枚举的类型指定了位掩码中的位。 此列不能包含 `NULL` 值。 有效值包括：<br />-   **DBCOLUMNFLAGS_ISNULLABLE** (`0x20`)<br />-   **DBCOLUMNFLAGS_MAYBENULL** (`0x40`)<br />-   **DBCOLUMNFLAGS_ISLONG** (`0x80`)|  
|`IS_NULLABLE`|`DBTYPE_BOOL`||指示此列是否有默认值的布尔值。<br /><br /> 如果该列可以包含 `TRUE`，则为 `NULL`；否则为 `FALSE`。|  
|`DATA_TYPE`|`DBTYPE_UI2`||列的数据类型的指示符。 例如：<br /><br /> -   "`TABLE`" = `DBTYPE_HCHAPTER`<br />-   "`TEXT`" = `DBTYPE_WCHAR`<br />-   "`LONG`" = `DBTYPE_I8`<br />-   "`DOUBLE`" = `DBTYPE_R8`<br />-   "`DATE`" = `DBTYPE_DATE`|  
|`TYPE_GUID`|`DBTYPE_GUID`||列的数据类型的 GUID。 不使用 GUID 来标识数据类型的访问接口应在此列中返回 `NULL`。|  
|`CHARACTER_MAXIMUM_LENGTH`|`DBTYPE_UI4`||列中值的最大可能长度。 对于字符列、二进制值列或位列，可以是下列值之一：<br /><br /> 的中的列最大长度字符、 字节或位列，分别，如果定义长度。 例如，SQL 表中的 `CHAR(5)` 列的最大长度为 5。<br />的数据最大长度分别在键入字符、 字节或位列，如果列不具有定义的长度。<br />零 (0)，如果列和数据类型都不具有定义的最大长度。<br />-   `NULL` 对于所有其他类型的列。|  
|`CHARACTER_OCTET_LENGTH`|`DBTYPE_UI4`||如果列的类型为字符或二进制值时，则为列的八进制最大长度（字节）。 零值 (0) 表示列没有最大长度。 所有其他类型的列均为 `NULL`。|  
|`NUMERIC_PRECISION`|`DBTYPE_UI2`||如果列的数据类型为非 `VARNUMERIC` 的数值数据类型，则为列的最大精度；如果列的数据类型不是数值或为 `NULL`，则为 `VARNUMERIC`。<br /><br /> 数据类型为 `DBTYPE_DECIMAL` 或 `DBTYPE_NUM`ERIC 的列的精度取决于该列的定义。|  
|`NUMERIC_SCALE`|`DBTYPE_I2`||如果列的类型指示符为 `DBTYPE_DECIMAL`、`DBTYPE_NUMERIC` 或 `DBTYPE_VARNUMERIC`，则为小数点右边的位数。 否则，这就是`NULL`。|  
|`DATETIME_PRECISION`|`DBTYPE_UI4`||如果列为 datetime 或间隔类型，则为列的 DateTime 精度（秒的小数部分的位数）。 如果此列的数据类型不是 datetime，此值为 `NULL`。|  
|`CHARACTER_SET_CATALOG`|`DBTYPE_WSTR`||在其中定义字符集的目录名称。 如果访问接口不支持目录或不同的字符集，则为 `NULL`。|  
|`CHARACTER_SET_SCHEMA`|`DBTYPE_WSTR`||定义在其中的字符集的非限定的架构名称。 如果访问接口不支持架构或不同的字符集，则为 `NULL`。|  
|`CHARACTER_SET_NAME`|`DBTYPE_WSTR`||字符集名称。 如果访问接口不支持不同的字符集，则为 `NULL`。|  
|`COLLATION_CATALOG`|`DBTYPE_WSTR`||在其中定义排序规则的目录名称。 如果访问接口不支持目录或不同的排序规则，则为 `NULL`。|  
|`COLLATION_SCHEMA`|`DBTYPE_WSTR`||在其中定义排序规则的非限定架构名称。 如果访问接口不支持架构或不同的排序规则，则为 `NULL`。|  
|`COLLATION_NAME`|`DBTYPE_WSTR`||排序规则名称。 如果访问接口不支持不同的排序规则，则为 `NULL`。|  
|`DOMAIN_CATALOG`|`DBTYPE_WSTR`||在其中定义域的目录名称。 如果访问接口不支持目录或域，则为 `NULL`。|  
|`DOMAIN_SCHEMA`|`DBTYPE_WSTR`||在其中定义域的非限定架构名称。 如果访问接口不支持架构或域，则为 `NULL`。|  
|`DOMAIN_NAME`|`DBTYPE_WSTR`||域名。 如果访问接口不支持域，则为 `NULL`。|  
|`DESCRIPTION`|`DBTYPE_WSTR`||易读的列说明。 如果没有与列相关的说明，则为 `NULL`。|  
|`DISTRIBUTION_FLAG`|`DBTYPE_WSTR`||挖掘结构列的分布：<br /><br /> -   "`NORMAL`"<br />-"`LOG_NORM`AL"<br />-   "`UNIFORM`"|  
|`CONTENT_TYPE`|`DBTYPE_WSTR`||挖掘结构列的内容类型：<br /><br /> -   "`KEY`"<br />-   "`DISCRETE`"<br />-   "`CONTINUOUS`"<br />-"`DISCRETIZED(`[参数]`)`"<br />-   "`ORDERED`"<br />-   "`SEQUENCE_TIME`"<br />-   "`CYCLICAL`"<br />-   "`PROBABILITY`"<br />-   "`VARIANCE`"<br />-   "`STDEV`"<br />-   "`SUPPORT`"<br />-   "`PROBABILITY_VARIANCE`"<br />-   "`PROBABILITY_STDEV`"|  
|`MODELING_FLAG`|`DBTYPE_WSTR`||逗号分隔的建模标志列表。 结构列支持的标志只有“`NOT NULL`”。|  
|`IS_RELATED_TO_KEY`|`DBTYPE_BOOL`||指示此列是否与键关联的布尔值。<br /><br /> 如果此列与键关联，则为 `VARIANT_TRUE`；否则为 `VARIANT_FALSE`。 如果键是单列，`RELATED_ATTRIBUTE`字段选择可能包含的列名称。|  
|`RELATED_ATTRIBUTE`|`DBTYPE_WSTR`||与当前列相关或为其特殊属性的目标列的名称。|  
|`CONTAINING_COLUMN`|`DBTYPE_WSTR`||名称`TABLE`列以包含此列。 如果没有表包含此列，则为 `NULL`。|  
|`IS_POPULATED`|`DBTYPE_BOOL`||指示此列是否了解可能的值集的布尔值。<br /><br /> 如果此列了解可能的值集，则为 `TRUE`；否则为 `FALSE`。|  
  
## <a name="restriction-columns"></a>限制列  
 可以使用以下表中的列对 `DMSCHEMA_MINING_STRUCTURE_COLUMNS` 行集进行限制。  
  
|列名|类型指示符|限制状态|  
|-----------------|--------------------|-----------------------|  
|`STRUCTURE_CATALOG`|`DBTYPE_WSTR`|可选。|  
|`STRUCTURE_SCHEMA`|`DBTYPE_WSTR`|可选。|  
|`STRUCTURE_NAME`|`DBTYPE_WSTR`|可选。|  
|`COLUMN_NAME`|`DBTYPE_WSTR`|可选。|  
  
## <a name="see-also"></a>请参阅  
 [数据挖掘架构行集](../../schema-rowsets/data-mining/data-mining-schema-rowsets.md) 
  
  
