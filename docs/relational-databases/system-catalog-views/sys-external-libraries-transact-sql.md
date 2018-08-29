---
title: sys.external_libraries (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 10/05/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
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
author: HeidiSteen
ms.author: heidist
manager: cgronlun
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1373849201dccbb36f7096549d63864a23330f14
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43075870"
---
# <a name="sysexternallibraries-transact-sql"></a>sys.external_libraries (Transact SQL)  
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]


支持的管理包库与 R 或 Python 等外部运行时相关。

## <a name="sysexternallibraries"></a>sys.external_libraries

目录视图 sys.external_libraries 列出已上载到数据库中每个外部库的行。

|列名 |数据类型 | Description|
|------|------|------|
|external_library_id |ssNoversion | 外部库对象的 ID。 |
|NAME |sysname |外部库的名称。 数据库中是唯一的每位所有者。|
|principal_id |ssNoversion |拥有此外部库的主体的 ID。 |
|language | sysname | 支持的外部库的运行时的语言的名称。 有效值为 'R'。 可能在将来添加其他运行时。|
|作用域 |ssNoversion |0 表示公共作用域;1 表示专用作用域 |  
|scope_desc |varchar(7) |指示包是否是公共或专用|


## <a name="see-also"></a>另请参阅  
[sys.external_library_files](sys-external-library-files-transact-sql.md)  
[创建外部库](../../t-sql/statements/create-external-library-transact-sql.md)  
[SQL Server R Services 的包管理](../../advanced-analytics/r/installing-and-managing-r-packages.md)  
