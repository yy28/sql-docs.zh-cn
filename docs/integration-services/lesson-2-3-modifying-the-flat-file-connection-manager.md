---
title: 步骤 3：修改平面文件连接管理器 | Microsoft Docs
ms.custom: ''
ms.date: 01/03/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 459e3995-2116-4f15-aaa2-32f26113869c
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 1de57ab14dc4dcfc07f838494ca48f8b12da6660
ms.sourcegitcommit: dd794633466b1da8ead9889f5e633bdf4b3389cd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/09/2019
ms.locfileid: "54143557"
---
# <a name="lesson-2-3-modify-the-flat-file-connection-manager"></a>第 2-3 课：修改平面文件连接管理器

在本任务中，将修改第 1 课中的平面文件连接管理器。 平面文件连接管理器配置为静态加载单个文件。 若要启用平面文件连接管理器以重复加载文件，请更改连接管理器的 ConnectionString 属性以使用用户定义的变量 `User::varFileName`，该变量包含要在运行时加载的文件的路径。  
  
通过修改连接管理器以使用用户定义变量的值来更改 ConnectionString 属性，连接管理器将连接到不同的平面文件。 在运行时，Foreach 循环容器的每次迭代都更新 `User::varFileName` 变量。 更新变量时，还会使连接管理器连接到不同的平面文件，并使数据流任务处理其他数据集。  
  
## <a name="configure-the-flat-file-connection-manager-to-use-a-variable"></a>配置平面文件连接管理器以使用变量  
  
1.  在 **“连接管理器”** 窗格中，右键单击 **Sample Flat File Source Data**，再选择 **“属性”**。  
  
2.  在“属性”窗口中，针对“表达式”，选择空单元，然后选择省略号按钮“(…)”。  
  
3.  在“属性表达式编辑器”对话框的“属性”列中，选择 ConnectionString。  
  
4.  在“表达式”列中，选择省略号按钮“(…)”以打开“表达式生成器”对话框。  
  
5.  在“表达式生成器”对话框中，展开“变量”节点。  
  
6.  将变量 User::varFileName 拖到“表达式”框中。  
  
7.  选择“确定”，关闭“表达式生成器”对话框。  
  
8.  再次选择“确定”，关闭“属性表达式编辑器”对话框。  
  
## <a name="go-to-next-task"></a>转到下一个任务  
[步骤 4：测试第 2 课教程包](../integration-services/lesson-2-4-testing-the-lesson-2-tutorial-package.md)  
  
  
  
