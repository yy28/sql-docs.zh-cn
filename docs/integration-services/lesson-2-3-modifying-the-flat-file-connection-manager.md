---
title: "步骤 3： 修改平面文件连接管理器 |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: integration-services
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 459e3995-2116-4f15-aaa2-32f26113869c
caps.latest.revision: 20
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 525557f034199c5e6823c18ab9fdb7c3b505a434
ms.contentlocale: zh-cn
ms.lasthandoff: 09/26/2017

---
# <a name="lesson-2-3---modifying-the-flat-file-connection-manager"></a>课程 2-3-修改平面文件连接管理器
在本任务中，您将修改在第 1 课中创建和配置的平面文件连接管理器。 平面文件连接管理器在最初创建时配置为静态加载单个文件。 若要启用平面文件连接管理器以重复加载文件，必须修改连接管理器的 ConnectionString 属性以接受用户定义的变量 `User:varFileName`，该变量包含要在运行时加载的文件的路径。  
  
通过将连接管理器修改为使用用户定义的变量 `User::varFileName`的值并填充连接管理器的 ConnectionString 属性，连接管理器将能够连接到不同的平面文件。 在运行时，Foreach 循环容器的每次迭代都将动态更新 `User::varFileName` 变量。 更新变量时，还会使连接管理器连接到不同的平面文件，并使数据流任务处理其他数据集。  
  
### <a name="to-configure-the-flat-file-connection-manager-to-use-a-variable-for-the-connection-string"></a>配置平面文件连接管理器以使用连接字符串的变量  
  
1.  在 **“连接管理器”** 窗格中，右键单击 **Sample Flat File Source Data**，再选择 **“属性”**。  
  
2.  在“属性”窗口中，针对 **“表达式”**，单击空单元，然后单击省略号按钮 **“(…)”**。  
  
3.  在 **“属性表达式编辑器”** 对话框的 **“属性”** 列中，键入或选择 **ConnectionString**。  
  
4.  在 **“表达式”** 列中，单击省略号按钮 **“(…)”** 以打开 **“表达式生成器”** 对话框。  
  
5.  在 **“表达式生成器”** 对话框中，展开 **“变量”** 节点。  
  
6.  将变量 **User::varFileName**拖到 **“表达式”** 框中。  
  
7.  单击 **“确定”** 关闭 **“表达式生成器”** 对话框。  
  
8.  再次单击 **“确定”** 关闭 **“属性表达式编辑器”** 对话框。  
  
## <a name="next-lesson-task"></a>下一课程任务  
[步骤 4：测试第 2 课教程包](../integration-services/lesson-2-4-testing-the-lesson-2-tutorial-package.md)  
  
  
  

