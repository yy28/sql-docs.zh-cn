---
title: DBSCHEMA_PROVIDER_TYPES 行集 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- DBSCHEMA_PROVIDER_TYPES
topic_type:
- apiref
helpviewer_keywords:
- DBSCHEMA_PROVIDER_TYPES rowset
ms.assetid: 255e01ba-53a9-478d-9b86-45faba76710e
caps.latest.revision: 30
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7bca2527b77df65dede59878e91ef88ec5f933e0
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37250947"
---
# <a name="dbschemaprovidertypes-rowset"></a>DBSCHEMA_PROVIDER_TYPES 行集
  标识数据访问接口支持的（基本）数据类型。  
  
## <a name="rowset-columns"></a>行集列  
 `DBSCHEMA_PROVIDER_TYPES`行集包含以下列。  
  
|列名|类型指示符|长度|Description|  
|-----------------|--------------------|------------|-----------------|  
|`TYPE_NAME`|`DBTYPE_WSTR`||特定于访问接口的数据类型名称。|  
|`DATA_TYPE`|`DBTYPE_UI2`||数据类型的指示符。|  
|`COLUMN_SIZE`|`DBTYPE_UI4`||非数值列的长度或以下参数，该参数或者是最大值或者是访问接口为此类型定义的长度。 对于字符数据，此为最大值或定义长度（以字符为单位）。 对于 DateTime 数据类型，本列为字符串表示形式的长度（假定精度允许的最大值为秒的小数形式）。<br /><br /> 如果数据类型为数值，则此为数据类型最大精度的上限。|  
|`LITERAL_PREFIX`|`DBTYPE_WSTR`||用于在文本命令中作为此类型文字的前缀的一个或多个字符。|  
|`LITERAL_SUFFIX`|`DBTYPE_WSTR`||用于在文本命令中作为此类型文字的后缀的一个或多个字符。|  
|`CREATE_PARAMS`|`DBTYPE_WSTR`||创建此数据类型的列时，由使用者指定的创建参数。 例如，SQL 数据类型 `DECIMAL,` 需要精度和小数位数。 在这种情况下，创建参数可能是字符串“precision,scale”。 在创建精度为 10、小数位数为 2 的 `DECIMAL` 列的文本命令中，`TYPE_NAME` 列的值可能是 `DECIMAL()` 且完整的类型规范应为 `DECIMAL(10,2)`。<br /><br /> 创建参数显示为逗号分隔的值列表，列表中的值按提供顺序排列，列表两边不带括号。 如果创建参数是长度、最大长度、精度、小数位数、种子或增量，则分别使用“length”、“max length”、“precision”、“scale”、“seed”或“increment”。 如果创建参数是其他某值，则访问接口将确定要使用什么文本来描述创建参数。<br /><br /> 如果数据类型需要创建参数，则“()”通常会显示在类型名称中。 这用于指示插入创建参数的位置。 如果类型名称不包括“()”，则将用括号括上创建参数并将其追加到数据类型名称中。|  
|`IS_NULLABLE`|`DBTYPE_BOOL`||指示数据类型是否可以为 Null 的布尔值。<br /><br /> `VARIANT_TRUE` 指示数据类型可以为 Null。<br /><br /> `VARIANT_FALSE` 指示数据类型不是可以为 null。<br /><br /> `NULL` 指示不知道数据类型是否可以为 Null。|  
|`CASE_SENSITIVE`|`DBTYPE_BOOL`||指示数据类型是否为字符类型及区分大小写的布尔值。<br /><br /> `VARIANT_TRUE` 指示数据类型为字符类型且区分大小写。<br /><br /> `VARIANT_FALSE` 指示数据类型不是字符类型或者不区分大小写。|  
|`SEARCHABLE`|`DBTYPE_UI4`||一个整数，用于指示当访问接口支持 `ICommandText` 时可以在搜索中如何使用数据类型；否则为 `NULL`。<br /><br /> 此列可以具有下列值：<br /><br /> -   `DB_UNSEARCHABLE` 指示数据类型，不能用于`WHERE`子句。<br />-   `DB_LIKE_ONLY` 指示数据类型可在`WHERE`子句只能与`LIKE`谓词。<br />-   `DB_ALL_EXCEPT_LIKE` 指示数据类型可在`WHERE`子句使用所有比较运算符除外`LIKE`。<br />-   `DB_SEARCHABLE` 指示数据类型可在`WHERE`包含任何比较运算符的子句。|  
|`UNSIGNED_ATTRIBUTE`|`DBTYPE_BOOL`||指示数据类型是否无符号的布尔值。<br /><br /> `VARIANT_TRUE` 指示数据类型无符号。<br /><br /> `VARIANT_FALSE` 指示数据类型有符号。<br /><br /> `NULL` 指示这不适用于数据类型。|  
|`FIXED_PREC_SCALE`|`DBTYPE_BOOL`||指示数据类型是否具有固定精度和小数位数的布尔值。<br /><br /> `VARIANT_TRUE` 指示数据类型具有固定精度和小数位数。<br /><br /> `VARIANT_FALSE` 指示数据类型不具有固定精度和小数位数。|  
|`AUTO_UNIQUE_VALUE`|`DBTYPE_BOOL`||指示数据类型是否自动递增的布尔值。<br /><br /> `VARIANT_TRUE` 指示该类型的值可以自动递增。<br /><br /> `VARIANT_FALSE` 指示该类型的值不能自动递增。<br /><br /> 如果该值是 `VARIANT_TRUE`，则该类型的列是否始终自动递增取决于访问接口的 `DBPROP_COL_AUTOINCREMENT` 列属性。 如果 `DBPROP_COL_AUTOINCREMENT` 属性是可读/写属性，则该类型的列是否自动递增取决于 `DBPROP_COL_AUTOINCREMENT` 属性的设置。 如果 `DBPROP_COL_AUTOINCREMENT` 是只读属性，则该类型的所有列都自动递增或都不自动递增。|  
|`LOCAL_TYPE_NAME`|`DBTYPE_WSTR`||`TYPE_NAME` 的本地化版本。 如果数据访问接口不支持本地化名称，则返回 `NULL`。|  
|`MINIMUM_SCALE`|`DBTYPE_I2`||如果类型指示符为 `DBTYPE_VARNUMERIC`、`DBTYPE_DECIMAL` 或 `DBTYPE_NUMERIC`，则为小数点右边允许的最小位数。 否则为`NULL`。|  
|`MAXIMUM_SCALE`|`DBTYPE_I2`||如果类型指示符为 `DBTYPE_VARNUMERIC`、`DBTYPE_DECIMAL` 或 `DBTYPE_NUMERIC`，则为小数点右边允许的最大位数；否则为 N`U`LL。|  
|`GUID`|`DBTYPE_GUID`||（以备将来使用）如果相应类型在类型库中进行了说明，则为该类型的 `GUID`。 否则为`NULL`。|  
|`TYPELIB`|`DBTYPE_WSTR`||（以备将来使用）如果类型在类型库中进行了说明，则为包含该类型说明的类型库。 否则，为 NULL。|  
|`VERSION`|`DBTYPE_WSTR`||（以备将来使用）类型定义的版本。 访问接口可能希望控制类型定义的版本。 不同的访问接口可能使用不同的版本控制方案，例如时间戳或数字（整数或浮点数）。 如果不支持，则为 `NULL`。|  
|`IS_LONG`|`DBTYPE_BOOL`||一个布尔值，指示数据类型是否是二进制大型对象块 (BLOB) 并具有非常长的数据。<br /><br /> `VARIANT_TRUE` 指示数据类型是包含非常长的数据的 `BLOB`；非常长数据的定义特定于访问接口。<br /><br /> `VARIANT_FALSE` 指示数据类型是不包含非常长的数据的 `BLOB` 或者不是 `BLOB`。<br /><br /> 该值确定由 `DBCOLUMNFLAGS_ISLONG` 中的 `GetColumnInfo` 和 `IColumnsInfo` 中的 `GetParameterInfo` 返回的 `ICommandWithParameters` 标志的设置。|  
|`BEST_MATCH`|`DBTYPE_BOOL`||指示数据类型是否是最佳匹配的布尔值。<br /><br /> `VARIANT_TRUE` 指示相应数据类型是数据存储区中所有数据类型和由 `DATA_TYPE` 列中的值指示的 OLE DB 数据类型之间的最佳匹配。<br /><br /> `VARIANT_FALSE` 指示相应数据类型不是最佳匹配。<br /><br /> 对于 `DATA_TYPE` 列的值相同的每个行集，只在一个行中将 `BEST_MATCH` 列设置为 `VARIANT_TRUE`。|  
|`IS_FIXEDLENGTH`|`DBTYPE_BOOL`||指示列的长度是否固定的布尔值。<br /><br /> `VARIANT_TRUE` 指示由数据定义语言 (DDL) 创建的此类型的列的长度将是固定的。<br /><br /> `VARIANT_FALSE` 指示由 DDL 创建的此类型的列的长度将是可变的。<br /><br /> 如果此字段为 `NULL`，则不知道访问接口将会使用固定长度列还是可变长度列映射此字段。|  
  
 行集按 `DATA_TYPE` 排序。  
  
## <a name="restriction-columns"></a>限制列  
 `DBSCHEMA_PROVIDER_TYPES`行集可以限制下表中列出的列。  
  
|列名|类型指示符|限制状态|  
|-----------------|--------------------|-----------------------|  
|`DATA_TYPE`|`DBTYPE_UI2`||  
|`BEST_MATCH`|`DBTYPE_BOOL`||  
  
## <a name="see-also"></a>请参阅  
 [OLE DB 架构行集](ole-db-schema-rowsets.md)  
  
  
