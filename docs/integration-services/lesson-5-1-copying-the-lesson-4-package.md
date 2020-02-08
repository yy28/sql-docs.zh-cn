---
title: 步骤 1：复制第 4 课包 | Microsoft Docs
ms.custom: ''
ms.date: 01/08/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 8aa7d690-4649-4c0a-ac6f-9504637ee426
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 17a72f7d11a2ed743bbede2852b6336ce808a75d
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "71295924"
---
# <a name="lesson-5-1-copy-the-lesson-4-package"></a>第 5-1 课：复制第 4 课包

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



在本任务中，为第 4 课中的 Lesson 4.dtsx 包创建一个副本  。 如果未完成第 4 课，则可以向项目添加本教程中附带的已完成的第 4 课包，然后再对其进行复制以供使用。 使用这一新副本来完成第 5 课的剩余部分。  
  
## <a name="create-the-lesson-5-package"></a>创建第 5 课包  
  
如果将复制已完成的第 4 课，请使用此过程。  若要复制第 4 课示例，请参阅下一节。

1.  如果 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools 尚未打开，请选择“开始” > “所有程序” > “Microsoft SQL Server 2017”，然后选择 SQL Server Data Tools     。

2.  在“文件”菜单中，选择“打开” > “项目/解决方案”，选择 SSIS Tutorial 文件夹，然后选择“打开”      。  然后，双击“SSIS Tutorial.sln”  。

3.  在“解决方案资源管理器”中，右键单击“Lesson 4.dtsx”，然后选择“复制”    。

4.  在“解决方案资源管理器”中，右键单击“SSIS 包”，再选择“粘贴”    。

    默认情况下，复制的包名称为 Lesson 4.dtsx  。

5.  在“解决方案资源管理器”中，双击“Lesson 4.dtsx”打开此包   。

6.  右键单击“控制流”设计图面背景的任意位置，再选择“属性”   。

7.  在“属性”窗口中，将“名称”属性更改为 Lesson 5    。

8.  选择 ID 属性框，选择下拉箭头，然后选择“\<生成新 ID>”   。

## <a name="add-the-completed-lesson-4-package"></a>添加已完成的第 4 课包

1.  依次打开 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools 和 SSIS Tutorial 项目。

2.  在解决方案资源管理器中，右键单击“SSIS 包”，再选择“添加现有包”    。

3.  在“添加现有包的副本”  对话框的“包位置”  中，选择“文件系统”  。

4.  选择浏览按钮 (…)，导航到计算机上的“Lesson 4.dtsx”，然后选择“打开”    。

5.  按上一节的步骤 3-8 中所述，复制并粘贴第 4 课包。
  
## <a name="go-to-next-task"></a>转到下一个任务  
[步骤 2：启用和配置包配置](../integration-services/lesson-5-2-enabling-and-configuring-package-configurations.md)  
  
