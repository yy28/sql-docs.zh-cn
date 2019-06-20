---
title: 避免与 FILESTREAM 应用程序中的数据库操作冲突 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.technology: filestream
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server], Win32 and Transact-SQL Conflicts
ms.assetid: 8b1ee196-69af-4f9b-9bf5-63d8ac2bc39b
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: fafb116e1e5c02d27ad3242edd27064ffae6e401
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66010371"
---
# <a name="avoid-conflicts-with-database-operations-in-filestream-applications"></a>避免与 FILESTREAM 应用程序中的数据库操作冲突
  使用 SqlOpenFilestream() 打开 Win32 文件句柄以读取或写入 FILESTREAM BLOB 数据的应用程序可能会遇到与在通用事务中管理的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句的冲突错误。 这包括花很长时间才能完成执行的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 或 MARS 查询。 为了有助于避免这些类型的冲突，必须精心设计应用程序。  
  
 当 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 或应用程序尝试打开 FILESTREAM BLOB 时， [!INCLUDE[ssDE](../../includes/ssde-md.md)] 会检查关联事务上下文。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 根据打开操作是在处理 DDL 语句、DML 语句，在检索数据还是在管理事务，从而允许或拒绝请求。 下表显示 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 如何根据事务中打开的文件的类型来确定是允许还是拒绝 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句。  
  
|Transact-SQL 语句|打开以进行读取|打开以进行写入|  
|------------------------------|---------------------|----------------------|  
|处理数据库元数据的 DDL 语句，例如 CREATE TABLE、CREATE INDEX、DROP TABLE 和 ALTER TABLE。|Allowed|被阻止，并因超时而失败。|  
|处理存储在数据库中的数据的 DML 语句，例如 UPDATE、DELETE 和 INSERT。|Allowed|拒绝|  
|SELECT|Allowed|Allowed|  
|COMMIT TRANSACTION|拒绝*|拒绝*|  
|SAVE TRANSACTION|拒绝*|拒绝*|  
|ROLLBACK|允许*|允许*|  
  
 \* 取消事务，并且事务上下文的打开句柄无效。 应用程序必须关闭所有打开句柄。  
  
## <a name="examples"></a>示例  
 以下示例显示 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句和 FILESTREAM Win32 访问是如何导致冲突的。  
  
### <a name="a-opening-a-filestream-blob-for-write-access"></a>A. 打开 FILESTREAM BLOB 以进行写访问  
 下例显示打开文件以仅进行写访问的效果。  
  
```  
dstHandle =  OpenSqlFilestream(dstFilePath, Write, 0,  
    transactionToken, cbTransactionToken, 0);  
  
//Write some date to the FILESTREAM BLOB.  
WriteFile(dstHandle, updateData, ...);  
  
//DDL statements will be denied.  
//DML statements will be denied.  
//SELECT statements will be allowed. The FILESTREAM BLOB is  
//returned without the modifications that are made by  
//WriteFile(dstHandle, updateData, ...).  
CloseHandle(dstHandle);  
  
//DDL statements will be allowed.  
//DML statements will be allowed.  
//SELECT statements will be allowed. The FILESTREAM BLOB  
//is returned with the updateData applied.  
```  
  
### <a name="b-opening-a-filestream-blob-for-read-access"></a>B. 打开 FILESTREAM BLOB 以进行读访问  
 下例显示打开文件以仅进行读访问的效果。  
  
```  
dstHandle =  OpenSqlFilestream(dstFilePath, Read, 0,  
    transactionToken, cbTransactionToken, 0);  
//DDL statements will be denied.  
//DML statements will be allowed. Any changes that are  
//made to the FILESTREAM BLOB will not be returned until  
//the dstHandle is closed.  
//SELECT statements will be allowed.  
CloseHandle(dstHandle);  
  
//DDL statements will be allowed.  
//DML statements will be allowed.  
//SELECT statements will be allowed.  
```  
  
### <a name="c-opening-and-closing-multiple-filestream-blob-files"></a>C. 打开和关闭多个 FILESTREAM BLOB 文件  
 如果打开多个文件，则会使用限制性最强的规则。 下例打开了两个文件。 打开第一个文件以进行读取，打开第二个文件以进行写入。 DML 语句将被拒绝，直到第二个文件打开为止。  
  
```  
dstHandle =  OpenSqlFilestream(dstFilePath, Read, 0,  
    transactionToken, cbTransactionToken, 0);  
//DDL statements will be denied.  
//DML statements will be allowed.  
//SELECT statements will be allowed.  
  
dstHandle1 =  OpenSqlFilestream(dstFilePath1, Write, 0,  
    transactionToken, cbTransactionToken, 0);  
  
//DDL statements will be denied.  
//DML statements will be denied.  
//SELECT statements will be allowed.  
  
//Close the read handle. The write handle is still open.  
CloseHandle(dstHandle);  
//DML statements are still denied because the write handle is open.  
  
//DDL statements will be denied.  
//DML statements will be denied.  
//SELECT statements will be allowed.  
  
CloseHandle(dstHandle1);  
//DDL statements will be allowed.  
//DML statements will be allowed.  
//SELECT statements will be allowed.  
```  
  
### <a name="d-failing-to-close-a-cursor"></a>D. 无法关闭游标  
 下例显示的是未关闭的语句游标如何阻止 `OpenSqlFilestream()` 打开 BLOB 进行写访问。  
  
```  
TCHAR *sqlDBQuery =  
TEXT("SELECT GET_FILESTREAM_TRANSACTION_CONTEXT(),")  
TEXT("Chart.PathName() FROM Archive.dbo.Records");  
  
//Execute a long-running Transact-SQL statement. Do not allow  
//the statement to complete before trying to  
//open the file.  
  
SQLExecDirect(hstmt, sqlDBQuery, SQL_NTS);  
  
//Before you call OpenSqlFilestream() any open files  
//that the Cursor the Transact-SQL statement is using  
// must be closed. In this example,  
//SQLCloseCursor(hstmt) is not called so that  
//the transaction will indicate that there is a file  
//open for reading. This will cause the call to  
//OpenSqlFilestream() to fail because the file is  
//still open.  
  
HANDLE srcHandle =  OpenSqlFilestream(srcFilePath,  
     Write, 0,  transactionToken,  cbTransactionToken,  0);  
  
//srcHandle will == INVALID_HANDLE_VALUE because the  
//cursor is still open.  
```  
  
## <a name="see-also"></a>请参阅  
 [使用 OpenSqlFilestream 访问 FILESTREAM 数据](access-filestream-data-with-opensqlfilestream.md)   
 [使用多个活动的结果集 (MARS)](../native-client/features/using-multiple-active-result-sets-mars.md)  
  
  
