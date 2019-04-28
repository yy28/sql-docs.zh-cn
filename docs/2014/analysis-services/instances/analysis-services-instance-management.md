---
title: Analysis Services 实例管理 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 0455fa4f-b92d-4a8b-a8f0-f2a268a5c84e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0ad91ac53d2ff041c3da32fd9a609e67e8b9d1c1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62730827"
---
# <a name="analysis-services-instance-management"></a>Analysis Services 实例管理
  Analysis Services 的实例是作为操作系统服务运行的 `msmdsrv.exe` 可执行程序的副本。 每个实例完全独立于同一服务器上的其他实例，且有自己的配置设置、权限、端口、启动帐户、文件存储和服务器模式属性。  
  
 每个 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例都作为 Windows 服务 (Msmdsrv.exe) 在定义的登录帐户的安全上下文中运行。  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 默认实例的服务名称为 MSSQLServerOLAPService。  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的每个命名实例的服务名称为 MSOLAP$InstanceName。  
  
> [!NOTE]  
>  如果安装了 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的多个实例，则安装程序也会安装重定向程序服务，该服务与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服务进行了集成。 重定向程序服务负责将客户端定向到适当的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]命名实例。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服务始终在本地服务帐户的安全上下文中运行，本地服务帐户是 Windows 针对不访问本地计算机外部资源的服务而使用的受限的用户帐户。  
  
 多实例意味着您可以通过在相同的硬件上安装多个服务器实例来进行扩展。 尤其对于 Analysis Services，这还意味着可以通过在相同服务器上安装多个实例（每个实例都配置为在特定模型下运行），从而支持不同的服务器模式。  
  
 服务器模式是一个服务器属性，用于确定哪些存储和内存体系结构用于此实例。 在多维模式下运行的服务器使用为多维数据集数据库和数据挖掘模型生成的资源管理层。 相比之下，表格服务器模式使用 xVelocity 内存中分析引擎 (VertiPaq) 和数据压缩来按要求聚合数据。  
  
 存储和内存体系结构之间的差异意味着 Analysis Services 的单个实例将运行表格数据库或多维数据库，但不同时运行这两个数据库。 服务器模式属性确定在实例上运行哪种类型的数据库。  
  
 在安装过程中，当您指定将在服务器上运行的数据库类型时设置服务器模式。 若要支持所有可用模式，您可以安装多个 Analysis Services 实例，每个实例部署在与您正要生成的项目相对应的服务器模式中。  
  
 通常，大多数必须执行的管理任务都不会根据模式发生改变。 作为 Analysis Services 系统管理员，您可以使用相同的过程和脚本来管理网络上的任何 Analysis Services 实例，而不必考虑该实例是如何安装的。  
  
> [!NOTE]  
>  PowerPivot for SharePoint 是例外情况。 针对 PowerPivot 部署进行服务器管理始终需要在 SharePoint 场的环境中进行。 PowerPivot 与其他服务器模式不同，因为它始终为单个实例且始终通过 SharePoint 管理中心或 PowerPivot 配置工具进行管理。 尽管它可能连接到 SQL Server Management Studio 或 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中的 PowerPivot for SharePoint，但并不推荐这样做。 SharePoint 场包括可同步服务器状态和监视服务器可用性的基础架构。 使用其他工具可能干扰这些操作。 有关 PowerPivot 服务器管理的详细信息，请参阅[PowerPivot for SharePoint &#40;SSAS&#41;](../power-pivot-sharepoint/power-pivot-for-sharepoint-ssas.md)。  
  
## <a name="in-this-section"></a>本节内容  
  
|链接|任务说明|  
|----------|----------------------|  
|[安装后配置 (Analysis Services)](post-install-configuration-analysis-services.md)|描述完成或修改 Analysis 的安装所必需的任务和可选任务。|  
|[连接到 Analysis Services](connect-to-analysis-services.md)|描述用于建立或清除连接的连接字符串属性、客户端库、身份验证方法和步骤。|  
|[监视 Analysis Services 实例](monitor-an-analysis-services-instance.md)|说明用于监视服务器实例的工具和技术，包括如何使用性能监视器和 SQL Server Profiler。|  
|[在 Analysis Services 中编写管理任务脚本](../script-administrative-tasks-in-analysis-services.md)|解释如何自动执行多个管理任务，包括处理。|  
|[Analysis Services Multiidimensional 的全球化方案](../globalization-scenarios-for-analysis-services-multiidimensional.md)|解释语言和排序规则支持、更改两个属性的步骤以及设置和测试语言和排序规则行为的提示。|  
|[Analysis Services 中的日志操作](log-operations-in-analysis-services.md)|描述日志并解释如何配置它们。|  
  
## <a name="see-also"></a>请参阅  
 [比较表格和多维解决方案 (SSAS)](../comparing-tabular-and-multidimensional-solutions-ssas.md)   
 [PowerPivot 配置工具](../power-pivot-sharepoint/power-pivot-configuration-tools.md)   
 [在管理中心的 PowerPivot 服务器管理和配置](../power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration.md)   
 [确定 Analysis Services 实例的服务器模式](determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  
