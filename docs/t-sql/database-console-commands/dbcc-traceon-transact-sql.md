---
title: "DBCC TRACEON (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 07/17/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|database-console-commands
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DBCC_TRACEON_TSQL
- TRACEON
- DBCC TRACEON
- TRACEON_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DBCC TRACEON statement
- trace flags [SQL Server], enabling
ms.assetid: 93085324-ebaa-4e38-aac8-5e57b4b0d36d
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 8c173779833562123c9ba3820fef76bf23b80a43
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="dbcc-traceon-transact-sql"></a>DBCC TRACEON (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

启用指定的跟踪标志。
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```sql
DBCC TRACEON ( trace# [ ,...n ][ , -1 ] ) [ WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>参数  
*trace#*  
要打开的跟踪标记的编号。  
  
*n*  
表示可指定多个跟踪标志的占位符。  
  
-1  
以全局方式打开指定的跟踪标记。  
  
WITH NO_INFOMSGS  
取消显示所有信息性消息。  
  
## <a name="remarks"></a>注释  
在生产服务器上，为了避免意外行为，建议您使用下列方法之一，仅在服务器范围内启用跟踪标记。
-   使用**-T**的 Sqlservr.exe 的命令行启动选项。 这是推荐的最佳实践，因为这样可确保在所有语句运行时使用已启用的跟踪标志。 这些语句包括启动脚本中的命令。 有关详细信息，请参阅 [sqlservr Application](../../tools/sqlservr-application.md)。  
-   使用 DBCC TRACEON  **(* * * 跟踪 #* [* *，**...*.n*]**、-1)**仅用户或应用程序不并发运行时语句系统上。  

跟踪标记用于通过控制 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的运行方式来自定义某些特征。 启用的跟踪标记将在服务器中一直保持启用状态，直到执行 DBCC TRACEOFF 语句将其禁用为止。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，有两种跟踪标志：会话和全局。 会话跟踪标志对某个连接是有效的，只对该连接可见。 全局跟踪标志在服务器级别上进行设置，对服务器上的每一个连接都可见。 若要确定跟踪标记的状态，请使用 DBCC TRACESTATUS。 若要禁用跟踪标记，请使用 DBCC TRACEOFF。
  
开启跟踪标志影响查询计划之后, 执行`DBCC FREEPROCCACHE;`以便缓存的计划，将重新编译使用新的计划影响行为。
  
## <a name="result-sets"></a>结果集  
 DBCC TRACEON 返回以下结果集（消息）：  
  
```sql
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
## <a name="permissions"></a>权限  
要求具有 **sysadmin** 固定服务器角色的成员身份。
  
## <a name="examples"></a>示例  
以下示例通过打开跟踪标记 `3205`，禁用磁带驱动程序的硬件压缩功能。 仅为当前连接打开此标记。
  
```sql  
DBCC TRACEON (3205);  
GO  
```  
  
以下示例以全局方式打开跟踪标记 `3205`。
  
```sql  
DBCC TRACEON (3205, -1);  
GO  
```  
  
以下示例以全局方式打开跟踪标记 `3205` 和 `260`。
  
```sql  
DBCC TRACEON (3205, 260, -1);  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
[DBCC (Transact-SQL)](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[DBCC TRACEOFF (Transact-SQL)](../../t-sql/database-console-commands/dbcc-traceoff-transact-sql.md)  
[DBCC TRACESTATUS &#40;Transact SQL &#41;](../../t-sql/database-console-commands/dbcc-tracestatus-transact-sql.md)  
[跟踪标志 (Transact-SQL)](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)  
[启用计划影响 SQL Server 查询优化器行为，可以控制由特定查询级别上的不同的跟踪标志](https://support.microsoft.com/kb/2801413)
  
  
