---
title: "FileTable DDL、函数、存储过程和视图 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: blob
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-blob
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: FileTables [SQL Server], database objects
ms.assetid: 7e2e0f7f-94a8-4178-8bc7-d2e14ac8528c
caps.latest.revision: "13"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 10e3fa99c03e3b01c512f78e1d14998dd9094b9b
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="filetable-ddl-functions-stored-procedures-and-views"></a>FileTable DDL、函数、存储过程和视图
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]列出用于在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中支持 FileTable 功能的新增或更改的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库对象。  
  
 下表中的“状态”列指示此项是 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]的新增功能，还是在早期版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中已存在但在 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 中已更改用于支持语义搜索。  
  
 有关支持 FILESTREAM 的语句和数据库对象的列表，请参阅 [FILESTREAM DDL, Functions, Stored Procedures, and Views](../../relational-databases/blob/filestream-ddl-functions-stored-procedures-and-views.md)。  
  
##  <a name="ddl"></a> Transact-SQL 数据定义语言 (DDL) 语句  
  
|对象|状态|详细信息|  
|------------|------------|----------------------|  
|[ALTER DATABASE (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql.md)<br /><br /> [ALTER DATABASE SET 选项 (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-set-options.md)|已更改|[启用 FileTable 的先决条件](../../relational-databases/blob/enable-the-prerequisites-for-filetable.md)<br /><br /> [管理 FileTable](../../relational-databases/blob/manage-filetables.md)|  
|[ALTER TABLE (Transact-SQL)](../../t-sql/statements/alter-table-transact-sql.md)|已更改|[创建、更改和删除 FileTable](../../relational-databases/blob/create-alter-and-drop-filetables.md)<br /><br /> [管理 FileTable](../../relational-databases/blob/manage-filetables.md)|  
|[CREATE DATABASE (SQL Server Transact-SQL)](../../t-sql/statements/create-database-sql-server-transact-sql.md)|已更改|[启用 FileTable 的先决条件](../../relational-databases/blob/enable-the-prerequisites-for-filetable.md)|  
|[CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md)|已更改|[创建、更改和删除 FileTable](../../relational-databases/blob/create-alter-and-drop-filetables.md)|  
|[RESTORE (Transact-SQL)](../../t-sql/statements/restore-statements-transact-sql.md)<br /><br /> [RESTORE 参数 (Transact-SQL)](../../t-sql/statements/restore-statements-arguments-transact-sql.md)|已更改||  
  
##  <a name="func"></a> 函数  
  
|对象|状态|详细信息|  
|------------|------------|----------------------|  
|[FileTableRootPath (Transact-SQL)](../../relational-databases/system-functions/filetablerootpath-transact-sql.md)|**已添加**|[在 FileTable 中使用目录和路径](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)|  
|[GetFileNamespacePath (Transact-SQL)](../../relational-databases/system-functions/getfilenamespacepath-transact-sql.md)|**已添加**|[在 FileTable 中使用目录和路径](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)|  
|[GetPathLocator (Transact-SQL)](../../relational-databases/system-functions/getpathlocator-transact-sql.md)|**已添加**|[在 FileTable 中使用目录和路径](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)|  
  
##  <a name="sproc"></a> 存储过程  
  
|对象|状态|详细信息|  
|------------|------------|----------------------|  
|[sp_kill_filestream_non_transacted_handles (Transact-SQL)](../../relational-databases/system-stored-procedures/filestream-and-filetable-sp-kill-filestream-non-transacted-handles.md)|**已添加**|[管理 FileTable](../../relational-databases/blob/manage-filetables.md)|  
  
##  <a name="cv"></a> 目录视图  
  
|对象|状态|详细信息|  
|------------|------------|----------------------|  
|[sys.database_filestream_options (Transact-SQL)](../../relational-databases/system-catalog-views/sys-database-filestream-options-transact-sql.md)|**已添加**|[启用 FileTable 的先决条件](../../relational-databases/blob/enable-the-prerequisites-for-filetable.md)|  
|[sys.filetable_system_defined_objects (Transact-SQL)](../../relational-databases/system-catalog-views/sys-filetable-system-defined-objects-transact-sql.md)|**已添加**|[创建、更改和删除 FileTable](../../relational-databases/blob/create-alter-and-drop-filetables.md)<br /><br /> [管理 FileTable](../../relational-databases/blob/manage-filetables.md)|  
|[sys.filetables (Transact-SQL)](../../relational-databases/system-catalog-views/sys-filetables-transact-sql.md)|**已添加**|[管理 FileTable](../../relational-databases/blob/manage-filetables.md)|  
|[sys.tables (Transact-SQL)](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md)|已更改|[管理 FileTable](../../relational-databases/blob/manage-filetables.md)|  
  
##  <a name="dmv"></a> 动态管理视图  
  
|对象|状态|详细信息|  
|------------|------------|----------------------|  
|[sys.dm_filestream_non_transacted_handles (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-filestream-non-transacted-handles-transact-sql.md)|**已添加**|[管理 FileTable](../../relational-databases/blob/manage-filetables.md)|  
  
## <a name="see-also"></a>另请参阅  
 [管理 FileTable](../../relational-databases/blob/manage-filetables.md)  
  
  
