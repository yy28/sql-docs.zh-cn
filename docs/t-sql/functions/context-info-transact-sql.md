---
title: "CONTEXT_INFO (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 07/24/2017
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
- CONTEXT_INFO_TSQL
- CONTEXT_INFO
dev_langs:
- TSQL
helpviewer_keywords:
- CONTEXT_INFO function
- Multiple Active Result Sets
- context information [SQL Server]
- MARS [SQL Server]
- session context information [SQL Server]
ms.assetid: 571320f5-7228-4b0e-9d01-ab732d2d1eab
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: a647bc7ced2188a45183200f08400f5507f7b328
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="contextinfo--transact-sql"></a>CONTEXT_INFO (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

返回**context_info**值，通过使用设置为当前会话或批处理[设置 CONTEXT_INFO](../../t-sql/statements/set-context-info-transact-sql.md)语句。
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```sql
CONTEXT_INFO()  
```  
  
## <a name="return-value"></a>返回值
值**context_info**。
  
如果**context_info**未设置：
-   在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回 NULL。  
-   在[!INCLUDE[ssSDS](../../includes/sssds-md.md)]返回唯一的特定于会话的 GUID。  
  
## <a name="remarks"></a>注释  
多个活动的结果集 (MARS) 将使应用程序能够使用相同连接同时运行多个批处理或请求。 当 MARS 连接中的一个批处理运行 SET CONTEXT_INFO 时，如果 CONTEXT_INFO 函数作为 SET 语句运行在同一批处理中，则该函数将返回新的上下文值。 在该连接上的其他一个或多个批处理中运行的 CONTEXT_INFO 函数不会返回新的值，除非这些批处理在运行 SET 语句的批处理完成之后启动。
  
## <a name="permissions"></a>Permissions  
不要求具有特殊权限。 上下文信息也存储在**sys.dm_exec_requests**， **sys.dm_exec_sessions**，和**sys.sysprocesses**系统视图，但直接查询这些视图需要选择和 VIEW SERVER STATE 权限。
  
## <a name="examples"></a>示例  
下面的简单示例设置**context_info**值赋给`0x1256698456`，然后使用`CONTEXT_INFO`函数以检索值。
  
```sql
SET CONTEXT_INFO 0x1256698456;  
GO  
SELECT CONTEXT_INFO();  
GO  
```  
  
## <a name="see-also"></a>另请参阅
[设置 CONTEXT_INFO &#40;Transact SQL &#41;](../../t-sql/statements/set-context-info-transact-sql.md)
  
  
