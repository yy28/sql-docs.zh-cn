---
title: "DBCC DROPCLEANBUFFERS (Transact SQL) |Microsoft 文档"
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
caps.latest.revision: 35
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d1a7a1507e230995df1c2b67a8499a12270b535c
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="dbcc-dropcleanbuffers-transact-sql"></a>DBCC DROPCLEANBUFFERS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw_md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

从缓冲池，并从列存储对象池中的列存储对象中移除所有清除缓冲区。
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法
SQL Server 的语法： 

```sql
DBCC DROPCLEANBUFFERS [ WITH NO_INFOMSGS ]  
```  
对于 Azure SQL 仓库和并行数据仓库的语法：

```sql  
DBCC DROPCLEANBUFFERS ( COMPUTE | ALL ) [ WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>参数  
 WITH NO_INFOMSGS  
 取消显示所有信息性消息。 信息性消息始终禁止上[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]。  
  
 COMPUTE  
 清除查询计划缓存中每个计算节点。  
  
 ALL  
 从每个计算节点和管理节点，请清除查询计划缓存。 如果不指定一个值，这是默认值。  
  
## <a name="remarks"></a>注释  
使用 DBCC DROPCLEANBUFFERS 测试包含冷缓存的查询，而不用关闭和重新启动服务器。
若要从缓冲区池和列存储对象从列存储对象池中删除干净的缓冲区，第一次使用检查点生成冷缓冲区缓存。 这可以强制将当前数据库的全部脏页写入磁盘，然后清除缓冲区。 完成此操作后，便可发出 DBCC DROPCLEANBUFFERS 命令来从缓冲池中删除所有缓冲区。
  
## <a name="result-sets"></a>结果集  
在 DBCC DROPCLEANBUFFERS[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回：
  
```sql
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
## <a name="permissions"></a>Permissions  

适用于： SQL Server，并行数据仓库 

- 要求具有 **sysadmin** 固定服务器角色的成员身份。  

适用于：Azure SQL 数据仓库

- 要求具有 DB_OWNER 固定的服务器角色的成员身份。  
  
## <a name="see-also"></a>另请参阅  
[DBCC (Transact-SQL)](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[检查点 (Transact-SQL)](../../t-sql/language-elements/checkpoint-transact-sql.md)  
  
  

