---
title: sys.external_libraries (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/27/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- external_libraries
- external_libraries_TSQL
- sys.external_libraries
- sys.external_libraries_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.external_libraries catalog view
author: dphansen
ms.author: davidph
manager: cgronlun
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d56d0c69b9e3bae87dda9b55d241a1c040210ca9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62637466"
---
# <a name="sysexternallibraries-transact-sql"></a>sys.external_libraries (Transact-SQL)  
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

支持管理的外部运行时，如 R、 Python 和 Java 与相关的包库。

> [!NOTE]
> 在 SQL Server 2017 中，支持 R 语言和 Windows 平台。 SQL Server 2019 CTP 2.4 中支持 Windows 和 Linux 平台上的 R、Python 和 Java。

## <a name="sysexternallibraries"></a>sys.external_libraries

目录视图 sys.external_libraries 列出已上载到数据库中每个外部库的行。

|列名 |数据类型 | Description|
|------|------|------|
|external_library_id |ssNoversion | 外部库对象的 ID。 |
|name |sysname |外部库的名称。 数据库中是唯一的每位所有者。|
|principal_id |ssNoversion |拥有此外部库的主体的 ID。 |
|language | sysname | 支持的外部库的运行时的语言的名称。 有效值为 R、 Python 和 Java。 可能在将来添加其他运行时。|
|作用域 |ssNoversion |0 表示公共作用域;1 表示专用作用域 |  
|scope_desc |varchar(7) |指示包是否是公共或专用|

## <a name="see-also"></a>另请参阅  

+ [sys.external_library_files](sys-external-library-files-transact-sql.md)  
+ [CREATE EXTERNAL LIBRARY](../../t-sql/statements/create-external-library-transact-sql.md)  
+ [在 SQL Server 上安装新 R 包](../../advanced-analytics/r/install-additional-r-packages-on-sql-server.md)  
+ [在 SQL Server 上安装新 Python 包](../../advanced-analytics/python/install-additional-python-packages-on-sql-server.md)  