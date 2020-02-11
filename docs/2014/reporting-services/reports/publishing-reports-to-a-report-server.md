---
title: 将报表发布到报表服务器 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
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
manager: kfile
ms.openlocfilehash: 5c73e75bbdf458b27d0f879a91e72ececc832b88
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66102484"
---
# <a name="publishing-reports-to-a-report-server"></a>将报表发布到报表服务器
  设计和测试报表或报表集之后，可以使用中[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]的内置部署功能将报表发布到 Report Server。 您可以发布单个报表或报表服务器项目。 发布报表服务器项目是发布多个报表的最简单方式。 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]使用术语 "*部署*"，而不是 "*发布*"。 这两个术语可以互换。  
  
 发布报表之前，您必须具有相应的权限。 权限是通过基于角色的安全性确定的，而安全性由报表服务器管理员定义。 发布操作通常由“发布者”角色授予。  
  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 为管理报表发布提供项目配置。 此配置指定报表服务器的位置、在报表服务器上安装的 SQL Server Reporting Services 的版本、发布到报表服务器的数据源是否被覆盖等等。 除了使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 提供的配置之外，还可以创建其他配置。  
  
## <a name="project-configurations"></a>项目配置  
 报表将在发布之前生成，以确保只将有效的报表定义发布到报表服务器。 项目配置包括用于生成报表的属性（如临时存储所生成的报表的文件夹）以及如何处理生成问题。 配置还具有用于指定报表服务器的位置和版本以及报表服务器上的文件夹的属性。  
  
 默认情况下， [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 提供三种配置：DebugLocal、Debug 和 Release。 默认配置为 DebugLocal。 通常，使用 DebugLocal 配置可以在本地预览窗口中查看报表，使用 Debug 配置可以将报表发布到测试服务器，使用 Release 配置可以将报表发布到生产服务器。 标准工具栏上的解决方案配置下拉列表中显示了活动的配置。 若要使用其他配置，请从列表中进行选择。  
  
 报告环境中可能安装了多个报表服务器和不同版本的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 。 您可以创建多个配置，然后根据部署方案选择不同的配置。 有关详细信息，请参阅[SQL Server Data Tools &#40;SSRS&#41;中的部署和版本支持](../tools/deployment-and-version-support-in-sql-server-data-tools-ssrs.md)，并[&#40;Reporting Services&#41;设置部署属性](../tools/set-deployment-properties-reporting-services.md)。  
  
## <a name="publishing-reports"></a>发布报表  
 您可以发布单个报表，也可以发布包含多个报表的报表服务器项目。 有关发布报表的说明，请参阅[发布报表](../publish-reports.md)。  
  
### <a name="publishing-a-single-report"></a>发布单个报表  
 如果不希望发布项目中的所有报表，可以选择只发布单个报表。 为此，请选择一种部署报表的配置（例如，“发布”配置），然后右键单击相应的报表，再单击“部署”  。  
  
 如果报表使用共享数据源，您还需要部署共享数据源，否则，部署的报表将不会运行。 右键单击该共享数据源，再单击“部署”  。  
  
 必须指定报表服务器的目标服务器 URL，并且可能需要更改将报表和共享数据源部署到的默认文件夹。  
  
### <a name="publishing-multiple-reports"></a>发布多个报表  
 当您发布报表服务器项目时，将会发布该项目中的所有报表。 将使用相同的项目配置部署所有报表：部署到同一个报表服务器、该服务器上的同一个文件夹等等。 若要将报表发布到不同服务器，请逐个发布这些报表，或者只包含报表服务器项目中您要发布的报表。 一个解决方案可以包含多个报表服务器项目，而使用多个项目可能会使管理报表部署的过程变得更为简单，因为您可以使用不同的配置来部署不同的项目。  
  
## <a name="see-also"></a>另请参阅  
 [“项目属性页”对话框](../tools/project-property-pages-dialog-box.md)   
 [报表服务器内容管理（SSRS 本机模式）](../report-server/report-server-content-management-ssrs-native-mode.md)   
 [升级报表](../install-windows/upgrade-reports.md)  
  
  
