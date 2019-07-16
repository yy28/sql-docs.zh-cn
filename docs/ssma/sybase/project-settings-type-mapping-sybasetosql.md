---
title: 项目设置 （类型映射） (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 2698fb3a-f9e6-4e04-94e0-dad289d7ed0a
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: d7b16bdf3717fa14f91af41663cbd65365eac52a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68028658"
---
# <a name="project-settings-type-mapping-sybasetosql"></a>项目设置（类型映射）(SybaseToSQL)
类型映射页**项目设置**对话框中包含自定义 SSMA 将 Sybase Adaptive Server Enterprise (ASE) 数据类型的转换设置的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据类型。  
  
类型映射页现已推出**项目设置**并**默认项目设置**对话框。  
  
-   若要指定所有将来的 SSMA 项目的类型映射设置上**工具**菜单中，选择**默认项目设置**，选择为其设置所需查看迁移的项目类型或从更改**迁移目标版本**下拉列表，然后选择**类型映射**在左窗格的底部。  
  
-   若要在指定的当前项目中，设置**工具**菜单中，选择**项目设置**，然后选择**类型映射**在左窗格的底部。  
  
## <a name="options"></a>选项  
**源类型**  
映射的 ASE 数据类型。  
  
**目标类型**  
目标[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]指定 ASE 数据类型的数据类型。  
  
请参阅以下部分的 Sybase 类型映射的默认值 SSMA 中的表。  
  
**“添加”**  
单击此项可将数据类型添加到映射列表。  
  
**编辑**  
单击可编辑所选的数据类型映射列表中。  
  
**删除**  
单击以从映射列表中删除所选的数据类型映射。  
  
重置为默认值   
单击以重置为 SSMA 默认值的类型映射列表。  
  
## <a name="default-type-mapping"></a>默认类型映射  
下表包含 ASE 之间的默认类型映射和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据类型。  
  
|ASE 数据类型|SQL Server 数据类型|  
|-----------------|------------------------|  
|**bigint**|**bigint**|  
|**binary**|**binary**|  
|**binary[\*..8000]**|**binary[\*]**|  
|**binary[8001..\*]**|**varbinary(max)**|  
|**bit**|**bit**|  
|**char**|**char**|  
|**char varying**|**varchar**|  
|**char varying [\*...8000]**|**varchar[\*]**|  
|**char varying [8001...\*]**|**varchar(max)**|  
|**char[\*..8000]**|**char[\*]**|  
|**char[8001..\*;]**|**varchar(max)**|  
|**character**|**char**|  
|**不同的字符**|**varchar**|  
|**不同的字符 [\*...8000]**|**varchar[\*]**|  
|**不同的字符 [8001...\*]**|**varchar(max)**|  
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
|**national char**|**nchar**|  
|**national char [\*...4000]**|**nchar[\*]**|  
|**national char varying**|**nvarchar**|  
|**national char varying [\*...4000]**|**nvarchar[\*]**|  
|**national char varying [4001...\*]**|**nvarchar(max)**|  
|**national char [4001...\*]**|**nvarchar(max)**|  
|**区域字符集**|**nchar**|  
|**区域字符集 [\*...4000]**|**nchar[\*]**|  
|**区域字符集 [4001...\*]**|**nvarchar(max)**|  
|**不同的区域字符集**|**nvarchar**|  
|**不同的区域字符集 [\*...4000]**|**nvarchar[\*]**|  
|**不同的区域字符集 [4001...\*]**|**nvarchar(max)**|  
|**国家/地区 varchar**|**nvarchar**|  
|**国家/地区 varchar [\*...4000]**|**nvarchar[\*]**|  
|**国家/地区 varchar [4001...\*]**|**nvarchar(max)**|  
|**nchar**|**nchar**|  
|**不同的 nchar**|**nvarchar**|  
|**不同的 nchar [\*...4000]**|**nvarchar[\*]**|  
|**nchar varying[4001..\*]**|**nvarchar(max)**|  
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
|**smallint**|**smallint**|  
|**smallmoney**|**smallmoney**|  
|**sysname**|**nvarchar[128]**|  
|**sysname[\*..\*]**|**nvarchar[255]**|  
|**text**|**text**|  
|**time**|**time[3]**|  
|**timestamp**|**rowversion**|  
|**tinyint**|**tinyint**|  
|**unichar**|**nchar**|  
|**unichar 改变**|**nvarchar**|  
|**unichar varying[\*..4000]**|**nvarchar[\*]**|  
|**unichar varying[4001..\*]**|**nvarchar(max)**|  
|**unichar[\*..4000]**|**nchar[\*]**|  
|**unichar[4001..\*]**|**nvarchar(max)**|  
|**unitext**|**nvarchar(max)**|  
|**univarchar**|**nvarchar**|  
|**univarchar[\*..4000]**|**nvarchar[\*]**|  
|**univarchar[4001..\*]**|**nvarchar(max)**|  
|**无符号的 bigint**|**numeric[20][0]**|  
|**unsigned int**|**bigint**|  
|**无符号的 smallint**|**int**|  
|**无符号的 tinyint**|**tinyint**|  
|**varbinary**|**varbinary**|  
|**varbinary[\*..8000]**|**varbinary[\*]**|  
|**varbinary[8001..\*]**|**varbinary(max)**|  
|**varchar**|**varchar**|  
|**varchar[\*..8000]**|**varchar[\*]**|  
|**varchar[8001..\*]**|**varchar(max)**|  
  
