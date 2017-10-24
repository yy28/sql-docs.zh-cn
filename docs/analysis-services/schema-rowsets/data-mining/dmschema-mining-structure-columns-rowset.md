---
title: "DMSCHEMA_MINING_STRUCTURE_COLUMNS 行集 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- DMSCHEMA_MINING_STRUCTURE_COLUMNS
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DMSCHEMA_MINING_STRUCTURE_COLUMNS rowset
ms.assetid: 81f25502-ac90-42f1-8ddf-7b0f9752ebfd
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ff811a339635f5ff914224a060e14a52e3f94d6c
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="dmschemaminingstructurecolumns-rowset"></a>DMSCHEMA_MINING_STRUCTURE_COLUMNS 行集
  描述部署在正在运行的服务器上的所有挖掘结构的各个列[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
## <a name="rowset-columns"></a>行集列  
 **DMSCHEMA_MINING_STRUCTURE_COLUMNS**行集包含以下各列。  
  
|列名|类型指示符|长度|Description|  
|-----------------|--------------------|------------|-----------------|  
|**STRUCTURE_CATALOG**|**DBTYPE_WSTR**||目录名称。|  
|**STRUCTURE_SCHEMA**|**DBTYPE_WSTR**||非限定的架构名称。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]不支持架构，因此此列始终是**NULL**。|  
|**STRUCTURE_NAME**|**DBTYPE_WSTR**||结构名称。 此列不能包含**NULL**。|  
|**COLUMN_NAME**|**DBTYPE_WSTR**||列的名称。 只保证在共享同一种模式的列之间具有唯一性。 例如，如果两个嵌套列属于同一结构中的两个不同嵌套表，则它们可能同名。|  
|**COLUMN_GUID**|**DBTYPE_GUID**||列 GUID。 不要使用 Guid 来标识列的提供程序应返回**NULL**此列中。|  
|**COLUMN_PROPID**|**DBTYPE_UI4**||列属性 ID。 未将属性 Id 与列的提供程序应返回**NULL**此列中。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)][!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]返回**NULL**此列。|  
|**ORDINAL_POSITION**|**DBTYPE_UI4**||列序号。 列从 1 开始编号。 **NULL**如果没有稳定序号值的列。|  
|**COLUMN_HASDEFAULT**|**DBTYPE_BOOL**||指示此列是否有默认值的布尔值。<br /><br /> **TRUE**如果列具有默认值。<br /><br /> **FALSE**如果列不具有默认值，或如果它是未知列是否具有默认值。|  
|**COLUMN_DEFAULT**|**DBTYPE_WSTR**||列的默认值。 一个提供程序可能会公开**DBCOLUMN_DEFAULTVALUE**但不是**DBCOLUMN_HASDEFAULT** （对于 ISO 表） 中返回的行集**IColumnsRowset::GetColumnsRowset**。<br /><br /> 如果默认值是**NULL**， **COLUMN_HASDEFAULT**是**TRUE**和**COLUMN_DEFAULT**列为**NULL**值。|  
|**COLUMN_FLAGS**|**DBTYPE_UI4**||描述列特征的位掩码。 **DBCOLUMNFLAGS**枚举的类型的位掩码中指定的位。 此列不能包含**NULL**值。 有效值包括：<br /><br /> **DBCOLUMNFLAGS_ISNULLABLE** (**0x20**)<br /><br /> **DBCOLUMNFLAGS_MAYBENULL** (**0x40**)<br /><br /> **DBCOLUMNFLAGS_ISLONG** (**0x80**)|  
|**IS_NULLABLE**|**DBTYPE_BOOL**||指示此列是否有默认值的布尔值。<br /><br /> **TRUE**如果列可以包含**NULL**;**FALSE**，否则为。|  
|**DATA_TYPE**|**DBTYPE_UI2**||列的数据类型的指示符。 例如：<br /><br /> "**表**"= **DBTYPE_HCHAPTER**<br /><br /> "**文本**"= **DBTYPE_WCHAR**<br /><br /> "**长**"=**是 DBTYPE_I8**<br /><br /> "**DOUBLE**"= **DBTYPE_R8**<br /><br /> "**日期**"= **DBTYPE_DATE**|  
|**TYPE_GUID**|**DBTYPE_GUID**||列的数据类型的 GUID。 不要使用 Guid 来确定数据类型的提供程序应返回**NULL**此列中。|  
|**CHARACTER_MAXIMUM_LENGTH**|**DBTYPE_UI4**||列中值的最大可能长度。 对于字符列、二进制值列或位列，可以是下列值之一：<br /><br /> 如果已定义列的长度，则为字符、字节或位列各自的最大长度。 例如，SQL 表中的 `CHAR(5)` 列的最大长度为 5。<br /><br /> 如果未定义列的长度，则为字符、字节或位列各自数据类型的最大长度。<br /><br /> 如果列和数据类型的最大长度均未定义，则为零 (0)。<br /><br /> **NULL**对于所有其他类型的列。|  
|**CHARACTER_OCTET_LENGTH**|**DBTYPE_UI4**||如果列的类型为字符或二进制值时，则为列的八进制最大长度（字节）。 零值 (0) 表示列没有最大长度。 **NULL**对于所有其他类型的列。|  
|**NUMERIC_PRECISION**|**DBTYPE_UI2**||如果列的数据类型而不是数值数据类型的列的最大精度**VARNUMERIC**;**NULL**如果列的数据类型不是数值或是**VARNUMERIC**。<br /><br /> 数据类型的列的精度**DBTYPE_DECIMAL**或**DBTYPE_NUM**ERIC 取决于列的定义。|  
|**NUMERIC_SCALE**|**DBTYPE_I2**||如果列的类型指示符为小数点右侧的数字个数**DBTYPE_DECIMAL**， **DBTYPE_NUMERIC**，或**DBTYPE_VARNUMERIC**。 否则，这就是**NULL**。|  
|**DATETIME_PRECISION**|**DBTYPE_UI4**||如果列为 datetime 或间隔类型，则为列的 DateTime 精度（秒的小数部分的位数）。 如果列的数据类型不是日期时间，这是**NULL**。|  
|**CHARACTER_SET_CATALOG**|**DBTYPE_WSTR**||在其中定义字符集的目录名称。 **NULL**如果提供程序不支持目录或不同的字符集。|  
|**CHARACTER_SET_SCHEMA**|**DBTYPE_WSTR**||定义在其中的字符集的架构的非限定的名称。 **NULL**如果提供程序不支持架构或不同的字符集。|  
|**CHARACTER_SET_NAME**|**DBTYPE_WSTR**||字符集名称。 **NULL**如果提供程序不支持不同的字符集。|  
|**COLLATION_CATALOG**|**DBTYPE_WSTR**||在其中定义排序规则的目录名称。 **NULL**如果提供程序不支持目录或不同的排序规则。|  
|**COLLATION_SCHEMA**|**DBTYPE_WSTR**||在其中定义排序规则的非限定架构名称。 **NULL**如果提供程序不支持架构或不同的排序规则。|  
|**COLLATION_NAME**|**DBTYPE_WSTR**||排序规则名称。 **NULL**如果提供程序不支持不同的排序规则。|  
|**DOMAIN_CATALOG**|**DBTYPE_WSTR**||在其中定义域的目录名称。 **NULL**如果提供程序不支持目录或域。|  
|**DOMAIN_SCHEMA**|**DBTYPE_WSTR**||在其中定义域的非限定架构名称。 **NULL**如果提供程序不支持架构或域。|  
|**A I N _**|**DBTYPE_WSTR**||域名。 **NULL**如果提供程序不支持域。|  
|**DESCRIPTION**|**DBTYPE_WSTR**||易读的列说明。 **NULL**如果没有描述与该列关联。|  
|**DISTRIBUTION_FLAG**|**DBTYPE_WSTR**||挖掘结构列的分布：<br /><br /> "**正常**"<br /><br /> "**LOG_NORM**AL"<br /><br /> "**统一**"|  
|**P E**|**DBTYPE_WSTR**||挖掘结构列的内容类型：<br /><br /> "**密钥**"<br /><br /> "**离散**"<br /><br /> "**连续**"<br /><br /> "**DISCRETIZED (**[参数]**)**"<br /><br /> "**ORDERED**"<br /><br /> "**SEQUENCE_TIME**"<br /><br /> "**CYCLICAL**"<br /><br /> "**概率**"<br /><br /> "**方差**"<br /><br /> "**STDEV**"<br /><br /> "**支持**"<br /><br /> "**PROBABILITY_VARIANCE**"<br /><br /> "**PROBABILITY_STDEV**"|  
|**MODELING_FLAG**|**DBTYPE_WSTR**||逗号分隔的建模标志列表。 唯一受支持的标志为结构列"**NOT NULL**"。|  
|**IS_RELATED_TO_KEY**|**DBTYPE_BOOL**||指示此列是否与键关联的布尔值。<br /><br /> **VARIANT_TRUE**如果此列相关的键;**VARIANT_FALSE**否则为。 如果键是一个列中， **RELATED_ATTRIBUTE**字段 （可选） 可以包含的列名称。|  
|**RELATED_ATTRIBUTE**|**DBTYPE_WSTR**||与当前列相关或为其特殊属性的目标列的名称。|  
|**CONTAINING_COLUMN**|**DBTYPE_WSTR**||名称**表**列以包含此列。 **NULL**如果没有表包含的列。|  
|**IS_POPULATED**|**DBTYPE_BOOL**||指示此列是否了解可能的值集的布尔值。<br /><br /> **TRUE**列学习了一组的可能的值; 如果**FALSE**，否则为。|  
  
## <a name="restriction-columns"></a>限制列  
 **DMSCHEMA_MINING_STRUCTURE_COLUMNS**行集可限制下表中的列。  
  
|列名|类型指示符|限制状态|  
|-----------------|--------------------|-----------------------|  
|**STRUCTURE_CATALOG**|**DBTYPE_WSTR**|可选。|  
|**STRUCTURE_SCHEMA**|**DBTYPE_WSTR**|可选。|  
|**STRUCTURE_NAME**|**DBTYPE_WSTR**|可选。|  
|**COLUMN_NAME**|**DBTYPE_WSTR**|可选。|  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘架构行集](../../../analysis-services/schema-rowsets/data-mining/data-mining-schema-rowsets.md)  
  
  

