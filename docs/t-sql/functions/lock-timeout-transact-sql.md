---
title: '@@LOCK_TIMEOUT (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 09/19/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- '@@LOCK_TIMEOUT'
- '@@LOCK_TIMEOUT_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- timeout options [SQL Server], locks
- '@@LOCK_TIMEOUT function'
- current lock time-out setting
- locking [SQL Server], time-outs
ms.assetid: 6bf8bf97-60b8-40c1-b89d-8f5a00bcae2e
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 10e21a229628f8c24e35e846a07ab0b847a8ff85
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/05/2020
ms.locfileid: "82822899"
---
# <a name="x40x40lock_timeout-transact-sql"></a>&#x40;&#x40;LOCK_TIMEOUT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  返回当前会话的当前锁定超时设置（毫秒）。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
@@LOCK_TIMEOUT  
```  
  
## <a name="return-types"></a>返回类型  
 **integer**  
  
## <a name="remarks"></a>备注  
 SET LOCK_TIMEOUT 允许应用程序设置语句等待阻塞资源的最长时间。 当一条语句等待的时间长度超过 LOCK_TIMEOUT 所设置的时间长度时，被锁住的语句将自动取消，并给应用程序返回一条错误消息。  
  
 如果当前会话中尚未运行 SET LOCK_TIMEOUT，@@LOCK_TIMEOUT 将返回值 -1。  
  
## <a name="examples"></a>示例  
 以下示例显示当未设置 LOCK_TIMEOUT 值时的结果集。  
  
```  
SELECT @@LOCK_TIMEOUT AS [Lock Timeout];  
GO  
```  
  
 下面是结果集：  
  
```  
Lock Timeout  
------------  
-1  
```  
  
 该示例将 LOCK_TIMEOUT 设置为 1800 毫秒，然后调用 @@LOCK_TIMEOUT。  
  
```  
SET LOCK_TIMEOUT 1800;  
SELECT @@LOCK_TIMEOUT AS [Lock Timeout];  
GO  
```  
  
 下面是结果集：  
  
```  
Lock Timeout  
------------  
1800          
```  
  
## <a name="see-also"></a>另请参阅  
 [配置函数 (Transact-SQL)](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [SET LOCK_TIMEOUT (Transact-SQL)](../../t-sql/statements/set-lock-timeout-transact-sql.md)  
  
  
