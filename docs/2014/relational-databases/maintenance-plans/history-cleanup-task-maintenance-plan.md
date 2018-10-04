---
title: “清除历史记录”任务（维护计划）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
f1_keywords:
- sql12.swb.maint.historycleanup.f1
helpviewer_keywords:
- History Cleanup Task dialog box
ms.assetid: 66bb6c39-958c-4053-a27f-b1118d2567f5
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 4a08c655b60feced8c3a116d2b5934647ec4e53b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48137279"
---
# <a name="history-cleanup-task-maintenance-plan"></a>“清除历史记录”任务（维护计划）
  使用 **“清除历史记录”** 对话框，可以放弃 msdb 数据库表中旧的历史信息。 此任务支持删除备份和还原历史记录、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理作业历史记录和维护计划历史记录。  
  
 此语句使用 **sp_purge_jobhistory** 和 **sp_delete_backuphistory** 语句。  
  
## <a name="uielement-list"></a>UIElement 列表  
 **连接**  
 选择执行此任务时使用的服务器连接。  
  
 **新建**  
 创建一个新的服务器连接，在执行此任务时使用。 本主题后面将介绍 **“新建连接”** 对话框。  
  
 **备份和还原历史记录**  
 当您希望还原数据库时，保留有关最近备份创建时间的记录可帮助 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 创建恢复计划。 保持期应当至少为完整数据库备份的频率。  
  
 **SQL Server 代理作业历史记录**  
 使用此历史记录有助于排除失败作业的故障，或者确定数据库操作发生的原因。  
  
 **维护计划历史记录**  
 使用此历史记录有助于排除失败的维护计划作业的故障，或者确定数据库操作发生的原因。  
  
 **删除历史数据，如果其保留时间超过**  
 指定要删除项的保留时间。  
  
 **查看 T-SQL**  
 根据所选选项，查看针对此任务的服务器执行的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句。  
  
> [!NOTE]  
>  当受影响的对象很多时，可能需要相当长的时间才可显示。  
  
## <a name="new-connection-dialog-box"></a>“新建连接”对话框  
 **连接名称**  
 输入新连接的名称。  
  
 **选择或输入服务器名称**  
 选择执行此任务时所要连接的服务器。  
  
 **“刷新”**  
 刷新可用服务器的列表。  
  
 **输入登录服务器所需的信息**  
 指定如何对服务器进行身份验证。  
  
 **使用 Windows 集成安全性**  
 使用 Microsoft Windows 身份验证连接到 SQL Server [!INCLUDE[ssDE](../../includes/ssde-md.md)] 实例。  
  
 **使用特定用户名和密码**  
 使用 SQL Server 身份验证连接到 SQL Server [!INCLUDE[ssDE](../../includes/ssde-md.md)] 实例。 此选项不可用。  
  
 **用户名**  
 提供一个在进行身份验证时要使用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名。 此选项不可用。  
  
 **密码**  
 提供一个在进行身份验证时要使用的密码。 此选项不可用。  
  
## <a name="see-also"></a>请参阅  
 [sp_purge_jobhistory (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-purge-jobhistory-transact-sql)   
 [sp_delete_backuphistory (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql)  
  
  
