---
title: MSSQLSERVER_17300 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 17300 (Database Engine error)
ms.assetid: c1d6bfb6-28af-4df6-8087-25807602d282
caps.latest.revision: 18
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 471156345c294b8ee6a6e446273eae923e19bb88
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="mssqlserver17300"></a>MSSQLSERVER_17300
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|17300|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|PROC_OUT_OF_SYSTASK_SESSIONS|  
|消息正文|SQL Server 无法运行新的系统任务，原因是内存不足或配置的会话数超过了服务器允许的最大数。 请查看服务器是否有足够的内存。 请使用 sp_configure 以及选项 '用户连接' 查看允许的最大用户连接数。 请使用 sys.dm_exec_sessions 检查当前会话数，包括用户进程。|  
  
## <a name="explanation"></a>解释  
尝试运行新系统任务失败，因为系统内存不足或超出了服务器中配置的会话数。  
  
## <a name="user-action"></a>用户操作  
查看服务器是否有足够的内存。 使用 sys.dm_exec_sessions 查看当前的系统任务数，然后使用 sp_configure 查看配置的最大用户连接值。  
  
根据需要执行以下任务：  
  
-   向服务器添加更多内存。  
  
-   终止一个或多个会话。  
  
-   增大服务器所允许的最大用户连接数。  
  
## <a name="see-also"></a>另请参阅  
[sp_configure (Transact-SQL)](~/relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
[服务器配置选项 (SQL Server)](~/database-engine/configure-windows/server-configuration-options-sql-server.md)  
[sys.dm_exec_sessions (Transact-SQL)](~/relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)  
[配置 user connections 服务器配置选项](~/database-engine/configure-windows/configure-the-user-connections-server-configuration-option.md)  
[KILL (Transact-SQL)](~/t-sql/language-elements/kill-transact-sql.md)  
  
