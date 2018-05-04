---
title: 项目设置 （类型映射） (DB2ToSQL) |Microsoft 文档
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-db2
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: cf426c69-6a8e-4d19-951d-6661d5ae2562
caps.latest.revision: 5
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: e6c81fab41d0e6d25ad442c8856b15edacf63b39
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="project-settings-type-mapping-db2tosql"></a>项目设置 （类型映射） (DB2ToSQL)
类型映射页**项目设置**对话框中包含自定义如何 SSMA 将转换到 DB2 数据类型的设置[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据类型。  
  
类型映射页可用于**项目设置**和**默认项目设置**对话框。  
  
-   若要对指定针对所有将来的 SSMA 项目中，设置**工具**菜单上，单击**默认项目设置**，选择为其设置所需查看或更改，不再是迁移项目类型**迁移目标版本**下拉列表中，然后单击**类型映射**在左窗格的底部。  
  
-   若要对指定为当前项目中，设置**工具**菜单上，单击**项目设置**，然后单击**类型映射**在左窗格的底部。  
  
若要指定设置的当前对象或对象的类，使用**类型映射**主 SSMA 窗口选项卡。  
  
## <a name="options"></a>选项  
下表显示**类型映射**选项卡上选项：  
  
**源类型**  
映射的 DB2 数据类型。  
  
**目标类型**  
目标[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]指定 DB2 数据类型的数据类型。  
  
请参阅下一部分对于 DB2 类型映射的默认 SSMA 中的表。  
  
**“添加”**  
单击此项可将数据类型添加到映射列表。  
  
**编辑**  
单击要编辑所选的数据类型映射列表中。  
  
**删除**  
单击以从映射列表中删除所选的数据类型映射。  
  
**重置为默认值**  
单击以将类型映射列表重置为 SSMA 默认值。  
  
## <a name="default-type-mappings"></a>默认类型映射  
SSMA for DB2，你可以设置为自变量、 列、 本地变量和返回值的自定义类型映射。 自变量和返回类型的默认映射是几乎完全相同。  
  
### <a name="default-argument-type-and-return-value-type-mapping"></a>默认自变量类型和返回值类型映射  
下表包含参数和返回值的默认数据类型映射。  
  
|DB2 数据类型|默认[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据类型|  
|-----------------|-------------------------------------------------------------------------|  
|Bfile|varbinary(max)|  
|binary_double|float [53]|  
|binary_float|float [53]|  
|binary_integer|int|  
|blob|varbinary(max)|  
|boolean|bit|  
|char|varchar(max)|  
|char varying|varchar(max)|  
|character|varchar(max)|  
|character varying|varchar(max)|  
|Clob|varchar(max)|  
|date|datetime2[0]|  
|dec|dec[38][0]|  
|decimal|float [53]|  
|双精度|float [53]|  
|float|float [53]|  
|int|int|  
|integer|int|  
|long|varchar(max)|  
|长时间原始|varbinary(max)|  
|长时间原始 [\*...8000]<sup>*</sup>|varbinary[*]|  
|长时间原始 [8001..\*]<sup>*</sup>|varbinary(max)|  
|国家/地区 char|nvarchar(max)|  
|不同的国家/地区 char|nvarchar(max)|  
|国家/地区字符|nvarchar(max)|  
|不同的国家/地区字符<sup>**</sup>|nvarchar(max)|  
|不同的国家/地区字符<sup>*</sup>|nvarchar(max)|  
|NCHAR|nvarchar(max)|  
|Nclob|nvarchar(max)|  
|number|float [53]|  
|numeric|float [53]|  
|nvarchar2|nvarchar(max)|  
|pls_integer|int|  
|raw|varbinary(max)|  
|real|float [53]|  
|Rowid|uniqueidentifier|  
|Signtype|smallint|  
|smallint|smallint|  
|string|varchar(max)|  
|timestamp|datetime2|  
|与本地时区的时间戳|datetimeoffset|  
|时区的时间戳|datetimeoffset|  
|Urowid|uniqueidentifier|  
|varchar|varchar(max)|  
|varchar2|varchar(max)|  
|xmltype|xml|  
  
<sup>*</sup> 适用于返回值类型映射仅。  
  
<sup>**</sup> 适用于自变量类型映射仅。  
  
### <a name="default-column-type-mapping"></a>默认列类型映射  
下表包含列的默认类型映射。  
  
|DB2 数据类型|默认[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据类型|  
|-----------------|-------------------------------------------------------------------------|  
|Bfile|varbinary(max)|  
|binary_double|float [53]|  
|binary_float|float [53]|  
|blob|varbinary(max)|  
|char|char|  
|不同的 char [*...\*]|varchar[*]|  
|char [*...\*]|char[*]|  
|character|char|  
|不同的字符 [*...\*]|varchar[*]|  
|字符 [*...\*]|char[*]|  
|Clob|varchar(max)|  
|date|datetime2[0]|  
|dec|dec[38][0]|  
|dec [*...\*]|dec[*][0]|  
|dec[*..\*][\*..\*]|dec[*][\*]|  
|decimal|decimal[38][0]|  
|十进制 [*...\*]|decimal[*][0]|  
|decimal[*..\*][\*..\*]|decimal[*][\*]|  
|双精度|float [53]|  
|float|float [53]|  
|float[*..53]|float[*]|  
|float[54..*]|float [53]|  
|int|int|  
|integer|int|  
|long|varchar(max)|  
|长时间原始|varbinary(max)|  
|长时间原始 [*...8000]|varbinary[*]|  
|长时间原始 [8001..*]|varbinary(max)|  
|long varchar|varchar(max)|  
|long[*..8000]|varchar[*]|  
|long[8001..*]|varchar(max)|  
|国家/地区 char|NCHAR|  
|不同的国家/地区 char [*...\*]|nvarchar[*]|  
|国家/地区 char [*...\*]|nchar[*]|  
|国家/地区字符|NCHAR|  
|不同的国家/地区字符 [*...\*]|nvarchar[*]|  
|国家/地区字符 [*...\*]|nchar[*]|  
|NCHAR|NCHAR|  
|nchar[*]|nchar[*]|  
|Nclob|nvarchar(max)|  
|number|float [53]|  
|数字 [*...\*]|numeric[*]|  
|number[*..\*][\*..\*]|numeric[*][\*]|  
|numeric|numeric|  
|数字 [*...\*]|numeric[*]|  
|numeric[*..\*][\*..\*]|numeric[*][\*]|  
|nvarchar2 [*...\*]|nvarchar[*]|  
|原始 [*...\*]|varbinary[*]|  
|real|float [53]|  
|Rowid|uniqueidentifier|  
|smallint|smallint|  
|timestamp|datetime2|  
|与本地时区的时间戳|datetimeoffset|  
|与本地时区的时间戳 [*...\*]|datetimeoffset[*]|  
|时区的时间戳|datetimeoffset|  
|时区的时间戳 [*...\*]|datetimeoffset[*]|  
|时间戳 [*...\*]|datetime2[*]|  
|Urowid|uniqueidentifier|  
|urowid [*...\*]|uniqueidentifier|  
|varchar [*...\*]|varchar[*]|  
|varchar2 [*...\*]|varchar[*]|  
|Xml 类型|xml|  
  
### <a name="default-local-variable-type-mapping"></a>默认本地变量的类型映射  
下表包含本地变量的默认类型映射。  
  
|DB2 数据类型|默认[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据类型|  
|-----------------|-------------------------------------------------------------------------|  
|Bfile|varbinary(max)|  
|binary_double|float [53]|  
|binary_float|float [53]|  
|binary_interger|int|  
|Blob|varbinary(max)|  
|Boolean|bit|  
|Char|char|  
|不同的 char [*...8000]|varchar[*]|  
|不同的 char [8001..*]|varchar(max)|  
|char[*..8000]|char[*]|  
|char[8001..*]|varchar(max)|  
|字符|char|  
|不同的字符 [*...8000]|varchar[*]|  
|不同的字符 [8001..*]|varchar(max)|  
|character[*..8000]|char[*]|  
|character[8001..*]|varchar(max)|  
|Clob|varchar(max)|  
|date|datetime2[0]|  
|dec|dec[38][0]|  
|dec [*...\*]|dec[*][0]|  
|dec[*..\*][\*..\*]|dec[*][\*]|  
|decimal|decimal[38][0]|  
|十进制 [*...\*]|decimal[*][0]|  
|decimal[*..\*][\*..\*]|decimal[*][\*]|  
|双精度|float [53]|  
|Float|float [53]|  
|float[*..53]|float[*]|  
|float[54..*]|float [53]|  
|int|int|  
|Integer|int|  
|integer[*..\*]|numeric[*][0]|  
|Long|varchar(max)|  
|长时间原始|varbinary(max)|  
|长时间原始 [*...8000]|varbinary[*]|  
|长时间原始 [8001..*]|varbinary(max)|  
|国家/地区 char|NCHAR|  
|不同的国家/地区 char [*...4000]|nvarchar[*]|  
|不同的国家/地区 char [4001..*]|nvarchar(max)|  
|国家/地区 char [*...4000]|nchar[*]|  
|国家/地区 char [4001..*]|nvarchar(max)|  
|国家/地区字符|NCHAR|  
|国家/地区字符 [*...4000]|nvarchar[*]|  
|国家/地区字符 [4001..*]|nvarchar(max)|  
|不同的国家/地区字符 [*...4000]|nvarchar[*]|  
|不同的国家/地区字符 [4001..*]|nvarchar(max)|  
|Nchar|NCHAR|  
|nchar[*..4000]|nchar[*]|  
|nchar[4001..*]|nvarchar(max)|  
|不同的 nchar [*...4000]|nvarchar[*]|  
|不同的 nchar [4001..*]|nvarchar(max)|  
|Nclob|nvarchar(max)|  
|Number|float [53]|  
|数字 [*...\*]|numeric[*]|  
|number[*..\*][\*..\*]|numeric[*][\*]|  
|数字|numeric[38][0]|  
|数字 [*...\*]|numeric[*]|  
|numeric[*..\*][\*..\*]|numeric[*][\*]|  
|nvarchar2[*..4000]|nvarchar[*]|  
|nvarchar2[4001..*]|nvarchar(max)|  
|pls_integer|int|  
|原始 [*...8000]|varbinary[*]|  
|raw[8001..*]|varbinary(max)|  
|Real|float [53]|  
|Rowid|uniqueidentifier|  
|Signtype|smallint|  
|Smallint|smallint|  
|string[*..8000]|varchar[*]|  
|string[8001..*]|varchar(max)|  
|timestamp|datetime2|  
|与本地时区的时间戳|datetimeoffset|  
|时区的时间戳|datetimeoffset|  
|与本地时区的时间戳 [*...\*]|datetimeoffset[*]|  
|时区的时间戳 [*...\*]|datetimeoffset[*]|  
|时间戳 [*...\*]|datetime2[*]|  
|Urowid|uniqueidentifier|  
|urowid [*...\*]|uniqueidentifier|  
|varchar[*..8000]|varchar[*]|  
|varchar[8001..*]|varchar(max)|  
|varchar2[*..8000]|varchar[*]|  
|varchar2[8001..*]|varcha(max)|  
|Xml 类型|xml|  
  
## <a name="see-also"></a>另请参阅  
[用户界面参考&#40;DB2ToSQL&#41;](../../ssma/db2/user-interface-reference-db2tosql.md)  
  
