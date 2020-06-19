---
title: 从 SQL Server Data Tools 部署（SSAS 表格） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.deploystatus.f1
ms.assetid: 67dde3fe-ba43-41f3-b56c-c656029ee93f
author: minewiskan
ms.author: owend
ms.openlocfilehash: 1690e2772de50258a69a4a33b048f16f7da2caca
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84939711"
---
# <a name="deploy-from-sql-server-data-tools-ssas-tabular"></a>从 SQL Server Data Tools 进行部署（SSAS 表格）
  使用本主题中的任务以通过在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中使用“部署”命令来部署表格模型解决方案。  
  
 本主题的内容：  
  
-   [配置部署选项和部署服务器属性](#bkmk_deploy)  
  
-   [部署表格模型解决方案](#bkmk_deploy_proc)  
  
-   [部署状态](#bkmk_deploy_status)  
  
##  <a name="configure-deployment-options-and-deployment-server-properties"></a><a name="bkmk_deploy"></a>配置部署选项和部署服务器属性  
 在您部署表格模型解决方案之前，必须首先指定“部署选项”属性和“部署服务器”属性。 有关部署属性和设置的详细信息，请参阅 [表格模型解决方案部署（SSAS 表格）](tabular-model-solution-deployment-ssas-tabular.md)中使用“部署”命令来部署表格模型解决方案。  
  
#### <a name="to-configure-deployment-options-and-deployment-server-properties"></a>配置“部署选项”和“部署服务器”属性  
  
1.  在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 中的“解决方案资源管理器”**** 中，右键单击项目名称，再单击“属性”****。  
  
2.  在 " ** \<project name> 属性**" 对话框的 "**部署选项**" 中，指定属性设置（如果不同于默认设置）。  
  
    > [!NOTE]  
    >  对于缓存模式下的模型，“查询模式”**** 始终为“内存中”****。  
  
    > [!NOTE]  
    >  不能为 DirectQuery 模式下的模型指定“模拟设置”****。  
  
3.  在“部署服务器”**** 中，指定“服务器”****（名称）、“版本”****、“数据库”（名称）**** 和“多维数据集名称”**** 属性设置（如果这些设置不同于默认设置），然后单击“确定”****。  
  
> [!NOTE]  
>  还可以指定“默认部署服务器”属性设置，以便您创建的任何新项目将自动部署到指定的服务器。 有关详细信息，请参阅 [配置默认数据建模和部署属性（SSAS 表格）](properties-ssas-tabular.md)。  
  
##  <a name="deploy-a-tabular-model-solution"></a><a name="bkmk_deploy_proc"></a>部署表格模型解决方案  
  
#### <a name="to-deploy-a-tabular-model-solution"></a>部署表格模型解决方案  
  
-   在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 的 "**生成**" 菜单上，单击 "**部署 \<project name> **"。  
  
     “部署”**** 对话框将出现，并且指示在模型中包括的每个表的元数据部署和处理的状态（除非将“处理选项”属性设置为“不处理”）。 在部署过程完成后，使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 连接到 Analysis Services 实例并且确认已创建新的模型数据库对象或使用客户端报告应用程序连接到已部署的模型。  
  
##  <a name="deploy-status"></a><a name="bkmk_deploy_status"></a> 部署状态  
 通过 **“部署”** 对话框，您可以监视“部署”操作的进度。 也可以停止部署操作。  
  
 **状态**  
 指示部署操作成功与否。  
  
 **详细信息**  
 列出已部署的元数据项、每个元数据项的状态并提供针对任何问题的一条消息。  
  
 **停止部署**  
 单击此选项可以暂停部署操作。 如果部署操作用时过长或出现太多错误，则此选项很有用。  
  
## <a name="see-also"></a>另请参阅  
 [&#40;SSAS 表格部署的表格模型解决方案部署&#41;](tabular-model-solution-deployment-ssas-tabular.md)   
 [配置默认数据建模和部署属性（SSAS 表格）](properties-ssas-tabular.md)  
  
  
