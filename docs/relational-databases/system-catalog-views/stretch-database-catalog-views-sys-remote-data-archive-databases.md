---
title: sys. remote_data_archive_databases （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.technology: stored-procedures
ms.topic: language-reference
f1_keywords:
- sys.remote_data_archive_databases
- sys.remote_data_archive_databases_TSQL
- remote_data_archive_databases
- remote_data_archive_databases_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.remote_data_archive_databases catalog view
ms.assetid: 25bffb0c-9821-40b4-88cf-75f854891a09
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
ms.openlocfilehash: a4d7717a6e89b156cd66ea96a44383d28cbecfb3
ms.sourcegitcommit: 703968b86a111111a82ef66bb7467dbf68126051
ms.contentlocale: zh-CN
ms.lasthandoff: 07/07/2020
ms.locfileid: "86053627"
---
# <a name="stretch-database-catalog-views---sysremote_data_archive_databases"></a>Stretch Database 目录视图-sys. remote_data_archive_databases
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  每个从已启用延伸的本地数据库中存储数据的远程数据库占一行。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**remote_database_id**|**int**|自动生成的远程数据库本地标识符。|  
|**remote_database_name**|**sysname**|远程数据库的名称。|  
|data_source_id|**int**|用于连接到远程服务器的数据源|  
  
## <a name="see-also"></a>另请参阅  
 [Stretch 数据库](../../sql-server/stretch-database/stretch-database.md)  
  
  
