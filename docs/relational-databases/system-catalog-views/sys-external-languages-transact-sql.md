---
title: sys.external_languages (Transact SQL)-SQL Server |Microsoft Docs
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
ms.openlocfilehash: 1cef52f066a07032240d17f88297b02ba3f7e5fb
ms.sourcegitcommit: be09f0f3708f2e8eb9f6f44e632162709b4daff6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/21/2019
ms.locfileid: "65995115"
---
# <a name="sysexternallanguages-transact-sql"></a>sys.external_languages (Transact-SQL)
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

此目录视图提供了一系列数据库中的外部语言。 **R**并**Python**是保留的名称，没有外部语言可以创建具有这些特定的名称。

## <a name="sysexternallanguages"></a>sys.external_languages

目录视图 sys.external_languages 列出了每个数据库中的外部语言对应的行。

|列名 |数据类型 | Description|
|------|------|------|
|external_language_id |ssNoversion | 外部语言 ID|
|language |sysname |外部语言的名称。 在该数据库中是唯一的。 R 和 Python 是每个实例的保留的名称|
|create_date |datetime2 |创建日期和时间|
|principal_id |ssNoversion |拥有此外部库的主体 ID|

## <a name="see-also"></a>另请参阅  

+ [sys.external_language_files](sys-external-language-files-transact-sql.md)  
+ [CREATE EXTERNAL LANGUAGE](../../t-sql/statements/create-external-language-transact-sql.md) 
