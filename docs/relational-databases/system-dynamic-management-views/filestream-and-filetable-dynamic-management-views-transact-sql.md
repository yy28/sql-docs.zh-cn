---
title: Filestream 和 FileTable 的动态管理视图 (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- FileTables [SQL Server], dynamic management views
ms.assetid: e50a135d-6644-42a4-a0df-1c7a2b722051
caps.latest.revision: 8
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 71dd6945f8452529dde925d666340bf88f4213f5
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="filestream-and-filetable-dynamic-management-views-transact-sql"></a>Filestream 和 FileTable 动态管理视图 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  本节介绍与 FILESTREAM 和 FileTable 功能相关的动态管理视图。  
  
## <a name="filestream-dynamic-management-views-and-functions"></a>Filestream 动态管理视图和函数  
 [sys.dm_filestream_file_io_handles (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-filestream-file-io-handles-transact-sql.md)  
 显示当前打开的事务性文件句柄。  
  
 [sys.dm_filestream_file_io_requests (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-filestream-file-io-requests-transact-sql.md)  
 显示当前文件输入和文件输出请求。  
  
## <a name="filetable-dynamic-management-views-and-functions"></a>FileTable 动态管理视图和函数  
 [sys.dm_filestream_non_transacted_handles (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-filestream-non-transacted-handles-transact-sql.md)  
 显示 FileTable 数据的当前打开的非事务性文件句柄。  

## <a name="see-also"></a>另请参阅
[Filestream](../../relational-databases/blob/filestream-sql-server.md)
<br>[Filetable](../../relational-databases/blob/filetables-sql-server.md)
<br>[Filestream 和 FileTable 目录视图 (Transact-SQL)](../system-catalog-views/filestream-and-filetable-catalog-views-transact-sql.md)
<br>[Filestream 和 FileTable 系统存储过程 (Transact-SQL)](../system-stored-procedures/filestream-and-filetable-system-stored-procedures.md)
  
