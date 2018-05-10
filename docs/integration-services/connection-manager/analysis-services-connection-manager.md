---
title: Analysis Services 连接管理器 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: connection-manager
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- connections [Integration Services], Analysis Services
- connection managers [Integration Services], Analysis Services
- Analysis Services connection manager
ms.assetid: 9f9cadad-a1d0-4db5-98f5-df5dbbec1be4
caps.latest.revision: 43
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ae8da583d883bbcaf3665f647495ed3e016a9cb1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="analysis-services-connection-manager"></a>Analysis Services 连接管理器
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 连接管理器使包能够连接到运行 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库的服务器，或连接到用于访问多维数据集和维度数据的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目。 在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中开发包时，仅可连接到 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]项目。 在运行时，包会连接到您已部署 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目的服务器和数据库。  
  
 任务（如 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 执行 DDL 任务和 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 处理任务）和目标（如数据挖掘模型定型目标）都使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 连接管理器。  
  
 有关 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库的详细信息，请参阅[多维模型数据库 (SSAS)](../../analysis-services/multidimensional-models/multidimensional-model-databases-ssas.md)。  
  
## <a name="configuration-of-the-analysis-services-connection-manager"></a>Analysis Services 连接管理器的配置  
 将 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 连接管理器添加到包时， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 会创建在运行时作为 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 连接进行解析的连接管理器，同时还会设置该连接管理器的属性，并将该连接管理器添加到包的 **Connections** 集合。 该连接管理器的 **ConnectionManagerType** 属性设置为 **MSOLAP100**。  
  
 可以通过下列方式配置 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 连接管理器：  
  
-   提供配置为符合 Microsoft OLE Provider for Analysis Services 访问接口要求的连接字符串。  
  
-   指定要连接到的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的实例或 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目。  
  
-   如果要连接到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]的实例，则应指定身份验证模式。  
  
-   指示是否在运行时保留从连接管理器中创建的连接。  
  
 可以通过 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器或以编程方式设置属性。  
  
 有关可以在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置的属性的详细信息，请单击以下主题之一：  
  
-   [“添加 Analysis Services 连接管理器”对话框 UI 参考](../../integration-services/connection-manager/add-analysis-services-connection-manager-dialog-box-ui-reference.md)  
  
 有关以编程方式配置连接管理器的信息，请参阅 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 和 [以编程方式添加连接](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md)项目。  
  
  
