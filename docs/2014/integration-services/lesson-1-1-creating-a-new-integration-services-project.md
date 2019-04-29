---
title: 第 1 步：创建新的 Integration Services 项目 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: f14521b5-941e-443b-8f5e-385f98e37fbf
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 2513a698fc073c751613e8e387d41ddb3e0fe9e4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62891756"
---
# <a name="step-1-creating-a-new-integration-services-project"></a>第 1 步：创建新的 Integration Services 项目
  若要在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 中创建包，第一步是创建一个 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目。 此项目包含在数据转换解决方案中使用的数据源、数据源视图和包等对象的模板。  
  
 将在本 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 教程中创建的包用于解释受区域设置影响的数据的值。 如果您的计算机未配置为使用区域选项“英语(美国)”，则需要在包中设置其他属性。 第 2 课到第 5 课中使用的包是从第 1 课中创建的包复制而来的，因此不需要更新复制的包中受区域设置影响的属性。  
  
> [!NOTE]  
>  本教程需要 Microsoft SQL Server Data Tools。  
>   
>  有关安装 SQL Server Data Tools 的详细信息，请参阅 [SQL Server Data Tools 下载](https://msdn.microsoft.com/data/hh297027)。  
  
### <a name="to-create-a-new-integration-services-project"></a>创建新的 Integration Services 项目  
  
1.  在 **“开始”** 菜单上，依次指向 **“所有程序”**、 **Microsoft SQL Server**，再单击 **SQL Server Data Tools**。  
  
2.  在“文件”菜单中，指向“新建”，再单击“项目”，以创建一个新的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目。  
  
3.  在“新建项目”对话框中，展开“已安装的模板”下的“商业智能”节点，并在“模板”窗格中选择“Integration Services 项目”。  
  
4.  在“名称”框中，将默认名称更改为 **SSIS Tutorial**。 或者，清除“创建解决方案的目录”复选框。  
  
5.  接受默认位置，或单击“浏览”，以浏览并找到要使用的文件夹。 在“项目位置”对话框中，单击文件夹，再单击“选择文件夹”。  
  
6.  单击“确定” 。  
  
     默认情况下，将创建一个名为 **Package.dtsx** 的空包，并将该包添加到项目中的“SSIS 包”之下。  
  
7.  在“解决方案资源管理器”工具栏中，右键单击“Package.dtsx”，再单击“重命名”，将默认包重命名为 **Lesson 1.dtsx**。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [步骤 2：添加和配置平面文件连接管理器](lesson-1-2-adding-and-configuring-a-flat-file-connection-manager.md)  
  
  
