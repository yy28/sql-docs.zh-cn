---
title: 使用部署向导部署模型解决方案 |Microsoft 文档
ms.custom: ''
ms.date: 03/27/2018
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Analysis Services Deployment Wizard
- deploying [Analysis Services], Analysis Services Deployment Wizard
- Analysis Services deployments, Analysis Services Deployment Wizard
- Analysis Services Deployment Wizard, about Analysis Services Deployment Wizard
ms.assetid: ff711e8e-971c-43ba-b479-effc034af4a4
caps.latest.revision: ''
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: f4e810f0ca82140f40f353a694b5c937764698b0
ms.sourcegitcommit: d6881107b51e1afe09c2d8b88b98d075589377de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/28/2018
---
# <a name="deploy-model-solutions-using-the-deployment-wizard"></a>使用部署向导部署模型解决方案
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]部署向导使用从生成的 JSON 输出文件[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]作为输入文件的项目。 可以轻松地修改这些输入文件，以自定义 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目的部署。 随后，可以立即运行生成的部署脚本，也可以保留此脚本供以后部署。  

> [!NOTE]
> [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]部署向导/实用工具随[SQL Server 管理 Studio](../../ssms/download-sql-server-management-studio-ssms.md) (SSMS)。 请确保你在使用最新版本。 如果默认情况下，从命令提示符下运行的部署向导的最新版本安装到 C:\Program Files (x86) \Microsoft SQL Server\140\Tools\Binn\ManagementStudio。 
  
 您可以使用此处介绍的向导来进行部署。 也可以实现自动部署或使用同步功能。 如果部署的数据库很大，则需要考虑在目标系统上使用分区。 你可以通过使用表格对象模型 (TOM)、 表格模型 Scriting 语言 (TMSL) 和分析管理对象 (AMO) 自动分区创建和填充。  
  
> [!IMPORTANT]  
>  既不输出文件，也不部署脚本将包含用户 id 或密码如果这些指定的连接字符串的数据源或出于模拟目的中。 在此情况下，由于处理时需要用户 ID 和密码，因此必须手动添加此信息。 如果部署不包括处理，则可以在部署后根据需要添加此连接和模拟信息。 如果部署包括处理，则可以在向导中添加此信息，也可以在保存部署脚本后在脚本中添加此信息。  
  
## <a name="in-this-section"></a>本节内容  
 以下主题说明了如何使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署向导、输入文件和部署脚本：  
  
|主题|Description|  
|-----------|-----------------|  
|[运行 Analysis Services 部署向导](../../analysis-services/multidimensional-models/running-the-analysis-services-deployment-wizard.md)|说明可用于运行 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署向导的各种方式。|  
|[了解用于创建部署脚本的输入的文件](../../analysis-services/multidimensional-models/deployment-script-files-input-used-to-create-deployment-script.md)|说明 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署向导将哪些文件用作输入值以及每个文件包含什么内容，并提供指向说明如何修改每个输入文件中的值的主题链接。|  
|[了解 Analysis Services 部署脚本](../../analysis-services/multidimensional-models/understanding-the-analysis-services-deployment-script.md)|说明部署脚本包含的内容以及脚本的运行方式。|  
  
## <a name="see-also"></a>另请参阅  
 [使用 XMLA 部署模型解决方案](../../analysis-services/multidimensional-models/deploy-model-solutions-using-xmla.md)   
 [同步 Analysis Services 数据库](../../analysis-services/multidimensional-models/synchronize-analysis-services-databases.md)   
 [了解用于创建部署脚本的输入的文件](../../analysis-services/multidimensional-models/deployment-script-files-input-used-to-create-deployment-script.md)   
 [使用部署实用工具部署模型解决方案](../../analysis-services/multidimensional-models/deploy-model-solutions-with-the-deployment-utility.md)  
  
  
