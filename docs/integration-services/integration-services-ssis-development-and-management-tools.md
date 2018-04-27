---
title: Integration Services (SSIS) 开发和管理工具 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: non-specific
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- studio environments [Integration Services]
- tools [Integration Services], Business Intelligence Development Studio
- Business Intelligence Development Studio, Integration Services in
- SQL Server Management Studio [Integration Services]
- SSIS, studio environments
- SQL Server Integration Services, studio environments
- tools [Integration Services], SQL Server Management Studio
ms.assetid: 4eb73e65-d9f3-4ac6-a408-abfa85afc537
caps.latest.revision: 52
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 1a5190bd675c6ab9fac9b14090ed553eed3bef09
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="integration-services-ssis-development-and-management-tools"></a>Integration Services (SSIS) 开发和管理工具
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 包含两个用于处理包的 Studio：  
  
-   [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] （用于开发商业解决方案所需的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 包）。 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 提供了可在其中创建包的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目。  
  
-   [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] （用于在生产环境中管理包）。  
  
## <a name="sql-server-data-tools"></a>SQL Server Data Tools  
 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]使用 ，您可以执行下列任务：  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 运行  导入和导出向导以创建将数据从源复制到目标的基本包。  
  
-   创建包含复杂的控制流、数据流、事件驱动逻辑和日志记录的包。  
  
-   [!INCLUDE[ssIS](../includes/ssis-md.md)] 使用 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]设计器中的故障排除和监视功能以及  中的调试功能测试并调试包。  
  
-   创建运行时更新包和包对象属性的配置。  
  
-   创建可在其他计算机上安装包及其依赖项的部署实用工具。  
  
-   将包的副本保存到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] msdb 数据库、[!INCLUDE[ssIS](../includes/ssis-md.md)] 包存储和文件系统。  
  
 有关 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]的详细信息，请参阅 [SQL Server Data Tools](https://msdn.microsoft.com/library/hh272686.aspx)。  
  
## <a name="sql-server-management-studio"></a>SQL Server Management Studio  
 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 提供 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务，该服务可用于管理包、监视正在运行的包和确定 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 和 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 对象的影响和数据沿袭。  
  
 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]使用 ，您可以执行下列任务：  
  
-   创建文件夹，用对您的单位有意义的方式来组织包。  
  
-   使用执行包实用工具，运行存储在本地计算机中的包。  
  
-   运行执行包实用工具，以生成运行 **dtexec** 命令提示实用工具 (dtexec.exe) 时要使用的命令行。  
  
-   对 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] msdb 数据库、[!INCLUDE[ssIS](../includes/ssis-md.md)] 包存储区和文件系统，执行包的导入和导出。  
