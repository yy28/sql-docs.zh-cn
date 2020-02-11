---
title: 安装后配置（Analysis Services） |Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 7f4417b2-0efb-4361-a79e-fa56e43ee054
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6a339ee307ed7a10f2ff7d2b1ce51d2e2177ee37
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66079659"
---
# <a name="post-install-configuration-analysis-services"></a>安装后配置 (Analysis Services)
  安装 Analysis Services 后，需要进行进一步配置以使服务器正常运行并可供常规使用。 本节介绍完成安装后的附加任务。 根据连接要求，还可能需要配置身份验证（请参阅 [连接到 Analysis Services](connect-to-analysis-services.md)）。  
  
 您具有可供部署的数据库后，需要完成一些额外工作。 换句话说，您需要在数据库上配置角色成员身份以授予用户对数据的访问权限、设计数据库备份和恢复策略，以及确定是否需要预定处理工作负荷以定期刷新数据。 有关数据库部署和管理的详细信息，请访问以下链接：[多维模型数据库 (SSAS)](../multidimensional-models/multidimensional-model-databases-ssas.md)和[表格模型数据库（SSAS 表格）](../tabular-models/tabular-model-databases-ssas-tabular.md)。  
  
## <a name="instance-configuration"></a>Instance Configuration  
 Analysis Services 是可复制的服务，这意味着您可以在单个服务器上安装该服务的多个实例。 使用 SQL Server 安装程序将每个其他实例作为命名实例单独安装，并单独进行配置以实现预定用途。 例如，开发服务器可能运行网络流量记录器或将默认值用于数据存储，您可能在支持生产工作负荷的服务器上对这些值进行更改。 需要调整系统配置的另一示例是在由其他服务共享的硬件上安装 Analysis Services 实例。 在同一硬件上承载多个包含大量数据的应用程序时，您可能需要配置用于降低内存阈值的服务器属性，以优化所有应用程序之间的可用资源。  
  
## <a name="post-installation-tasks"></a>安装后任务  
  
|链接|任务说明|  
|----------|----------------------|  
|[配置 Windows 防火墙以允许 Analysis Services 访问](configure-the-windows-firewall-to-allow-analysis-services-access.md)|在 Windows 防火墙中创建入站规则，以便可以通过 Analysis Services 实例使用的 TCP 端口路由请求。 此任务是必需的。 在定义入站防火墙规则之前，任何人都无法从远程计算机访问 Analysis Services。|  
|[&#40;Analysis Services 授予服务器管理员权限&#41;](grant-server-admin-rights-to-an-analysis-services-instance.md)|在安装期间，您必须将至少一个用户帐户添加到 Analysis Services 实例的“管理员”角色。 很多例行服务器操作（如处理外部关系数据库的数据）需要管理权限。 使用本主题中的信息添加或修改“管理员”角色的成员身份。|  
|[&#40;Analysis Services 配置服务帐户&#41;](configure-service-accounts-analysis-services.md)|安装过程中，将设置 Analysis Services 服务帐户，并为之授予允许对可执行程序和数据库文件进行受控访问的适当权限。 安装之后，应考虑在执行其他任务时是否允许使用该服务帐户。 处理和查询工作负荷均可在该服务帐户下执行。 仅当该服务帐户具有适当权限时，这些操作才会成功。|  
|[在服务器组中注册 Analysis Services 实例](register-an-analysis-services-instance-in-a-server-group.md)|通过 SQL Server Management Studio (SSMS)，您可以创建服务器组来组织自己的 SQL Server 实例。 包含多个服务器实例的可扩展的部署更易于在服务器组中进行管理。 使用本主题中的信息将 Analysis Services 实例组织为 SSMS 中的组。|  
|[确定 Analysis Services 实例的服务器模式](determine-the-server-mode-of-an-analysis-services-instance.md)|在安装期间，您选择了确定在服务器上运行的模型类型（多维或表格）的服务器模式。 如果您不清楚服务器模式，请使用本主题中的信息来确定安装了哪种模式。|  
|[重命名 Analysis Services 实例](rename-an-analysis-services-instance.md)|描述性名称可以帮助您区分具有不同服务器模式的多个实例，或区分在您的组织中主要由部门或团队使用的各个实例。 如果您要将实例名称更改为便于管理安装的名称，请使用本主题中的信息了解如何进行更改。|  
  
## <a name="next-steps"></a>后续步骤  
 了解如何使用客户端库从 Microsoft 应用程序或自定义应用程序连接到 Analysis Services。 根据您的解决方案要求，您还可能需要为 Kerberos 身份验证配置服务。 必须跨域边界的连接将需要进行 HTTP 访问。 有关后续步骤的说明，请参阅 [Connect to Analysis Services](connect-to-analysis-services.md) 。  
  
## <a name="see-also"></a>另请参阅  
 [安装 SQL Server 2014](../../../2014/database-engine/install-windows/installation-for-sql-server.md)   
 [在多维和数据挖掘模式下安装 Analysis Services](../../sql-server/install/install-analysis-services-in-multidimensional-and-data-mining-mode.md)   
 [在表格模式下安装 Analysis Services](install-windows/install-analysis-services.md)   
 [PowerPivot for SharePoint 2013 安装](install-windows/install-analysis-services-in-power-pivot-mode.md)  
  
  
