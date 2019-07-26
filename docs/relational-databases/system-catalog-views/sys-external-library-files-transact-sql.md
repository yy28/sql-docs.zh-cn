---
title: sys. external_library_files (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 07/24/2019
ms.prod: sql
ms.technology: machine-learning
ms.topic: language-reference
f1_keywords:
- external_library_files
- external_library_files_TSQL
- sys.external_library_files
- sys.external_library_files_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.external_library_files catalog view
author: dphansen
ms.author: davidph
manager: cgronlun
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d7af0a7fcb639ae3beab6216e77f9b7b95a398da
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/24/2019
ms.locfileid: "68471098"
---
# <a name="sysexternallibraryfiles-transact-sql"></a>sys. external_library_files (Transact-sql)  
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

列出组成外部库的每个文件对应一行。

|列名 |数据类型 |描述|
|------|------|-----|
|external_library_id | INT |外部库对象的 ID。 |
|content |varbinary(max) |外部库文件项目的内容。 |
|平台 |TINYINT |安装 SQL Server 的主机平台的 ID。 |
|platform_desc | nvarchar(60) |主机平台的名称。 有效值为 "WINDOWS"、"LINUX"。 |

### <a name="see-also"></a>请参阅  

[sys.external_libraries](sys-external-libraries-transact-sql.md)  
[创建外部库](../../t-sql/statements/create-external-library-transact-sql.md)  
[SQL Server 机器学习服务的包管理](../../advanced-analytics/r/installing-and-managing-r-packages.md)  
