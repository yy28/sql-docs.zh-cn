---
title: FILE_IDEX (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- FILE_IDEX
- FILE_IDEX_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- FILE_IDEX function
- IDs [SQL Server], files
- file IDs [SQL Server]
- names [SQL Server], files
- identification numbers [SQL Server], files
- file names [SQL Server], FILE_IDEX
ms.assetid: 7532fea5-ee5e-4edd-b98b-111a7ba56c8e
caps.latest.revision: 35
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 54224c2b6f977f21764553ceddfb7e7be5fd10c7
ms.sourcegitcommit: 05e18a1e80e61d9ffe28b14fb070728b67b98c7d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/04/2018
ms.locfileid: "37788358"
---
# <a name="fileidex-transact-sql"></a>FILE_IDEX (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

返回当前数据库中的数据、日志或全文文件的指定逻辑文件名的文件标识 (ID) 号。  
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
FILE_IDEX ( file_name )  
```  
  
## <a name="arguments"></a>参数  
 file_name  
 一个 sysname 类型的表达式，表示要返回文件 ID 的文件的名称。  
  
## <a name="return-types"></a>返回类型  
 **int**  
  
 出现错误时，返回 NULL  
  
## <a name="remarks"></a>Remarks  
 file_name 对应于 [sys.master_files](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md) 或 [sys.database_files](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md) 目录视图的 name 列中所显示的逻辑文件名。  
  
 FILE_IDEX 可以在选择列表、WHERE 子句和允许使用表达式的任何地方使用。 有关详细信息，请参阅[表达式 (Transact-SQL)](../../t-sql/language-elements/expressions-transact-sql.md)。  
  
## <a name="examples"></a>示例  
  
### <a name="a-retrieving-the-file-id-of-a-specified-file"></a>A. 检索指定文件的文件 ID  
以下示例返回 `AdventureWorks_Data` 文件的文件 ID。  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT FILE_IDEX('AdventureWorks2012_Data') AS 'File ID';  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
File ID   
-------   
1  
(1 row(s) affected)  
```  
  
### <a name="b-retrieving-the-file-id-when-the-file-name-is-not-known"></a>B. 在文件名未知时检索文件 ID  
以下示例通过从文件类型等于 `1`（日志）的 `sys.database_files` 目录视图中选择逻辑文件名来返回 `AdventureWorks` 日志文件的文件 ID。  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT FILE_IDEX((SELECT TOP (1) name FROM sys.database_files WHERE type = 1)) AS 'File ID';  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
File ID   
-------   
2  
```  
  
### <a name="c-retrieving-the-file-id-of-a-full-text-catalog-file"></a>C. 检索全文目录文件的文件 ID  
以下示例通过从文件类型等于 `4`（全文本）的 `sys.database_files` 目录视图中选择逻辑文件名来返回全文本文件的文件 ID。 如果全文目录不存在，则此示例将返回 NULL。  
  
```sql  
SELECT FILE_IDEX((SELECT name FROM sys.master_files WHERE type = 4))  
AS 'File_ID';  
```  
  
## <a name="see-also"></a>另请参阅  
 [元数据函数 (Transact-SQL)](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [sys.database_files (Transact-SQL)](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.master_files (Transact-SQL)](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)  
  
  
