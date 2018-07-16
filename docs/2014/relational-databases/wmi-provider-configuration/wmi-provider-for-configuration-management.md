---
title: 配置管理概念的 WMI 提供程序 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- WMI Provider for Configuration Management
- SQL Server WMI Provider
- configuration management [WMI]
- WMI Provider for Configuration Management, about WMI Provider for Configuration Management
ms.assetid: 7e41db24-b915-4eb8-a1d6-e6948ee915b7
caps.latest.revision: 23
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 5e19f7bda872dbf29c018599430f40bfd353ae42
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37290283"
---
# <a name="wmi-provider-for-configuration-management-concepts"></a>用于配置管理的 WMI 提供程序的概念
  WMI 提供程序是与一起使用的已发布的层[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]配置管理器管理单元[!INCLUDE[msCoName](../../includes/msconame-md.md)]管理控制台 (MMC) 和[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]配置管理器。 它提供了一种统一的方式，用于与管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器所请求注册表操作的 API 调用进行连接，并可对选定的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务提供增强的控制和操作。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] WMI 提供程序是一个 DLL 和一个 MOF 文件，这些文件由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序自动编译。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] WMI 提供程序包含一组用于控制对象类[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]服务使用以下方法：  
  
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
 <xref:Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer> 对象是一个托管 SMO 对象，它提供对用于配置管理的 WMI 提供程序的访问。 通过使用 SMO 程序，可使用 <xref:Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer> 对象查看和修改 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务、网络设置和别名设置。 有关详细信息，请参阅[管理服务和通过使用 WMI 提供程序的网络设置](../server-management-objects-smo/tasks/managing-services-and-network-settings-by-using-wmi-provider.md)。  
  
## <a name="using-the-microsoft-management-console-or-sql-server-configuration-manager"></a>使用 Microsoft 管理控制台或 SQL Server 配置管理器  
 与脚本语言或托管代码程序相反，Microsoft 管理控制台 (MMC) 提供一个用于管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务的接口。 可使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理 MMC 管理单元停止和启动服务，以及更改服务帐户。  
  
 此外，还可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务、客户端和服务器协议以及服务器别名。  
  
## <a name="see-also"></a>请参阅  
 [了解配置管理的 WMI 提供程序](understanding-the-wmi-provider-for-configuration-management.md)   
 [使用配置管理的 WMI 提供程序](working-with-the-wmi-provider-for-configuration-management.md)   
 [将 WQL 和脚本语言用于配置管理的 WMI 提供程序](using-wql-and-scripting-languages-with-the-wmi-provider.md)  
  
  
