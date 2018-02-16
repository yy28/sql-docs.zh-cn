---
title: "指定安装目标 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining - "setup-install"
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- input files [Analysis Services]
- installation targets [Analysis Services]
- Analysis Services deployments, installation targets
- Analysis Services Deployment Wizard, installation targets
- deploying [Analysis Services], installation targets
- modifying installation targets
ms.assetid: cb706817-6f63-4771-92c3-b70030bbce3d
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 1d17bf0953012ef95537bd3649c06cceda344db1
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/15/2018
---
# <a name="deployment-script-files---specifying-the-installation-target"></a>部署脚本文件-指定安装目标
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]部署向导读取安装目标信息\<*项目名称*>.deploymenttargets 文件。 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]生成时创建此文件[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]项目。 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 使用的数据库和服务器上指定**部署**页*\<项目名称 >* **属性页**对话框创建\<*项目名称*>.targets 文件。  
  
## <a name="modifying-the-installation-target-for-deployment"></a>修改部署的安装目标  
 在有些情况下，可能需要将 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目部署到与 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] “部署” **页上指定的项不同的数据库或** 实例。 例如，可能要在部署之前将项目部署到用于测试的服务器，再在测试完成后将其部署到生产服务器。 此外，还可能需要将已完成且经过测试的项目部署到网络负载平衡群集中的多台生产服务器，或将其部署到临时服务器和生产服务器。  
  
 若要将 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目部署到其他数据库或 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例，可使用下列过程中介绍的方法之一，在输入文件中更改安装目标。  
  
#### <a name="to-change-the-installation-target-after-the-input-files-have-been-generated"></a>在生成了输入文件后更改安装目标  
  
-   以交互方式运行 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署向导。 在 **“安装目标”** 页上，为 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例和数据库指定新的目标。  
  
     — 或 —  
  
-   在命令提示符下运行 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署向导，并设置向导，使其以应答文件模式运行。 有关应答文件模式的详细信息，请参阅 [Running the Analysis Services Deployment Wizard](../../analysis-services/multidimensional-models/running-the-analysis-services-deployment-wizard.md)。  
  
     — 或 —  
  
-   修改\<*项目名称*>.deploymenttargets 文件使用的任何文本编辑器。  
  
## <a name="see-also"></a>另请参阅  
 [指定分区和角色部署选项](../../analysis-services/multidimensional-models/deployment-script-files-partition-and-role-deployment-options.md)   
 [指定解决方案部署的配置的设置](../../analysis-services/multidimensional-models/deployment-script-files-solution-deployment-config-settings.md)   
 [指定处理选项](../../analysis-services/multidimensional-models/deployment-script-files-specifying-processing-options.md)  
  
  
