---
title: 日期和时间以及架构行集 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- date/time [OLE DB], schema rowsets
ms.assetid: 8c35e86f-0597-4ef4-b2b8-f643e53ed4c2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 710fbfdfd57608c24c56def1f2f9c4ec373f1957
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63238016"
---
# <a name="date-and-time-and-schema-rowsets"></a>日期和时间以及架构行集
  本主题提供有关 COLUMNS 行集和 PROCEDURE_PARAMETERS 行集的信息。 该信息与 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 中引入的 OLE DB 日期和时间增强功能相关。  
  
## <a name="columns-rowset"></a>COLUMNS 行集  
 对于日期/时间类型将返回以下列值：  
  
|列类型|DATA_TYPE|COLUMN_FLAGS, DBCOLUMFLAGS_SS_ISVARIABLESCALE|DATETIME_PRECISION|  
|-----------------|----------------|------------------------------------------------------|-------------------------|  
|date|DBTYPE_DBDATE|Clear|0|  
|time|DBTYPE_DBTIME2|将|0..7|  
|smalldatetime|DBTYPE_DBTIMESTAMP|Clear|0|  
|DATETIME|DBTYPE_DBTIMESTAMP|Clear|3|  
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
  
 仅当连接到 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 或更高版本服务器时 DBCOLUMNFLAGS_SS_ISVARIABLESCALE 才有效。 连接到下级服务器时，未定义 DBCOLUMNFLAGS_SS_ISFIXEDSCALE。  
  
## <a name="procedureparameters-rowset"></a>PROCEDURE_PARAMETERS 行集  
 DATA_TYPE 包含与 COLUMNS 架构行集相同的值，并且 TYPE_NAME 包含服务器类型。  
  
 已添加新列 SS_DATETIME_PRECISION，以便返回类似于 COLUMNS 行集的 DATETIME_PRECISION 列中的类型精度。  
  
## <a name="providertypes-rowset"></a>PROVIDER_TYPES 行集  
 对于日期/时间类型将返回以下行：  
  
|类型-><br /><br /> “列”|date|time|smalldatetime|DATETIME|datetime2|datetimeoffset|  
|--------------------------|----------|----------|-------------------|--------------|---------------|--------------------|  
|TYPE_NAME|date|time|smalldatetime|DATETIME|datetime2|datetimeoffset|  
|DATA_TYPE|DBTYPE_DBDATE|DBTYPE_DBTIME2|DBTYPE_DBTIMESTAMP|DBTYPE_DBTIMESTAMP|DBTYPE_DBTIMESTAMP|DBTYPE_DBTIMESTAMPOFFSET|  
|COLUMN_SIZE|10|16|16|23|27|34|  
|LITERAL_PREFIX|”启用|”启用|”启用|”启用|”启用|”启用|  
|LITERAL_SUFFIX|”启用|”启用|”启用|”启用|”启用|”启用|  
|CREATE_PARAMS|NULL|小数位数|NULL|NULL|小数位数|小数位数|  
|IS_NULLABLE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|  
|CASE_SENSITIVE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|  
|UNSIGNED_ATTRIBUTE|NULL|NULL|NULL|NULL|NULL|NULL|  
|FIXED_PREC_SCALE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|AUTO_UNIQUE_VALUE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|LOCAL_TYPE_NAME|date|time|smalldatetime|DATETIME|datetime2|datetimeoffset|  
|MINIMUM_SCALE|NULL|0|NULL|NULL|0|0|  
|MAXIMUM_SCALE|NULL|7|NULL|NULL|7|7|  
|GUID|NULL|NULL|NULL|NULL|NULL|NULL|  
|TYPELIB|NULL|NULL|NULL|NULL|NULL|NULL|  
|VERSION|NULL|NULL|NULL|NULL|NULL|NULL|  
|IS_LONG|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|BEST_MATCH|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE，除非符合以下某项条件：<br /><br /> -是客户端连接到下级服务器。<br />的数据类型兼容性连接属性指定兼容性级别为 80。|VARIANT_TRUE，除非符合以下某项条件：<br /><br /> -是客户端连接到下级服务器。<br />的数据类型兼容性连接属性指定兼容性级别为 80。|VARIANT_TRUE|  
|IS_FIXEDLENGTH|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|  
  
 对于数字和小数类型，OLE DB 仅定义了 MINIMUM_SCALE 和 MAXIMUM_SCALE，因此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 对 time、datetime2 和 datetimeoffset 使用这些列是非标准行为。  
  
## <a name="see-also"></a>请参阅  
 [Metadata &#40;OLE DB&#41;](../../database-engine/dev-guide/metadata-ole-db.md)  
  
  
