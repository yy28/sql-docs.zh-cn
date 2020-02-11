---
title: 设置 SQL Server 代理服务的 SQL Server 别名（SQL Server Management Studio） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- aliases [SQL Server], creating
- SQL Server Agent, aliases
ms.assetid: 02d6295d-ab52-44f0-8f1b-f3910a507d8f
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 752796caafa86ece1b471beb25a77ea381497409
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "62774386"
---
# <a name="set-a-sql-server-alias-for-the-sql-server-agent-service-sql-server-management-studio"></a>Set a SQL Server Alias for the SQL Server Agent Service (SQL Server Management Studio)
  本主题介绍如何通过使用[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../includes/ssde-md.md)] [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]设置用于连接到的代理的别名。 默认情况下， [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 代理服务将通过命名管道，使用无需额外客户端配置的动态服务器名称连接到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的实例。 如果当前使用的不是默认网络传输或连接的是侦听备用命名管道的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例，则需要配置服务器连接别名。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [限制和局限](#Restrictions)  
  
     [安全性](#Security)  
  
-   [使用 SQL Server Management Studio 设置 SQL Server 代理服务的 SQL Server 别名](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Restrictions"></a> 限制和局限  
  
-   
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 必须选择引用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]本地实例的别名，代理才能正常工作。  
  
-   “对象资源管理器”仅在您拥有使用权限时才显示 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 代理节点。  
  
###  <a name="Security"></a> Security  
  
####  <a name="Permissions"></a> 权限  
 在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中，必须将 **代理配置为使用** sysadmin [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]固定服务器角色的成员帐户的凭据，才能执行其功能。 该帐户必须拥有以下 Windows 权限：  
  
-   以服务身份登录 (SeServiceLogonRight)  
  
-   替换进程级别标记 (SeAssignPrimaryTokenPrivilege)  
  
-   跳过遍历检查 (SeChangeNotifyPrivilege)  
  
-   调整进程的内存配额 (SeIncreaseQuotaPrivilege)  
  
 有关[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]代理服务帐户所需的 Windows 权限的详细信息，请参阅为[SQL Server 代理服务选择帐户](../ssms/agent/select-an-account-for-the-sql-server-agent-service.md)和[配置 Windows 服务帐户和权限](configure-windows/configure-windows-service-accounts-and-permissions.md)。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-set-a-sql-server-alias-for-the-sql-server-agent-service"></a>为 SQL Server 代理服务设置 SQL Server 别名  
  
1.  在 **对象资源管理器**中，连接到 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 实例，再展开该实例。  
  
2.  右键单击“SQL Server 代理”****，然后单击“属性”****。  
  
3.  在 " **SQL Server 代理属性**"_server_name_ "对话框中的"**选择页**"下，选择"**连接**"，然后  
  
4.  在 **“本地主机服务器别名”** 框中，键入 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 代理应连接到的服务器别名的类型。  
  
5.  单击“确定”。   
  
  
