---
title: 日期和时间以及架构行集 |Microsoft 文档
description: 日期和时间以及架构行集
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-date-time
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- date/time [OLE DB], schema rowsets
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 0b854408bff304dd15255b19ab470df41cdb0bc5
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="metadata---date-and-time-and-schema-rowsets"></a>元数据的日期和时间以及架构行集
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  本主题提供有关 COLUMNS 行集和 PROCEDURE_PARAMETERS 行集的信息。 该信息与 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 中引入的 OLE DB 日期和时间增强功能相关。  
  
## <a name="columns-rowset"></a>COLUMNS 行集  
 对于日期/时间类型将返回以下列值：  
  
|列类型|DATA_TYPE|COLUMN_FLAGS, DBCOLUMFLAGS_SS_ISVARIABLESCALE|DATETIME_PRECISION|  
|-----------------|----------------|------------------------------------------------------|-------------------------|  
|date|DBTYPE_DBDATE|Clear|0|  
|time|DBTYPE_DBTIME2|将|0..7|  
|smalldatetime|DBTYPE_DBTIMESTAMP|Clear|0|  
|datetime|DBTYPE_DBTIMESTAMP|Clear|3|  
|datetime2|DBTYPE_DBTIMESTAMP|将|0..7|  
|datetimeoffset|DBTYPE_DBTIMESTAMPOFFSET|将|0..7|  
  
 在 COLUMN_FLAGS 中，对于日期/时间类型，DBCOLUMNFLAGS_ISFIXEDLENGTH 始终为 True，并且以下标记始终为 False：  
  
-   DBCOLUMNFLAGS_CACHEDEFERRED  
  
-   DBCOLUMNFLAGS_ISBOOKMARK  
  
-   DBCOLUMNFLAGS_ISCHAPTER  
  
-   DBCOLUMNFLAGS_ISLONG  
  
-   DBCOLUMNFLAGS_ISROWID  
  
-   DBCOLUMNFLAGS_ISROWVER  
  
-   DBCOLUMNFLAGS_MAYDEFER  
  
 其余的标记（DBCOLUMNFLAGS_ISNULLABLE、DBCOLUMNFLAGS_MAYBENULL、DBCOLUMNFLAGS_WRITE 和 DBCOLUMNFLAGS_WRITEUNKNOWN）可能被设置，具体取决于列的定义方式。  
  
 在 COLUMN_FLAGS 中提供了新标记 DBCOLUMNFLAGS_SS_ISVARIABLESCALE，以允许应用程序确定 DATA_TYPE 为 DBTYPE_DBTIMESTAMP 的那些列的服务器类型。 为标识服务器类型还必须使用 DATETIME_PRECISION。  
  
 仅在 DBCOLUMNFLAGS_SS_ISVARIABLESCALE 时连接到时有效[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]或更高版本的服务器。 连接到下级服务器时，未定义 DBCOLUMNFLAGS_SS_ISFIXEDSCALE。  
  
## <a name="procedureparameters-rowset"></a>PROCEDURE_PARAMETERS 行集  
 DATA_TYPE 包含与 COLUMNS 架构行集相同的值，并且 TYPE_NAME 包含服务器类型。  
  
 已添加新列 SS_DATETIME_PRECISION，以便返回类似于 COLUMNS 行集的 DATETIME_PRECISION 列中的类型精度。  
  
## <a name="providertypes-rowset"></a>PROVIDER_TYPES 行集  
 对于日期/时间类型将返回以下行：  
  
|类型 -><br /><br /> 列|date|time|smalldatetime|datetime|datetime2|datetimeoffset|  
|--------------------------|----------|----------|-------------------|--------------|---------------|--------------------|  
|TYPE_NAME|date|time|smalldatetime|datetime|datetime2|datetimeoffset|  
|DATA_TYPE|DBTYPE_DBDATE|DBTYPE_DBTIME2|DBTYPE_DBTIMESTAMP|DBTYPE_DBTIMESTAMP|DBTYPE_DBTIMESTAMP|DBTYPE_DBTIMESTAMPOFFSET|  
|COLUMN_SIZE|10|16|16|23|27|34|  
|LITERAL_PREFIX|‘|‘|‘|‘|‘|‘|  
|LITERAL_SUFFIX|‘|‘|‘|‘|‘|‘|  
|CREATE_PARAMS|NULL|小数位数|NULL|NULL|小数位数|小数位数|  
|IS_NULLABLE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|  
|CASE_SENSITIVE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|  
|UNSIGNED_ATTRIBUTE|NULL|NULL|NULL|NULL|NULL|NULL|  
|FIXED_PREC_SCALE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|AUTO_UNIQUE_VALUE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|LOCAL_TYPE_NAME|date|time|smalldatetime|datetime|datetime2|datetimeoffset|  
|MINIMUM_SCALE|NULL|0|NULL|NULL|0|0|  
|MAXIMUM_SCALE|NULL|7|NULL|NULL|7|7|  
|GUID|NULL|NULL|NULL|NULL|NULL|NULL|  
|TYPELIB|NULL|NULL|NULL|NULL|NULL|NULL|  
|VERSION|NULL|NULL|NULL|NULL|NULL|NULL|  
|IS_LONG|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|BEST_MATCH|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE，除非符合以下某项条件：<br /><br /> 是连接到下级服务器的客户端。<br /><br /> 数据类型兼容性连接属性指定兼容性级别为 80。|VARIANT_TRUE，除非符合以下某项条件：<br /><br /> 是连接到下级服务器的客户端。<br /><br /> 数据类型兼容性连接属性指定兼容性级别为 80。|VARIANT_TRUE|  
|IS_FIXEDLENGTH|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|  
  
 OLE DB 仅定义 MINIMUM_SCALE 和 MAXIMUM_SCALE 对于数值和十进制类型，因此 OLE DB 驱动程序用于 SQL Server 的这些列的 datetime2 和 datetimeoffset 时间为非标准。  
  
## <a name="see-also"></a>另请参阅  
 [元数据&#40;OLE DB&#41;](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md)  
  
  
