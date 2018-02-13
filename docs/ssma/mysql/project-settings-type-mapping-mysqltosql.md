---
title: "项目设置 （类型映射） (MySQLToSQL) |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-mysql
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 136fdf6d-657f-447b-af41-49bbc6e0e93e
caps.latest.revision: 
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7ca62e82b85d401f99a6e59f6f440d9a6519e58d
ms.sourcegitcommit: f02598eb8665a9c2dc01991c36f27943701fdd2d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/13/2018
---
# <a name="project-settings-type-mapping-mysqltosql"></a>项目设置 （类型映射） (MySQLToSQL)
类型映射的项目设置，可以设置 SSMA 项目的默认类型映射。  

在项目设置和默认项目设置对话框中，类型映射将可用：  
  
-   使用项目设置对话框中设置为当前项目的配置选项。 若要访问工具菜单上的类型映射设置选择项目设置，然后单击左窗格中的类型映射。  
  
-   使用默认项目设置对话框中设置的所有项目的配置选项。 若要访问的类型映射设置，请在工具菜单中，选择默认项目设置，选择迁移项目类型的设置为需要查看 / 更改，不再是**迁移目标版本**下拉列表中，然后单击左窗格中的类型映射。  
  
## <a name="options"></a>选项  
  
##### <a name="source-type"></a>源类型  
它是 MySQL 数据类型，它已被映射到目标数据库数据类型。  
  
##### <a name="target-type"></a>目标类型  
目标数据库数据类型指定的 MySQL 数据类型。  
  
##### <a name="add"></a>“添加”  
单击此项可将数据类型添加到映射列表。  
  
##### <a name="edit"></a>编辑  
单击要编辑所选的数据类型映射列表中。  
  
##### <a name="remove"></a>删除  
单击以从映射列表中删除所选的数据类型映射。  
  
##### <a name="reset-to-default"></a>重置为默认值  
单击以将类型映射列表重置为 SSMA 默认值。  
  
## <a name="type-mappings"></a>类型映射  
下表显示源和目标数据类型之间的默认映射  
  
|||  
|-|-|  
|**MySQL 数据类型**|**SQL Server 数据类型**|  
|bigint|bigint|  
|bigint[*..255]|bigint|  
|BINARY|binary[1]|  
|binary[0..1]|binary[1]|  
|binary[2..255]|binary[*]|  
|bit|binary[1]|  
|bit[0..8]|binary[1]|  
|bit[17..24]|binary[3]|  
|bit[25..32]|binary[4]|  
|bit[33..40]|binary[5]|  
|bit[41..48]|binary[6]|  
|bit[49..56]|binary[7]|  
|bit[57..64]|binary[8]|  
|bit[9..16]|binary[2]|  
|blob|varbinary(max)|  
|blob[0..1]|varbinary[1]|  
|blob[2..8000]|varbinary[*]|  
|blob[8001..*]|varbinary(max)|  
|bool|bit|  
|boolean|bit|  
|char|nchar[1]|  
|char 字节|binary[1]|  
|char 字节 [0..1]|binary[1]|  
|char 字节 [2..255]|binary[*]|  
|char[0..1]|nchar[1]|  
|char[2..255]|nchar[*]|  
|character|nchar[1]|  
|字符不同 [0..1]|nvarchar[1]|  
|字符不同 [2..255]|nvarchar|  
|character[0..1]|nchar[1]|  
|character[2..255]|nchar[*]|  
|date|date|  
|datetime|datetime2[0]|  
|dec|decimal|  
|dec[*..65]|decimal[*][0]|  
|dec[*..65][\*..30]|decimal[*][\*]|  
|decimal|decimal|  
|decimal[*..65]|decimal[*][0]|  
|decimal[*..65][\*..30]|decimal[*][\*]|  
|double|float[53]|  
|双精度|float[53]|  
|double precision[*..255][\*..30]|numeric[*][\*]|  
|double[*..255][\*..30]|numeric[*][\*]|  
|固定|numeric|  
|fixed[*..65][\*..30]|numeric[*][\*]|  
|float|float[24]|  
|float[*..255][\*..30]|numeric[*][\*]|  
|float[*..53]|float[53]|  
|int|int|  
|int[*..255]|int|  
|integer|int|  
|integer[*..255]|int|  
|longblob|varbinary(max)|  
|长文本|nvarchar(max)|  
|mediumblob|varbinary(max)|  
|mediumint|int|  
|mediumint[*..255]|int|  
|mediumtext|nvarchar(max)|  
|国家/地区 char|nchar[1]|  
|国家/地区 char [0..1]|nchar[1]|  
|国家/地区 char [2..255]|nchar[*]|  
|国家/地区字符|nchar[1]|  
|不同的国家/地区字符|nvarchar[1]|  
|国家/地区字符不同 [0..1]|nvarchar[1]|  
|国家/地区字符不同 [2..4000]|nvarchar[*]|  
|不同的国家/地区字符 [4001..*]|nvarchar(max)|  
|国家/地区字符 [0..1]|nchar[1]|  
|国家/地区字符 [2..255]|nchar[*]|  
|国家/地区 varchar|nvarchar[1]|  
|国家/地区 varchar [0..1]|nvarchar[1]|  
|national varchar[2..4000]|nvarchar[*]|  
|national varchar[4001..*]|nvarchar(max)|  
|NCHAR|nchar[1]|  
|nchar varchar|nvarchar[1]|  
|nchar varchar [0..1]|nvarchar[1]|  
|nchar varchar[2..4000]|nvarchar[*]|  
|nchar varchar[4001..*]|nvarchar(max)|  
|nchar[0..1]|nchar[1]|  
|nchar[2..255]|nchar[*]|  
|numeric|numeric|  
|numeric[*..65]|numeric[*][0]|  
|numeric[*..65][\*..30]|numeric[*][\*]|  
|nvarchar|nvarchar[1]|  
|nvarchar[0..1]|nvarchar[1]|  
|nvarchar[2..4000]|nvarchar[*]|  
|nvarchar[4001..*]|nvarchar(max)|  
|real|float[53]|  
|real[*..255][\*..30]|numeric[*][\*]|  
|串行|bigint|  
|smallint|smallint|  
|smallint[*..255]|smallint|  
|text|nvarchar(max)|  
|text[0..1]|nvarchar[1]|  
|text[2..4000]|nvarchar[*]|  
|text[4001..*]|nvarchar(max)|  
|time|time|  
|timestamp|datetime|  
|tinyblob|varbinary[255]|  
|tinyint|smallint|  
|tinyint[*..255]|smallint|  
|tinytext|nvarchar[255]|  
|无符号的 bigint|bigint|  
|无符号的 bigint [*...255]|bigint|  
|无符号年 12 月|decimal|  
|无符号的 dec [*...65]|decimal[*][0]|  
|unsigned dec[*..65][\*..30]|decimal[*][\*]|  
|无符号的十进制数|decimal|  
|unsigned decimal[*..65]|decimal[*][0]|  
|unsigned decimal[*..65][\*..30]|decimal[*][\*]|  
|无符号的双|float[53]|  
|无符号的双精度|float[53]|  
|未签名的双精度 [*...255][\*..30]|numeric[*][\*]|  
|unsigned double[*..255][\*..30]|numeric[*][\*]|  
|未签名的固定|numeric|  
|未签名的固定 [*...65][\*..30]|numeric[*][\*]|  
|无符号的浮点|float[24]|  
|无符号的浮点型 [*...255][\*..30]|numeric[*][\*]|  
|无符号的浮点型 [*...53]|float[53]|  
|unsigned int|bigint|  
|无符号的整数 [*...255]|bigint|  
|无符号的整数|bigint|  
|无符号的整数 [*...255]|bigint|  
|无符号的 mediumint|int|  
|无符号的 mediumint [*...255]|int|  
|无符号的数字|numeric|  
|unsigned numeric[*..65]|numeric[*][0]|  
|unsigned numeric[*..65][\*..30]|numeric[*][\*]|  
|未签名的实际|float[53]|  
|unsigned real[*..255[[\*..30]|numeric[*][\*]|  
|无符号的 smallint|int|  
|unsigned smallint[*..255]|int|  
|无符号的 tinyint|tinyint|  
|无符号的 tinyint [*...255]|tinyint|  
|varbinary[0..1]|varbinary[1]|  
|varbinary[2..8000]|varbinary[*]|  
|varbinary[8001..*]|varbinary(max)|  
|varchar[0..1]|nvarchar[1]|  
|varchar[2..4000]|nvarchar[*]|  
|varchar[4001..*]|nvarchar(max)|  
|year|smallint|  
|year[2..2]|smallint|  
|year[4..4]|smallint|  
  
##### <a name="add"></a>“添加”  
单击此项可将数据类型添加到映射列表。  
  
##### <a name="edit"></a>编辑  
单击此项可编辑的映射列表中的数据类型。  
  
##### <a name="remove"></a>删除  
单击以从映射列表中删除所选的数据类型映射。  
  
##### <a name="reset-to-default"></a>重置为默认值  
单击以将所有数据类型映射重都置为 SSMA 默认值。  
  
