---
title: Filestream 和 FileTable 目录视图 (Transact SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- FileTables [SQL Server], catalog views
ms.assetid: 2c83a4a7-720b-4435-a3b5-788c29f56949
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 710ac16c93c725c17a0f8c83d15c81f2bc45a5ab
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47724935"
---
# <a name="filestream-and-filetable-catalog-views-transact-sql"></a>Filestream 和 FileTable 目录视图 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  本节介绍与 FileTable 功能相关的目录视图。  
  
## <a name="filestream-and-filetable-catalog-views-transact-sql"></a>Filestream 和 filetable 目录视图 (Transact SQL)
 [sys.database_filestream_options (Transact-SQL)](../../relational-databases/system-catalog-views/sys-database-filestream-options-transact-sql.md)  
 显示已启用的针对 FileTable 中的 FILESTREAM 数据的非事务性访问级别的相关信息。 为 SQL Server 实例中的每个数据库包含一行。  
  
 [sys.filetable_system_defined_objects (Transact-SQL)](../../relational-databases/system-catalog-views/sys-filetable-system-defined-objects-transact-sql.md)  
 显示与 FileTable 相关的系统定义对象的列表。 为每个系统定义对象包含一行。  
  
 [sys.filetables (Transact-SQL)](../../relational-databases/system-catalog-views/sys-filetables-transact-sql.md)  
 为每个 FileTable 返回一行。 继承自**sys.tables**。  

## <a name="see-also"></a>请参阅
[Filestream](../../relational-databases/blob/filestream-sql-server.md)
<br>[Filetable](../../relational-databases/blob/filetables-sql-server.md)
<br>[Filestream 和 FileTable 动态管理视图 (Transact-SQL)](../system-dynamic-management-views/filestream-and-filetable-dynamic-management-views-transact-sql.md)
<br>[Filestream 和 FileTable 系统存储过程 (Transact-SQL)](../system-stored-procedures/filestream-and-filetable-system-stored-procedures.md)
  
  
