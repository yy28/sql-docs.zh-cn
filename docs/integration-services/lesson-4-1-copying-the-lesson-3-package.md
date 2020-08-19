---
description: 第 4-1 课：复制第 3 课包
title: 步骤 1：复制第 3 课包 | Microsoft Docs
ms.custom: ''
ms.date: 01/07/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 0d053786-5203-43f3-a613-27a8dd2bc44a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 7476bf5318efcdc7c188dda74a1231d8d4aed094
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449635"
---
# <a name="lesson-4-1-copy-the-lesson-3-package"></a>第 4-1 课：复制第 3 课包

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]



在本任务中，为第 3 课中的 Lesson 3.dtsx 包创建一个副本。 如果未完成第 3 课，则可以向项目添加本教程中附带的已完成的第 3 课包，然后再对其进行复制以供使用。 使用这一新副本来完成第 4 课剩余部分。  
  
## <a name="create-the-lesson-4-package"></a>创建第 4 课包  
  
如果将复制已完成的第 3 课，请使用此过程。  若要复制第 3 课的示例，请参阅下一节。

1.  如果 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools 尚未打开，请选择“开始” > “所有程序” > “Microsoft SQL Server 2017”，然后选择 SQL Server Data Tools     。

2.  在“文件”菜单中，选择“打开” > “项目/解决方案”，选择“SSIS Tutorial”文件夹，选择“打开”，然后双击“SSIS Tutorial.sln”       。

3.  在解决方案资源管理器中，右键单击“Lesson 3.dtsx”，然后选择“复制”    。

4.  在解决方案资源管理器中，右键单击“SSIS 包”，再选择“粘贴”    。

    默认情况下，复制的包名称为 Lesson 4.dtsx  。

5.  在解决方案资源管理器中，双击“Lesson 4.dtsx”打开此包

6.  右键单击“控制流”设计图面背景的任意位置，再选择“属性”   。

7.  在“属性”窗口中，将 Name 属性更改为 Lesson 4    。

8.  选择 ID 属性框，选择下拉箭头，然后选择“\<Generate New ID>” 。

## <a name="add-the-completed-lesson-3-package"></a>添加已完成的第 3 课包

1.  依次打开 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools 和 SSIS Tutorial 项目。

2.  在解决方案资源管理器中，右键单击“SSIS 包”，再选择“添加现有包”    。

3.  在“添加现有包的副本”  对话框的“包位置”  中，选择“文件系统”  。

4.  选择浏览按钮 (…)，导航到计算机上的“Lesson 3.dtsx”，然后选择“打开”    。

5.  按上一节中的步骤 3-8 中所述，复制并粘贴第 3 课包。

  
## <a name="go-to-next-task"></a>转到下一个任务  
[步骤 2：创建损坏的文件](../integration-services/lesson-4-2-creating-a-corrupted-file.md)  
  
