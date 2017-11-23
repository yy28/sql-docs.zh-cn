---
title: "WMI Provider for Configuration Management Concepts |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: wmi
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- WMI Provider for Configuration Management
- SQL Server WMI Provider
- configuration management [WMI]
- WMI Provider for Configuration Management, about WMI Provider for Configuration Management
ms.assetid: 7e41db24-b915-4eb8-a1d6-e6948ee915b7
caps.latest.revision: "24"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5e7c3fcda1c2e3a8e210dc0f4fa5d2e1018bd83d
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="wmi-provider-for-configuration-management"></a>配置管理的 WMI 提供程序
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]WMI 提供程序是与一起使用的已发布的层[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]配置管理器管理单元用于接[!INCLUDE[msCoName](../../includes/msconame-md.md)]管理控制台 (MMC) 和[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager。 它提供了一种统一的方式，用于与管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器所请求注册表操作的 API 调用进行连接，并可对选定的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务提供增强的控制和操作。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] WMI 提供程序是一个 DLL 和一个 MOF 文件，这些文件由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序自动编译。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] WMI 提供程序包含一组的对象类用于控制[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]服务使用以下方法：  
  
-   可以在其中嵌入 Windows 查询语言 (WQL) 的脚本语言，如 VBScript、[!INCLUDE[jsprjscript](../../includes/jsprjscript-md.md)] 或 Perl。  
  
-   SMO 托管代码程序中的 <xref:Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer> 对象。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器或带有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] WMI 提供程序管理单元的 MMC。  
  
## <a name="using-a-script-language"></a>使用脚本语言  
 使用脚本语言具有以下优点：  
  
-   无需开发环境。  
  
-   支持脚本语言的文件可以广泛地使用。  
  
 除了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] WMI 提供程序之外，脚本还可以与其他 WMI 提供程序配合使用。 域管理员可以使用脚本在网络中的多台计算机上设置服务、网络设置和别名设置。  
  
 本节将更为细致地介绍如何通过脚本访问用于配置管理的 WMI 提供程序。  
  
## <a name="using-the-smo-managedcomputer-object"></a>使用 SMO ManagedComputer 对象  
 <xref:Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer> 对象是一个托管 SMO 对象，它提供对用于配置管理的 WMI 提供程序的访问。 通过使用 SMO 程序，可使用 <xref:Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer> 对象查看和修改 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务、网络设置和别名设置。 有关详细信息，请参阅[管理服务和通过使用 WMI 提供程序的网络设置](../../relational-databases/server-management-objects-smo/tasks/managing-services-and-network-settings-by-using-wmi-provider.md)。  
  
## <a name="using-the-microsoft-management-console-or-sql-server-configuration-manager"></a>使用 Microsoft 管理控制台或 SQL Server 配置管理器  
 与脚本语言或托管代码程序相反，Microsoft 管理控制台 (MMC) 提供一个用于管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务的接口。 可使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理 MMC 管理单元停止和启动服务，以及更改服务帐户。  
  
 此外，还可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务、客户端和服务器协议以及服务器别名。  
  
## <a name="see-also"></a>另请参阅  
 [了解的 WMI 提供程序的配置管理](../../relational-databases/wmi-provider-configuration/understanding-the-wmi-provider-for-configuration-management.md)   
 [使用的 WMI 提供程序的配置管理](../../relational-databases/wmi-provider-configuration/working-with-the-wmi-provider-for-configuration-management.md)   
 [使用 WQL 和脚本编写语言使用的 WMI 提供程序的配置管理](../../relational-databases/wmi-provider-configuration/using-wql-and-scripting-languages-with-the-wmi-provider.md)  
  
  
