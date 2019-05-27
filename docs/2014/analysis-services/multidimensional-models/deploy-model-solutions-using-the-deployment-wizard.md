---
title: 使用部署向导部署模型解决方案 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Analysis Services Deployment Wizard
- deploying [Analysis Services], Analysis Services Deployment Wizard
- Analysis Services deployments, Analysis Services Deployment Wizard
- Analysis Services Deployment Wizard, about Analysis Services Deployment Wizard
ms.assetid: ff711e8e-971c-43ba-b479-effc034af4a4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e18b1786201be9ba671bc08fe7b24ba2207469e9
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66075379"
---
# <a name="deploy-model-solutions-using-the-deployment-wizard"></a>使用部署向导部署模型解决方案
   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署向导将从 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目中生成的 XML 输出文件作为输入文件。 可以轻松地修改这些输入文件，以自定义 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目的部署。 随后，可以立即运行生成的部署脚本，也可以保留此脚本供以后部署。  
  
 您可以使用此处介绍的向导来进行部署。 也可以实现自动部署或使用同步功能。 如果部署的数据库很大，则需要考虑在目标系统上使用分区。 您还可以使用分析管理对象 (AMO)，实现分区创建和填充自动化。  
  
> [!IMPORTANT]  
>  如果在用于数据源的连接字符串中指定用户 ID 或密码或出于模拟目的而指定用户 ID 和密码，则 XML 输出文件和部署脚本都不包含该用户 ID 或密码。 在此情况下，由于处理时需要用户 ID 和密码，因此必须手动添加此信息。 如果部署不包括处理，则可以在部署后根据需要添加此连接和模拟信息。 如果部署包括处理，则可以在向导中添加此信息，也可以在保存部署脚本后在脚本中添加此信息。  
  
## <a name="in-this-section"></a>本节内容  
 以下主题说明了如何使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署向导、输入文件和部署脚本：  
  
|主题|Description|  
|-----------|-----------------|  
|[运行 Analysis Services 部署向导](running-the-analysis-services-deployment-wizard.md)|说明可用于运行 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署向导的各种方式。|  
|[了解用于创建部署脚本的输入文件](deployment-script-files-input-used-to-create-deployment-script.md)|说明 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署向导将哪些文件用作输入值以及每个文件包含什么内容，并提供指向说明如何修改每个输入文件中的值的主题链接。|  
|[了解 Analysis Services 部署脚本](understanding-the-analysis-services-deployment-script.md)|说明部署脚本包含的内容以及脚本的运行方式。|  
  
## <a name="see-also"></a>请参阅  
 [使用 XMLA 部署模型解决方案](deploy-model-solutions-using-xmla.md)   
 [同步 Analysis Services 数据库](synchronize-analysis-services-databases.md)   
 [了解用于创建部署脚本的输入文件](deployment-script-files-input-used-to-create-deployment-script.md)   
 [使用部署实用工具部署模型解决方案](deploy-model-solutions-with-the-deployment-utility.md)  
  
  
