---
title: 设置用于全文筛选器后台程序启动器的服务帐户 | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- full-text search [SQL Server], FDHOST Launcher (MSSQLFDLauncher) service account
- FDHOST Launcher (MSSQLFDLauncher) [SQL Server]
ms.assetid: 3ab1d101-7ae0-488f-9b57-468e2517b737
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 8f327cefbb916bf83f695db40a1d3c3025b7a5d2
ms.sourcegitcommit: 45a9d7ffc99502c73f08cb937cbe9e89d9412397
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/22/2019
ms.locfileid: "66010939"
---
# <a name="set-the-service-account-for-the-full-text-filter-daemon-launcher"></a>设置用于全文筛选器后台程序启动器的服务帐户
  本主题介绍如何使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器为 SQL 全文筛选器后台程序启动器服务 (MSSQLFDLauncher) 设置服务帐户。 全文搜索 ssNoVersionto 将使用 SQL 全文筛选器后台程序启动器服务来启动筛选器后台程序主机进程，此进程用于处理全文搜索筛选和断字。 必须运行此服务才能使用全文搜索。  
  
 SQL 全文筛选器后台程序启动器服务是可识别实例的服务，它与特定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例相关联。 SQL 全文筛选器后台程序启动器服务将服务帐户信息传播到每个筛选器后台程序主机进程。  
  
  
##  <a name="setting"></a> 设置服务帐户  
  
#### <a name="to-set-the-sql-full-text-filter-daemon-launcher-service-account-for-full-text-search"></a>为全文搜索设置 SQL 全文筛选器后台程序启动器服务帐户  
  
1.  在 **“开始”** 菜单中，依次指向 **“所有程序”**、 [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]、 **“配置工具”**，然后单击 **“SQL Server 配置管理器”**。  
  
2.  在中**SQL Server 配置管理器**，单击**SQL Server Services**，右键单击**SQL 全文筛选器后台程序启动器 (*`instance name`*)**，然后单击**属性**。  
  
3.  单击此对话框的“登录”选项卡，选择或输入用于运行由 SQL 全文筛选器后台程序启动器服务创建的每个进程的帐户。  
  
4.  关闭此对话框之后，单击“重新启动”以重新启动 SQL 全文筛选器后台程序启动器服务。  
  
  
##  <a name="error"></a> 如果 SQL 全文筛选器后台程序启动器服务未启动  
 如果 SQL 全文筛选器后台程序启动器服务未启动，可能是由以下一种或多种情况引起的：  
  
-   与 SQL 全文筛选器后台程序启动器服务帐户关联的密码已过期。  
  
     如果对 SQL 全文筛选器后台程序启动器服务使用本地用户帐户并且您的密码已过期，您需要执行以下操作：  
  
    1.  为此帐户设置一个新的 Windows 密码。  
  
    2.  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器中，更新 SQL 全文筛选器后台程序启动器服务以便使用新密码。  
  
-   此服务帐户的用户帐户或密码不正确。  
  
     SQL 全文筛选器后台程序启动器服务可能试图以错误的用户帐户和密码登录。 按照上述过程，验证该服务的用户帐户是否发生了更改。  
  
-   用来登录到该服务的帐户没有相应的特权。  
  
     您使用的帐户可能对安装该服务器实例的计算机不具有登录特权。 请验证您用于登录的帐户是否对相应本地计算机具有用户权限。  
  
-   相同命名管道的另一个实例已在运行。  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务充当 SQL 全文筛选器后台程序启动器服务客户端的命名管道服务器。 如果在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 启动之前另一进程便已创建该命名管道，则将在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误日志和 Windows 事件日志中记录一条错误，并且将无法使用全文搜索。  确定哪个进程或应用程序在试图使用该命名管道并停止相应的应用程序。  
  
-   未正确地配置 SQL 全文筛选器后台程序启动器服务。  
  
     该服务在本地计算机上的配置可能不正确。  
  
     如果本地计算机已禁用命名管道功能，或者已将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置为使用非默认命名管道，则 SQL 全文筛选器后台程序启动器服务可能无法启动。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务组没有启动 SQL 全文筛选器后台程序启动器服务的权限。  
  
     在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的安装过程中，向 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务组授予了管理、查询和启动 SQL 全文筛选器后台程序启动器服务的默认权限。 如果在安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 后删除了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务组对 SQL 全文筛选器后台程序启动器服务帐户的权限，则 SQL 全文筛选器后台程序启动器服务将无法启动，并且全文搜索也将被禁用。 请确保 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务组拥有对 SQL 全文筛选器后台程序启动器服务帐户的权限。  
  
  
## <a name="see-also"></a>请参阅  
 [管理服务操作指南主题（SQL Server 配置管理器）](../../database-engine/managing-services-how-to-topics-sql-server-configuration-manager.md)  
 [升级全文搜索](upgrade-full-text-search.md)  
  
  
