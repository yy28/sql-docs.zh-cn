---
title: 步骤 1：创建新的 Integration Services 项目 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: tutorial
applies_to:
- SQL Server 2016
ms.assetid: f14521b5-941e-443b-8f5e-385f98e37fbf
caps.latest.revision: 21
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 8a069c182303a3eae720a492b6e3a9013b2b0998
ms.sourcegitcommit: de5e726db2f287bb32b7910831a0c4649ccf3c4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/12/2018
ms.locfileid: "35329361"
---
# <a name="lesson-1-1---creating-a-new-integration-services-project"></a>第 1-1 课 - 创建新的 Integration Services 项目
若要在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 中创建包，第一步是创建一个 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目。 此项目包含在数据转换解决方案中使用的数据源、数据源视图和包等对象的模板。  
  
将在本 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 教程中创建的包用于解释受区域设置影响的数据的值。 如果您的计算机未配置为使用区域选项“英语(美国)”，则需要在包中设置其他属性。 第 2 课到第 5 课中使用的包是从第 1 课中创建的包复制而来的，因此不需要更新复制的包中受区域设置影响的属性。  
  
> [!NOTE]  
> 本教程需要 Microsoft SQL Server Data Tools。  
>   
> 有关安装 SQL Server Data Tools 的详细信息，请参阅 [SQL Server Data Tools 下载](http://msdn.microsoft.com/data/hh297027)。  
  
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
[步骤 2：添加和配置平面文件连接管理器](../integration-services/lesson-1-2-adding-and-configuring-a-flat-file-connection-manager.md)  
  
