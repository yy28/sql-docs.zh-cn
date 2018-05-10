---
title: 步骤 1：复制第 5 课包 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
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
ms.assetid: a25fcc13-987e-4f3d-8f0c-76f7e6e59920
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 54e8f15d4cb049fa6dd79041668e3db998d196af
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="lesson-6-1---copying-the-lesson-5-package"></a>第 6-1 课 - 复制第 5 课包
在本任务中，您将为第 5 课中创建的 Lesson 5.dtsx 包创建一个副本。 或者将本教程中附带的已完成的 Lesson 5 包添加到项目中，然后再对其进行复制。 您将使用这一新副本来完成第 6 课剩余部分。  
  
### <a name="to-copy-the-lesson-5-package"></a>复制 Lesson 5 包  
  
1.  如果 SQL Server Data Tools 尚未打开，请单击“开始”，依次指向“所有程序”和“Microsoft SQL Server 2012”，然后单击“SQL Server Data Tools”。  
  
2.  在“文件”菜单中，单击“打开”，单击“项目/解决方案”，选择 SSIS Tutorial，再单击“打开”，然后双击 SSIS Tutorial.sln。  
  
3.  在解决方案资源管理器中，右键单击“Lesson 5.dtsx”，然后单击“复制”。  
  
4.  在解决方案资源管理器中，右键单击“SSIS 包”，再单击“粘贴”。  
  
    默认情况下，复制的包命名为 Lesson 6.dtsx。  
  
5.  在解决方案资源管理器中，双击“Lesson 6.dtsx”打开该包。  
  
6.  右键单击“控制流”选项卡背景的任意位置，再单击“属性”。  
  
7.  在“属性”窗口中，将 Name 属性更新为 Lesson 6。  
  
8.  依次单击“ID”属性框和下拉箭头，然后单击“ <Generate New ID>”。  
  
### <a name="to-add-the-completed-lesson-5-package"></a>添加已完成的 Lesson 5 包  
  
1.  依次打开 SQL Server Data Tools 和 SSIS Tutorial 项目。  
  
2.  在解决方案资源管理器中，右键单击“SSIS 包”，再单击“添加现有包”。  
  
3.  在“添加现有包的副本”对话框的“包位置”中，选择“文件系统”。  
  
4.  依次单击浏览“(...)”按钮和计算机上的 Lesson 5.dtsx，然后单击“打开”。  
  
    要下载此教程的所有课程包，请执行以下操作：  
  
    1.  导航到 [Integration Services 产品示例](http://go.microsoft.com/fwlink/?LinkId=275027)  
  
    2.  单击 **“下载”** 选项卡。  
  
    3.  单击 SQL2012.Integration_Services.Create_Simple_ETL_Tutorial.Sample.zip 文件。  
  
5.  按先前过程中的步骤 3-8 中所述，复制并粘贴 Lesson 5 包。  
  
    在复制 Lesson 5 包后，如果当前解决方案中有来自以前课程的包，请右键单击来自课程 1-5 的每个包并单击“从项目中排除”。 完成后，您的解决方案中应只有 Lesson 6.dtsx。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
[步骤 2：将项目转换为项目部署模型](../integration-services/lesson-6-2-converting-the-project-to-the-project-deployment-model.md)  
  
