---
title: 管理 Integration Services 服务 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services service, configuring
- services [Integration Services], configuring
ms.assetid: 45554117-a0df-4830-b41c-5ebb33b764a5
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: d6b8ea946def4811332e6783e881e968c5a91f4a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48193397"
---
# <a name="manage-the-integration-services-service"></a>管理 Integration Services 服务
    
> [!IMPORTANT]  
>  本主题论述 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务，该服务是用于管理 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 包的一种 Windows 服务。 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 支持该服务以便与 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 的早期版本向后兼容。 从 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]开始，您可以在 Integration Services 服务器上管理诸如包之类的对象。  
  
 在安装 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]组件时，也会安装 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务。 默认情况下， [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务已启动，该服务的启动类型已设置为自动。 不过，若要使用该服务来管理已存储的和正在运行的 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 包，还必须安装 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 。  
  
> [!NOTE]  
>  无法连接到的实例[!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)][!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]服务从[!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]版本[!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]。 即，在**连接到服务器**对话框中，您不能输入服务器的名称在其上仅[!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]版本的[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]服务是否正在运行。 但是，可以编辑服务配置文件，从而管理的实例中存储的包[!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]从[!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]版本的[!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]。 有关详细信息，请参阅[配置 Integration Services 服务（SSIS 服务）](service/integration-services-service-ssis-service.md)。  
  
 在一台计算机上可以只安装 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务的一个实例。 该服务并非特定于某个 [!INCLUDE[ssDE](../includes/ssde-md.md)]实例。 可以使用正在运行该服务的计算机的名称连接到该服务。  
  
 可以使用以下任一 Microsoft 管理控制台 (MMC) 管理单元来管理 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务：SQL Server 配置管理器或服务。 若要在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]中管理包，必须首先确保该服务已启动。  
  
 默认情况下，[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务配置为管理[!INCLUDE[ssDE](../includes/ssde-md.md)]实例的 msdb 数据库中的包，该实例与 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 同时安装。 如果未同时安装[!INCLUDE[ssDE](../includes/ssde-md.md)]实例，则 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务可配置为管理本地默认[!INCLUDE[ssDE](../includes/ssde-md.md)]实例的 msdb 数据库中的包。 若要管理 [!INCLUDE[ssDE](../includes/ssde-md.md)]某个命名实例或远程实例中存储的包或 [!INCLUDE[ssDE](../includes/ssde-md.md)]的多个实例中存储的包，则必须修改该服务的配置文件。 有关详细信息，请参阅[配置 Integration Services 服务（SSIS 服务）](service/integration-services-service-ssis-service.md)。  
  
 默认情况下， [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务配置为在该服务停止时停止正在运行的包。 但是， [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务不会等待包停止，因此，在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务停止后，一些包可能仍在运行。  
  
 如果 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务已停止，可使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 导入和导出向导、[!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器、执行包实用工具以及 **dtexec** 命令提示实用工具 (dtexec.exe) 继续运行包。 但是，您无法监视正在运行的包。  
  
 默认情况下， [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务在 NETWORK SERVICE 帐户的上下文中运行。  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务将信息写入 Windows 事件日志。 您可以在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]中查看服务事件。 也可以通过 Windows 事件查看器查看服务事件。  
  
### <a name="to-set-properties-of-integration-services-service-using-the-services-snap-in"></a>使用“服务”管理单元设置 Integration Services 服务的属性  
  
-   [设置 Integration Services 服务的属性](../../2014/integration-services/set-the-properties-of-the-integration-services-service.md)  
  
### <a name="to-view-service-events-for-integration-services-service"></a>查看 Integration Services 服务的服务事件  
  
-   [查看 Integration Services 服务的事件](../../2014/integration-services/view-events-for-the-integration-services-service.md)  
  
## <a name="see-also"></a>请参阅  
 [Integration Services 服务&#40;SSIS 服务&#41;](service/integration-services-service-ssis-service.md)   
 [配置 Integration Services 服务&#40;SSIS 服务&#41;](configuring-the-integration-services-service-ssis-service.md)   
 [SQL Server 导入和导出向导](import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md)   
 [dtexec 实用工具](packages/dtexec-utility.md)   
 [项目和包的执行](packages/run-integration-services-ssis-packages.md)  
  
  
