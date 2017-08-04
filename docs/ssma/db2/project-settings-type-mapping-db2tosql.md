---
title: "项目设置 （类型映射） (DB2ToSQL) |Microsoft 文档"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: cf426c69-6a8e-4d19-951d-6661d5ae2562
caps.latest.revision: 5
author: sabotta
ms.author: carlasab
manager: lonnyb
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 0b9bc26477c4b43e47588280e2cce74096b810c5
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

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
|bfile|varbinary(max)|  
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
|date|datetime2 [0]|  
|dec|dec [38] [0]|  
|decimal|float [53]|  
|双精度|float [53]|  
|float|float [53]|  
|int|int|  
|integer|int|  
|long|varchar(max)|  
|长时间原始|varbinary(max)|  
|长时间原始 [\*...8000]<sup>*</sup>|varbinary [*]|  
|长时间原始 [8001..\*]<sup>*</sup>|varbinary(max)|  
|国家/地区 char|nvarchar(max)|  
|不同的国家/地区 char|nvarchar(max)|  
|国家/地区字符|nvarchar(max)|  
|不同的国家/地区字符<sup>**</sup>|nvarchar(max)|  
|不同的国家/地区字符<sup>*</sup>|nvarchar(max)|  
|nchar|nvarchar(max)|  
|nclob|nvarchar(max)|  
|number|float [53]|  
|numeric|float [53]|  
|nvarchar2|nvarchar(max)|  
|pls_integer|int|  
|raw|varbinary(max)|  
|real|float [53]|  
|rowid|uniqueidentifier|  
|signtype|smallint|  
|smallint|smallint|  
|string|varchar(max)|  
|timestamp|datetime2|  
|与本地时区的时间戳|datetimeoffset|  
|时区的时间戳|datetimeoffset|  
|urowid|uniqueidentifier|  
|varchar|varchar(max)|  
|varchar2|varchar(max)|  
|xml 类型|xml|  
  
<sup>*</sup>适用于返回值类型映射仅。  
  
<sup>**</sup>适用于自变量类型映射仅。  
  
### <a name="default-column-type-mapping"></a>默认列类型映射  
下表包含列的默认类型映射。  
  
|DB2 数据类型|默认[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据类型|  
|-----------------|-------------------------------------------------------------------------|  
|bfile|varbinary(max)|  
|binary_double|float [53]|  
|binary_float|float [53]|  
|blob|varbinary(max)|  
|char|char|  
|不同的 char [*...\*]|varchar [*]|  
|char [*...\*]|char [*]|  
|character|char|  
|不同的字符 [*...\*]|varchar [*]|  
|字符 [*...\*]|char [*]|  
|Clob|varchar(max)|  
|date|datetime2 [0]|  
|dec|dec [38] [0]|  
|dec [*...\*]|dec [*] [0]|  
|dec [*...\*][\*..\*]|dec[*][\*]|  
|decimal|小数 [38] [0]|  
|十进制 [*...\*]|小数 [*] [0]|  
|十进制 [*...\*][\*..\*]|小数 [*] [\*]|  
|双精度|float [53]|  
|float|float [53]|  
|float [*...53]|float [*]|  
|float [54..*]|float [53]|  
|int|int|  
|integer|int|  
|long|varchar(max)|  
|长时间原始|varbinary(max)|  
|长时间原始 [*...8000]|varbinary [*]|  
|长时间原始 [8001..*]|varbinary(max)|  
|long varchar|varchar(max)|  
|长 [*...8000]|varchar [*]|  
|长 [8001..*]|varchar(max)|  
|国家/地区 char|nchar|  
|不同的国家/地区 char [*...\*]|nvarchar [*]|  
|国家/地区 char [*...\*]|nchar [*]|  
|国家/地区字符|nchar|  
|不同的国家/地区字符 [*...\*]|nvarchar [*]|  
|国家/地区字符 [*...\*]|nchar [*]|  
|nchar|nchar|  
|nchar [*]|nchar [*]|  
|nclob|nvarchar(max)|  
|number|float [53]|  
|数字 [*...\*]|数字 [*]|  
|数字 [*...\*][\*..\*]|数字 [*] [\*]|  
|numeric|numeric|  
|数字 [*...\*]|数字 [*]|  
|数字 [*...\*][\*..\*]|数字 [*] [\*]|  
|nvarchar2 [*...\*]|nvarchar [*]|  
|原始 [*...\*]|varbinary [*]|  
|real|float [53]|  
|rowid|uniqueidentifier|  
|smallint|smallint|  
|timestamp|datetime2|  
|与本地时区的时间戳|datetimeoffset|  
|与本地时区的时间戳 [*...\*]|datetimeoffset [*]|  
|时区的时间戳|datetimeoffset|  
|时区的时间戳 [*...\*]|datetimeoffset [*]|  
|时间戳 [*...\*]|datetime2 [*]|  
|Urowid|uniqueidentifier|  
|urowid [*...\*]|uniqueidentifier|  
|varchar [*...\*]|varchar [*]|  
|varchar2 [*...\*]|varchar [*]|  
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
|不同的 char [*...8000]|varchar [*]|  
|不同的 char [8001..*]|varchar(max)|  
|char [*...8000]|char [*]|  
|char [8001..*]|varchar(max)|  
|字符|char|  
|不同的字符 [*...8000]|varchar [*]|  
|不同的字符 [8001..*]|varchar(max)|  
|字符 [*...8000]|char [*]|  
|字符 [8001..*]|varchar(max)|  
|Clob|varchar(max)|  
|date|datetime2 [0]|  
|dec|dec [38] [0]|  
|dec [*...\*]|dec [*] [0]|  
|dec [*...\*][\*..\*]|dec[*][\*]|  
|decimal|小数 [38] [0]|  
|十进制 [*...\*]|小数 [*] [0]|  
|十进制 [*...\*][\*..\*]|小数 [*] [\*]|  
|双精度|float [53]|  
|Float|float [53]|  
|float [*...53]|float [*]|  
|float [54..*]|float [53]|  
|int|int|  
|Integer|int|  
|整数 [*...\*]|数字 [*] [0]|  
|Long|varchar(max)|  
|长时间原始|varbinary(max)|  
|长时间原始 [*...8000]|varbinary [*]|  
|长时间原始 [8001..*]|varbinary(max)|  
|国家/地区 char|nchar|  
|不同的国家/地区 char [*...4000]|nvarchar [*]|  
|不同的国家/地区 char [4001..*]|nvarchar(max)|  
|国家/地区 char [*...4000]|nchar [*]|  
|国家/地区 char [4001..*]|nvarchar(max)|  
|国家/地区字符|nchar|  
|国家/地区字符 [*...4000]|nvarchar [*]|  
|国家/地区字符 [4001..*]|nvarchar(max)|  
|不同的国家/地区字符 [*...4000]|nvarchar [*]|  
|不同的国家/地区字符 [4001..*]|nvarchar(max)|  
|Nchar|nchar|  
|nchar [*...4000]|nchar [*]|  
|nchar [4001..*]|nvarchar(max)|  
|不同的 nchar [*...4000]|nvarchar [*]|  
|不同的 nchar [4001..*]|nvarchar(max)|  
|Nclob|nvarchar(max)|  
|Number|float [53]|  
|数字 [*...\*]|数字 [*]|  
|数字 [*...\*][\*..\*]|数字 [*] [\*]|  
|数字|数字 [38] [0]|  
|数字 [*...\*]|数字 [*]|  
|数字 [*...\*][\*..\*]|数字 [*] [\*]|  
|nvarchar2 [*...4000]|nvarchar [*]|  
|nvarchar2 [4001..*]|nvarchar(max)|  
|pls_integer|int|  
|原始 [*...8000]|varbinary [*]|  
|原始 [8001..*]|varbinary(max)|  
|Real|float [53]|  
|Rowid|uniqueidentifier|  
|Signtype|smallint|  
|Smallint|smallint|  
|字符串 [*...8000]|varchar [*]|  
|字符串 [8001..*]|varchar(max)|  
|timestamp|datetime2|  
|与本地时区的时间戳|datetimeoffset|  
|时区的时间戳|datetimeoffset|  
|与本地时区的时间戳 [*...\*]|datetimeoffset [*]|  
|时区的时间戳 [*...\*]|datetimeoffset [*]|  
|时间戳 [*...\*]|datetime2 [*]|  
|Urowid|uniqueidentifier|  
|urowid [*...\*]|uniqueidentifier|  
|varchar [*...8000]|varchar [*]|  
|varchar [8001..*]|varchar(max)|  
|varchar2 [*...8000]|varchar [*]|  
|varchar2 [8001..*]|varcha(max)|  
|Xml 类型|xml|  
  
## <a name="see-also"></a>另請參閱  
[用户界面参考 &#40; DB2ToSQL &#41;](../../ssma/db2/user-interface-reference-db2tosql.md)  
  

