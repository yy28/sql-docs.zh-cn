---
title: SQL Server Analysis Services 服务器管理 |Microsoft Docs
ms.date: 11/15/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 41c689b2dfb122b94204cfbb8d52f9f8e9a1a8fb
ms.sourcegitcommit: 50b60ea99551b688caf0aa2d897029b95e5c01f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/15/2018
ms.locfileid: "51700435"
---
# <a name="sql-server-analysis-services-server-management"></a>SQL Server Analysis Services 服务器管理
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]

Azure Analysis Services，请参阅[管理 Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-manage)。

  Analysis Services 的服务器实例，是一份**msmdsrv.exe**作为操作系统服务运行的可执行文件。 每个实例完全独立于同一服务器上的其他实例，且有自己的配置设置、权限、端口、启动帐户、文件存储和服务器模式属性。  
  
 每个实例作为 Windows 服务 （Msmdsrv.exe) 定义的登录帐户的安全上下文中运行。  
  
-   默认实例的服务名称为 MSSQLServerOLAPService。  
  
-   每个命名实例的服务名称为 MSOLAP$ InstanceName。  
  
> [!NOTE]  
>  如果安装了多个实例，安装程序还会安装一个重定向程序服务，它与集成[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]浏览器服务。 重定向程序服务负责将客户端定向到适当的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]命名实例。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服务始终在本地服务帐户的安全上下文中运行，本地服务帐户是 Windows 针对不访问本地计算机外部资源的服务而使用的受限的用户帐户。  
  
 多实例意味着您可以通过在相同的硬件上安装多个服务器实例来进行扩展。 尤其对于 Analysis Services，这还意味着可以通过在相同服务器上安装多个实例（每个实例都配置为在特定模型下运行），从而支持不同的服务器模式。  
  
 服务器模式是一个服务器属性，用于确定哪些存储和内存体系结构用于此实例。 在多维模式下运行的服务器使用为多维数据集数据库和数据挖掘模型生成的资源管理层。 相比之下，表格服务器模式使用 VertiPaq 内存中分析引擎和数据压缩来按要求聚合数据。  
  
 存储和内存体系结构之间的差异意味着 Analysis Services 的单个实例将运行表格数据库或多维数据库，但不同时运行这两个数据库。 服务器模式属性确定在实例上运行哪种类型的数据库。  
  
 在安装过程中，当您指定将在服务器上运行的数据库类型时设置服务器模式。 若要支持所有可用模式，您可以安装多个 Analysis Services 实例，每个实例部署在与您正要生成的项目相对应的服务器模式中。  
  
 通常，大多数必须执行的管理任务都不会根据模式发生改变。 作为 Analysis Services 系统管理员，您可以使用相同的过程和脚本来管理网络上的任何 Analysis Services 实例，而不必考虑该实例是如何安装的。  
  
> [!NOTE]  
>  [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 属于例外情况。 针对 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 部署进行服务器管理始终是在 SharePoint 场的上下文中进行的。 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 与其他服务器模式的不同之处在于，它始终为单实例模式，且始终通过 SharePoint 管理中心或 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 配置工具进行管理。 尽管可以在 SQL Server Management Studio 或 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 中连接到 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]for SharePoint，但这并不是理想做法。 SharePoint 场包括可同步服务器状态和监视服务器可用性的基础架构。 使用其他工具可能干扰这些操作。 有关详细信息[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]服务器管理，请参阅[Powerpivot for SharePoint ](../../analysis-services/power-pivot-sharepoint/power-pivot-for-sharepoint-ssas.md)。  
  
## <a name="common-server-management-topics"></a>常见的服务器管理主题  
  
|链接|任务说明|  
|----------|----------------------|  
|[安装后配置](../../analysis-services/instances/post-install-configuration-analysis-services.md)|描述完成或修改 Analysis 的安装所必需的任务和可选任务。|  
|[连接到 Analysis Services](../../analysis-services/instances/connect-to-analysis-services.md)|描述用于建立或清除连接的连接字符串属性、客户端库、身份验证方法和步骤。|  
|[监视 Analysis Services 实例](../../analysis-services/instances/monitor-an-analysis-services-instance.md)|说明用于监视服务器实例的工具和技术，包括如何使用性能监视器和 SQL Server Profiler。|  
|[高可用性和可伸缩性](../../analysis-services/instances/high-availability-and-scalability-in-analysis-services.md)|介绍了提高 Analysis Services 数据库可用性和可伸缩性的最常用方法。 |  
|[Analysis Services 的全球化方案](../../analysis-services/globalization-scenarios-for-analysis-services.md)|解释语言和排序规则支持、更改两个属性的步骤以及设置和测试语言和排序规则行为的提示。|  
|[Analysis Services 中的日志操作](../../analysis-services/instances/log-operations-in-analysis-services.md)|描述日志并解释如何配置它们。|  
  
  
## <a name="see-also"></a>请参阅  
 [比较表格和多维解决方案 ](../../analysis-services/comparing-tabular-and-multidimensional-solutions-ssas.md)   
 [确定 Analysis Services 实例的服务器模式](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  
