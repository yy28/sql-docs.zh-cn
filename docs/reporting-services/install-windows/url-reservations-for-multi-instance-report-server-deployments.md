---
title: "多实例的 URL 保留项报告服务器部署 |Microsoft 文档"
ms.custom: 
ms.date: 05/18/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- URL reservations
ms.assetid: f67c83c0-1f74-42bb-bfc1-e50c38152d3d
caps.latest.revision: 7
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: e046d1afc8cc2f774e56f70ac9448e9ba9660cbb
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---
# <a name="url-reservations-for-multi-instance-report-server-deployments"></a>多实例报表服务器部署的 URL 保留项
  如果将多个 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 实例安装在同一台计算机上，则必须考虑如何为每个实例定义 URL 保留项。 在每个实例中，报表服务器 Web 服务和 [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] 都必须至少有一个 URL 保留项。 整组保留项在 HTTP.SYS 中必须保持唯一。  
  
 在 URL 注册（发生在服务启动时）过程中会检测 URL 是否重复。 如果您创建的 URL 保留项不唯一，那么，直到启动服务时，才会检测到名称冲突。 因此，请确保遵循命名约定或规则以确保所有的值保持唯一。  
  
## <a name="default-naming-conventions"></a>默认的命名约定  
 可以将 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安装到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 命名实例中。 当您在命名实例中安装或配置报表服务器时，实例名称会自动包括在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 提供的默认 URL 保留项中的虚拟目录中。 下表显示了默认实例和命名实例的 URL 保留项。  
  
|SQL Server 实例|默认 URL 保留项|  
|-------------------------|-----------------------------|  
|默认实例 (MSSQLServer)|`http://+:80/reportserver`|  
|命名实例 (MynamedInstance)|`http://+:80/reportserver_MyNamedInstance`|  
  
 对于命名实例，虚拟目录中包括实例名称。 默认实例和命名实例在同一个端口上侦听，但是唯一的虚拟目录名称确定了请求将由哪个报表服务器获取。  
  
 建议的最佳实践是使用虚拟目录名称来区分报表服务器实例， 这样可在 URL 和目标实例之间提供清楚的对应关系，并确保应用程序名称在整个系统中保持唯一。  
  
## <a name="custom-naming-conventions"></a>自定义命名约定  
 尽管建议使用实例名称，但是您可以使用 URL 语法和自己的命名约定来满足 URL 保留项的唯一名称约束。 下面的示例说明了用来为每个实例创建唯一 URL 的不同方法。  
  
|报表服务器的默认实例 (MSSQLSERVER)|ReportServer_MyNamedInstance|唯一性|  
|----------------------------------------------------|-----------------------------------|----------------|  
|`http://+:80/reportserver`|`http://+:8888/reportserver`|每个实例都在一个不同的端口上侦听。|  
|`http://www.contoso.com/reportserver`|`http://SRVR-46/reportserver`|每个实例都对应不同的服务器名称（完全限定域名和计算机名称）。|  
  
## <a name="uniqueness-requirements"></a>唯一性要求  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 使用的基础技术对于唯一名称施加了一定的要求。 HTTP.SYS 要求其存储库中的所有 URL 保持唯一。 您可以通过改变端口、主机名或虚拟目录名称来创建唯一的 URL。 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 要求同一个进程内的应用程序标识保持唯一。 此要求会影响虚拟目录名称。 它规定您不能在同一个报表服务器实例中复制虚拟目录名称。  
  
## <a name="see-also"></a>另请参阅  
 [配置报表服务器 Url &#40;SSRS 配置管理器 &#41;](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)   
 [配置 URL &#40;SSRS 配置管理器 &#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)  
  
  

