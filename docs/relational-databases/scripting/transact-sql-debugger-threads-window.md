---
title: "“线程”窗口 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- vs.debug.threads
helpviewer_keywords:
- Threads Window [Transact-SQL]
ms.assetid: e153f619-0049-4162-9076-c24a454f3278
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 50d5602a6bf16946b95e7baae0ffcc4181e38eca
ms.sourcegitcommit: a0aa5e611a0e6ebb74ac1e2f613e8916dc7a7617
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
# <a name="transact-sql-debugger---threads-window"></a>Transact-SQL 调试器 -“线程”窗口
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]“线程”窗口显示有关正在调试的 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查询编辑器会话使用的 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 线程的信息。 只有在调试模式下才可以显示此线程信息。  
  
## <a name="task-list"></a>任务列表  
 **访问“线程”窗口**  
  
-   在 **“调试”** 菜单上单击 **“窗口”**，然后单击 **“线程”**。  
  
## <a name="columns"></a>“列”  
 **ID**  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 调试器分配给该线程的唯一标识号。 从 sys.dm_os_threads 动态管理视图中选择某一行，即可找到有关此线程的详细信息。  
  
 如果当前未在轻型池模式下运行，则请选择满足以下条件的行：此行中 os_thread_id 列的值与 **ID** 列的值相匹配。 如果当前在轻型池模式下运行，则请选择满足以下条件的行：此行中 fiber_context_address 列的值与 **ID** 列的值相匹配。  
  
 **名称**  
 以 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 计算机名/实例名 [SPID] **格式显示有关**会话的信息。  
  
 **计算机名**  
 运行查询编辑器会话连接到的 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 实例的计算机的名称。  
  
 **InstanceName**  
 查询编辑器会话连接到的 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 实例的名称。  
  
 **[SPID]**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 会话进程 ID，用于唯一标识此会话。 通过在 sys.sysprocesses 视图中选择 spid 列中此 ID 值所在的行，可以获取有关此会话的更多信息。  
  
 **位置**  
 显示正在调试的查询编辑器会话使用的脚本文件的名称。  
  
 **Priority**  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 调试器不支持此功能。  
  
 **挂起**  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 调试器不支持此功能。  
  
## <a name="see-also"></a>另请参阅  
 [Transact-SQL 调试器](../../relational-databases/scripting/transact-sql-debugger.md)   
 [Transact-SQL 调试器信息](../../relational-databases/scripting/transact-sql-debugger-information.md)   
 [sys.dm_os_threads (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-os-threads-transact-sql.md)   
 [sys.sysprocesses (Transact-SQL)](../../relational-databases/system-compatibility-views/sys-sysprocesses-transact-sql.md)  
  
  
