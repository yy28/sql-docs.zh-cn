---
title: "集 LOCK_TIMEOUT (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 09/11/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- LOCK_TIMEOUT_TSQL
- SET_LOCK_TIMEOUT_TSQL
- SET LOCK_TIMEOUT
- LOCK_TIMEOUT
dev_langs:
- TSQL
helpviewer_keywords:
- timeout options [SQL Server], locks
- releasing locks
- LOCK_TIMEOUT option
- SET LOCK_TIMEOUT statement
- locking [SQL Server], time-outs
- wait time for lock releases [SQL Server]
ms.assetid: dd0c389e-956d-435e-bf71-e16624a0a215
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 0e19a9acd7378615433364ac1b30db31a1a84b3a
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="set-locktimeout-transact-sql"></a>SET LOCK_TIMEOUT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  指定语句等待锁释放的毫秒数。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
SET LOCK_TIMEOUT timeout_period  
```  
  
## <a name="arguments"></a>参数  
 *timeout_period*  
 为将传递之前的毫秒数[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回出现锁定错误。 值为 -1（默认值）时表示没有超时期限（即无限期等待）。  
  
 当锁等待超过超时值时，将返回错误。 值为 0 时表示根本不等待，一遇到锁就返回消息。  
  
## <a name="remarks"></a>注释  
 在连接开始时，此设置的值为 -1。 设置更改后，新设置在其余的连接时间里一直有效。  
  
 SET LOCK_TIMEOUT 的设置是在执行或运行时设置，而不是在分析时设置。  
  
 READPAST 锁提示为该 SET 选项提供了另一种方式。  
  
 CREATE DATABASE、ALTER DATABASE 和 DROP DATABASE 语句不使用 SET LOCK_TIMEOUT 设置。  
  
## <a name="permissions"></a>Permissions  
 要求 **公共** 角色具有成员身份。  
  
## <a name="examples"></a>示例  
  
### <a name="a-set-the-lock-timeout-to-1800-milliseconds"></a>答： 在锁定超时设置为 1800年毫秒  
 下面的示例将锁超时期限设置为 `1800` 毫秒。  
  
```sql  
SET LOCK_TIMEOUT 1800;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="b-set-the-lock-timeout-to-wait-forever-for-a-lock-to-be-released"></a>B. 设置永远等待被释放锁在锁定超时。  
 下面的示例设置在锁定超时永远等待并永不过期。 这是已设置开头的每个连接的默认行为。  
  
```sql  
SET LOCK_TIMEOUT -1;  
```  
  
 下面的示例将锁超时期限设置为 `1800` 毫秒。 在此版本中，[!INCLUDE[ssDW](../../includes/ssdw-md.md)]将分析该语句已成功，但将忽略值 1800年并继续使用默认行为。  
  
```sql  
SET LOCK_TIMEOUT 1800;  
```  
  
## <a name="see-also"></a>另请参阅  
 [@@LOCK_TIMEOUT (Transact-SQL)](../../t-sql/functions/lock-timeout-transact-sql.md)   
 [SET 语句 (Transact-SQL)](../../t-sql/statements/set-statements-transact-sql.md)  
  
  

