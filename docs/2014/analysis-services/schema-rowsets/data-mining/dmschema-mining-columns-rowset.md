---
title: DMSCHEMA_MINING_COLUMNS 行集 |Microsoft Docs
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
- DMSCHEMA_MINING_COLUMNS
topic_type:
- apiref
helpviewer_keywords:
- DMSCHEMA_MINING_COLUMNS rowset
ms.assetid: ae35ccde-4438-46f4-8611-40b2b1a42fce
caps.latest.revision: 35
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 60dc2e773b93f27fe96489bcb55fdfe22c3168d4
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37232057"
---
# <a name="dmschemaminingcolumns-rowset"></a>DMSCHEMA_MINING_COLUMNS 行集
  描述中的所有数据挖掘模型的各个列[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。 此行集只限于当前目录。  
  
## <a name="rowset-columns"></a>行集列  
 `DMSCHEMA_MINING_COLUMNS`行集包含以下列。  
  
|列名|类型指示符|长度|Description|  
|-----------------|--------------------|------------|-----------------|  
|`MODEL_CATALOG`|`DBTYPE_WSTR`||目录名称。 使用模型为其成员的数据库的名称填充。|  
|`MODEL_SCHEMA`|`DBTYPE_WSTR`||非限定的架构名称。 此列不受[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; 它始终包含`NULL`。|  
|`MODEL_NAME`|`DBTYPE_WSTR`||挖掘模型名称。 此列包含与某列关联的挖掘模型的名称，并且永远不为空。|  
|`COLUMN_NAME`|`DBTYPE_WSTR`||列的名称。|  
|`COLUMN_GUID`|`DBTYPE_GUID`||列 GUID。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 不支持此列；该列始终包含 `NULL`。|  
|`COLUMN_PROPID`|`DBTYPE_UI4`||列属性 ID。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 不支持此列；该列始终包含 `NULL`。|  
|`ORDINAL_POSITION`|`DBTYPE_UI4`||列的序号位置。 列从 1 开始编号。 如果列没有固定的序号值，则该列包含 `NULL`。|  
|`COLUMN_HAS_DEFAULT`|`DBTYPE_BOOL`||一个布尔值，该值指示列是否具有默认值。<br /><br /> 如果该列有默认值，则为 `TRUE`；否则为 `FALSE`。|  
|`COLUMN_DEFAULT`|`DBTYPE_WSTR`||列的默认值。<br /><br /> 如果默认值为 `NULL` 值，则 `COLUMN_HASDEFAULT` 将包含 `TRUE`，并且此列将包含 `NULL`。|  
|`COLUMN_FLAGS`|`DBTYPE_UI4`||介绍特征的列的位掩码。 `DBCOLUMNFLAGS` 枚举的类型指定了位掩码中的位。 此列永远不为空。|  
|`IS_NULLABLE`|`DBTYPE_BOOL`||指示列是否可以为 Null 的布尔值。<br /><br /> 如果列已知不可为 Null，则为 `FALSE`；否则为 `TRUE`。|  
|`DATA_TYPE`|`DBTYPE_UI2`||列的数据类型的指示符。 以下列表显示了返回的指示符类型的示例：<br /><br /> “`TABLE`”将返回 `DBTYPE_HCHAPTER`。<br /><br /> “`TEXT`”将返回 `DBTYPE_WCHAR`。<br /><br /> “`LONG`”将返回 `DBTYPE_I8`。<br /><br /> “`DOUBLE`”将返回 `DBTYPE_R8`。<br /><br /> “`DATE`”将返回 `DBTYPE_DATE`。|  
|`TYPE_GUID`|`DBTYPE_GUID`||列的数据类型的 GUID。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 不支持此列；该列始终包含 `VT_NULL`。|  
|`CHARACTER_MAXIMUM_LENGTH`|`DBTYPE_UI4`||列中值的最大可能长度。 对于字符列、二进制值列或位列，可以是下列值之一：<br /><br /> 的中的字符、 字节或位列各自列类型，如果定义长度的列最大长度。 例如，SQL 表中的 `CHAR(5)` 列的最大长度为 5。<br />的中的字符、 字节或位列各自列类型，如果列不具有定义的长度的数据类型最大长度。<br />零 (0)，如果列和数据类型都不具有定义的最大长度。<br />-   `NULL` 对于所有其他类型的列|  
|`CHARACTER_OCTET_LENGTH`|`DBTYPE_UI4`||如果列的类型为字符或二进制值时，则为列的八进制最大长度（字节）。 零值 (0) 表示列没有最大长度。 对于所有其他类型的列，此列均包含 `NULL`。|  
|`NUMERIC_PRECISION`|`DBTYPE_UI2`||如果列的数据类型为非 `VARNUMERIC` 的数值数据类型，则为该列的最大精度。<br /><br /> 如果该列的数据类型不是数值或为 `NULL`，则为 `VARNUMERIC`。<br /><br /> 数据类型为 `DBTYPE_DECIMAL` 或 `DBTYPE_NUMERIC` 的列的精度取决于该列的定义。|  
|`NUMERIC_SCALE`|`DBTYPE_I2`||如果列的类型指示符为 `DBTYPE_DECIMAL`、`DBTYPE_NUMERIC` 或 `DBTYPE_VARNUMERIC`，则为小数点右边的位数。 否则，此列将包含 `VT_NULL`。|  
|`DATETIME_PRECISION`|`DBTYPE_UI4`||如果列为 DateTime 或间隔类型时，则为列的 date/time 精度（秒的小数部分的位数）；否则为 `NULL`。|  
|`CHARACTER_SET_CATALOG`|`DBTYPE_WSTR`||在其中定义字符集的目录名称。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 不支持此列；该列始终包含 `NULL`。|  
|`CHARACTER_SET_SCHEMA`|`DBTYPE_WSTR`||在其中定义字符集的非限定架构名称。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 不支持此列；该列始终包含 `NULL`。|  
|`CHARACTER_SET_NAME`|`DBTYPE_WSTR`||字符集名称。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 不支持此列；该列始终包含 `NULL`。|  
|`COLLATION_CATALOG`|`DBTYPE_WSTR`||在其中定义排序规则的目录名称。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 不支持此列；该列始终包含 `NULL`。|  
|`COLLATION_SCHEMA`|`DBTYPE_WSTR`||在其中定义排序规则的非限定的架构名称。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 不支持此列；该列始终包含 `NULL`。|  
|`COLLATION_NAME`|`DBTYPE_WSTR`||排序规则名称。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 不支持此列；该列始终包含 `NULL`。|  
|`DOMAIN_CATALOG`|`DBTYPE_WSTR`||在其中定义域的目录名称。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 不支持此列；该列始终包含 `NULL`。|  
|`DOMAIN_SCHEMA`|`DBTYPE_WSTR`||在其中定义域的非限定架构名称。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 不支持此列；该列始终包含 `NULL`。|  
|`DOMAIN_NAME`|`DBTYPE_WSTR`||域名。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 不支持此列；该列始终包含 `NULL`。|  
|`DESCRIPTION`|`DBTYPE_WSTR`||列的用户友好说明。[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 不支持此列；该列始终包含 `NULL`。|  
|`DISTRIBUTION_FLAG`|`DBTYPE_WSTR`||列的统计分布情况的说明。 此列包含以下内容之一：<br /><br /> -   "`NORMAL`"<br />-   "`LOG_NORMAL`"<br />-   "`UNIFORM`"|  
|`CONTENT_TYPE`|`DBTYPE_WSTR`||列的内容说明。 此列包含以下内容之一：<br /><br /> -   "`KEY`"<br />-   "`DISCRETE`"<br />-   "`CONTINUOUS`"<br />-"`DISCRETIZED(`[参数]`)`"<br />-   "`ORDERED`"<br />-   "`KEY TIME`"<br />-   "`CYCLICAL`"<br />-   "`PROBABILITY`"<br />-   "`VARIANCE`"<br />-   "`STDEV`"<br />-   "`SUPPORT`"<br />-   "`PROBABILITY_VARIANCE`"<br />-   "`PROBABILITY_STDEV`"<br />-   `"KEY SEQUENCE`"|  
|`MODELING_FLAG`|`DBTYPE_WSTR`||逗号分隔的标志列表。 已定义的标志为：<br /><br /> -   "`MODEL_EXISTENCE_ONLY`"<br />-   "`REGRESSOR`"<br /><br /> 特定于算法的建模标志也可包含在此列中。|  
|`IS_RELATED_TO_KEY`|`DBTYPE_BOOL`||一个布尔值，该值指示是否与键相关列。<br /><br /> 如果此列与键关联，则为 `TRUE`。 如果键是单列，则 `RELATED_ATTRIBUTE` 字段可以选择包含其列名。|  
|`RELATED_ATTRIBUTE`|`DBTYPE_WSTR`||向其当前列相关或为其特殊属性的目标列的名称。|  
|`IS_INPUT`|`DBTYPE_BOOL`||指示列是否为输入列的布尔值。<br /><br /> 如果此列为输入列，则为 `VARIANT_TRUE`。|  
|`IS_PREDICTABLE`|`DBTYPE_BOOL`||指示列是否可预测的布尔值。<br /><br /> 如果该列可预测，则为 `TRUE`。|  
|`CONTAINING_COLUMN`|`DBTYPE_WSTR`||包含此列的 `TABLE` 列的名称。 如果此列未包含在其他列中，则此列将包含 `NULL`。|  
|`PREDICTION_SCALAR_FUNCTIONS`|`DBTYPE_WSTR`||可对列执行的标量函数的逗号分隔列表。|  
|`PREDICTION_TABLE_FUNCTIONS`|`DBTYPE_WSTR`||可应用于该列的函数的逗号分隔列表。 这些函数应返回一个表。 列表的格式如下：<br /><br /> `<function name>(<column1> [, <column2>], ...)`<br /><br /> 此格式允许客户端应用程序确定各函数的签名（参数列表）。|  
|`IS_POPULATED`|`DBTYPE_BOOL`||指示是否已使用一组可能的值为列定型的布尔值。<br /><br /> 如果已使用一组可能的值为列定型，则为 `TRUE`。<br /><br /> 如果未填充列，则包含 `FALSE`。|  
|`PREDICTION_SCORE`|`DBTYPE_R8`||对列进行预测所针对的模型的分数。 分数用于度量模型的准确性。|  
|`SOURCE_COLUMN`|`DBTYPE_WSTR`||当前挖掘列的源挖掘结构列的名称。|  
  
## <a name="restriction-columns"></a>限制列  
 `DMSCHEMA_MINING_COLUMNS`行集可以限制下表中列出的列。  
  
|列名|类型指示符|限制状态|  
|-----------------|--------------------|-----------------------|  
|`MODEL_CATALOG`|`DBTYPE_WSTR`|可选。|  
|`MODEL_SCHEMA`|`DBTYPE_WSTR`|可选。|  
|`MODEL_NAME`|`DBTYPE_WSTR`|可选。|  
|`COLUMN_NAME`|`DBTYPE_WSTR`|可选。|  
  
## <a name="see-also"></a>请参阅  
 [数据挖掘架构行集](../../schema-rowsets/data-mining/data-mining-schema-rowsets.md) 
  
  
