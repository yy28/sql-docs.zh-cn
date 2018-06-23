---
title: Analysis Services 连接管理器 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- connections [Integration Services], Analysis Services
- connection managers [Integration Services], Analysis Services
- Analysis Services connection manager
ms.assetid: 9f9cadad-a1d0-4db5-98f5-df5dbbec1be4
caps.latest.revision: 43
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 1055a76b227bbd965150a2372ac798b3c20ca8c9
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36127765"
---
# <a name="analysis-services-connection-manager"></a>Analysis Services 连接管理器
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 连接管理器使包能够连接到运行 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库的服务器，或连接到用于访问多维数据集和维度数据的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目。 在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中开发包时，仅可连接到 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]项目。 在运行时，包会连接到您已部署 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目的服务器和数据库。  
  
 任务（如 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 执行 DDL 任务和 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 处理任务）和目标（如数据挖掘模型定型目标）都使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 连接管理器。  
  
 有关 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库的详细信息，请参阅[多维模型数据库 (SSAS)](../../analysis-services/multidimensional-models/multidimensional-model-databases-ssas.md)。  
  
## <a name="configuration-of-the-analysis-services-connection-manager"></a>Analysis Services 连接管理器的配置  
 当你将添加[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]到包中，连接管理器[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]创建连接管理器，它被解析为[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]在运行时，连接设置连接管理器属性，并添加的连接管理器`Connections`上包的集合。 `ConnectionManagerType`的连接管理器的属性设置为`MSOLAP100`。  
  
 可以通过下列方式配置 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 连接管理器：  
  
-   提供配置为符合 Microsoft OLE Provider for Analysis Services 访问接口要求的连接字符串。  
  
-   指定要连接到的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的实例或 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目。  
  
-   如果要连接到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]的实例，则应指定身份验证模式。  
  
-   指示是否在运行时保留从连接管理器中创建的连接。  
  
 可以通过 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器或以编程方式设置属性。  
  
 有关可以在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置的属性的详细信息，请单击以下主题之一：  
  
-   [“添加 Analysis Services 连接管理器”对话框 UI 参考](add-analysis-services-connection-manager-dialog-box-ui-reference.md)  
  
 有关以编程方式配置连接管理器的信息，请参阅<xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager>和[添加连接以编程方式](../building-packages-programmatically/adding-connections-programmatically.md)。  
  
  