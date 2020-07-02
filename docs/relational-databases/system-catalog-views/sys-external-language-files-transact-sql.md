---
title: sys. external_language_files （Transact-sql）-SQL Server |Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- external_languages
- external_languages_TSQL
- sys.external_languages
- sys.external_languages_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.external_languages catalog view
author: nelgson
ms.author: negust
ms.reviewer: dphansen
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: e90925354a9a48d3a2b0ff8e789d940ece6cb476
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85751738"
---
# <a name="sysexternal_language_files-transact-sql"></a>sys. external_language_files （Transact-sql）
[!INCLUDE[SQL Server 2019](../../includes/applies-to-version/sqlserver2019.md)]

此目录视图提供数据库中的外部语言扩展文件的列表。 “R”和“Python”是保留名称，不能使用这些特定名称创建外部语言   。

从 file_spec 创建外部语言时，此视图中列出了该扩展本身及其属性。 此视图将包含每个语言每个操作系统一个条目。

## <a name="sysexternal_languages"></a>sys.external_languages

目录视图 sys.databases 列出了数据库中每个外部语言扩展的行 external_language_files。 参数

|列名称 |数据类型 | 说明|
|------|------|------|
|external_language_id |int | 外部语言的 ID|
|内容|varbinary(max) |外部语言扩展文件的内容|
|file_name|nvarchar （有）|语言扩展文件的名称|
|平台|tinyint|安装 SQL Server 的主机平台的 ID|
|platform_desc |nvarchar(60)|主机平台的名称。 有效值为 "WINDOWS"、"LINUX"。|
|parameters|nvarchar(4000)|外部语言 prameters|
|environment_variables |nvarchar(4000)|外部语言环境变量|

## <a name="see-also"></a>请参阅  

+ [sys.external_languages](sys-external-languages-transact-sql.md)  
+ [创建外部语言](../../t-sql/statements/create-external-language-transact-sql.md)  
