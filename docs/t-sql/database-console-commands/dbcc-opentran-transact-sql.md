---
title: "DBCC OPENTRAN (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 07/16/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DBCC_OPENTRAN_TSQL
- DBCC OPENTRAN
- OPENTRAN_TSQL
- OPENTRAN
dev_langs:
- TSQL
helpviewer_keywords:
- status information [SQL Server], transactions
- transactions [SQL Server], status information
- DBCC OPENTRAN statement
- open transactions
- displaying transaction information
- checking open transactions
- oldest transactions [SQL Server]
ms.assetid: 63163843-226f-42d3-9e2c-b634fbf06943
caps.latest.revision: 40
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f3d3b47d9bc553edd49f6f401d1a1c7a857d0a7d
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="dbcc-opentran-transact-sql"></a>DBCC OPENTRAN (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

DBCC OPENTRAN 可帮助识别可能阻止日志截断的活动事务。 如果在指定数据库的事务日志中存在最早的活动事务以及最早的分布式和非分布式复制事务，DBCC OPENTRAN 将显示与之相关的信息。 仅当日志中存在活动事务或数据库包含复制信息时，才显示结果。 如果日志中没有活动事务，则显示信息性消息。
  
> [!NOTE]  
>  非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 发布服务器不支持 DBCC OPENTRAN。  
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```sql
DBCC OPENTRAN   
[   
    ( [ database_name | database_id | 0 ] ) ]  
    { [ WITH TABLERESULTS ]  
      [ , [ NO_INFOMSGS ] ]  
    }  
]   
```  
  
## <a name="arguments"></a>参数  
 *database_name* | *database_id*| 0  
 显示其中的最早事务信息的数据库名称或 ID。 如果未指定，或者指定为 0，则使用当前数据库。 数据库名称必须符合的规则[标识符](../../relational-databases/databases/database-identifiers.md)。  
  
 TABLERESULTS  
 以表格格式指定结果以便可以加载到表中。 使用此选项创建结果表，可以将该结果表插入到表中以进行比较。 未指定此选项时，对结果进行格式化以增加可读性。  
  
 NO_INFOMSGS  
 取消显示所有信息性消息。  
  
## <a name="remarks"></a>注释  
使用 DBCC OPENTRAN 确定打开的事务是否存在于事务日志中。 使用 BACKUP LOG 语句时，只能截断日志的非活动部分；打开的事务会阻止日志被完全截断。 若要标识打开的事务，请使用 sp_who 获取系统进程 ID。
  
## <a name="result-sets"></a>结果集  
如果没有打开的事务，DBCC OPENTRAN 返回以下结果集：
  
```sql
No active open transactions.  
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
## <a name="permissions"></a>Permissions  
要求具有 **sysadmin** 固定服务器角色或 **db_owner** 固定数据库角色的成员身份。
  
## <a name="examples"></a>示例  
### <a name="a-returning-the-oldest-active-transaction"></a>A. 返回最早的活动事务  
下面的示例获取当前数据库的事务信息。 结果可能会有变化。
  
```sql  
CREATE TABLE T1(Col1 int, Col2 char(3));  
GO  
BEGIN TRAN  
INSERT INTO T1 VALUES (101, 'abc');  
GO  
DBCC OPENTRAN;  
ROLLBACK TRAN;  
GO  
DROP TABLE T1;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
Transaction information for database 'master'.
Oldest active transaction:
SPID (server process ID) : 52
UID (user ID) : -1
Name          : user_transaction
LSN           : (518:1576:1)
Start time    : Jun  1 2004  3:30:07:197PM
SID           : 0x010500000000000515000000a065cf7e784b9b5fe77c87709e611500
DBCC execution completed. If DBCC printed error messages, contact your system administrator.
```
  
> [!NOTE]  
>  “UID (user ID)”结果无意义，将在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的未来版本中将其删除。  
  
### <a name="b-specifying-the-with-tableresults-option"></a>B. 指定 WITH TABLERESULTS 选项  
下面的示例将 DBCC OPENTRAN 命令的结果加载到临时表中。
  
```sql  
-- Create the temporary table to accept the results.  
CREATE TABLE #OpenTranStatus (  
   ActiveTransaction varchar(25),  
   Details sql_variant   
   );  
-- Execute the command, putting the results in the table.  
INSERT INTO #OpenTranStatus   
   EXEC ('DBCC OPENTRAN WITH TABLERESULTS, NO_INFOMSGS');  
  
-- Display the results.  
SELECT * FROM #OpenTranStatus;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
[BEGIN TRANSACTION (Transact-SQL)](../../t-sql/language-elements/begin-transaction-transact-sql.md)  
[提交事务 &#40;Transact SQL &#41;](../../t-sql/language-elements/commit-transaction-transact-sql.md)  
[DBCC (Transact-SQL)](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[DB_ID &#40;Transact SQL &#41;](../../t-sql/functions/db-id-transact-sql.md)  
[ROLLBACK TRANSACTION &#40;Transact SQL &#41;](../../t-sql/language-elements/rollback-transaction-transact-sql.md)
  
  

