---
title: FILESTREAM DDL、函数、存储过程和视图 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
ms.assetid: 9ecb49ee-f64e-4d30-a803-e4064a21950a
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 7ec7d554c8dedd2fb48d1af8a44dbee550e376ef
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48189847"
---
# <a name="filestream-ddl-functions-stored-procedures-and-views"></a>FILESTREAM DDL、函数、存储过程和视图
  列出用于支持 FILESTREAM 的 Transact-SQL 语句和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库对象。  
  
 有关支持 FileTable 功能的数据库对象的列表，请参阅 [FileTable DDL, Functions, Stored Procedures, and Views](../views/views.md)。  
  
##  <a name="ddl"></a> Transact-SQL 数据定义语言 (DDL) 语句  
  
-   [CREATE DATABASE (SQL Server Transact-SQL)](/sql/t-sql/statements/create-database-sql-server-transact-sql)  
  
-   [ALTER DATABASE (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql)  
  
-   [CREATE TABLE (Transact-SQL)](/sql/t-sql/statements/create-table-transact-sql)  
  
-   [ALTER TABLE (Transact-SQL)](/sql/t-sql/statements/alter-table-transact-sql)  
  
-   [CREATE INDEX (Transact-SQL)](/sql/t-sql/statements/create-index-transact-sql)  
  
-   [DROP INDEX (Transact-SQL)](/sql/t-sql/statements/drop-index-transact-sql)DROP INDEX  
  
##  <a name="func"></a> 系统函数  
  
-   [GET_FILESTREAM_TRANSACTION_CONTEXT (Transact-SQL)](/sql/t-sql/functions/get-filestream-transaction-context-transact-sql)  
  
-   [PathName (Transact-SQL)](/sql/relational-databases/system-functions/pathname-transact-sql)  
  
##  <a name="proc"></a> 系统存储过程  
  
-   [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
-   [sp_filestream_force_garbage_collection (Transact-SQL)](/sql/relational-databases/system-stored-procedures/filestream-and-filetable-sp-filestream-force-garbage-collection)  
  
##  <a name="cat"></a> 系统视图 – 目录视图  
  
-   [sys.database_filestream_options (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-database-filestream-options-transact-sql)  
  
##  <a name="dmv"></a> 系统视图 – 动态管理视图  
  
-   [sys.dm_filestream_file_io_handles (Transact-SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-filestream-file-io-handles-transact-sql)  
  
-   [sys.dm_filestream_file_io_requests (Transact-SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-filestream-file-io-requests-transact-sql)  
  
##  <a name="api"></a> 编程 API  
  
-   [使用 OpenSqlFilestream 访问 FILESTREAM 数据](access-filestream-data-with-opensqlfilestream.md)  
  
-   [托管 API - SqlFileStream 类](http://go.microsoft.com/fwlink/?LinkId=220875)  
  
  
