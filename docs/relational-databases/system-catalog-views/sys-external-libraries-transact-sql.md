---
title: sys.external_libraries (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 10/05/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
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
author: jeannt
ms.author: jeannt
manager: craigg
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: d8fa8a4d41cff452379c420b712f13b2d4415a74
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="sysexternallibraries-transact-sql"></a>sys.external_libraries (TRANSACT-SQL)  
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]


支持的管理包库与诸如 R 或 Python 等的外部运行时相关。

## <a name="sysexternallibraries"></a>sys.external_libraries

目录视图 sys.external_libraries 列出每个外部库已上载到数据库的行。

|列名 |数据类型 | Description|
|------|------|------|
|external_library_id |int | 外部库对象的 ID。 |
|name |sysname |外部库的名称。 在中是唯一的每位所有者的数据库。|
|principal_id |int |拥有此外部库的主体 ID。 |
|language | sysname | 支持外部库的运行时的语言的名称。 有效值为 'R'。 可能在将来添加其他运行时。|
|作用域 |int |公共作用域; 的 0私有的作用域的 1 |  
|scope_desc |varchar(7) |指示包是否为公用或专用|


## <a name="see-also"></a>另请参阅  
[sys.external_library_files](sys-external-library-files-transact-sql.md)  
[创建外部库](../../t-sql/statements/create-external-library-transact-sql.md)  
[SQL Server R Services 的包管理](../../advanced-analytics/r/installing-and-managing-r-packages.md)  
