---
title: 步骤 1：复制第 5 课包 | Microsoft Docs
ms.custom: ''
ms.date: 01/11/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: a25fcc13-987e-4f3d-8f0c-76f7e6e59920
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 2c4c895e71da13d7de38bf5dfc64f27829206d25
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/26/2019
ms.locfileid: "71283117"
---
# <a name="lesson-6-1-copy-the-lesson-5-package"></a>第 6-1 课：复制第 5 课包

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



在本任务中，为第 5 课中的 Lesson 5.dtsx 包创建一个副本  。 如果未完成第 5 课，则可以向项目添加本教程中附带的已完成的第 5 课包，然后再对其进行复制以供使用。 使用这一新副本来完成第 6 课剩余部分。 

> [!IMPORTANT]
> 在复制 Lesson 5 包后，如果当前解决方案中有来自以前课程的包，请右键单击来自课程 1-5 的每个包并选择“从项目中排除”  。 完成后，解决方案中应只有 Lesson 6.dtsx  。   
  
## <a name="create-the-lesson-6-package"></a>创建第 6 课包  
  
如果将复制已完成的第 5 课，请使用此过程。  若要复制第 5 课示例，请参阅下一节。

1.  如果 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools 尚未打开，请选择“开始” > “所有程序” > “Microsoft SQL Server 2017”，然后选择 SQL Server Data Tools     。

2.  在“文件”菜单中，选择“打开” > “项目/解决方案”，选择“SSIS Tutorial”文件夹，选择“打开”，然后双击“SSIS Tutorial.sln”       。

3.  在“解决方案资源管理器”中，右键单击“Lesson 5.dtsx”，然后选择“复制”    。

4.  在解决方案资源管理器中，右键单击“SSIS 包”，再选择“粘贴”    。

    默认情况下，复制的包名为 Lesson 5.dtsx  。

5.  在“解决方案资源管理器”中，双击“Lesson 5.dtsx”打开此包  

6.  右键单击“控制流”设计图面背景的任意位置，再选择“属性”   。

7.  在“属性”窗口中，将“名称”属性更改为 Lesson 6    。

8.  选择 ID 属性框，选择下拉箭头，然后选择“\<生成新 ID>”   。

## <a name="add-the-completed-lesson-5-package"></a>添加已完成的第 5 课包

1.  依次打开 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools 和 SSIS Tutorial 项目。

2.  在解决方案资源管理器中，右键单击“SSIS 包”，再选择“添加现有包”    。

3.  在“添加现有包的副本”  对话框的“包位置”  中，选择“文件系统”  。

4.  选择浏览按钮 (…)，导航到计算机上的“Lesson 5.dtsx”，然后选择“打开”    。

5.  按上一节的步骤 3-8 中所述，复制并粘贴第 5 课包。

## <a name="go-to-next-task"></a>转到下一个任务
[步骤 2：将项目转换为项目部署模型](../integration-services/lesson-6-2-converting-the-project-to-the-project-deployment-model.md)  
  
