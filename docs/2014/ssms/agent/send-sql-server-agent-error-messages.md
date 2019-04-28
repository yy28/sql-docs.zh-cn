---
title: 发送 SQL Server 代理错误消息 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- messages [SQL Server], SQL Server Agent
- sending messages
- SQL Server Agent, errors
- errors [SQL Server Agent]
ms.assetid: 2597d0d7-951a-48cf-989f-abb67b9fdb36
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c1aa0faafc6fb1cca693fe58665c7344db84c9f1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62666784"
---
# <a name="send-sql-server-agent-error-messages"></a>Send SQL Server Agent Error Messages
  本主题介绍如何配置 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理以使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中通过 net send 的方式来发送其错误消息。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [限制和局限](#Restrictions)  
  
     [安全性](#Security)  
  
-   [使用 SQL Server Management Studio 发送 SQL Server 代理错误消息](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Restrictions"></a> 限制和局限  
  
-   “对象资源管理器”仅在您拥有使用权限时才显示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理节点。  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows Messenger 服务必须正在运行，才能接收 net send 事件。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，必须将 **代理配置为使用** sysadmin [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]固定服务器角色的成员帐户的凭据，才能执行其功能。 该帐户必须拥有以下 Windows 权限：  
  
-   以服务身份登录 (SeServiceLogonRight)  
  
-   替换进程级别标记 (SeAssignPrimaryTokenPrivilege)  
  
-   跳过遍历检查 (SeChangeNotifyPrivilege)  
  
-   调整进程的内存配额 (SeIncreaseQuotaPrivilege)  
  
 有关所需的 Windows 权限的详细信息[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理服务帐户，请参阅[为 SQL Server 代理服务选择帐户](select-an-account-for-the-sql-server-agent-service.md)和[配置 Windows 服务帐户和权限](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-send-sql-server-agent-error-messages"></a>发送 SQL Server 代理错误消息  
  
1.  在 **“对象资源管理器”** 中，单击加号以展开包含要通过 net send 从其发送错误消息的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理错误日志的服务器。  
  
2.  右键单击“SQL Server 代理”，然后选择“属性”。  
  
3.  在中**SQL Server 代理属性-**_server_name_对话框中的**错误日志**上**常规**页上，键入用户名称或你想要发送错误的计算机名称中的消息**Net send 收件人**框。  
  
4.  单击“确定” 。  
  
  
