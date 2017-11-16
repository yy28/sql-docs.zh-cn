---
title: "SQL Server Management Studio for BI 简介 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL Server Management Studio for Integration Services
- SQL Server Management Studio for Reporting Services
- SQL Server Management Studio for Analysis Services
ms.assetid: ffaa77b7-03d0-4d7a-aa42-c5091a4f2ceb
caps.latest.revision: "5"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 626db0505010dc75499f1b14a4d5708e47c33550
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="introduction-to-sql-server-management-studio-for-business-intelligence"></a>SQL Server Management Studio for Business Intelligence 简介
若要访问、配置和管理 [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)]、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion_md.md)]和 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion_md.md)]，请使用 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull_md.md)]。 虽然这三种商业智能技术均依赖于 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull_md.md)]，但与每种技术关联的管理任务却略有不同。  
  
> [!NOTE]  
> 若要创建和修改 [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)]、 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion_md.md)]和 [!INCLUDE[ssISnoversion](../includes/ssisnoversion_md.md)] 解决方案，请使用 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull_md.md)]，而不是 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull_md.md)]。 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull_md.md)] 是一个基于 [!INCLUDE[msCoName](../includes/msconame_md.md)][!INCLUDE[vsprvs](../includes/vsprvs_md.md)]的开发环境。  
  
## <a name="managing-analysis-services-solutions-using-sql-server-management-studio"></a>使用 SQL Server Management Studio 管理 Analysis Services 解决方案  
[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull_md.md)] 可以管理 [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)] 对象，如执行备份和处理对象。  
  
[!INCLUDE[ssManStudio](../includes/ssmanstudio_md.md)] 提供一个 [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)] 脚本项目，可在其中开发并保存使用多维表达式 (MDX)、数据挖掘扩展插件 (DMX) 和 XML for Analysis (XMLA) 编写的脚本。 可以使用 [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)] 脚本项目在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)] 实例中执行管理任务或重新创建对象（如数据库和多维数据集）。 例如，可以在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)] 脚本项目中开发一个 XMLA 脚本，以直接在现有 [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)] 实例中创建新的对象。 可以将 [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)] 脚本项目保存为解决方案的一部分，以及与源代码管理集成在一起。  
  
有关如何使用 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull_md.md)]的详细信息，请参阅 [使用 SQL Server Management Studio 进行开发和实现](http://msdn.microsoft.com/en-us/c4f5a06b-e2e4-4660-a3a8-6fd356742c02)  
  
## <a name="managing-integration-services-solutions-using-sql-server-management-studio"></a>使用 SQL Server Management Studio 管理 Integration Services 解决方案  
[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull_md.md)] 可以使用 [!INCLUDE[ssISnoversion](../includes/ssisnoversion_md.md)] 服务管理包并监视正在运行的包。 还可以使用 [!INCLUDE[ssManStudio](../includes/ssmanstudio_md.md)] 将包组织到文件夹中、运行包、导入和导出包、迁移 Data Transformation Services (DTS) 包以及升级 [!INCLUDE[ssISnoversion](../includes/ssisnoversion_md.md)] 包。  
  
## <a name="managing-reporting-services-projects-using-sql-server-management-studio"></a>使用 SQL Server Management Studio 管理 Reporting Services 项目  
可以使用 SQL Server Management Studio 启用 Reporting Services 功能、管理服务器和数据库以及管理角色和作业。  
  
可通过使用“共享计划”文件夹来管理共享计划以及管理报表服务器数据库（ReportServer、ReportServerTempdb）。 在将报表服务器数据库移动到新的或不同的 SQL Server 数据库引擎（[!INCLUDE[ssNoVersion](../includes/ssnoversion_md.md)] [!INCLUDE[ssDE](../includes/ssde_md.md)]）时，还可以在 Master 系统数据库中创建 RSExecRole。 有关这些任务的详细信息，请参阅以下主题：  
  
-   [Management Studio 操作指南主题](http://msdn.microsoft.com/en-us/60685458-9108-47bf-820a-5e7db454d408)  
  
-   [管理报表服务器数据库](http://msdn.microsoft.com/en-us/97b2e1b5-3869-4766-97b9-9bf206b52262)  
  
-   [如何创建 RSExecRole](http://msdn.microsoft.com/en-us/7ac17341-df7e-4401-870e-652caa2859c0)  
  
也可以通过以下方法来管理服务器：启用并配置各种功能、设置服务器默认设置以及管理角色和作业。 有关这些任务的详细信息，请参阅以下主题：  
  
-   [如何设置报表服务器属性 (Management Studio)](http://msdn.microsoft.com/en-us/1ed0f84b-b12a-4e49-b65c-a11a99f9093f)  
  
-   [如何创建、删除或修改角色 (Management Studio)](http://msdn.microsoft.com/en-us/3d1d56e6-a283-44a7-8417-36cb4d2c74d1)  
  
-   [启用和禁用 Reporting Services 的客户端打印](http://msdn.microsoft.com/en-us/0e709c96-7517-4547-8ef6-5632f8118524)  
  
## <a name="see-also"></a>另请参阅  
[使用 SQL Server Data Tools 进行开发和实现](http://msdn.microsoft.com/en-us/132ed779-3ec8-4734-9698-802116d1b017)  
[SQL Server Data Tools 中的 Reporting Services](http://msdn.microsoft.com/en-us/0903c7b2-ac59-45f1-b7d0-922ecd9d76f8)  
  
