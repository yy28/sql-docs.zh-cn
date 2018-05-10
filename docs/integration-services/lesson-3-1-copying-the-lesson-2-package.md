---
title: 步骤 1：复制第 2 课包 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: tutorial
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 4bd91402-4e37-41de-ab78-8ca5a1948a37
caps.latest.revision: 29
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: f3070c1ec86e43a88b0128a140c49e8f9c509333
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="lesson-3-1---copying-the-lesson-2-package"></a>第 3-1 课 - 复制第 2 课包
在本任务中，将为第 2 课中创建的 Lesson 2.dtsx 包创建一个副本。 或者，可以将本教程中附带的已完成的 Lesson 2 包添加到项目中，然后再对其进行复制。 将使用这个新副本来完成第 3 课的剩余部分。  
  
### <a name="to-create-the-lesson-3-package"></a>创建 Lesson 3 包  
  
1.  如果 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools 尚未打开，请单击“开始”，依次指向“所有程序”和“Microsoft SQL Server 2012”，然后单击“SQL Server Data Tools”。  
  
2.  在“文件”菜单中，依次单击“打开”和“项目/解决方案”，选择“SSIS Tutorial”，单击“打开”，然后双击“SSIS Tutorial.sln”。  
  
3.  在解决方案资源管理器中，右键单击“Lesson 2.dtsx”，然后单击“复制”。  
  
4.  在解决方案资源管理器中，右键单击“SSIS 包”，然后单击“粘贴”。  
  
    默认情况下，复制的包命名为 Lesson 3.dtsx。  
  
5.  在解决方案资源管理器中，双击“Lesson 3.dtsx”打开此包。  
  
6.  右键单击“控制流”选项卡背景的任意位置，然后单击“属性”。  
  
7.  在“属性”窗口中，将“Name”属性更新为 **Lesson 3**。  
  
8.  单击“ID”属性框，然后在列表中，单击“<Generate New ID>”。  
  
### <a name="to-add-the-completed-lesson2-package"></a>添加已完成的 Lesson 2 包  
  
1.  依次打开 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 和 SSIS Tutorial 项目。  
  
2.  在解决方案资源管理器中，右键单击“SSIS 包”，然后单击“添加现有包”。  
  
3.  在“添加现有包的副本”对话框的“包位置”中，选择“文件系统”。  
  
4.  单击浏览 **(…)** 按钮，导航到计算机上的“Lesson 2.dtsx”，然后单击“打开”。  
  
    要下载此教程的所有课程包，请执行以下操作：  
  
    1.  导航到 [Integration Services 产品示例](http://go.microsoft.com/fwlink/?LinkId=275027)  
  
    2.  单击 **“下载”** 选项卡。  
  
    3.  单击 SQL2012.Integration_Services.Create_Simple_ETL_Tutorial.Sample.zip 文件。  
  
5.  按先前过程中的步骤 3-8 中所述，复制并粘贴 Lesson 3 包。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
[步骤 2：添加并配置日志记录](../integration-services/lesson-3-2-adding-and-configuring-logging.md)  
  
