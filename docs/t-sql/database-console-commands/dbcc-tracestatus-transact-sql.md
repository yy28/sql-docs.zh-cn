---
title: "DBCC TRACESTATUS (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 07/17/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DBCC_TRACESTATUS_TSQL
- DBCC TRACESTATUS
- TRACESTATUS_TSQL
- TRACESTATUS
dev_langs:
- TSQL
helpviewer_keywords:
- global trace flags [SQL Server]
- status information [SQL Server], trace flags
- trace flags [SQL Server], status information
- DBCC TRACESTATUS statement
- session trace flags [SQL Server]
- displaying trace flag status
ms.assetid: 9be51199-78b4-4b87-ae6e-557246b7e29a
caps.latest.revision: 36
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 75d78069427891cfab6f7aaef7192d498912611a
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="dbcc-tracestatus-transact-sql"></a>DBCC TRACESTATUS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

显示跟踪标志的状态。
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```sql
DBCC TRACESTATUS ( [ [ trace# [ ,...n ] ] [ , ] [ -1 ] ] )   
[ WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>参数  
*跟踪 #*  
将要显示其状态的跟踪标志的编号。 如果*trace #*，和未指定-1，会显示为会话启用的所有跟踪标志。
  
*n*  
表示可指定多个跟踪标志的占位符。
  
-1  
显示全局启用的跟踪标志的状态。 如果没有指定-1 *trace #*，显示已启用的所有全局跟踪标志。
  
WITH NO_INFOMSGS  
取消严重级别从 0 到 10 的所有信息性消息。
  
## <a name="result-sets"></a>结果集  
下表对结果集中的信息进行了说明。
  
|列名|Description|  
|---|---|
|**跟踪标志**|跟踪标志的名称|  
|**状态**|表示跟踪标志是设置为 ON 还是 OFF，是全局启用的还是针对会话启用的。<br /><br /> 1 = ON<br /><br /> 0 = OFF|  
|**全局**|表示跟踪标志是否是全局设置的<br /><br /> 1 = True<br /><br /> 0 = False|  
|**会话**|表示跟踪标志是否是针对会话设置的<br /><br /> 1 = True<br /><br /> 0 = False|  
  
DBCC TRACESTATUS 将针对跟踪标志号和状态各返回一列。 这表示跟踪标志为 ON (1) 还是 OFF (0)。 列标题，为跟踪标志号是**全局跟踪标志**或**会话跟踪标志**，取决于是否检查全局或会话跟踪标志的状态。
  
## <a name="remarks"></a>注释  
在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，有两种跟踪标志：会话和全局。 会话跟踪标志对某个连接是有效的，只对该连接可见。 全局跟踪标志在服务器级别上进行设置，对服务器上的每一个连接都可见。
  
## <a name="permissions"></a>Permissions  
要求 **公共** 角色具有成员身份。
  
## <a name="examples"></a>示例  
以下示例显示当前全局启用的所有跟踪标志的状态。
  
```sql  
DBCC TRACESTATUS(-1);  
GO  
```  
  
以下示例显示跟踪标志 `2528` 和 `3205` 的状态。
  
```sql  
DBCC TRACESTATUS (2528, 3205);  
GO  
```  
  
以下示例显示跟踪标志 `3205` 是否是全局启用的。
  
```sql  
DBCC TRACESTATUS (3205, -1);  
GO  
```  
  
以下示例列出针对当前会话启用的所有跟踪标志。
  
```sql  
DBCC TRACESTATUS();  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
[DBCC (Transact-SQL)](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[DBCC TRACEOFF (Transact-SQL)](../../t-sql/database-console-commands/dbcc-traceoff-transact-sql.md)  
[DBCC TRACEON (Transact-SQL)](../../t-sql/database-console-commands/dbcc-traceon-transact-sql.md)  
[跟踪标志 (Transact-SQL)](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)
  
  

