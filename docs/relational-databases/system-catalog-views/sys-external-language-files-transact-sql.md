---
title: sys.external_language_files (Transact SQL)-SQL Server |Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.reviewer: dphansen
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
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 0d1325311ef0b708f5a3abd5f4494e099863efc2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "65995085"
---
# <a name="sysexternallanguagefiles-transact-sql"></a>sys.external_language_files (Transact SQL)
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

此目录视图提供了一系列数据库中的外部语言扩展文件。 “R”和“Python”是保留名称，不能使用这些特定名称创建外部语言   。

从 file_spec 创建外部语言后，在此视图中列出扩展本身和它的属性。 此视图将包含每种语言，每个 OS 的一个条目。

## <a name="sysexternallanguages"></a>sys.external_languages

目录视图 sys.external_language_files 列出了在数据库中每个外部语言扩展的行。 Parameters

|列名 |数据类型 | Description|
|------|------|------|
|external_language_id |ssNoversion | 外部语言 ID|
|content|varbinary(max) |外部语言扩展文件的内容|
|file_name|nvarchar(266)|语言扩展文件的名称|
|平台|TINYINT|安装 SQL Server 的主机平台的 ID|
|platform_desc |nvarchar(60)|主机平台的名称。 有效值为 WINDOWS、 LINUX。|
|参数|nvarchar(4000)|外部语言 prameters|
|environment_variables |nvarchar(4000)|外部语言环境变量|

## <a name="see-also"></a>另请参阅  

+ [sys.external_languages](sys-external-languages-transact-sql.md)  
+ [CREATE EXTERNAL LANGUAGE](../../t-sql/statements/create-external-language-transact-sql.md)  
