---
title: "DBCC SHRINKLOG （Azure SQL 数据仓库） |Microsoft 文档"
ms.custom: 
ms.date: 07/17/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|database-console-commands
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: d06917a784e507ab5568e28b4d34273f5fe71063
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="dbcc-shrinklog-azure-sql-data-warehouse"></a>DBCC SHRINKLOG （Azure SQL 数据仓库）
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

减少了事务日志的大小*跨设备*当前[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]数据库。 数据是为了收缩事务日志已进行碎片整理。 随着时间推移，数据库事务日志可能会变得零碎且效率低下。 使用 DBCC SHRINKLOG 要减少碎片，减少日志大小。
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定 &#40;Transact SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```sql
DBCC SHRINKLOG   
    [ ( SIZE = { target_size [ MB | GB | TB ]  } | DEFAULT ) ]   
    [ WITH NO_INFOMSGS ]   
[;]  
```  
  
## <a name="arguments"></a>参数  
大小 = { *target_size* [MB |**GB** |TB]} |**默认**。  
*target_size* DBCC SHRINKLOG 完成后的所有计算节点上，为所需的事务日志大小。 它是大于 0 的整数。  
日志大小的单位为兆字节 (MB)、 千兆字节 (GB) 或千兆字节 (TB)。 它是事务日志的所有计算节点上的组合的大小。  
默认情况下，DBCC SHRINKLOG 到数据库的元数据中存储的日志大小减少事务日志。 元数据中的日志大小由中的 LOG_SIZE 参数[CREATE DATABASE &#40;Azure SQL 数据仓库 &#41;](../../t-sql/statements/create-database-azure-sql-data-warehouse.md)或[ALTER DATABASE &#40;Azure SQL 数据仓库 &#41;](../../t-sql/statements/alter-database-azure-sql-data-warehouse.md). DBCC SHRINKLOG 事务日志大小减小到默认大小时`SIZE=DEFAULT`指定，或当`SIZE`省略子句。
  
WITH NO_INFOMSGS  
在 DBCC SHRINKLOG 结果中不显示信息性消息。  
  
## <a name="permissions"></a>权限  
需要 ALTER SERVER STATE 权限。
  
## <a name="general-remarks"></a>一般备注  
DBCC SHRINKLOG 不会更改数据库的元数据中存储的日志大小。 元数据将继续以包含在 CREATE DATABASE 或 ALTER DATABASE 语句中指定的 LOG_SIZE 参数。
  
## <a name="examples-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
### <a name="a-shrink-the-transaction-log-to-the-original-size-specified-by-create-database"></a>A. 创建数据库指定的原始大小收缩事务日志。  
假设已创建地址数据库时，地址数据库的事务日志已设置为 100 MB。 即，地址的 CREATE DATABASE 语句必须 LOG_SIZE = 100 MB。 现在，假设日志数已增加到 150 MB，并且你要压缩回 100 MB。
  
每个以下语句将尝试将地址数据库的事务日志收缩到 100 MB 的默认大小。 如果为 100 MB 收缩日志会导致数据丢失，DBCC SHRINKLOG 将不会丢失数据到可能的最小大小，大于 100 MB，收缩日志。
  
```sql
USE Addresses;  
DBCC SHRINKLOG ( SIZE = 100 MB );  
DBCC SHRINKLOG ( SIZE = DEFAULT );  
DBCC SHRINKLOG;  
```  
  
  
