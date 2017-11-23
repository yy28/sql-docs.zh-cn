---
title: "sys.external_library_files (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 10/05/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- external_library_files
- external_library_files_TSQL
- sys.external_library_files
- sys.external_library_files_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.external_library_files catalog view
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.openlocfilehash: a3196218bbb886544a77c2fd1184c806591b16e6
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="sysexternallibraryfiles-transact-sql"></a>sys.external_library_files (TRANSACT-SQL)  
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

列出每个文件组成外部库一行。

|列名 |数据类型 |Description|
|------|------|-----|
|external_library_id | int |外部库对象的 ID。 |
|content |varbinary(max) |外部库文件项目的内容。 |
|平台 |tinyint |在其上安装 SQL Server 的主机平台的 ID。 |
|platform_desc | nvarchar(60) |主机平台的名称。 有效值为 WINDOWS、 LINUX。 |

### <a name="see-also"></a>另请参阅  

[sys.external_libraries](sys-external-libraries-transact-sql.md)  
[创建外部库](../../t-sql/statements/create-external-library-transact-sql.md)  
[SQL Server 机器学习服务管理包](../../advanced-analytics/r/installing-and-managing-r-packages.md)  
