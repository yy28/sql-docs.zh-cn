---
title: "DBCC CHECKCATALOG (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 11/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|database-console-commands
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DBCC_CHECKCATALOG_TSQL
- DBCC CHECKCATALOG
- CHECKCATALOG_TSQL
- CHECKCATALOG
dev_langs: TSQL
helpviewer_keywords:
- catalogs [SQL Server], consistency checks
- checking catalog consistency
- DBCC CHECKCATALOG statement
- integrity [SQL Server], catalogs
- consistency [SQL Server], catalogs
ms.assetid: 8076eb4e-f049-44bf-9a35-45cdd6ef0105
caps.latest.revision: "51"
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 7c8b73259e599e0001706cfaf09dca30d7d31a5b
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="dbcc-checkcatalog-transact-sql"></a>DBCC CHECKCATALOG (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  检查指定数据库内的目录一致性。 数据库必须联机。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
DBCC CHECKCATALOG   
[   
    (   
    database_name | database_id | 0  
    )  
]  
    [ WITH NO_INFOMSGS ]   
```  
  
## <a name="arguments"></a>参数  
 *database_name* | *database_id* | 0  
 要检查其目录一致性的数据库的名称和 ID。 如果未指定，或者指定为 0，则使用当前数据库。 数据库名称必须符合的规则[标识符](../../relational-databases/databases/database-identifiers.md)。  
  
 WITH NO_INFOMSGS  
 取消显示所有信息性消息。  
  
## <a name="remarks"></a>注释  
DBCC CATALOG 命令完成后，会将一条消息写入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误日志。 如果 DBCC 命令成功执行，则消息指示成功完成以及命令运行的时间。 如果由于出错，导致完成检查之前将停止 DBCC 命令，则消息将指示该命令已终止，状态值，并运行该命令的时间量。 下表列出并说明了此消息中可包含的状态值。
  
|State|Description|  
|-----------|-----------------|  
|0|出现错误号 8930。 这指示导致 DBCC 命令终止的元数据损坏。|  
|1|出现错误号 8967。 存在一个内部 DBCC 错误。|  
|2|在紧急模式数据库修复过程中出错。|  
|3|这指示导致 DBCC 命令终止的元数据损坏。|  
|4|检测到断定或访问违规。|  
|5|出现终止了 DBCC 命令的未知错误。|  
  
DBCC CHECKCATALOG 在系统元数据表之间执行各种一致性检查。 DBCC CHECKCATALOG 使用内部数据库快照来提供需要执行这些检查的事务一致性。 有关详细信息，请参阅[查看数据库快照 &#40; 的稀疏文件的大小Transact SQL &#41;](../../relational-databases/databases/view-the-size-of-the-sparse-file-of-a-database-snapshot-transact-sql.md)和中的"DBCC 内部数据库快照使用情况"一节[DBCC &#40;Transact SQL &#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md).
如果无法创建快照，则 DBCC CHECKCATALOG 将获取一个排他数据库锁以获得要求的一致性。 如果检测到任何不一致，则无法修复这些不一致问题，必须使用备份来还原数据库。
  
> [!NOTE]  
> 运行 DBCC CHECKCATALOG 针对**tempdb**不执行任何检查。 这是因为，出于性能原因，数据库快照上不可用**tempdb**。 这意味着，无法获得所需的事务一致性。 回收服务器以解决任何**tempdb**元数据问题。  
  
> [!NOTE]  
> DBCC CHECKCATALOG 不会检查 FILESTREAM 数据。 FILESTREAM 在文件系统中存储二进制大型对象 (BLOB)。  
  
作为的一部分也运行 DBCC CHECKCATALOG [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)。
  
## <a name="result-sets"></a>结果集  
如果未指定数据库，则 DBCC CHECKCATALOG 返回以下内容：
  
```
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
如果将 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 指定为数据库名，则 DBCC CHECKCATALOG 返回以下内容：
  
```
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
## <a name="permissions"></a>权限  
 要求的成员身份**sysadmin**固定服务器角色或**db_owner**固定的数据库角色。  
  
## <a name="examples"></a>示例  
以下示例将检查当前数据库和 `AdventureWorks` 数据库中的目录完整性。
  
```sql
-- Check the current database.  
DBCC CHECKCATALOG;  
GO  
-- Check the AdventureWorks2012 database.  
DBCC CHECKCATALOG (AdventureWorks2012);  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
[DBCC (Transact-SQL)](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[系统表 &#40;Transact SQL &#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)
  
