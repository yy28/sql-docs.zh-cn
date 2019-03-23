---
title: 第 6 课：使用项目部署模型使用参数 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 9216f18c-1762-4f2d-8c22-bd0ab7107555
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d559defe1dd08f26077738cdd0aea219e8f7554b
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/22/2019
ms.locfileid: "58384955"
---
# <a name="lesson-6-using-parameters-with-the-project-deployment-model"></a>第 6 课：对项目部署模型使用参数
  SQL Server 2012 引入了一个新的部署模型，可用于将您的项目部署到 Integration Services 服务器。 通过 Integration Services 服务器，您可以管理和运行包，以及为包配置运行时值。  
  
 在本课程中，您将修改你在中创建的包[第 5 课：为包部署模型中添加包配置](lesson-5-add-ssis-package-configurations-for-the-package-deployment-model.md)以便使用项目部署模型。 您将使用一个参数替换该配置值，以便指定示例数据位置。 还可以复制本教程附带的已完成的 Lesson 5 包。  
  
 使用 Integration Services 项目配置向导，您将该项目转换为项目部署模型，并且使用参数而不是配置值来设置 Directory 属性。 本课部分介绍了您将现有 SSIS 包转换为新的项目部署模型时要遵循的步骤。  
  
 再次运行包时，Integration Services 服务使用参数填充变量的值，而变量又会更新 Directory 属性。 结果，包将遍历该参数值指定的新数据文件夹中的文件，而不是遍历在包配置文件中设置的文件夹。  
  
> [!IMPORTANT]  
>  本教程需要 **AdventureWorksDW2012** 示例数据库。 有关如何安装和部署 **AdventureWorksDW2012** 的详细信息，请参阅[安装 SQL Server 示例和示例数据库的注意事项](https://technet.microsoft.com/library/ms161556%28v=sql.105%29)。  
  
## <a name="lesson-tasks"></a>课程任务  
 本课程包含以下任务：  
  
1.  [第 1 步：复制第 5 课包](lesson-6-1-copying-the-lesson-5-package.md)  
  
2.  [步骤 2：将项目转换为项目部署模型](lesson-6-2-converting-the-project-to-the-project-deployment-model.md)  
  
3.  [步骤 3：测试第 6 课包](lesson-6-3-testing-the-lesson-6-package.md)  
  
4.  [步骤 4：部署第 6 课包](lesson-6-4-deploying-the-lesson-6-package.md)  
  
## <a name="start-the-lesson"></a>开始课程  
 [第 1 步：复制第 5 课包](lesson-6-1-copying-the-lesson-5-package.md)  
  
  
