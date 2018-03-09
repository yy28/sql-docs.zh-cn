---
title: "@@LOCK_TIMEOUT (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 09/19/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 84b885d21e5d940e3c532eef43040ba29c2b45ea
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="x40x40locktimeout-transact-sql"></a>&#x40;&#x40;LOCK_TIMEOUT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  返回当前会话的当前锁定超时设置（毫秒）。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
@@LOCK_TIMEOUT  
```  
  
## <a name="return-types"></a>返回类型  
 **integer**  
  
## <a name="remarks"></a>注释  
 SET LOCK_TIMEOUT 允许应用程序设置语句等待阻塞资源的最长时间。 当一条语句等待的时间长度超过 LOCK_TIMEOUT 所设置的时间长度时，被锁住的语句将自动取消，并给应用程序返回一条错误消息。  
  
 @@LOCK_TIMEOUT如果 SET LOCK_TIMEOUT 尚未已运行在当前会话中，则返回值-1。  
  
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
  
 此示例将 LOCK_TIMEOUT 设置为 1800年毫秒，然后调用@LOCK_TIMEOUT 。  
  
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
 [设置 LOCK_TIMEOUT &#40;Transact SQL &#41;](../../t-sql/statements/set-lock-timeout-transact-sql.md)  
  
  
