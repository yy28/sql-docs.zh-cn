---
description: FileTable DDL、函数、存储过程和视图
title: FileTable 函数、存储过程、视图 | Microsoft Docs
descriptions: Learn which Transact-SQL statements and which SQL Server functions, stored procedures, and views have been added or changed to support the FileTable feature.
ms.custom: seo-lt-2019
ms.date: 12/13/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FileTables [SQL Server], database objects
ms.assetid: 7e2e0f7f-94a8-4178-8bc7-d2e14ac8528c
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 41ffb4997f4c0680eac62f2b55630b9651cfe70d
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/07/2020
ms.locfileid: "91809930"
---
# <a name="filetable-ddl-functions-stored-procedures-and-views"></a>FileTable DDL、函数、存储过程和视图

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  列出用于在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中支持 FileTable 功能的新增或更改的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 语句和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库对象。  
  
 下表中的“状态”列指示此项是 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]的新增功能，还是在早期版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中已存在但在 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 中已更改用于支持语义搜索。  
  
 有关支持 FILESTREAM 的语句和数据库对象的列表，请参阅 [FILESTREAM DDL, Functions, Stored Procedures, and Views](../../relational-databases/blob/filestream-ddl-functions-stored-procedures-and-views.md)。  
  
##  <a name="transact-sql-data-definition-language-ddl-statements"></a><a name="ddl"></a> Transact-SQL 数据定义语言 (DDL) 语句  
  
|Object|状态|更多信息|  
|------------|------------|----------------------|  
|[ALTER DATABASE (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql.md)<br /><br /> [ALTER DATABASE SET 选项 (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-set-options.md)|已更改|[启用 FileTable 的先决条件](../../relational-databases/blob/enable-the-prerequisites-for-filetable.md)<br /><br /> [管理 FileTable](../../relational-databases/blob/manage-filetables.md)|  
|[ALTER TABLE (Transact-SQL)](../../t-sql/statements/alter-table-transact-sql.md)|已更改|[创建、更改和删除 FileTable](../../relational-databases/blob/create-alter-and-drop-filetables.md)<br /><br /> [管理 FileTable](../../relational-databases/blob/manage-filetables.md)|  
|[CREATE DATABASE (SQL Server Transact-SQL)](../../t-sql/statements/create-database-transact-sql.md)|已更改|[启用 FileTable 的先决条件](../../relational-databases/blob/enable-the-prerequisites-for-filetable.md)|  
|[CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md)|已更改|[创建、更改和删除 FileTable](../../relational-databases/blob/create-alter-and-drop-filetables.md)|  
|[RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)<br /><br /> [RESTORE 参数 (Transact-SQL)](../../t-sql/statements/restore-statements-arguments-transact-sql.md)|已更改||  
  
##  <a name="functions"></a><a name="func"></a> 函数  
  
|Object|状态|更多信息|  
|------------|------------|----------------------|  
|[FileTableRootPath (Transact-SQL)](../../relational-databases/system-functions/filetablerootpath-transact-sql.md)|**已添加**|[在 FileTable 中使用目录和路径](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)|  
|[GetFileNamespacePath (Transact-SQL)](../../relational-databases/system-functions/getfilenamespacepath-transact-sql.md)|**已添加**|[在 FileTable 中使用目录和路径](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)|  
|[GetPathLocator (Transact-SQL)](../../relational-databases/system-functions/getpathlocator-transact-sql.md)|**已添加**|[在 FileTable 中使用目录和路径](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)|  
  
##  <a name="stored-procedures"></a><a name="sproc"></a> 存储过程  
  
|Object|状态|更多信息|  
|------------|------------|----------------------|  
|[sp_kill_filestream_non_transacted_handles (Transact-SQL)](../../relational-databases/system-stored-procedures/filestream-and-filetable-sp-kill-filestream-non-transacted-handles.md)|**已添加**|[管理 FileTable](../../relational-databases/blob/manage-filetables.md)|  
  
##  <a name="catalog-views"></a><a name="cv"></a> 目录视图  
  
|Object|状态|更多信息|  
|------------|------------|----------------------|  
|[sys.database_filestream_options (Transact-SQL)](../../relational-databases/system-catalog-views/sys-database-filestream-options-transact-sql.md)|**已添加**|[启用 FileTable 的先决条件](../../relational-databases/blob/enable-the-prerequisites-for-filetable.md)|  
|[sys.filetable_system_defined_objects (Transact-SQL)](../../relational-databases/system-catalog-views/sys-filetable-system-defined-objects-transact-sql.md)|**已添加**|[创建、更改和删除 FileTable](../../relational-databases/blob/create-alter-and-drop-filetables.md)<br /><br /> [管理 FileTable](../../relational-databases/blob/manage-filetables.md)|  
|[sys.filetables (Transact-SQL)](../../relational-databases/system-catalog-views/sys-filetables-transact-sql.md)|**已添加**|[管理 FileTable](../../relational-databases/blob/manage-filetables.md)|  
|[sys.tables (Transact-SQL)](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md)|已更改|[管理 FileTable](../../relational-databases/blob/manage-filetables.md)|  
  
##  <a name="dynamic-management-views"></a><a name="dmv"></a> 动态管理视图  
  
|Object|状态|更多信息|  
|------------|------------|----------------------|  
|[sys.dm_filestream_non_transacted_handles (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-filestream-non-transacted-handles-transact-sql.md)|**已添加**|[管理 FileTable](../../relational-databases/blob/manage-filetables.md)|  
  
## <a name="see-also"></a>另请参阅  
 [管理 FileTable](../../relational-databases/blob/manage-filetables.md)  
  
