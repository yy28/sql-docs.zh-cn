---
title: DBCC TRACEON (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: uc-msft
ms.author: umajay
manager: craigg
ms.openlocfilehash: 8ae88c08604236c74915275c3b7edb515697d8ba
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47652867"
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
trace#  
要打开的跟踪标记的编号。  
  
*n*  
表示可指定多个跟踪标志的占位符。  
  
-1  
以全局方式打开指定的跟踪标记。  
  
WITH NO_INFOMSGS  
取消显示所有信息性消息。  
  
## <a name="remarks"></a>Remarks  
在生产服务器上，为了避免意外行为，建议您使用下列方法之一，仅在服务器范围内启用跟踪标记。
-   使用 Sqlservr.exe 的 -T 命令行启动选项。 这是推荐的最佳实践，因为这样可确保在所有语句运行时使用已启用的跟踪标志。 这些语句包括启动脚本中的命令。 有关详细信息，请参阅 [sqlservr Application](../../tools/sqlservr-application.md)。  
-   仅在用户或应用程序未对系统以并行方式运行语句时，才使用 DBCC TRACEON (***trace# [**,* ....n],-1)。  

跟踪标记用于通过控制 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的运行方式来自定义某些特征。 启用的跟踪标记将在服务器中一直保持启用状态，直到执行 DBCC TRACEOFF 语句将其禁用为止。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，有两种跟踪标志：会话和全局。 会话跟踪标志对某个连接是有效的，只对该连接可见。 全局跟踪标志在服务器级别上进行设置，对服务器上的每一个连接都可见。 若要确定跟踪标记的状态，请使用 DBCC TRACESTATUS。 若要禁用跟踪标记，请使用 DBCC TRACEOFF。
  
开启影响查询计划的跟踪标志后，执行 `DBCC FREEPROCCACHE;`，以便使用新的影响计划的行为重新编译缓存计划。
  
## <a name="result-sets"></a>结果集  
 DBCC TRACEON 返回以下结果集（消息）：  
  
```sql
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
## <a name="permissions"></a>Permissions  
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
[DBCC TRACESTATUS (Transact-SQL)](../../t-sql/database-console-commands/dbcc-tracestatus-transact-sql.md)  
[跟踪标志 (Transact-SQL)](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)  
[启用可通过特定查询级别上的不同跟踪标志控制的影响计划的 SQL Server 查询优化器行为](https://support.microsoft.com/kb/2801413)
  
  
