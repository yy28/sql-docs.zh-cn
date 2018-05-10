---
title: 第 6 课：在 SSIS 中对项目部署模型使用参数 | Microsoft Docs
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
ms.assetid: 9216f18c-1762-4f2d-8c22-bd0ab7107555
caps.latest.revision: 5
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 84c96d55cc2aead955b637f5246ead7bff610c97
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="lesson-6-using-parameters-with-the-project-deployment-model-in-ssis"></a>第 6 课：在 SSIS 中对项目部署模型使用参数
SQL Server 2012 引入了一个新的部署模型，可用于将您的项目部署到 Integration Services 服务器。 通过 Integration Services 服务器，您可以管理和运行包，以及为包配置运行时值。  
  
在本课中，将修改在 [第 5 课：为包部署模型添加 SSIS 包配置](../integration-services/lesson-5-add-ssis-package-configurations-for-the-package-deployment-model.md) 中创建的包，以便使用项目部署模型。 您将使用一个参数替换该配置值，以便指定示例数据位置。 还可以复制本教程附带的已完成的 Lesson 5 包。  
  
使用 Integration Services 项目配置向导，您将该项目转换为项目部署模型，并且使用参数而不是配置值来设置 Directory 属性。 本课部分介绍了您将现有 SSIS 包转换为新的项目部署模型时要遵循的步骤。  
  
再次运行包时，Integration Services 服务使用参数填充变量的值，而变量又会更新 Directory 属性。 结果，包将遍历该参数值指定的新数据文件夹中的文件，而不是遍历在包配置文件中设置的文件夹。  
  
> [!IMPORTANT]  
> 本教程需要 **AdventureWorksDW2012** 示例数据库。 有关如何安装和部署 **AdventureWorksDW2012** 的详细信息，请参阅[安装 SQL Server 示例和示例数据库的注意事项](http://technet.microsoft.com/library/ms161556%28v=sql.105%29)。  
  
## <a name="lesson-tasks"></a>课程任务  
本课程包含以下任务：  
  
1.  [步骤 1：复制第 5 课包](../integration-services/lesson-6-1-copying-the-lesson-5-package.md)  
  
2.  [步骤 2：将项目转换为项目部署模型](../integration-services/lesson-6-2-converting-the-project-to-the-project-deployment-model.md)  
  
3.  [步骤 3：测试 Lesson 6 包](../integration-services/lesson-6-3-testing-the-lesson-6-package.md)  
  
4.  [步骤 4：部署第 6 课包](../integration-services/lesson-6-4-deploying-the-lesson-6-package.md)  
  
## <a name="start-the-lesson"></a>开始课程  
[步骤 1：复制第 5 课包](../integration-services/lesson-6-1-copying-the-lesson-5-package.md)  
  
