---
title: 在解决方案中添加或删除 Integration Services 项目 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- adding projects
- Integration Services projects, adding
- SQL Server Integration Services projects, adding
- SSIS projects, adding
- projects [Integration Services], adding
ms.assetid: f01f6475-b63c-41dc-82ac-b62162b3adf7
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 7d338cac89b7b6c8f2588817cfd6718d4f415589
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84925940"
---
# <a name="add-or-remove-an-integration-services-project-in-a-solution"></a>在解决方案中添加或删除 Integration Services 项目
  下列过程介绍如何在解决方案中添加或删除 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目。  
  
 仅当解决方案在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中可见时，才能向现有解决方案中添加项目或从解决方案中删除项目。 如果在中选择了 "**始终显示解决方案**" 选项 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ， [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 则即使该解决方案只包含一个项目，也会显示该解决方案。 否则， [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 将只显示包含多个项目的解决方案。 其他项目可以是 [!INCLUDE[ssIS](../includes/ssis-md.md)] 项目或其他类型的项目。  
  
## <a name="adding-an-integration-services-project"></a>添加 Integration Services 项目  
 在添加项目时，可以让 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 创建新的空白项目，或者你可以添加已为其他解决方案创建的项目。 仅当现有解决方案在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中可见时，才能向该解决方案中添加项目。  
  
#### <a name="to-add-a-new-integration-services-project-to-a-solution"></a>将新 Integration Services 项目添加到解决方案  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，打开要添加新 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目的解决方案，然后进行下列操作之一：  
  
    -   右键单击该解决方案，单击“添加”，再单击“新建项目”。********  
  
    -   在 **“文件”** 菜单上，指向 **“添加”**，再单击 **“新建项目”**。  
  
2.  在 **“添加新项目”** 对话框中，单击 **“模板”** 窗格中的 **“Integration Services 项目”** 。  
  
3.  或者，编辑项目的名称和位置。  
  
4.  单击“确定”。  
  
#### <a name="to-add-an-existing-integration-services-project-to-a-solution"></a>将现有 Integration Services 项目添加到解决方案中  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中打开要把现有 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目添加到其中的解决方案，并且执行下列操作之一：  
  
    -   右键单击该解决方案，指向“添加”，然后单击“现有项目”。********  
  
    -   在 **“文件”** 菜单上，单击 **“添加”**，然后单击 **“现有项目”**。  
  
2.  在 **“添加现有项目”** 对话框中，浏览并找到要添加的项目，然后单击 **“打开”**。  
  
3.  此项目即添加到 **解决方案资源管理器**中的解决方案文件夹中。  
  
## <a name="removing-an-integration-services-project"></a>删除 Integration Services 项目  
 仅当解决方案在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中可见时，才能从解决方案中删除项目。 解决方案可见后，则可以保留一个项目而删除其余所有项目。 只要仅剩余一个项目， [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 就不再显示解决方案文件夹，并且您无法删除最后一个项目。  
  
#### <a name="to-remove-an-integration-services-project-from-a-solution"></a>从解决方案中删除 Integration Services 项目  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，打开要删除 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目的解决方案。  
  
2.  在解决方案资源管理器中，右键单击该项目，然后单击“卸载项目”。****  
  
3.  单击“确定”以确认删除。****  
  
## <a name="see-also"></a>另请参阅  
 [Integration Services &#40;SSIS&#41; 项目](integration-services-ssis-projects-and-solutions.md)   
 [创建新的 Integration Services 项目](../../2014/integration-services/create-a-new-integration-services-project.md)  
  
  
