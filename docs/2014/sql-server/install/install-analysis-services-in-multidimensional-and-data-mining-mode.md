---
title: 在多维和数据挖掘模式下安装 Analysis Services |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- installing Analysis Services, about installing Analysis Services
- installing Analysis Services
- SSAS, installing
- Analysis Services, installing
- SQL Server Analysis Services, installing
ms.assetid: 8a1f33e8-2bd6-4fb8-bd46-c86f2a067f60
author: heidisteen
ms.author: heidist
manager: craigg
ms.openlocfilehash: 002a4ce66108622ce5efcf33231edaed9cd1c99b
ms.sourcegitcommit: e914effe771a1ee323bb3653626cd4ba83d77308
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/04/2020
ms.locfileid: "78280834"
---
# <a name="install-analysis-services-in-multidimensional-and-data-mining-mode"></a>在多维和数据挖掘模式下安装 Analysis Services
  
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 为商业智能应用程序提供联机分析处理 (OLAP) 和数据挖掘功能。 在此版本中，在[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] *多维模式下*安装时，支持 OLAP 数据库和数据挖掘模型。 多维模式是 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 运行时所采用的三种服务器模式之一。 它是默认模式。 如果使用默认值安装 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]，则将获得运行多维数据库和数据挖掘模型的实例。  
  
 
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 是一种多实例功能，这意味着您可以在单个计算机上安装 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的多个实例，或者与早期版本并行运行 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的新实例。 服务器模式特定于实例。 使用其他模式要求安装服务器的其他实例。  
  
 您可以单独安装 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 或将其与其他组件一起安装。 如果只[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]安装了，则在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安装向导的 "功能选择" 页上选择 " **Analysis Services** " 时，将安装以下功能：  
  
-   用于运行 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库和数据挖掘模型的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服务器  
  
-   用于对源数据库进行 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据访问的数据访问接口  
  
-   SQL Server 配置管理器  
  
## <a name="choosing-additional-features"></a>选择其他功能  
 Analysis Services OLAP 和数据仓库解决方案将要求安装附加的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 组件，以便实现 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库的开发、部署和管理。 下列附加功能是许多典型用户应用场景的可选项：  
  
-   
  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]，用于创建和查看 Analysis Services 数据结构和数据挖掘模型。  
  
-   客户端工具连接组件，用于客户端与服务器之间通信的组件，包括用于 DB-Library、ODBC 和 OLE DB 的网络库。  
  
-   
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]，一组用于移动、复制和转换数据的图形化和可编程的对象。  
  
-   管理工具，包括 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 和复制监视器。  
  
## <a name="installation-tasks"></a>安装任务  
 安装任务包括以下内容：  
  
|链接|任务|  
|-----------|-----------|  
|[安装 SQL Server 2014 的硬件和软件要求](hardware-and-software-requirements-for-installing-sql-server.md)，并[配置 Windows 服务帐户和权限](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)。|在您运行安装程序前，请检查安装 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的先决条件，并确定将用于设置服务器的帐户。|  
|[从安装向导安装 SQL Server 2014 &#40;安装&#41;](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)。|运行 SQL Server 安装程序以便安装该软件。|  
|[配置 Windows 防火墙以允许 Analysis Services 访问](https://docs.microsoft.com/analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access)|在完成安装后，必须配置防火墙设置，以便允许与服务器的远程连接。|  
|[授权对对象和操作的访问 &#40;Analysis Services&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/authorizing-access-to-objects-and-operations-analysis-services)|访问 Analysis Services 数据库的用户必须对服务器上的至少一个数据库具有读取权限。|  
  
## <a name="related-content"></a>相关内容  
 其他安装程序内容可以在下列主题中找到：  
  
 [在表格模式下安装 Analysis Services](https://docs.microsoft.com/analysis-services/instances/install-windows/install-analysis-services)  
  
 [PowerPivot for SharePoint 2010 安装](../../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md)  
  
 [确定 Analysis Services 实例的服务器模式](https://docs.microsoft.com/analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance)  
  
 [SQL Server 数据挖掘外接程序](https://www.microsoft.com/download/details.aspx?id=35578)  
  
 默认情况下，不会将示例数据库、示例代码和客户端应用程序外接程序作为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序的一部分进行安装。 若要安装示例数据库和示例代码，请参阅 [CodePlex 网站](https://go.microsoft.com/fwlink/?LinkId=87843)。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server 2012 的各个版本支持的功能](https://go.microsoft.com/fwlink/?linkid=232473)   
 [语言和排序规则 &#40;Analysis Services&#41;](../../../2014/analysis-services/languages-and-collations-analysis-services.md)   
 [升级 Analysis Services](../../database-engine/install-windows/upgrade-analysis-services.md)  
  
  
