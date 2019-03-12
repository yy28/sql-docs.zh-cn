---
title: DBCC SHRINKLOG（并行数据仓库）| Microsoft Docs
ms.custom: ''
ms.date: 03/16/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
author: pmasl
ms.author: umajay
manager: craigg
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 3a40717a472970a0e2d463e958330e2d46473ab1
ms.sourcegitcommit: 0a7beb2f51e48889b4a85f7c896fb650b208eb36
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57685384"
---
# <a name="dbcc-shrinklog-parallel-data-warehouse"></a>DBCC SHRINKLOG（并行数据仓库）
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

减少当前 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 数据库在设备中的事务日志大小。 已对数据进行碎片整理，以便收缩事务日志。 随着时间推移，数据库事务日志可能会变得零碎且效率低下。 使用 DBCC SHRINKLOG 减少碎片并减小日志大小。
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [Transact-SQL 语法约定 (Transact-SQL)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```sql
DBCC SHRINKLOG   
    [ ( SIZE = { target_size [ MB | GB | TB ]  } | DEFAULT ) ]   
    [ WITH NO_INFOMSGS ]   
[;]  
```  
  
## <a name="arguments"></a>参数  
SIZE = { target_size [MB |GB |TB]} |DEFAULT。  
target_size 是 DBCC SHRINKLOG 完成后所有计算节点上所需的事务日志大小。 它必须是大于 0 的整数。  
日志大小的单位为兆字节 (MB)、千兆字节 (GB) 或兆兆字节 (TB)。 它是所有计算节点上事务日志的组合大小。  
默认情况下，DBCC SHRINKLOG 可将事务日志减小到数据库的元数据中存储的日志大小。 元数据中的日志大小是由 [CREATE DATABASE（Azure SQL 数据仓库）](../../t-sql/statements/create-database-azure-sql-data-warehouse.md)或 [ALTER DATABASE（Azure SQL 数据仓库）](../../t-sql/statements/alter-database-azure-sql-data-warehouse.md)中的 LOG_SIZE 参数确定的。 已指定 `SIZE=DEFAULT` 或省略 `SIZE` 子句时，DBCC SHRINKLOG 可将事务日志大小减小到默认大小。
  
WITH NO_INFOMSGS  
DBCC SHRINKLOG 结果中不显示信息性消息。  
  
## <a name="permissions"></a>Permissions  
需要 ALTER SERVER STATE 权限。
  
## <a name="general-remarks"></a>一般备注  
DBCC SHRINKLOG 不会更改数据库的元数据中存储的日志大小。 元数据会继续包含 CREATE DATABASE 或 ALTER DATABASE 语句中指定的 LOG_SIZE 参数。
  
## <a name="examples"></a>示例 
### <a name="a-shrink-the-transaction-log-to-the-original-size-specified-by-create-database"></a>A. 将事务日志收缩到 CREATE DATABASE 指定的原始大小。  
假设创建 Addresses 数据库时，Addresses 数据库的事务日志已设置为 100 MB。 即 Addresses 的 CREATE DATABASE 语句的 LOG_SIZE = 100 MB。 现在，假设日志大小已增加到 150 MB，而你希望将其收缩到 100 MB。
  
以下每个语句都会尝试将 Addresses 数据库的事务日志收缩到 100 MB 的默认大小。 如果将日志收缩到 100 MB 会导致数据丢失，DBCC SHRINKLOG 会尽可能地将日志收缩到最小（大于 100 MB），而不会丢失数据。
  
```sql
USE Addresses;  
DBCC SHRINKLOG ( SIZE = 100 MB );  
DBCC SHRINKLOG ( SIZE = DEFAULT );  
DBCC SHRINKLOG;  
```  
  
  
