---
title: 启动、停止或暂停 SQL Server 代理服务 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQL Server Agent, starting
- SQL Server Agent, pausing
- SQL Server Agent, stopping
ms.assetid: c95a9759-dd30-4ab6-9ab0-087bb3bfb97c
caps.latest.revision: 30
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 79b32b0cd24073bd08fe9b93fcb5ce79cb22b442
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36025639"
---
# <a name="start-stop-or-pause-the-sql-server-agent-service"></a>Start, Stop, or Pause the SQL Server Agent Service
  本主题说明如何在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]启动、停止或重新启动 SQL Server 代理服务。  
  
 您可以配置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理服务，使其在操作系统启动时自动启动，也可以在需要完成作业时手动启动。 您可以停止或暂停 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理服务以挂起作业、操作员通知和警报。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [限制和局限](#Restrictions)  
  
     [Security](#Security)  
  
-   [使用 SQL Server Management Studio 启动、停止或重新启动 SQL Server 代理服务](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Restrictions"></a> 限制和局限  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理必须作为服务运行，才能自动执行管理任务。 有关详细信息，请参阅 [Configure SQL Server Agent](configure-sql-server-agent.md)。  
  
-   “对象资源管理器”仅在您拥有使用权限时才显示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理节点。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，必须将 **代理配置为使用** sysadmin [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]固定服务器角色的成员帐户的凭据，才能执行其功能。 该帐户必须拥有以下 Windows 权限：  
  
-   以服务身份登录 (SeServiceLogonRight)  
  
-   替换进程级别标记 (SeAssignPrimaryTokenPrivilege)  
  
-   跳过遍历检查 (SeChangeNotifyPrivilege)  
  
-   调整进程的内存配额 (SeIncreaseQuotaPrivilege)  
  
 有关所需的 Windows 权限的详细信息[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理服务帐户，请参阅[为 SQL Server 代理服务选择帐户](select-an-account-for-the-sql-server-agent-service.md)和[配置 Windows 服务帐户和权限](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-start-stop-or-restart-the-sql-server-agent-service"></a>启动、停止或重新启动 SQL Server 代理服务  
  
1.  在 **“对象资源管理器”** 中，单击加号以展开要管理 SQL Server 代理服务的服务器。  
  
2.  右键单击“SQL Server 代理”，然后选择“启动”、“停止”或“重启”。  
  
3.  在 **“用户帐户控制”** 对话框中，请单击 **“是”**。  
  
4.  系统提示是否要执行该操作时，请单击 **“是”**。  
  
 有关详细信息，请参阅：  
  
-   [启动、停止、暂停、继续、重新启动数据库引擎、SQL Server 代理或 SQL Server Browser 服务](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)  
  
-   [自动启动 SQL Server 代理 (SQL Server Management Studio)](autostart-sql-server-agent-sql-server-management-studio.md)  
  
  