---
title: Integration Services 部署向导 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.deploymentwizard.f1
ms.assetid: f3d93e13-2d85-47ff-a913-cda4046491c4
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 721953c31a44a2ea02f480c9830e6347adfd4eb3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66058008"
---
# <a name="integration-services-deployment-wizard"></a>Integration Services 部署向导
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 部署向导使用项目部署模型将项目部署到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例上的 SSISDB 目录。  
  
 若要启动[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]从打开的项目中的部署向导[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]，选择**部署**从**项目**菜单。 若要启动向导[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]，展开**Integration Services 目录** > **SSISDB**节点在对象资源管理器，右键单击**项目**文件夹，，然后单击**部署项目**。  
  
 该向导继续执行以下四个步骤。 单击**下一步**若要将移动到下一步中，或**上一步**以返回到上一步。  
  
1.  **选择源**-选择[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]你想要部署的项目。  
  
2.  **选择目标**-选择项目目标。  
  
3.  **查看**-显示您的选择。  
  
4.  **部署/结果**-部署项目，并显示结果。  
  
## <a name="select-source"></a>选择源  
 若要部署你创建的项目部署文件，选择**项目部署文件**并输入.ispac 文件的路径或单击**浏览**若要查找在[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]项目文件夹。 若要部署位于 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 目录中的项目，请选择 **“Integration Services 目录”** ，然后输入目录中指向该项目的服务器名称和路径。  
  
 如果在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 中启动该向导，则默认情况下该向导选择打开的项目作为源并跳过此步骤。 若要返回到此步骤并选择不同的源，请单击**上一步**或单击**选择源**的左窗格中。  
  
## <a name="select-destination"></a>选择目标  
 若要在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 目录中选择项目的目标文件夹，请输入 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例或单击 **“浏览”** 从服务器列表中选择。 然后输入 SSISDB 中的项目路径或单击 **“浏览”** 以选择此路径。  
  
 如果在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中启动该向导，则默认情况下该向导选择连接的服务器实例并输入所选项目的路径。 您可以更改这些值，以将项目部署到其他位置。  
  
## <a name="review"></a>评审  
 该向导允许您在部署项目前检查所选的设置。 可以通过单击 **“上一步”** 或单击左窗格中的任意步骤来更改所做的选择。  
  
## <a name="deployresults"></a>部署/结果  
 当您单击**部署**从**评审**页上，该项目部署并**结果**页将显示每个操作成功与否。 如果操作失败，单击 **“结果”** 列中的 **“失败”** 可以显示错误说明。 单击**保存报表...** 将结果保存到 XML 文件。  
  
 单击“关闭”以退出向导  。  
  
## <a name="see-also"></a>请参阅  
 [将项目部署到 Integration Services 服务器](../../2014/integration-services/deploy-projects-to-integration-services-server.md)   
 [项目和包的部署](packages/deploy-integration-services-ssis-projects-and-packages.md)  
  
  
