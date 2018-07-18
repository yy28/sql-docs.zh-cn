---
title: 参数和行集元数据 |Microsoft 文档
description: 参数和行集的元数据
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db-date-time
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- metadata [OLE DB]
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 92be2b0f5ed0ae3911bd5593f82c6e493075646e
ms.sourcegitcommit: e1bc8c486680e6d6929c0f5885d97d013a537149
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2018
ms.locfileid: "35666367"
---
# <a name="metadata---parameter-and-rowset"></a>元数据的参数和行集
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-asdbmi-md](../../../includes/appliesto-ss-asdb-asdw-pdw-asdbmi-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  本文提供有关以下类型和类型成员，与 OLE DB 日期和时间增强功能相关信息。  
  
-   DBBINDING 结构  
  
-   **ICommandWithParameters::GetParameterInfo**  
  
-   **ICommandWithParameters::SetParameterInfo**  
  
-   **IColumnsRowset::GetColumnsRowset**  
  
-   **IColumnsInfo::GetColumnInfo**  
  
## <a name="icommandwithparametersgetparameterinfo"></a>ICommandWithParameters::GetParameterInfo  
 通过 DBPARAMINFO 结构中返回的以下信息*prgParamInfo*:  
  
|参数类型|*wType*|*ulParamSize*|*bPrecision*|*bScale*|*dwFlags*<br /><br /> DBPARAMFLAGS_SS_ISVARIABLESCALE|  
|--------------------|-------------|-------------------|------------------|--------------|-----------------------------------------------------|  
|日期|DBTYPE_DBDATE|6|10|0|Clear|  
|time|DBTYPE_DBTIME2|10|8, 10..16|0..7|将|  
|smalldatetime|DBTYPE_DBTIMESTAMP|16|16|0|Clear|  
|DATETIME|DBTYPE_DBTIMESTAMP|16|23|3|Clear|  
|datetime2|DBTYPE_DBTIMESTAMP|16|19, 21..27|0..7|将|  
|datetimeoffset|DBTYPE_DBTIMESTAMPOFFSET|20|26, 28..34|0..7|将|  
  
 请注意，在某些情况下，值范围不是连续的。 这是因为当小数精度大于零时添加了小数点。  
  
 仅在 DBPARAMFLAGS_SS_ISVARIABLESCALE 时连接到时有效[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]（或更高版本） 服务器。 DBPARAMFLAGS_SS_ISVARIABLESCALE 永远不会连接到下层的服务器时设置。  
  
## <a name="icommandwithparameterssetparameterinfo-and-implied-parameter-types"></a>ICommandWithParameters::SetParameterInfo 和隐含的参数类型  
 在 DBPARAMBINDINFO 结构中提供的信息必须符合以下规定：  
  
|*pwszDataSourceType*<br /><br /> （特定于访问接口）|*pwszDataSourceType*<br /><br /> （一般 OLE DB）|*ulParamSize*|*bScale*|  
|----------------------------------------------------|-------------------------------------------------|-------------------|--------------|  
||DBTYPE_DATE|6|忽略|  
|日期|DBTYPE_DBDATE|6|忽略|  
||DBTYPE_DBTIME|10|忽略|  
|time|DBTYPE_DBTIME2|10|0..7|  
|smalldatetime||16|忽略|  
|DATETIME||16|忽略|  
|datetime2 或 DBTYPE_DBTIMESTAMP|DBTYPE_DBTIMESTAMP|16|0..7|  
|datetimeoffset|DBTYPE_DBTIMESTAMPOFFSET|20|0..7|  
  
 *BPrecision*参数将被忽略。  
  
 向服务器发送数据时将忽略“DBPARAMFLAGS_SS_ISVARIABLESCALE”。 应用程序可以通过使用提供程序特定的类型名称，强制旧表格数据数据流 (TDS) 类型的使用"**datetime**"和"**smalldatetime**"。 当连接到[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]（或更高版本） 服务器，"**datetime2**"将使用格式和隐式服务器转换时将发生，如有必要，类型名称是"**datetime2**"或"DBTYPE_DBTIMESTAMP"。 *bScale*如果特定于提供程序类型名称，则忽略"**datetime**"**smalldatetime**"使用。 否则，应用程序必须确保*bScale*正确设置。 应用程序从 MDAC 和 OLE DB 驱动程序从 SQL Server 的升级[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]"DBTYPE_DBTIMESTAMP"将会失败，如果它们没有设置该使用*bScale*正确。 连接到服务器实例时早于[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]、 *bScale* 0 或 3 的"DBTYPE_DBTIMESTAMP"以外的值是一个错误，将返回 E_FAIL。  
  
 当不调用 ICommandWithParameters::SetParameterInfo 时，该提供程序，如下所示意味着从 IAccessor::CreateAccessor 中指定的绑定类型的服务器类型：  
  
|绑定类型|*pwszDataSourceType*<br /><br /> （特定于访问接口）|  
|------------------|----------------------------------------------------|  
|DBTYPE_DATE|datetime2(0)|  
|DBTYPE_DBDATE|日期|  
|DBTYPE_DBTIME|time(0)|  
|DBTYPE_DBTIME2|time(7)|  
|DBTYPE_DBTIMESTAMP|datetime2(7)|  
|DBTYPE_DBTIMESTAMPOFFSET|datetimeoffset(7)|  
  
## <a name="icolumnsrowsetgetcolumnsrowset"></a>IColumnsRowset::GetColumnsRowset  
 **IColumnsRowset::GetColumnsRowset**返回以下各列：  
  
|列类型|DBCOLUMN_TYPE|DBCOLUM_COLUMNSIZE|DBCOLUMN_PRECISION|DBCOLUMN_SCALE、DBCOLUMN_DATETIMEPRECISION|DBCOLUMN_FLAGS、DBCOLUMNFLAGS_SS_ISVARIABLESCALE|  
|-----------------|--------------------|-------------------------|-------------------------|--------------------------------------------------|---------------------------------------------------------|  
|日期|DBTYPE_DBDATE|6|10|0|Clear|  
|time|DBTYPE_DBTIME2|10|8, 10..16|0..7|将|  
|smalldatetime|DBTYPE_DBTIMESTAMP|16|16|0|Clear|  
|DATETIME|DBTYPE_DBTIMESTAMP|16|23|3|Clear|  
|datetime2|DBTYPE_DBTIMESTAMP|16|19, 21..27|0..7|将|  
|datetimeoffset|DBTYPE_DBTIMESTAMPOFFSET|20|26, 28..34|0..7|将|  
  
 在 DBCOLUMN_FLAGS 中，对于日期/时间类型，DBCOLUMNFLAGS_ISFIXEDLENGTH 始终为 True，而下列标志则始终为 False：  
  
-   DBCOLUMNFLAGS_CACHEDEFERRED  
  
-   DBCOLUMNFLAGS_ISBOOKMARK  
  
-   DBCOLUMNFLAGS_ISCHAPTER  
  
-   DBCOLUMNFLAGS_ISLONG  
  
-   DBCOLUMNFLAGS_ISROWID  
  
-   DBCOLUMNFLAGS_ISROWVER  
  
-   DBCOLUMNFLAGS_MAYDEFER  
  
 可根据列的定义方式和实际查询设置其余标志（DBCOLUMNFLAGS_ISNULLABLE、DBCOLUMNFLAGS_MAYBENULL、DBCOLUMNFLAGS_WRITE 和 DBCOLUMNFLAGS_WRITEUNKNOWN）。  
  
 DBCOLUMN_FLAGS 中提供了新的 DBCOLUMNFLAGS_SS_ISVARIABLESCALE 标志，以使应用程序可以确定列的服务器类型，其中 DBCOLUMN_TYPE 为 DBTYPE_DBTIMESTAMP。 还必须使用 DBCOLUMN_SCALE 或 DBCOLUMN_DATETIMEPRECISION 标识服务器类型。  
  
 仅在 DBCOLUMNFLAGS_SS_ISVARIABLESCALE 时连接到时有效[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]（或更高版本） 服务器。 当连接到下级服务器时，未定义 DBCOLUMNFLAGS_SS_ISVARIABLESCALE。  
  
## <a name="icolumnsinfogetcolumninfo"></a>IColumnsInfo::GetColumnInfo  
 DBCOLUMNINFO 结构返回以下信息：  
  
|参数类型|*wType*|*ulColumnSize*|*bPrecision*|*bScale*|*dwFlags*<br /><br /> DBPARAMFLAGS_SS_ISVARIABLESCALE|  
|--------------------|-------------|--------------------|------------------|--------------|-----------------------------------------------------|  
|日期|DBTYPE_DBDATE|6|10|0|Clear|  
|time(1..7)|DBTYPE_DBTIME2|10|8, 10..16|0..7|将|  
|smalldatetime|DBTYPE_DBTIMESTAMP|16|16|0|Clear|  
|DATETIME|DBTYPE_DBTIMESTAMP|16|23|3|Clear|  
|datetime2|DBTYPE_DBTIMESTAMP|16|19, 21..27|0..7|将|  
|datetimeoffset|DBTYPE_DBTIMESTAMPOFFSET|20|26, 28..34|0..7|将|  
  
 在*dwFlags*、 DBCOLUMNFLAGS_ISFIXEDLENGTH 始终为 true 的日期/时间类型和以下标志均始终为 false:  
  
-   DBCOLUMNFLAGS_CACHEDEFERRED  
  
-   DBCOLUMNFLAGS_ISBOOKMARK  
  
-   DBCOLUMNFLAGS_ISCHAPTER  
  
-   DBCOLUMNFLAGS_ISLONG  
  
-   DBCOLUMNFLAGS_ISROWID  
  
-   DBCOLUMNFLAGS_ISROWVER、MAYDEFER  
  
 可以设置其余标志（DBCOLUMNFLAGS_ISNULLABLE、DBCOLUMNFLAGS_MAYBENULL、DBCOLUMNFLAGS_WRITE 和 DBCOLUMNFLAGS_WRITEUNKNOWN）。  
  
 新的标志中提供 DBCOLUMNFLAGS_SS_ISVARIABLESCALE *dwFlags*以允许应用程序确定的 server 类型的列，其中*wType*是 DBTYPE_DBTIMESTAMP。 *bScale*还必须使用来标识服务器类型。  
  
## <a name="see-also"></a>请参阅  
 [针对 OLE DB 日期和时间改进的数据类型支持](../../oledb/ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md)  
  
  
