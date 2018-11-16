---
title: 参数和行集元数据 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- metadata [OLE DB]
ms.assetid: 31b318a4-20e7-4db0-b367-eb9938859029
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 64690a297e70ac9d8d07a7ade58b03bee01df3da
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/15/2018
ms.locfileid: "51662436"
---
# <a name="metadata---parameter-and-rowset"></a>元数据 - 参数和行集
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  本主题提供了与 OLE DB 日期和时间增强功能相关的以下类型和类型成员的相关信息。  
  
-   DBBINDING 结构  
  
-   **ICommandWithParameters::GetParameterInfo**  
  
-   **ICommandWithParameters::SetParameterInfo**  
  
-   **IColumnsRowset::GetColumnsRowset**  
  
-   **IColumnsInfo::GetColumnInfo**  
  
## <a name="icommandwithparametersgetparameterinfo"></a>ICommandWithParameters::GetParameterInfo  
 通过 prgParamInfo 在 DBPARAMINFO 结构中返回以下信息：  
  
|参数类型|wType|*ulParamSize*|*bPrecision*|*bScale*|*dwFlags*<br /><br /> DBPARAMFLAGS_SS_ISVARIABLESCALE|  
|--------------------|-------------|-------------------|------------------|--------------|-----------------------------------------------------|  
|日期|DBTYPE_DBDATE|6|10|0|Clear|  
|time|DBTYPE_DBTIME2|10|8, 10..16|0..7|将|  
|smalldatetime|DBTYPE_DBTIMESTAMP|16|16|0|Clear|  
|DATETIME|DBTYPE_DBTIMESTAMP|16|23|3|Clear|  
|datetime2|DBTYPE_DBTIMESTAMP|16|19,21..27|0..7|将|  
|datetimeoffset|DBTYPE_DBTIMESTAMPOFFSET|20|26,28..34|0..7|将|  
  
 请注意，在某些情况下，值范围不是连续的。 这是因为当小数精度大于零时添加了小数点。  
  
 DBPARAMFLAGS_SS_ISVARIABLESCALE 只有在连接到 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]（或更高版本）服务器时才有效。 当连接到下级服务器时，永远不会设置 DBPARAMFLAGS_SS_ISVARIABLESCALE。  
  
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
  
 向服务器发送数据时将忽略“DBPARAMFLAGS_SS_ISVARIABLESCALE”。 通过使用特定于提供程序的类型名称“datetime”和“smalldatetime”，应用程序可以强制使用旧的表格格式数据流 (TDS) 类型。 当连接到 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]（或更高版本）服务器时，如果类型名称为“datetime2”或“DBTYPE_DBTIMESTAMP”，将使用“datetime2”格式，并在必要时进行隐式服务器转换。 *bScale*如果提供程序特定于类型名称，则忽略"**datetime**"**smalldatetime**"使用。 否则，应用程序必须确保*bScale*已正确设置。 从 MDAC 升级的应用程序和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]使用"DBTYPE_DBTIMESTAMP"，如果它们没有设置将失败*bScale*正确。 当连接到早于 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 的服务器实例时，采用“DBTYPE_DBTIMESTAMP”且值不为 0 或 3 的 bScale 值不正确，并且将返回 E_FAIL。  
  
 不调用 icommandwithparameters:: Setparameterinfo 时，提供程序表示服务器类型 iaccessor:: Createaccessor 中指定的绑定类型，如下所示：  
  
|绑定类型|*pwszDataSourceType*<br /><br /> （特定于访问接口）|  
|------------------|----------------------------------------------------|  
|DBTYPE_DATE|datetime2(0)|  
|DBTYPE_DBDATE|日期|  
|DBTYPE_DBTIME|time(0)|  
|DBTYPE_DBTIME2|time(7)|  
|DBTYPE_DBTIMESTAMP|datetime2(7)|  
|DBTYPE_DBTIMESTAMPOFFSET|datetimeoffset(7)|  
  
## <a name="icolumnsrowsetgetcolumnsrowset"></a>IColumnsRowset::GetColumnsRowset  
 **Icolumnsrowset:: Getcolumnsrowset**返回以下列：  
  
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
  
 仅当连接到 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]（或更高版本）服务器时 DBCOLUMNFLAGS_SS_ISVARIABLESCALE 才有效。 当连接到下级服务器时，未定义 DBCOLUMNFLAGS_SS_ISVARIABLESCALE。  
  
## <a name="icolumnsinfogetcolumninfo"></a>IColumnsInfo::GetColumnInfo  
 DBCOLUMNINFO 结构返回以下信息：  
  
|参数类型|wType|*ulColumnSize*|*bPrecision*|*bScale*|*dwFlags*<br /><br /> DBPARAMFLAGS_SS_ISVARIABLESCALE|  
|--------------------|-------------|--------------------|------------------|--------------|-----------------------------------------------------|  
|日期|DBTYPE_DBDATE|6|10|0|Clear|  
|time(1..7)|DBTYPE_DBTIME2|10|8, 10..16|0..7|将|  
|smalldatetime|DBTYPE_DBTIMESTAMP|16|16|0|Clear|  
|DATETIME|DBTYPE_DBTIMESTAMP|16|23|3|Clear|  
|datetime2|DBTYPE_DBTIMESTAMP|16|19, 21..27|0..7|将|  
|datetimeoffset|DBTYPE_DBTIMESTAMPOFFSET|20|26, 28..34|0..7|将|  
  
 在 dwFlags 中，对于日期/时间类型，DBCOLUMNFLAGS_ISFIXEDLENGTH 始终为 True，而下列标志则始终为 False：  
  
-   DBCOLUMNFLAGS_CACHEDEFERRED  
  
-   DBCOLUMNFLAGS_ISBOOKMARK  
  
-   DBCOLUMNFLAGS_ISCHAPTER  
  
-   DBCOLUMNFLAGS_ISLONG  
  
-   DBCOLUMNFLAGS_ISROWID  
  
-   DBCOLUMNFLAGS_ISROWVER、MAYDEFER  
  
 可以设置其余标志（DBCOLUMNFLAGS_ISNULLABLE、DBCOLUMNFLAGS_MAYBENULL、DBCOLUMNFLAGS_WRITE 和 DBCOLUMNFLAGS_WRITEUNKNOWN）。  
  
 dwFlags 中提供了新的 DBCOLUMNFLAGS_SS_ISVARIABLESCALE 标志，以使应用程序可以确定列的服务器类型，其中 wType 为 DBTYPE_DBTIMESTAMP。 还必须使用 bScale 来标识服务器类型。  
  
## <a name="see-also"></a>请参阅  
 [元数据&#40;OLE DB&#41;](https://msdn.microsoft.com/library/605e3be5-aeea-4573-9847-b866ed3c8bff)  
  
  
