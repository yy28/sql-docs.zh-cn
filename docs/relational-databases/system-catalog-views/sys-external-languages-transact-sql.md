---
description: sys. external_languages (Transact-sql) -SQL Server
title: sys. external_languages (Transact-sql) -SQL Server |Microsoft Docs
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
ms.openlocfilehash: 1f44ce24baf72b5bb93e8d649d8fa4ebed1d6e99
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88420121"
---
# <a name="sysexternal_languages-transact-sql"></a>sys. external_languages (Transact-sql) 
[!INCLUDE[SQL Server 2019](../../includes/applies-to-version/sqlserver2019.md)]

此目录视图提供数据库中的外部语言列表。 “R”和“Python”是保留名称，不能使用这些特定名称创建外部语言   。

## <a name="sysexternal_languages"></a>sys.external_languages

目录视图 external_languages sys.databases 列出了数据库中每个外部语言的行。

|列名称 |数据类型 | 说明|
|------|------|------|
|external_language_id |int | 外部语言的 ID|
|语言 |sysname |外部语言的名称。 在该数据库中是唯一的。 R 和 Python 是每个实例的保留名称|
|create_date |datetime2 |创建日期和时间|
|principal_id |int |拥有此外部库的主体的 ID|

## <a name="see-also"></a>另请参阅  

+ [sys.external_language_files](sys-external-language-files-transact-sql.md)  
+ [创建外部语言](../../t-sql/statements/create-external-language-transact-sql.md) 
