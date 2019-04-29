---
title: 第 2 步：创建部署项目 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 59990fe2-7036-4e9c-8efc-6ece9e66eda7
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 6f5b0cc2c86ef483a7e2b2c0f5dccba21383641f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62891843"
---
# <a name="step-2-creating-the-deployment-project"></a>第 2 步：创建部署项目
  在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]中，可部署的单元是 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目。 必须先创建一个新的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目，再将所有包和要与包一起部署的任何辅助文件添加到该项目，才能部署包。  
  
### <a name="to-create-the-integration-services-project"></a>创建 Integration Services 项目  
  
1.  单击“开始”，依次指向“所有程序”和“Microsoft SQL Server”，然后依次单击“SQL Server”和“SQL Server Data Tools”。  
  
2.  在“文件”菜单上，指向“新建”，然后单击“项目”创建新的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目。  
  
3.  在“新建项目”对话框的“模板”窗格中，选择“Integration Services 项目”。  
  
4.  在“名称”框中，将默认名称更改为“Deployment Tutorial”。 或者，清除“创建解决方案的目录”复选框。  
  
5.  接受默认位置，或单击“浏览”找到要使用的文件夹。  
  
6.  在“项目位置”对话框中，单击文件夹，再单击“打开”。  
  
7.  单击“确定” 。  
  
8.  默认情况下，将创建一个名为 Package.dtsx 的空包，并将该包添加到项目中。 但是您将不使用此包；相反您将现有的包添加到项目。 由于项目中的所有包都包括在部署中，因此您应该删除 Package.dtsx。 若要删除它，右键单击它，再单击“删除”。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [步骤 3：添加包和其他文件](../integration-services/lesson-1-3-adding-packages-and-other-files.md)  
  
![集成服务图标 （小）](media/dts-16.gif "Integration Services 图标 （小）")**保持最新的 Integration Services**<br /> 若要从 Microsoft 获得最新的下载内容、文章、示例和视频，以及从社区获得所选解决方案，请访问 MSDN 上的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 页：<br /><br /> [访问 MSDN 上的 Integration Services 页](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要获得有关这些更新的自动通知，请订阅该页上提供的 RSS 源。  
  
## <a name="see-also"></a>请参阅  
 [Integration Services (SSIS) 项目](integration-services-ssis-projects-and-solutions.md)  
  
  
