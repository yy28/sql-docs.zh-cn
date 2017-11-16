---
title: "DBSCHEMA_PROVIDER_TYPES 行集 |Microsoft 文档"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: schema-rowsets
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- DBSCHEMA_PROVIDER_TYPES
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DBSCHEMA_PROVIDER_TYPES rowset
ms.assetid: 255e01ba-53a9-478d-9b86-45faba76710e
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 6906aec1d1c1dd53b8c833d59483aa0453cf284b
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="dbschemaprovidertypes-rowset"></a>DBSCHEMA_PROVIDER_TYPES 行集
  标识数据访问接口支持的（基本）数据类型。  
  
## <a name="rowset-columns"></a>行集列  
 **DBSCHEMA_PROVIDER_TYPES**行集包含以下各列。  
  
|列名|类型指示符|Description|  
|-----------------|--------------------|-----------------|  
|**类型 _ 名称**|**DBTYPE_WSTR**|特定于访问接口的数据类型名称。|  
|**DATA_TYPE**|**DBTYPE_UI2**|数据类型的指示符。|  
|**COLUMN_SIZE**|**DBTYPE_UI4**|非数值列的长度或以下参数，该参数或者是最大值或者是访问接口为此类型定义的长度。 对于字符数据，此为最大值或定义长度（以字符为单位）。 对于 DateTime 数据类型，本列为字符串表示形式的长度（假定精度允许的最大值为秒的小数形式）。<br /><br /> 如果数据类型为数值，则此为数据类型最大精度的上限。|  
|**LITERAL_PREFIX**|**DBTYPE_WSTR**|用于在文本命令中作为此类型文字的前缀的一个或多个字符。|  
|**LITERAL_SUFFIX**|**DBTYPE_WSTR**|用于在文本命令中作为此类型文字的后缀的一个或多个字符。|  
|**CREATE_PARAMS**|**DBTYPE_WSTR**|创建此数据类型的列时，由使用者指定的创建参数。 例如，SQL 数据类型，**十进制，**需要精度和小数位数。 在这种情况下，创建参数可能是字符串“precision,scale”。 中的文本命令创建**十进制**具有 10 精度和小数位数为 2，值的列**TYPE_NAME**列可能是**DECIMAL()**和完整的类型说明将为**DECIMAL(10,2)**。<br /><br /> 创建参数显示为逗号分隔的值列表，列表中的值按提供顺序排列，列表两边不带括号。 如果创建参数是长度、最大长度、精度、小数位数、种子或增量，则分别使用“length”、“max length”、“precision”、“scale”、“seed”或“increment”。 如果创建参数是其他某值，则访问接口将确定要使用什么文本来描述创建参数。<br /><br /> 如果数据类型需要创建参数，则“()”通常会显示在类型名称中。 这用于指示插入创建参数的位置。 如果类型名称不包括“()”，则将用括号括上创建参数并将其追加到数据类型名称中。|  
|**IS_NULLABLE**|**DBTYPE_BOOL**|指示数据类型是否可以为 Null 的布尔值。<br /><br /> **VARIANT_TRUE**该值指示数据类型为 null。<br /><br /> **VARIANT_FALSE**指示数据类型不是可以为 null。<br /><br /> **NULL**-指示，并不知道数据类型是否可以为 null。|  
|**CASE_SENSITIVE**|**DBTYPE_BOOL**|指示数据类型是否为字符类型及区分大小写的布尔值。<br /><br /> **VARIANT_TRUE**指示的数据类型是字符类型，并且区分大小写。<br /><br /> **VARIANT_FALSE**指示的数据类型不是字符类型，或不区分大小写。|  
|**可搜索**|**DBTYPE_UI4**|一个整数，指示如何的数据类型可在搜索如果提供程序支持**ICommandText**; 否则为**NULL**。 此列可以具有下列值：<br /><br /> **DB_UNSEARCHABLE**指示的数据类型不能使用在**其中**子句。<br /><br /> **DB_LIKE_ONLY**指示的数据类型可在**其中**子句只能与**如**谓词。<br /><br /> **DB_ALL_EXCEPT_LIKE**指示的数据类型可在**其中**子句与除之外的所有比较运算符**如**。<br /><br /> **DB_SEARCHABLE**指示的数据类型可在**其中**子句的任何比较运算符。|  
|**UNSIGNED_ATTRIBUTE**|**DBTYPE_BOOL**|指示数据类型是否无符号的布尔值。<br /><br /> **VARIANT_TRUE**指示的数据类型是无符号。<br /><br /> **VARIANT_FALSE**指示的数据类型进行签名。<br /><br /> **NULL**指示这不是最适用于该数据类型。|  
|**FIXED_PREC_SCALE**|**DBTYPE_BOOL**|指示数据类型是否具有固定精度和小数位数的布尔值。<br /><br /> **VARIANT_TRUE**指示的数据类型具有固定的精度和小数位数。<br /><br /> **VARIANT_FALSE**指示的数据类型不具有固定的精度和小数位数。|  
|**AUTO_UNIQUE_VALUE**|**DBTYPE_BOOL**|指示数据类型是否自动递增的布尔值。<br /><br /> **VARIANT_TRUE**指示，此类型的值可以是自动增量。<br /><br /> **VARIANT_FALSE**指示此类型的值不能为自动增量。<br /><br /> 如果此值为**VARIANT_TRUE**、 指示是否在此类型的列始终自动增量取决于提供程序的**DBPROP_COL_AUTOINCREMENT**列属性。 如果**DBPROP_COL_AUTOINCREMENT**属性为读/写，指示是否在此类型的列自动增量依赖于设置**DBPROP_COL_AUTOINCREMENT**属性。 如果**DBPROP_COL_AUTOINCREMENT**是只读属性，所有或此类型的列是自动增量。|  
|**LOCAL_TYPE_NAME**|**DBTYPE_WSTR**|本地化的版本**TYPE_NAME**。 **NULL**返回如果数据提供程序不支持具有本地化的名称。|  
|**MINIMUM_SCALE**|**DBTYPE_I2**|如果类型指示符为**DBTYPE_VARNUMERIC**， **DBTYPE_DECIMAL**，或**DBTYPE_NUMERIC**，数字的小数点右侧允许的最小数。 否则为**NULL**。|  
|**MAXIMUM_SCALE**|**DBTYPE_I2**|如果类型指示符为小数点右侧允许的数字的最大数**DBTYPE_VARNUMERIC**， **DBTYPE_DECIMAL**，或**DBTYPE_NUMERIC**; 否则为N**U**LL。|  
|**GUID**|**DBTYPE_GUID**|（专供将来使用）**GUID**的类型，如果将类型描述的类型库中。 否则为**NULL**。|  
|**类型库**|**DBTYPE_WSTR**|（以备将来使用）如果类型在类型库中进行了说明，则为包含该类型说明的类型库。 否则，为 NULL。|  
|**版本**|**DBTYPE_WSTR**|（以备将来使用）类型定义的版本。 访问接口可能希望控制类型定义的版本。 不同的访问接口可能使用不同的版本控制方案，例如时间戳或数字（整数或浮点数）。 **NULL**如果不支持。|  
|**IS_LONG**|**DBTYPE_BOOL**|一个布尔值，指示数据类型是否是二进制大型对象块 (BLOB) 并具有非常长的数据。<br /><br /> **VARIANT_TRUE**指示数据类型是**BLOB**包含很长的数据; 很长的数据的定义是特定于提供程序。<br /><br /> **VARIANT_FALSE**指示数据类型是**BLOB** ，不包含很长的数据或不是**BLOB**。<br /><br /> 此值确定的设置**DBCOLUMNFLAGS_ISLONG**标志返回**GetColumnInfo**中**IColumnsInfo**和**GetParameterInfo**中**ICommandWithParameters**。|  
|**BEST_MATCH**|**DBTYPE_BOOL**|指示数据类型是否是最佳匹配的布尔值。<br /><br /> **VARIANT_TRUE**指示的数据类型是数据存储区中的所有数据类型与中的值指示的 OLE DB 数据类型之间的最佳匹配**DATA_TYPE**列。<br /><br /> **VARIANT_FALSE**指示数据类型不是最佳匹配。<br /><br /> 为每个在其中的行集的值**DATA_TYPE**列是相同的**BEST_MATCH**列设置为**VARIANT_TRUE**仅包含一行。|  
|**IS_FIXEDLENGTH**|**DBTYPE_BOOL**|指示列的长度是否固定的布尔值。<br /><br /> **VARIANT_TRUE**指示的由数据定义语言 (DDL) 创建此类型的列将为固定长度。<br /><br /> **VARIANT_FALSE**指示 DDL 创建此类型的列将会的可变长度。<br /><br /> 如果此字段为**NULL**，并不知道该提供程序是否将映射具有固定长度或可变长度列此字段。|  
  
 行集按排序**DATA_TYPE**。  
  
## <a name="restriction-columns"></a>限制列  
 **DBSCHEMA_PROVIDER_TYPES**行集可限制在下表中列出的列。  
  
|列名|类型指示符|  
|-----------------|--------------------|  
|**DATA_TYPE**|**DBTYPE_UI2**|  
|**BEST_MATCH**|**DBTYPE_BOOL**|  
  
## <a name="see-also"></a>另请参阅  
 [OLE DB 架构行集合](../../../analysis-services/schema-rowsets/ole-db/ole-db-schema-rowsets.md)  
  
  

