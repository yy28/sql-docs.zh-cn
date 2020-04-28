---
title: 多实例报表服务器部署的 URL 保留项（SSRS Configuration Manager） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- URL reservations
ms.assetid: f67c83c0-1f74-42bb-bfc1-e50c38152d3d
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c91db169984bbb2969a8339ed20e8e6bc5b804b6
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "80380688"
---
# <a name="url-reservations-for-multi-instance-report-server-deployments--ssrs-configuration-manager"></a>多实例报表服务器部署的 URL 预留（SSRS 配置管理器）
  如果将多个 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 实例安装在同一台计算机上，则必须考虑如何为每个实例定义 URL 预留。 在每个实例中，报表服务器 Web 服务和报表管理器都必须至少有一个 URL 预留。 整组预留在 HTTP.SYS 中必须保持唯一。  
  
 在 URL 注册（发生在服务启动时）过程中会检测 URL 是否重复。 如果你创建的 URL 预留不唯一，那么，直到启动服务时，才会检测到名称冲突。 因此，请确保遵循命名约定或规则以确保所有的值保持唯一。  
  
## <a name="default-naming-conventions"></a>默认的命名约定  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安装到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 命名实例中。 当你在命名实例中安装或配置报表服务器时，实例名称会自动包括在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 提供的默认 URL 预留中的虚拟目录中。 下表显示了默认实例和命名实例的 URL 预留。  
  
|SQL Server 实例|默认 URL 预留|  
|-------------------------|-----------------------------|  
|默认实例 (MSSQLServer)|http://+:80/reportserver|  
|命名实例 (MynamedInstance)|http://+:80/reportserver_MyNamedInstance|  
  
 对于命名实例，虚拟目录中包括实例名称。 默认实例和命名实例在同一个端口上侦听，但是唯一的虚拟目录名称确定了请求将由哪个报表服务器获取。  
  
 建议的最佳实践是使用虚拟目录名称来区分报表服务器实例， 这样可在 URL 和目标实例之间提供清楚的对应关系，并确保应用程序名称在整个系统中保持唯一。  
  
## <a name="custom-naming-conventions"></a>自定义命名约定  
 尽管建议使用实例名称，但是你可以使用 URL 语法和自己的命名约定来满足 URL 预留的唯一名称约束。 下面的示例说明了用来为每个实例创建唯一 URL 的不同方法。  
  
|报表服务器的默认实例 (MSSQLSERVER)|ReportServer_MyNamedInstance|唯一性|  
|----------------------------------------------------|-----------------------------------|----------------|  
|http://+:80/reportserver|http://+:8888/reportserver|每个实例都在一个不同的端口上侦听。|  
|`http://www.contoso.com/reportserver`|`http://SRVR-46/reportserver`|每个实例都对应不同的服务器名称（完全限定域名和计算机名称）。|  
  
## <a name="uniqueness-requirements"></a>唯一性要求  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 使用的基础技术对于唯一名称施加了一定的要求。 HTTP.SYS 要求其存储库中的所有 URL 保持唯一。 您可以通过改变端口、主机名或虚拟目录名称来创建唯一的 URL。 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 要求同一个进程内的应用程序标识保持唯一。 此要求会影响虚拟目录名称。 它规定您不能在同一个报表服务器实例中复制虚拟目录名称。  
  
## <a name="see-also"></a>另请参阅  
 [配置报表服务器 URL（SSRS 配置管理器）](configure-report-server-urls-ssrs-configuration-manager.md)   
 [配置 URL（SSRS 配置管理器）](configure-a-url-ssrs-configuration-manager.md)  
  
  
