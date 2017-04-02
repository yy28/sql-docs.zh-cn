---
title: "使用部署向导部署模型解决方案 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Analysis Services 部署向导"
  - "部署 [Analysis Services], Analysis Services 部署向导"
  - "Analysis Services 部署, Analysis Services 部署向导"
  - "Analysis Services 部署向导, 关于 Analysis Services 部署向导"
ms.assetid: ff711e8e-971c-43ba-b479-effc034af4a4
caps.latest.revision: 39
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 37
---
# 使用部署向导部署模型解决方案
   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署向导将从 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目中生成的 XML 输出文件作为输入文件。 可以轻松地修改这些输入文件，以自定义 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目的部署。 随后，可以立即运行生成的部署脚本，也可以保留此脚本供以后部署。  
  
 您可以使用此处介绍的向导来进行部署。 也可以实现自动部署或使用同步功能。 如果部署的数据库很大，则需要考虑在目标系统上使用分区。 你还可以使用分析管理对象 \(AMO\)，实现分区创建和填充自动化。  
  
> [!IMPORTANT]  
>  如果在用于数据源的连接字符串中指定用户 ID 或密码或出于模拟目的而指定用户 ID 和密码，则 XML 输出文件和部署脚本都不包含该用户 ID 或密码。 在此情况下，由于处理时需要用户 ID 和密码，因此必须手动添加此信息。 如果部署不包括处理，则可以在部署后根据需要添加此连接和模拟信息。 如果部署包括处理，则可以在向导中添加此信息，也可以在保存部署脚本后在脚本中添加此信息。  
  
## 本节内容  
 以下主题说明了如何使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署向导、输入文件和部署脚本：  
  
|主题|Description|  
|-----------|-----------------|  
|[运行 Analysis Services 部署向导](../../analysis-services/multidimensional-models/running-the-analysis-services-deployment-wizard.md)|说明可用于运行 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署向导的各种方式。|  
|[了解用于创建部署脚本的输入文件](../../analysis-services/multidimensional-models/understanding-the-input-files-used-to-create-the-deployment-script.md)|说明 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署向导将哪些文件用作输入值以及每个文件包含什么内容，并提供指向说明如何修改每个输入文件中的值的主题链接。|  
|[了解 Analysis Services 部署脚本](../../analysis-services/multidimensional-models/understanding-the-analysis-services-deployment-script.md)|说明部署脚本包含的内容以及脚本的运行方式。|  
  
## 另请参阅  
 [使用 XMLA 部署模型解决方案](../../analysis-services/multidimensional-models/deploy-model-solutions-using-xmla.md)   
 [同步 Analysis Services 数据库](../../analysis-services/multidimensional-models/synchronize-analysis-services-databases.md)   
 [了解用于创建部署脚本的输入文件](../../analysis-services/multidimensional-models/understanding-the-input-files-used-to-create-the-deployment-script.md)   
 [使用部署实用工具部署模型解决方案](../../analysis-services/multidimensional-models/deploy-model-solutions-with-the-deployment-utility.md)  
  
  