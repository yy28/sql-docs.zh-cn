---
title: 系统external_libraries（转用-SQL） |微软文档
ms.custom: ''
ms.date: 11/04/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: machine-learning
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
ms.openlocfilehash: 6b1bfc00b403fa76f692db78593ed4c0e6b53ce8
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/04/2020
ms.locfileid: "80664434"
---
# <a name="sysexternal_libraries-transact-sql"></a>sys.external_libraries (Transact-SQL)  
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

支持管理与外部运行时（如 R、Python 和 Java）相关的包库。

> [!NOTE]
> 在 SQL Server 2017 中，支持 R 语言和 Windows 平台。 SQL Server 2019 及更高版本支持 Windows 和 Linux 平台上的 R、Python 和 Java。

## <a name="sysexternal_libraries"></a>sys.external_libraries

目录视图 sys.external_libraries列出已上载到数据库的每个外部库的行。

|列名称 |数据类型 | 说明|
|------|------|------|
|external_library_id |int | 外部库对象的 ID。 |
|name |sysname |外部库的名称。 每个所有者的数据库中是唯一的。|
|principal_id |int |拥有此外部库的委托人 ID。 |
|语言 | sysname | 支持外部库的语言或运行时的名称。 有效值为"R"、"Python"和"Java"。 将来可能会添加其他运行时。|
|scope |int |0 表示公共范围;1 表示专用范围 |  
|scope_desc |瓦尔查尔（7） |指示包是公共包还是私有包|

## <a name="see-also"></a>请参阅  

+ [sys.external_library_files](sys-external-library-files-transact-sql.md)  
+ [创建外部库](../../t-sql/statements/create-external-library-transact-sql.md)  
+ [在 SQL Server 上安装新 R 包](../../machine-learning/package-management/install-additional-r-packages-on-sql-server.md)  
+ [在 SQL Server 上安装新 Python 包](../../machine-learning/package-management/install-additional-python-packages-on-sql-server.md)  