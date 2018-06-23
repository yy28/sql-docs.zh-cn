---
title: 管理服务的安全要求 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQL Server Agent service, security
- services [SQL Server], security
- SQL Server services, security
- WMI Providers [SQL Server]
- server configuration [SQL Server]
- security [SQL Server], services
- services [SQL Server], WMI
ms.assetid: 1874a317-ddb2-425d-98d9-b53e1be6fc6a
caps.latest.revision: 27
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 1d6e5ad2e6afb25be29ba5ab7fd22ea6cfb25145
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36129513"
---
# <a name="security-requirements-for-managing-services"></a>管理服务的安全要求
  若要管理 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理服务，请使用 SQL Server 配置管理器或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。 使用群集管理器管理群集服务器上的服务。  
  
 若要管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务并设置服务器配置选项，您必须是 **serveradmin** 固定服务器角色或 **sysadmin** 固定服务器角色的成员。 Windows 管理员  组的成员可以启动和停止服务，配置 Windows 提供的服务器选项。  
  
> [!NOTE]  
>  必须使用正确的域、文件系统和注册表权限配置服务使用的帐户，才能正确操作。 有关所需权限的信息，请参阅 [配置 Windows 服务帐户和权限](configure-windows-service-accounts-and-permissions.md)。  
  
## <a name="windows-management-instrumentation"></a>Windows Management Instrumentation  
 SQL Server 配置管理器和 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 使用 Windows Management Instrumentation (WMI) 显示和修改某些服务器属性。 若要管理服务并获取服务状态，用户必须具有访问 WMI 对象的权限。 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，下列服务器属性页使用 WMI：  
  
-   自动启动服务  
  
-   引导参数  
  
-   Security  
  
-   杂项服务器设置  
  
## <a name="related-tasks"></a>Related Tasks  
 [在 SQL Server 工具中将 WMI 配置为显示服务器状态](../../ssms/configure-wmi-to-show-server-status-in-sql-server-tools.md)  
  
## <a name="related-content"></a>相关内容  
 [用于配置管理的 WMI 提供程序的概念](../../relational-databases/wmi-provider-configuration/wmi-provider-for-configuration-management.md)  
  
  