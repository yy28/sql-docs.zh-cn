---
title: "项目设置 （类型映射） (OracleToSQL) |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-oracle
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4bb8466e-2199-4f00-8513-b04e9586723d
caps.latest.revision: 
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: Inactive
ms.openlocfilehash: f4be0d12ce3067f46c934cfa7e053ddd1779ac9f
ms.sourcegitcommit: f02598eb8665a9c2dc01991c36f27943701fdd2d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/13/2018
---
# <a name="project-settings-type-mapping-oracletosql"></a>项目设置 （类型映射） (OracleToSQL)
类型映射页**项目设置**对话框中包含自定义如何 SSMA 将转换到的 Oracle 数据类型的设置[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据类型。  
  
类型映射页可用于**项目设置**和**默认项目设置**对话框。  
  
-   若要对指定针对所有将来的 SSMA 项目中，设置**工具**菜单上，单击**默认项目设置**，选择为其设置所需查看或更改，不再是迁移项目类型**迁移目标版本**下拉列表中，然后单击**类型映射**在左窗格的底部。  
  
-   若要对指定为当前项目中，设置**工具**菜单上，单击**项目设置**，然后单击**类型映射**在左窗格的底部。  
  
若要指定设置的当前对象或对象的类，使用**类型映射**主 SSMA 窗口选项卡。  
  
## <a name="options"></a>选项  
下表显示**类型映射**选项卡上选项：  
  
**源类型**  
映射的 Oracle 数据类型。  
  
**目标类型**  
目标[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]指定 Oracle 数据类型的数据类型。  
  
请参阅下一部分对于 Oracle 类型映射的默认 SSMA 中的表。  
  
**“添加”**  
单击此项可将数据类型添加到映射列表。  
  
**编辑**  
单击要编辑所选的数据类型映射列表中。  
  
**删除**  
单击以从映射列表中删除所选的数据类型映射。  
  
**重置为默认值**  
单击以将类型映射列表重置为 SSMA 默认值。  
  
## <a name="default-type-mappings"></a>默认类型映射  
在适用于 Oracle 的 SSMA，可以设置为自变量、 列、 本地变量和返回值的自定义类型映射。 自变量和返回类型的默认映射是几乎完全相同。  
  
### <a name="default-argument-type-and-return-value-type-mapping"></a>默认自变量类型和返回值类型映射  
下表包含参数和返回值的默认数据类型映射。  
  
|Oracle 数据类型|默认[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据类型|  
|--------------------|-------------------------------------------------------------------------|  
|Bfile|varbinary(max)|  
|binary_double|float[53]|  
|binary_float|float[53]|  
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
|decimal|float[53]|  
|双精度|float[53]|  
|float|float[53]|  
|int|int|  
|integer|int|  
|long|varchar(max)|  
|长时间原始|varbinary(max)|  
|long raw[\*..8000]<sup>*</sup>|varbinary[*]|  
|长时间原始 [8001..\*]<sup>*</sup>|varbinary(max)|  
|国家/地区 char|nvarchar(max)|  
|不同的国家/地区 char|nvarchar(max)|  
|国家/地区字符|nvarchar(max)|  
|不同的国家/地区字符<sup>**</sup>|nvarchar(max)|  
|不同的国家/地区字符<sup>*</sup>|nvarchar(max)|  
|NCHAR|nvarchar(max)|  
|Nclob|nvarchar(max)|  
|number|float[53]|  
|numeric|float[53]|  
|nvarchar2|nvarchar(max)|  
|pls_integer|int|  
|raw|varbinary(max)|  
|real|float[53]|  
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
  
|Oracle 数据类型|默认[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据类型|  
|--------------------|-------------------------------------------------------------------------|  
|Bfile|varbinary(max)|  
|binary_double|float[53]|  
|binary_float|float[53]|  
|blob|varbinary(max)|  
|char|char|  
|不同的 char [*...\*]|varchar[*]|  
|char[*..\*]|char[*]|  
|character|char|  
|不同的字符 [*...\*]|varchar[*]|  
|character[*..\*]|char[*]|  
|Clob|varchar(max)|  
|date|datetime2[0]|  
|dec|dec[38][0]|  
|dec[*..\*]|dec[*][0]|  
|dec[*..\*][\*..\*]|dec[*][\*]|  
|decimal|decimal[38][0]|  
|decimal[*..\*]|decimal[*][0]|  
|decimal[*..\*][\*..\*]|decimal[*][\*]|  
|双精度|float[53]|  
|float|float[53]|  
|float[*..53]|float[*]|  
|float[54..*]|float[53]|  
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
|number|float[53]|  
|number[*..\*]|numeric[*]|  
|number[*..\*][\*..\*]|numeric[*][\*]|  
|numeric|numeric|  
|numeric[*..\*]|numeric[*]|  
|numeric[*..\*][\*..\*]|numeric[*][\*]|  
|nvarchar2[*..\*]|nvarchar[*]|  
|raw[*..\*]|varbinary[*]|  
|real|float[53]|  
|Rowid|uniqueidentifier|  
|smallint|smallint|  
|timestamp|datetime2|  
|与本地时区的时间戳|datetimeoffset|  
|与本地时区的时间戳 [*...\*]|datetimeoffset[*]|  
|时区的时间戳|datetimeoffset|  
|时区的时间戳 [*...\*]|datetimeoffset[*]|  
|timestamp[*..\*]|datetime2[*]|  
|Urowid|uniqueidentifier|  
|urowid[*..\*]|uniqueidentifier|  
|varchar[*..\*]|varchar[*]|  
|varchar2[*..\*]|varchar[*]|  
|Xmltype|xml|  
  
### <a name="default-local-variable-type-mapping"></a>默认本地变量的类型映射  
下表包含本地变量的默认类型映射。  
  
|Oracle 数据类型|默认[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据类型|  
|--------------------|-------------------------------------------------------------------------|  
|Bfile|varbinary(max)|  
|binary_double|float[53]|  
|binary_float|float[53]|  
|binary_interger|int|  
|Blob|varbinary(max)|  
|Boolean|bit|  
|Char|char|  
|char varying[*..8000]|varchar[*]|  
|char varying[8001..*]|varchar(max)|  
|char[*..8000]|char[*]|  
|char[8001..*]|varchar(max)|  
|字符|char|  
|character varying[*..8000]|varchar[*]|  
|character varying[8001..*]|varchar(max)|  
|character[*..8000]|char[*]|  
|character[8001..*]|varchar(max)|  
|Clob|varchar(max)|  
|date|datetime2[0]|  
|dec|dec[38][0]|  
|dec[*..\*]|dec[*][0]|  
|dec[*..\*][\*..\*]|dec[*][\*]|  
|decimal|decimal[38][0]|  
|decimal[*..\*]|decimal[*][0]|  
|decimal[*..\*][\*..\*]|decimal[*][\*]|  
|双精度|float[53]|  
|Float|float[53]|  
|float[*..53]|float[*]|  
|float[54..*]|float[53]|  
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
|national character[*..4000]|nvarchar[*]|  
|national character[4001..*]|nvarchar(max)|  
|不同的国家/地区字符 [*...4000]|nvarchar[*]|  
|不同的国家/地区字符 [4001..*]|nvarchar(max)|  
|Nchar|NCHAR|  
|nchar[*..4000]|nchar[*]|  
|nchar[4001..*]|nvarchar(max)|  
|不同的 nchar [*...4000]|nvarchar[*]|  
|不同的 nchar [4001..*]|nvarchar(max)|  
|Nclob|nvarchar(max)|  
|Number|float[53]|  
|number[*..\*]|numeric[*]|  
|number[*..\*][\*..\*]|numeric[*][\*]|  
|数字|numeric[38][0]|  
|numeric[*..\*]|numeric[*]|  
|numeric[*..\*][\*..\*]|numeric[*][\*]|  
|nvarchar2[*..4000]|nvarchar[*]|  
|nvarchar2[4001..*]|nvarchar(max)|  
|pls_integer|int|  
|raw[*..8000]|varbinary[*]|  
|raw[8001..*]|varbinary(max)|  
|Real|float[53]|  
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
|timestamp[*..\*]|datetime2[*]|  
|Urowid|uniqueidentifier|  
|urowid[*..\*]|uniqueidentifier|  
|varchar[*..8000]|varchar[*]|  
|varchar[8001..*]|varchar(max)|  
|varchar2[*..8000]|varchar[*]|  
|varchar2[8001..*]|varcha(max)|  
|Xmltype|xml|  
  
## <a name="see-also"></a>另请参阅  
[用户界面参考 &#40; OracleToSQL &#41;](../../ssma/oracle/user-interface-reference-oracletosql.md)  
  
