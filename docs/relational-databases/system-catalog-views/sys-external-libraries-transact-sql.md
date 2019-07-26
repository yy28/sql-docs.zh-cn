---
title: sys. external_libraries (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 07/24/2019
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
ms.openlocfilehash: 78923a0eb1404c1437c6e1144888261e542ebc5a
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/24/2019
ms.locfileid: "68471103"
---
# <a name="sysexternallibraries-transact-sql"></a>sys. external_libraries (Transact-sql)  
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

支持管理与外部运行时 (如 R、Python 和 Java) 相关的包库。

> [!NOTE]
> 在 SQL Server 2017 中，支持 R 语言和 Windows 平台。 SQL Server 2019 CTP 2.4 中支持 Windows 和 Linux 平台上的 R、Python 和 Java。

## <a name="sysexternallibraries"></a>sys.external_libraries

目录视图 external_libraries 将为已上传到数据库的每个外部库列出一行。

|列名 |数据类型 | 描述|
|------|------|------|
|external_library_id |INT | 外部库对象的 ID。 |
|name |sysname |外部库的名称。 在数据库中每个所有者都是唯一的。|
|principal_id |INT |拥有此外部库的主体的 ID。 |
|language | sysname | 支持外部库的语言或运行时的名称。 有效值为 "R"、"Python" 和 "Java"。 将来可能会添加其他运行时。|
|作用域 |INT |0表示公共作用域;1用于专用范围 |  
|scope_desc |varchar (7) |指示包是公共包还是私有包|

## <a name="see-also"></a>请参阅  

+ [sys.external_library_files](sys-external-library-files-transact-sql.md)  
+ [创建外部库](../../t-sql/statements/create-external-library-transact-sql.md)  
+ [在 SQL Server 上安装新 R 包](../../advanced-analytics/r/install-additional-r-packages-on-sql-server.md)  
+ [在 SQL Server 上安装新 Python 包](../../advanced-analytics/python/install-additional-python-packages-on-sql-server.md)  