---
title: 项目设置 （类型映射） (SybaseToSQL) |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-sybase
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 2698fb3a-f9e6-4e04-94e0-dad289d7ed0a
caps.latest.revision: 6
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: b2f515d906a827169c948f4ff2a6e6ae99000abe
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="project-settings-type-mapping-sybasetosql"></a>项目设置 （类型映射） (SybaseToSQL)
类型映射页**项目设置**对话框中包含自定义如何 SSMA 将转换到的 Sybase 自适应 Server Enterprise (ASE) 数据类型的设置[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据类型。  
  
类型映射页可用于**项目设置**和**默认项目设置**对话框。  
  
-   若要指定类型映射设置针对所有将来的 SSMA 项目，**工具**菜单上，选择**默认项目设置**，选择为其设置所需查看或更改，不再是迁移项目类型**迁移目标版本**下拉列表中，然后选择**类型映射**在左窗格的底部。  
  
-   若要对指定为当前项目中，设置**工具**菜单上，选择**项目设置**，然后选择**类型映射**在左窗格的底部。  
  
## <a name="options"></a>选项  
**源类型**  
映射的 ASE 数据类型。  
  
**目标类型**  
目标[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]指定 ASE 数据类型的数据类型。  
  
请参阅 Sybase 类型映射的默认 SSMA 下一节中的表。  
  
**“添加”**  
单击此项可将数据类型添加到映射列表。  
  
**编辑**  
单击要编辑所选的数据类型映射列表中。  
  
**删除**  
单击以从映射列表中删除所选的数据类型映射。  
  
**重置为默认值**  
单击以将类型映射列表重置为 SSMA 默认值。  
  
## <a name="default-type-mapping"></a>默认类型映射  
下表包含 ASE 之间的默认类型映射和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据类型。  
  
|ASE 数据类型|SQL Server 数据类型|  
|-----------------|------------------------|  
|**bigint**|**bigint**|  
|**binary**|**binary**|  
|**binary[\*..8000]**|**binary[\*]**|  
|**binary[8001..\*]**|**varbinary(max)**|  
|**bit**|**bit**|  
|**char**|**char**|  
|**char varying**|**varchar**|  
|**不同的 char [\*...8000]**|**varchar[\*]**|  
|**不同的 char [8001..\*]**|**varchar(max)**|  
|**char[\*..8000]**|**char[\*]**|  
|**char[8001..\*;]**|**varchar(max)**|  
|**character**|**char**|  
|**不同的字符**|**varchar**|  
|**不同的字符 [\*...8000]**|**varchar[\*]**|  
|**不同的字符 [8001..\*]**|**varchar(max)**|  
|**character[\*..8000]**|**char[\*]**|  
|**character[8001..\*]**|**varchar(max)**|  
|**date**|**date**|  
|**datetime**|**datetime2[3]**|  
|**dec**|**decimal**|  
|**dec[\*..\*]**|**decimal[\*]**|  
|**dec[\*..\*][\*..\*]**|**decimal[\*][\*]**|  
|**decimal**|**decimal**|  
|**decimal[\*..\*]**|**decimal[\*]**|  
|**decimal[\*..\*][\*..\*]**|**decimal[\*][\*]**|  
|**双精度**|**float[53]**|  
|**float**|**float[53]**|  
|**float[\*..15]**|**float[24]**|  
|**float[16..\*]**|**float[53]**|  
|**image**|**image**|  
|**int**|**int**|  
|**integer**|**int**|  
|**longsysname**|**nvarchar[255]**|  
|**money**|**money**|  
|**国家/地区 char**|**nchar**|  
|**国家/地区 char [\*...4000]**|**nchar[\*]**|  
|**不同的国家/地区 char**|**nvarchar**|  
|**不同的国家/地区 char [\*...4000]**|**nvarchar[\*]**|  
|**不同的国家/地区 char [4001..\*]**|**nvarchar(max)**|  
|**国家/地区 char [4001..\*]**|**nvarchar(max)**|  
|**国家/地区字符**|**nchar**|  
|**国家/地区字符 [\*...4000]**|**nchar[\*]**|  
|**国家/地区字符 [4001..\*]**|**nvarchar(max)**|  
|**不同的国家/地区字符**|**nvarchar**|  
|**不同的国家/地区字符 [\*...4000]**|**nvarchar[\*]**|  
|**不同的国家/地区字符 [4001..\*]**|**nvarchar(max)**|  
|**国家/地区 varchar**|**nvarchar**|  
|**国家/地区 varchar [\*...4000]**|**nvarchar[\*]**|  
|**国家/地区 varchar [4001..\*]**|**nvarchar(max)**|  
|**nchar**|**nchar**|  
|**不同的 nchar**|**nvarchar**|  
|**不同的 nchar [\*...4000]**|**nvarchar[\*]**|  
|**不同的 nchar [4001..\*]**|**nvarchar(max)**|  
|**nchar[\*..4000]**|**nchar[\*]**|  
|**nchar[4001..\*]**|**nvarchar(max)**|  
|**numeric**|**numeric**|  
|**numeric[\*..\*]**|**numeric[\*]**|  
|**numeric[\*..\*][\*..\*]**|**numeric[\*][\*]**|  
|**nvarchar**|**nvarchar**|  
|**nvarchar[\*..4000]**|**nvarchar[\*]**|  
|**nvarchar[4001..\*]**|**nvarchar(max)**|  
|**real**|**float[24]**|  
|**smalldatetime**|**smalldatetime**|  
|**int**|**int**|  
|**smallmoney**|**smallmoney**|  
|**sysname**|**nvarchar[128]**|  
|**sysname[\*..\*]**|**nvarchar[255]**|  
|**text**|**text**|  
|**time**|**time[3]**|  
|**timestamp**|**rowversion**|  
|**tinyint**|**tinyint**|  
|**unichar**|**nchar**|  
|**unichar 不同**|**nvarchar**|  
|**unichar varying[\*..4000]**|**nvarchar[\*]**|  
|**unichar 改变 [4001..\*]**|**nvarchar(max)**|  
|**unichar[\*..4000]**|**nchar[\*]**|  
|**unichar[4001..\*]**|**nvarchar(max)**|  
|**unitext**|**nvarchar(max)**|  
|**univarchar**|**nvarchar**|  
|**univarchar[\*..4000]**|**nvarchar[\*]**|  
|**univarchar[4001..\*]**|**nvarchar(max)**|  
|**无符号的 bigint**|**numeric[20][0]**|  
|**无符号的整数**|**bigint**|  
|**无符号的 smallint**|**int**|  
|**无符号的 tinyint**|**tinyint**|  
|**varbinary**|**varbinary**|  
|**varbinary[\*..8000]**|**varbinary[\*]**|  
|**varbinary[8001..\*]**|**varbinary(max)**|  
|**varchar**|**varchar**|  
|**varchar[\*..8000]**|**varchar[\*]**|  
|**varchar[8001..\*]**|**varchar(max)**|  
  
