---
title: 项目设置 （类型映射） (DB2ToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: cf426c69-6a8e-4d19-951d-6661d5ae2562
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 91498db5535c99c7c8afaba85efc35639510a079
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63270008"
---
# <a name="project-settings-type-mapping-db2tosql"></a>项目设置 （类型映射） (DB2ToSQL)
类型映射页**项目设置**对话框中包含自定义如何 SSMA 将转换到 DB2 数据类型设置的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据类型。  
  
类型映射页现已推出**项目设置**并**默认项目设置**对话框。  
  
-   若要在指定的所有将来的 SSMA 项目设置**工具**菜单上，单击**默认项目设置**，选择迁移项目类型设置为其所需查看或更改从**迁移目标版本**下拉列表中，然后单击**类型映射**在左窗格的底部。  
  
-   在指定的当前项目中，设置**工具**菜单上，单击**项目设置**，然后单击**类型映射**在左窗格的底部。  
  
若要指定当前对象或对象类设置，请使用**类型映射**主 SSMA 窗口中的选项卡。  
  
## <a name="options"></a>选项  
下表显示**类型映射**选项卡上选项：  
  
**源类型**  
映射的 DB2 数据类型。  
  
**目标类型**  
目标[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]指定 DB2 数据类型的数据类型。  
  
请参阅下节，了解 DB2 类型映射的默认值 SSMA 中的表。  
  
**“添加”**  
单击此项可将数据类型添加到映射列表。  
  
**编辑**  
单击可编辑所选的数据类型映射列表中。  
  
**删除**  
单击以从映射列表中删除所选的数据类型映射。  
  
重置为默认值   
单击以重置为 SSMA 默认值的类型映射列表。  
  
## <a name="default-type-mappings"></a>默认类型映射  
在适用于 DB2 的 SSMA，可以设置自变量、 列、 局部变量和返回值的自定义类型的映射。 参数和返回类型的默认映射是几乎完全相同。  
  
### <a name="default-argument-type-and-return-value-type-mapping"></a>默认自变量类型和返回值类型映射  
下表包含有关参数和返回值的默认数据类型映射。  
  
|DB2 数据类型|默认[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据类型|  
|-----------------|-------------------------------------------------------------------------|  
|bfile|varbinary(max)|  
|binary_double|float[53]|  
|binary_float|float[53]|  
|binary_integer|ssNoversion|  
|blob|varbinary(max)|  
|boolean|bit|  
|char|varchar(max)|  
|char varying|varchar(max)|  
|character|varchar(max)|  
|character varying|varchar(max)|  
|clob|varchar(max)|  
|date|datetime2[0]|  
|dec|dec[38][0]|  
|Decimal|float[53]|  
|double precision|float[53]|  
|FLOAT|float[53]|  
|ssNoversion|ssNoversion|  
|integer|ssNoversion|  
|long|varchar(max)|  
|原始长时间|varbinary(max)|  
|long raw[\*..8000]<sup>\*</sup>|varbinary[\*]|  
|long raw[8001..\*]<sup>\*</sup>|varbinary(max)|  
|national char|nvarchar(max)|  
|national char varying|nvarchar(max)|  
|区域字符集|nvarchar(max)|  
|不同的区域字符集<sup>\*\*</sup>|nvarchar(max)|  
|不同的国家/地区字符<sup>\*</sup>|nvarchar(max)|  
|NCHAR|nvarchar(max)|  
|nclob|nvarchar(max)|  
|number|float[53]|  
|NUMERIC|float[53]|  
|nvarchar2|nvarchar(max)|  
|pls_integer|ssNoversion|  
|raw|varbinary(max)|  
|REAL|float[53]|  
|rowid|UNIQUEIDENTIFIER|  
|signtype|SMALLINT|  
|SMALLINT|SMALLINT|  
|string|varchar(max)|  
|TIMESTAMP|datetime2|  
|使用本地时区的时间戳|datetimeoffset|  
|带时区的时间戳|datetimeoffset|  
|urowid|UNIQUEIDENTIFIER|  
|varchar|varchar(max)|  
|varchar2|varchar(max)|  
|xmltype|xml|  
  
<sup>\*</sup> 适用于返回值类型映射仅。  
  
<sup>\*\*</sup> 适用于自变量类型映射仅。  
  
### <a name="default-column-type-mapping"></a>默认列类型映射  
下表包含列的默认类型映射。  
  
|DB2 数据类型|默认[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据类型|  
|-----------------|-------------------------------------------------------------------------|  
|bfile|varbinary(max)|  
|binary_double|float[53]|  
|binary_float|float[53]|  
|blob|varbinary(max)|  
|char|char|  
|char varying[\*..\*]|varchar[\*]|  
|char[\*..\*]|char[\*]|  
|character|char|  
|character varying[\*..\*]|varchar[\*]|  
|character[\*..\*]|char[\*]|  
|clob|varchar(max)|  
|date|datetime2[0]|  
|dec|dec[38][0]|  
|dec[\*..\*]|dec[\*][0]|  
|dec[\*..\*][\*..\*]|dec[\*][\*]|  
|Decimal|decimal[38][0]|  
|decimal[\*..\*]|decimal[\*][0]|  
|decimal[\*..\*][\*..\*]|decimal[\*][\*]|  
|double precision|float[53]|  
|FLOAT|float[53]|  
|float[\*..53]|float[\*]|  
|float[54..\*]|float[53]|  
|ssNoversion|ssNoversion|  
|integer|ssNoversion|  
|long|varchar(max)|  
|原始长时间|varbinary(max)|  
|长时间原始 [\*...8000]|varbinary[\*]|  
|长时间原始 [8001...\*]|varbinary(max)|  
|long varchar|varchar(max)|  
|long[\*..8000]|varchar[\*]|  
|long[8001..\*]|varchar(max)|  
|national char|NCHAR|  
|national char varying [\*...\*]|nvarchar[\*]|  
|national char [\*...\*]|nchar[\*]|  
|区域字符集|NCHAR|  
|不同的区域字符集 [\*...\*]|nvarchar[\*]|  
|区域字符集 [\*...\*]|nchar[\*]|  
|NCHAR|NCHAR|  
|nchar[\*]|nchar[\*]|  
|nclob|nvarchar(max)|  
|number|float[53]|  
|number[\*..\*]|numeric[\*]|  
|number[\*..\*][\*..\*]|numeric[\*][\*]|  
|NUMERIC|NUMERIC|  
|numeric[\*..\*]|numeric[\*]|  
|numeric[\*..\*][\*..\*]|numeric[\*][\*]|  
|nvarchar2[\*..\*]|nvarchar[\*]|  
|raw[\*..\*]|varbinary[\*]|  
|REAL|float[53]|  
|rowid|UNIQUEIDENTIFIER|  
|SMALLINT|SMALLINT|  
|TIMESTAMP|datetime2|  
|使用本地时区的时间戳|datetimeoffset|  
|使用本地时区的时间戳 [\*...\*]|datetimeoffset[\*]|  
|带时区的时间戳|datetimeoffset|  
|带时区的时间戳 [\*...\*]|datetimeoffset[\*]|  
|timestamp[\*..\*]|datetime2[\*]|  
|urowid|UNIQUEIDENTIFIER|  
|urowid[\*..\*]|UNIQUEIDENTIFIER|  
|varchar[\*..\*]|varchar[\*]|  
|varchar2[\*..\*]|varchar[\*]|  
|Xmltype|xml|  
  
### <a name="default-local-variable-type-mapping"></a>默认本地变量的类型映射  
下表包含本地变量的默认类型映射。  
  
|DB2 数据类型|默认[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据类型|  
|-----------------|-------------------------------------------------------------------------|  
|Bfile|varbinary(max)|  
|binary_double|float[53]|  
|binary_float|float[53]|  
|binary_interger|ssNoversion|  
|Blob|varbinary(max)|  
|Boolean|bit|  
|Char|char|  
|char varying[\*..8000]|varchar[\*]|  
|char varying [8001...\*]|varchar(max)|  
|char[\*..8000]|char[\*]|  
|char[8001..\*]|varchar(max)|  
|字符|char|  
|character varying[\*..8000]|varchar[\*]|  
|不同的字符 [8001...\*]|varchar(max)|  
|character[\*..8000]|char[\*]|  
|character[8001..\*]|varchar(max)|  
|clob|varchar(max)|  
|date|datetime2[0]|  
|dec|dec[38][0]|  
|dec[\*..\*]|dec[\*][0]|  
|dec[\*..\*][\*..\*]|dec[\*][\*]|  
|Decimal|decimal[38][0]|  
|decimal[\*..\*]|decimal[\*][0]|  
|decimal[\*..\*][\*..\*]|decimal[\*][\*]|  
|double precision|float[53]|  
|float|float[53]|  
|float[\*..53]|float[\*]|  
|float[54..\*]|float[53]|  
|smallint|ssNoversion|  
|Integer|ssNoversion|  
|integer[\*..\*]|numeric[\*][0]|  
|Long|varchar(max)|  
|原始长时间|varbinary(max)|  
|长时间原始 [\*...8000]|varbinary[\*]|  
|长时间原始 [8001...\*]|varbinary(max)|  
|national char|NCHAR|  
|national char varying [\*...4000]|nvarchar[\*]|  
|national char varying [4001...\*]|nvarchar(max)|  
|national char [\*...4000]|nchar[\*]|  
|national char [4001...\*]|nvarchar(max)|  
|区域字符集|NCHAR|  
|区域字符集 [\*...4000]|nvarchar[\*]|  
|区域字符集 [4001...\*]|nvarchar(max)|  
|不同的区域字符集 [\*...4000]|nvarchar[\*]|  
|不同的区域字符集 [4001...\*]|nvarchar(max)|  
|Nchar|NCHAR|  
|nchar[\*..4000]|nchar[\*]|  
|nchar[4001..\*]|nvarchar(max)|  
|不同的 nchar [\*...4000]|nvarchar[\*]|  
|不同的 nchar [4001...\*]|nvarchar(max)|  
|Nclob|nvarchar(max)|  
|Number|float[53]|  
|number[\*..\*]|numeric[\*]|  
|number[\*..\*][\*..\*]|numeric[\*][\*]|  
|Numeric|numeric[38][0]|  
|numeric[\*..\*]|numeric[\*]|  
|numeric[\*..\*][\*..\*]|numeric[\*][\*]|  
|nvarchar2[\*..4000]|nvarchar[\*]|  
|nvarchar2[4001..\*]|nvarchar(max)|  
|pls_integer|ssNoversion|  
|raw[\*..8000]|varbinary[\*]|  
|raw[8001..\*]|varbinary(max)|  
|Real|float[53]|  
|Rowid|UNIQUEIDENTIFIER|  
|signtype|SMALLINT|  
|Smallint|SMALLINT|  
|string[\*..8000]|varchar[\*]|  
|string[8001..\*]|varchar(max)|  
|TIMESTAMP|datetime2|  
|使用本地时区的时间戳|datetimeoffset|  
|带时区的时间戳|datetimeoffset|  
|使用本地时区的时间戳 [\*...\*]|datetimeoffset[\*]|  
|带时区的时间戳 [\*...\*]|datetimeoffset[\*]|  
|timestamp[\*..\*]|datetime2[\*]|  
|urowid|UNIQUEIDENTIFIER|  
|urowid[\*..\*]|UNIQUEIDENTIFIER|  
|varchar[\*..8000]|varchar[\*]|  
|varchar[8001..\*]|varchar(max)|  
|varchar2[\*..8000]|varchar[\*]|  
|varchar2[8001..\*]|varcha(max)|  
|Xmltype|xml|  
  
## <a name="see-also"></a>请参阅  
[用户界面参考&#40;DB2ToSQL&#41;](../../ssma/db2/user-interface-reference-db2tosql.md)  
  
