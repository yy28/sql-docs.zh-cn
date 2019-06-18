---
title: 将报表发布到报表服务器 | Microsoft Docs
ms.date: 06/01/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reports
ms.topic: conceptual
helpviewer_keywords:
- production environments [Reporting Services]
- report projects [Reporting Services]
- Debug configuration [Reporting Services]
- report publishing [Reporting Services]
- publishing reports [Reporting Services]
- report properties [Reporting Services]
- Report Designer [Reporting Services], deploying reports
- Production configuration [Reporting Services]
- publishing reports [Reporting Services], production environments
- DebugLocal configuration [Reporting Services]
- deploying [Reporting Services], reports
- Report Designer [Reporting Services], publishing reports
ms.assetid: bd7aa5e0-61ce-43fd-8f74-5d1aeed078bb
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: bc4d75a6af4441d2030a71306801449ee74a6a02
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "65579979"
---
# <a name="publishing-reports-to-a-report-server"></a>将报表发布到报表服务器
  在设计并测试完一个或一组报表后，可以使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中的部署功能将报表发布到报表服务器上。 可以发布单独报表或包含多个报表和数据源的报表服务器项目。 发布报表服务器项目是发布多个报表的最简单方式。 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 使用术语“部署”替代术语“发布”   。 这两个术语可以互换。  
  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 为管理报表发布提供项目配置。 此配置指定报表服务器的位置、在报表服务器上安装的 SQL Server Reporting Services 的版本、发布到报表服务器的数据源是否被覆盖等等。 例如，“Debug”配置可以发布到与“release”配置不同的服务器。 除了使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 提供的配置之外，还可以创建其他配置。  
 
## <a name="requirements-to-publish"></a>发布要求
权限是通过基于角色的安全性确定的，而安全性由报表服务器管理员定义。 发布操作通常由“发布者角色”授予  。  
  
## <a name="project-configurations"></a>项目配置  
 报告环境中可能安装了多个报表服务器和不同版本的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 。 您可以创建多个配置，然后根据部署方案选择不同的配置。 项目配置包括用于生成报表的属性（如临时存储所生成的报表的文件夹）以及如何处理生成问题。 配置还具有用于指定报表服务器的位置和版本以及报表服务器上的文件夹的属性。  
  
 默认情况下， [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 提供三种项目配置： **DebugLocal**、 **Debug**和 **Release**。 默认配置为 DebugLocal。 通常，使用 DebugLocal 配置可以在本地预览窗口中查看报表，使用 Debug 配置可以将报表发布到测试服务器，使用 Release 配置可以将报表发布到生产服务器。 标准工具栏上的解决方案配置下拉列表中显示了活动的配置。 若要使用其他配置，请从列表中进行选择。  
  
 ![ssrs_project_properties](../../reporting-services/reports/media/ssrs-project-properties.png) 
  
 有关详细信息，请参见以下内容
 + [“项目属性页”对话框](../../reporting-services/tools/project-property-pages-dialog-box.md)
 + [SQL Server Data Tools 中的部署和版本支持](../../reporting-services/tools/deployment-and-version-support-in-sql-server-data-tools-ssrs.md)
 + [为 SSDT 中的 Reporting Services 项目设置部署属性](../../reporting-services/tools/set-deployment-properties-reporting-services.md)
  
## <a name="to-publish-all-reports-in-a-project"></a>发布项目中的所有报表  
  
在“生成”菜单中，单击“部署 \<报表项目名称>”   。 或者，在解决方案资源管理器中，右键单击报表项目，然后单击“部署”  。 可以在“输出”窗口中查看发布过程的状态。  
  
当您部署报表服务器项目时，也会部署报表服务器中的共享数据源。 将使用相同的项目配置部署所有报表：部署到同一个报表服务器、该服务器上的同一个文件夹等等。 若要将报表发布到不同服务器，请逐个发布这些报表，或者只包含报表服务器项目中您要发布的报表。 一个解决方案可以包含多个报表服务器项目，而使用多个项目可能会使管理报表部署的过程变得更为简单，因为您可以使用不同的配置来部署不同的项目。 
  
## <a name="to-publish-a-single-report"></a>发布单个报表  
  
在解决方案资源管理器中，右键单击报表，然后单击 **“部署”** 。 可以在“输出”窗口中查看发布过程的状态。  
  
 当您发布报表时，还必须部署报表使用的共享数据源。   
 如果不希望发布项目中的所有报表，可以选择只发布单个报表。 为此，请选择一种部署报表的配置（例如，“发布”配置），然后右键单击相应的报表，再单击“部署”  。  
  
 如果报表使用共享数据源，您还需要部署共享数据源，否则，部署的报表将不会运行。 右键单击该共享数据源，再单击“部署”  。  
  
 必须指定报表服务器的目标服务器 URL，并且可能需要更改将报表和共享数据源部署到的默认文件夹。  

  
## <a name="see-also"></a>另请参阅  
 [“项目属性页”对话框](../../reporting-services/tools/project-property-pages-dialog-box.md)   
 [报表服务器内容管理（SSRS 本机模式）](../../reporting-services/report-server/report-server-content-management-ssrs-native-mode.md)   
 [升级报表](../../reporting-services/install-windows/upgrade-reports.md)  
  
  
