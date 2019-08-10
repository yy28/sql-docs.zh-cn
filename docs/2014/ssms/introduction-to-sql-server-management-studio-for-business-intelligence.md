---
title: 商业智能 SQL Server Management Studio 简介 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Management Studio for Integration Services
- SQL Server Management Studio for Reporting Services
- SQL Server Management Studio for Analysis Services
ms.assetid: ffaa77b7-03d0-4d7a-aa42-c5091a4f2ceb
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3a914aeeae889189453b4f4e6f47ebfbcd0fc44c
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68892276"
---
# <a name="introduction-to-sql-server-management-studio-for-business-intelligence"></a>SQL Server Management Studio for Business Intelligence 简介
  若要访问、配置和管理 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]、[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 和 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]，请使用 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]。 虽然这三种商业智能技术均依赖于 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]，但与每种技术关联的管理任务却略有不同。  
  
> [!NOTE]  
>  若要创建和修改 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]、 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]和 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 解决方案，请使用 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]，而不是 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]。 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 是一个基于 [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[vsprvs](../includes/vsprvs-md.md)]的开发环境。  
  
## <a name="managing-analysis-services-solutions-using-sql-server-management-studio"></a>使用 SQL Server Management Studio 管理 Analysis Services 解决方案  
 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 可以管理 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 对象，如执行备份和处理对象。  
  
 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 提供一个 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 脚本项目，可在其中开发并保存使用多维表达式 (MDX)、数据挖掘扩展插件 (DMX) 和 XML for Analysis (XMLA) 编写的脚本。 可以使用 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 脚本项目在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例中执行管理任务或重新创建对象（如数据库和多维数据集）。 例如，可以在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 脚本项目中开发一个 XMLA 脚本，以直接在现有 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例中创建新的对象。 可以将 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 脚本项目保存为解决方案的一部分，以及与源代码管理集成在一起。  
  
 有关如何使用[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]的详细信息, 请参阅[SQL Server Management Studio 中的 Analysis Services 脚本项目](https://docs.microsoft.com/analysis-services/instances/analysis-services-scripts-project-in-sql-server-management-studio)。  
  
## <a name="managing-integration-services-solutions-using-sql-server-management-studio"></a>使用 SQL Server Management Studio 管理 Integration Services 解决方案  
 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 可以使用 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务管理包并监视正在运行的包。 还可以使用 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 将包组织到文件夹中、运行包、导入和导出包、迁移 Data Transformation Services (DTS) 包以及升级 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 包。  
  
## <a name="managing-reporting-services-projects-using-sql-server-management-studio"></a>使用 SQL Server Management Studio 管理 Reporting Services 项目  
 可以使用 SQL Server Management Studio 启用 Reporting Services 功能、管理服务器和数据库以及管理角色和作业。  
  
 可通过使用“共享计划”文件夹来管理共享计划以及管理报表服务器数据库（ReportServer、ReportServerTempdb）。 在将报表服务器数据库移动到新的或不同的 SQL Server 数据库引擎（[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../includes/ssde-md.md)]）时，还可以在 Master 系统数据库中创建 RSExecRole。 有关这些任务的详细信息，请参阅以下主题：  
  
-   [SQL Server Management Studio 中的 Reporting Services (SSRS)](../reporting-services/tools/reporting-services-in-sql-server-management-studio-ssrs.md)  
  
-   [管理报表服务器数据库&#40;SSRS 本机模式&#41;](../reporting-services/report-server/report-server-database-ssrs-native-mode.md)  
  
-   [创建 RSExecRole](../reporting-services/security/create-the-rsexecrole.md)  
  
 也可以通过以下方法来管理服务器：启用并配置各种功能、设置服务器默认设置以及管理角色和作业。 有关这些任务的详细信息，请参阅以下主题：  
  
-   [设置报表服务器属性 (Management Studio)](../reporting-services/tools/set-report-server-properties-management-studio.md)  
  
-   [创建、删除或修改角色 (Management Studio)](../reporting-services/security/role-definitions-create-delete-or-modify.md)  
  
-   [启用和禁用 Reporting Services 的客户端打印](../reporting-services/report-server/enable-and-disable-client-side-printing-for-reporting-services.md)  
  
## <a name="see-also"></a>请参阅  
 [使用 SQL Server Data Tools 创建多维模型 (SSDT)](https://docs.microsoft.com/analysis-services/multidimensional-models/creating-multidimensional-models-using-sql-server-data-tools-ssdt)   
 [SQL Server Data Tools &#40;SSDT 中的 Reporting Services&#41;](../reporting-services/tools/reporting-services-in-sql-server-data-tools-ssdt.md)  
  
  
