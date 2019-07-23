---
title: DBCC DROPCLEANBUFFERS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/16/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROPCLEANBUFFERS
- DBCC_DROPCLEANBUFFERS_TSQL
- DROPCLEANBUFFERS_TSQL
- DBCC DROPCLEANBUFFERS
dev_langs:
- TSQL
helpviewer_keywords:
- clean buffers
- cold buffer cache
- buffer pools [SQL Server]
- dropping buffers
- removing buffers
- DBCC DROPCLEANBUFFERS statement
ms.assetid: a4121927-f2ce-4926-aa2c-9b1519dac048
author: pmasl
ms.author: umajay
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a3b2d2ff81fddaae0b0ae68da9d4477819a61073
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68101936"
---
# <a name="dbcc-dropcleanbuffers-transact-sql"></a>DBCC DROPCLEANBUFFERS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

从缓冲池删除所有清除缓冲区，并从列存储对象池中删除列存储对象。
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法
SQL Server 语法： 

```sql
DBCC DROPCLEANBUFFERS [ WITH NO_INFOMSGS ]  
```  
Azure SQL 数据仓库和并行数据仓库语法：

```sql  
DBCC DROPCLEANBUFFERS ( COMPUTE | ALL ) [ WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>参数  
 WITH NO_INFOMSGS  
 取消显示所有信息性消息。 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 中始终禁止信息性消息。  
  
 COMPUTE  
 从每个“计算”节点清除内存中的数据缓存。  
  
 ALL  
 从每个“计算”节点和“管理”节点，清除内存中的数据缓存。 如果不指定值，则使用此默认值。  
  
## <a name="remarks"></a>Remarks  
使用 DBCC DROPCLEANBUFFERS 测试包含冷缓存的查询，而不用关闭和重新启动服务器。
若要从缓冲池删除清除缓冲区，并从列存储对象池删除列存储对象，请首先使用 CHECKPOINT 生成一个冷缓冲区缓存。 这可以强制将当前数据库的全部脏页写入磁盘，然后清除缓冲区。 完成此操作后，便可发出 DBCC DROPCLEANBUFFERS 命令来从缓冲池中删除所有缓冲区。
  
## <a name="result-sets"></a>结果集  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 上的 DBCC DROPCLEANBUFFERS 返回：
  
```sql
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
## <a name="permissions"></a>权限  

适用范围：SQL Server、并行数据仓库 

- 要求具有 **sysadmin** 固定服务器角色的成员身份。  

适用范围：Azure SQL 数据仓库

- 要求具有 DB_OWNER 固定服务器角色中的成员资格。  
  
## <a name="see-also"></a>另请参阅  
[DBCC (Transact-SQL)](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[检查点 (Transact-SQL)](../../t-sql/language-elements/checkpoint-transact-sql.md)  
  
  
