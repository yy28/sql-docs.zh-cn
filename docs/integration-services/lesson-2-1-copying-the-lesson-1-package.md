---
title: 步骤 1：复制第 1 课包 | Microsoft Docs
ms.custom: ''
ms.date: 01/03/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 7f1616c2-2b4e-4010-be50-27d7b897403a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: c6cc61605413b84e3fed5e3ea507429693ad0d3d
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/22/2020
ms.locfileid: "86917273"
---
# <a name="lesson-2-1-copy-the-lesson-1-package"></a>第 2-1 课：复制第 1 课包

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]



在本任务中，创建 Lesson 1.dtsx 包的副本  。 如果未完成第 1 课，可以使用此本教程中附带的已完成的第 1 课包。 使用这一新副本来完成第 2 课剩余部分。  
  
## <a name="create-the-lesson-2-package"></a>创建第 2 课包  

如果将复制已完成的第 1 课，请使用此过程。  若要复制第 1 课的示例，请参阅下一节。
  
1.  如果 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools 尚未打开，请选择“开始” > “所有程序” > “Microsoft SQL Server 2017”，然后选择 SQL Server Data Tools     。  
  
2.  在“文件”菜单中，选择“打开” > “项目/解决方案”，选择“SSIS Tutorial”文件夹，选择“打开”，然后双击“SSIS Tutorial.sln”       。  
  
3.  在解决方案资源管理器中，右键单击“Lesson 1.dtsx”，然后选择“复制”    。  
  
4.  在解决方案资源管理器中，右键单击“SSIS 包”，再选择“粘贴”    。  
  
    默认情况下，复制的包命名为 Lesson 2.dtsx  。  
  
5.  在解决方案资源管理器中，双击“Lesson 2.dtsx”打开此包  
  
6.  右键单击“控制流”设计图面背景的任意位置，再选择“属性”   。  
  
7.  在“属性”窗口中，将 Name 属性更改为 Lesson 2    。  
  
8.  选择 ID 属性框，选择下拉箭头，然后选择“\<Generate New ID>” 。  
  
## <a name="use-the-sample-lesson-1-package"></a>使用示例第 1 课包  
  
1.  依次打开 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools 和 SSIS Tutorial 项目。  
  
2.  在解决方案资源管理器中，右键单击“SSIS 包”，再选择“添加现有包”    。  
  
3.  在“添加现有包的副本”对话框的“包位置”中，选择“文件系统”    。  
  
4.  选择浏览按钮 (…)，导航到计算机上的“Lesson 1.dtsx”，然后选择“打开”    。  
  
5.  按上一节中的步骤 3-8 中所述，复制并粘贴第 1 课包。  
  
## <a name="go-to-next-task"></a>转到下一个任务

[步骤 2：添加和配置 Foreach 循环容器](../integration-services/lesson-2-2-adding-and-configuring-the-foreach-loop-container.md)  
  
