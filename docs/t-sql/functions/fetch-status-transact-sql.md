---
title: "@@FETCH_STATUS (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 09/18/2017
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
- '@@FETCH_STATUS'
- '@@FETCH_STATUS_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- FETCH statement
- status information [SQL Server], FETCH
- '@@FETCH_STATUS function'
ms.assetid: 93659193-e4ff-4dfb-9043-0c4114921b91
caps.latest.revision: 39
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: c6ea46c5187f00190cb39ba9a502b3ecb6a28bc6
ms.openlocfilehash: 61e209f7cf2a3a654b33979129e9500d3734fe64
ms.contentlocale: zh-cn
ms.lasthandoff: 09/19/2017

---
# <a name="x40x40fetchstatus-transact-sql"></a>& #x 40; 和 #x 40;FETCH_STATUS (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  返回针对连接当前打开的任何游标发出的最后一条游标 FETCH 语句的状态。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
@@FETCH_STATUS  
```  
  
## <a name="return-type"></a>返回类型  
 **integer**  
  
## <a name="return-value"></a>返回值  
  
|返回值|Description|  
|------------------|-----------------|  
|0|FETCH 语句成功。|  
|-1|FETCH 语句失败或行不在结果集中。|  
|-2|提取的行不存在。|
|-9|光标未执行提取操作。|  
  
## <a name="remarks"></a>注释  
 因为 @@FETCH_STATUS适用于所有游标连接时，使用 @@FETCH_STATUS仔细。 FETCH 语句执行后，测试 @@FETCH_STATUS对另一个游标执行任何其他 FETCH 语句之前，必须执行。 值 @@FETCH_STATUS之前连接上发生的所有读取操作是不确定。  
  
 例如，用户从一个游标执行一条 FETCH 语句，然后调用一个存储过程，此存储过程打开并处理另一个游标的结果。 从调用的存储过程，返回控件时@FETCH_STATUS反映上次提取在存储的过程中，不执行之前调用存储的过程的 FETCH 语句执行。  
  
 若要检索特定光标的最后一个提取状态，查询**fetch_status**列**sys.dm_exec_cursors**动态管理函数。  
  
## <a name="examples"></a>示例  
 以下示例使用 `@@FETCH_STATUS` 来控制 `WHILE` 循环中的游标活动。  
  
```  
DECLARE Employee_Cursor CURSOR FOR  
SELECT BusinessEntityID, JobTitle  
FROM AdventureWorks2012.HumanResources.Employee;  
OPEN Employee_Cursor;  
FETCH NEXT FROM Employee_Cursor;  
WHILE @@FETCH_STATUS = 0  
   BEGIN  
      FETCH NEXT FROM Employee_Cursor;  
   END;  
CLOSE Employee_Cursor;  
DEALLOCATE Employee_Cursor;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [游标函数 (Transact-SQL)](../../t-sql/functions/cursor-functions-transact-sql.md)   
 [提取 &#40;Transact SQL &#41;](../../t-sql/language-elements/fetch-transact-sql.md)  
  
  

