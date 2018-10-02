---
title: DBCC DBREPAIR (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- TRACEOFF_TSQL
- TRACEOFF
- DBCC TRACEOFF
- DBCC_TRACEOFF_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- trace flags [SQL Server], disabling
- DBCC TRACEOFF statement
- disabling trace flags
ms.assetid: 1379afba-6480-454b-9c65-5e64cb4f3415
author: uc-msft
ms.author: umajay
manager: craigg
ms.openlocfilehash: 9c138fbfc750bce13c9146c2a4c1416b291c8ecf
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47773985"
---
# <a name="dbcc-traceoff-transact-sql"></a>DBCC DBREPAIR (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

禁用指定的跟踪标记。
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```sql
DBCC TRACEOFF ( trace# [ ,...n ] [ , -1 ] ) [ WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>参数  
trace#  
要禁用的跟踪标记号。  
  
**-1**  
全局禁用指定的跟踪标记。  
  
WITH NO_INFOMSGS  
取消严重级别从 0 到 10 的所有信息性消息。  
  
## <a name="remarks"></a>Remarks  
跟踪表记用于自定义某些控制 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的操作方式的特征。
  
## <a name="result-sets"></a>结果集  
DBCC TRACEOFF 返回：
  
```sql
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
## <a name="permissions"></a>Permissions  
要求具有 **sysadmin** 固定服务器角色的成员身份。
  
## <a name="examples"></a>示例  
以下示例禁用跟踪标记 `3205`。
  
```sql
DBCC TRACEOFF (3205);   
GO  
```  
  
以下示例首先全局禁用跟踪标记 `3205`。
  
```sql
DBCC TRACEOFF (3205, -1);   
GO  
```  
  
以下示例全局禁用跟踪标记 `3205` 和 `260`。
  
```sql
DBCC TRACEOFF (3205, 260, -1);  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
[DBCC (Transact-SQL)](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[DBCC TRACEON (Transact-SQL)](../../t-sql/database-console-commands/dbcc-traceon-transact-sql.md)  
[DBCC TRACESTATUS (Transact-SQL)](../../t-sql/database-console-commands/dbcc-tracestatus-transact-sql.md)  
[跟踪标志 (Transact-SQL)](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)
  
  
