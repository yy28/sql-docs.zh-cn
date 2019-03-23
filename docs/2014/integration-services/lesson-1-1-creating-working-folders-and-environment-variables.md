---
title: 步骤 1：创建工作文件夹和环境变量 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 45091ba2-ea3d-4399-9814-489d812b42cc
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b58da11d973d169a0372e59c7e8d7e174e3cf789
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/22/2019
ms.locfileid: "58392125"
---
# <a name="step-1-creating-working-folders-and-environment-variables"></a>步骤 1：创建工作文件夹和环境变量
  在此任务中，您将创建工作文件夹 (C:\DeploymentTutorial) 和新的系统环境变量（`DataTransfer` 和 `LoadXMLData`），在后面的教程任务中您将使用它们。  
  
 工作文件夹位于 C 驱动器的根目录。 如果必须使用其他驱动器或位置，也可以使用其他驱动器或位置。 但是，您需要记下此位置；然后，只要教程引用 DeploymentTutorial 工作文件夹的位置，就使用它。  
  
 在后面的课程中，需将保存到文件系统的包部署到 msdb[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 数据库中的 sysssispackages 表中。 理想的情况是，将 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 包部署到其他计算机。 如果这是不可能的，则仍可以通过将包部署到本地计算机上的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例而从本教程中学到许多知识。 在本地计算机和目标计算机上使用的环境变量具有相同的变量名称，但是在变量中存储的值不同。 例如，在本地计算机上，环境变量 `DataTransfer` 的值引用 C:\DeploymentTutorial 文件夹，而在目标计算机上，环境变量 `DataTransfer` 引用 C:\DeploymentTutorialInstall 文件夹。  
  
 如果计划部署到本地计算机，则只需要创建一组环境变量；但是，在执行本地部署之前，您需要将环境变量的值更新为相应值。  
  
 如果计划将包部署到其他计算机，则必须创建两组环境变量：一组用于本地计算机，另一组用于目标计算机。 您能够眼下只为源计算机创建变量，稍后再为目标计算机创建变量；但是要在目标计算机上安装包，您必须先使文件夹和环境变量在该计算机上都可用。  
  
### <a name="to-create-the-local-working-folder"></a>创建本地工作文件夹  
  
1.  右键单击“开始”菜单，再单击“资源管理器”。  
  
2.  单击“本地磁盘 (C:)”。  
  
3.  在“文件”菜单上，指向“新建”，再单击“文件夹”。  
  
4.  重命名为新文件夹`DeploymentTutorial`。  
  
### <a name="to-create-local-environment-variables"></a>创建本地环境变量  
  
1.  在 **“开始”** 菜单上，单击 **“控制面板”**。  
  
2.  在控制面板中，双击“系统”。  
  
3.  在 **“系统属性”** 对话框中，单击 **“高级”** 选项卡，再单击 **“环境变量”**。  
  
4.  在“环境变量”对话框的“系统变量”框架中，单击“新建”。  
  
5.  在中**新建系统变量**对话框中，键入`DataTransfer`中**变量名**框中，和`C:\DeploymentTutorial\datatransferconfig.dtsconfig`中**变量值**框。  
  
6.  单击“确定” 。  
  
7.  单击**新建**同样，然后键入`LoadXMLData`中**变量名**框中，和`C:\DeploymentTutorial\loadxmldataconfig.dtsconfig`中**变量值**框。  
  
8.  单击“确定”退出“环境变量”对话框。  
  
9. 单击“确定”退出“系统属性”对话框。  
  
10. （可选）重新启动计算机。 如果不重新启动计算机，则在包配置向导中将不显示新变量的名称，但是您仍可以使用它。  
  
### <a name="to-create-destination-environment-variables"></a>创建目标环境变量  
  
1.  在 **“开始”** 菜单上，单击 **“控制面板”**。  
  
2.  在控制面板中，双击“系统”。  
  
3.  在 **“系统属性”** 对话框中，单击 **“高级”** 选项卡，再单击 **“环境变量”**。  
  
4.  在“环境变量”对话框的“系统变量”框架中，单击“新建”。  
  
5.  在中**新建系统变量**对话框中，键入`DataTransfer`中**变量名**框中，和`C:\DeploymentTutorialInstall\datatransferconfig.dtsconfig`中**变量值**框。  
  
6.  单击“确定” 。  
  
7.  单击**新建**同样，然后键入`LoadXMLData`中**变量名**框中，和`C:\DeploymentTutorialInstall\loadxmldataconfig.dtsconfig`中**变量值**框。  
  
8.  单击“确定”退出“环境变量”对话框。  
  
9. 单击“确定”退出“系统属性”对话框。  
  
10. （可选）重新启动计算机。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [步骤 2：创建部署项目](../integration-services/lesson-1-2-creating-the-deployment-project.md)  
  
![集成服务图标 （小）](media/dts-16.gif "Integration Services 图标 （小）")**保持最新的 Integration Services**<br /> 若要从 Microsoft 获得最新的下载内容、文章、示例和视频，以及从社区获得所选解决方案，请访问 MSDN 上的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 页：<br /><br /> [访问 MSDN 上的 Integration Services 页](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要获得有关这些更新的自动通知，请订阅该页上提供的 RSS 源。  
  
  
