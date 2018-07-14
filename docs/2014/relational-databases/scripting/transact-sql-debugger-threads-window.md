---
title: “线程”窗口 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- vs.debug.threads
helpviewer_keywords:
- Threads Window [Transact-SQL]
ms.assetid: e153f619-0049-4162-9076-c24a454f3278
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3d80d45fe58e6778dd0caef18cdf067f4055da01
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37256119"
---
# <a name="threads-window"></a>“线程”窗口
  “线程”  窗口显示有关正在调试的 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查询编辑器会话使用的 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 线程的信息。 只有在调试模式下才可以显示此线程信息。  
  
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
  
## <a name="see-also"></a>请参阅  
 [Transact-SQL 调试器](transact-sql-debugger.md)   
 [Transact-SQL 调试器信息](transact-sql-debugger-information.md)   
 [sys.dm_os_threads (Transact-SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-threads-transact-sql)   
 [sys.sysprocesses (Transact-SQL)](/sql/relational-databases/system-compatibility-views/sys-sysprocesses-transact-sql)  
  
  
