---
title: sys. external_libraries （Transact-sql） |Microsoft Docs
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
ms.openlocfilehash: ac6ad0872e813d36d9884a00f979b2a5284cd4a3
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/04/2019
ms.locfileid: "73536162"
---
# <a name="sysexternal_libraries-transact-sql"></a>sys. external_libraries （Transact-sql）  
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

支持管理与外部运行时（如 R、Python 和 Java）相关的包库。

> [!NOTE]
> 在 SQL Server 2017 中，支持 R 语言和 Windows 平台。 Windows 和 Linux 平台上的 R、Python 和 Java 在 SQL Server 2019 及更高版本中受支持。

## <a name="sysexternal_libraries"></a>sys.external_libraries

目录视图 external_libraries 将为已上传到数据库的每个外部库列出一行。

|列名 |数据类型 | 说明|
|------|------|------|
|external_library_id |int | 外部库对象的 ID。 |
|name |sysname |外部库的名称。 在数据库中每个所有者都是唯一的。|
|principal_id |int |拥有此外部库的主体的 ID。 |
|language | sysname | 支持外部库的语言或运行时的名称。 有效值为 "R"、"Python" 和 "Java"。 将来可能会添加其他运行时。|
|作用域 |int |0表示公共作用域;1用于专用范围 |  
|scope_desc |varchar （7） |指示包是公共包还是私有包|

## <a name="see-also"></a>另请参阅  

+ [sys.external_library_files](sys-external-library-files-transact-sql.md)  
+ [创建外部库](../../t-sql/statements/create-external-library-transact-sql.md)  
+ [在 SQL Server 上安装新 R 包](../../advanced-analytics/r/install-additional-r-packages-on-sql-server.md)  
+ [在 SQL Server 上安装新 Python 包](../../advanced-analytics/python/install-additional-python-packages-on-sql-server.md)  