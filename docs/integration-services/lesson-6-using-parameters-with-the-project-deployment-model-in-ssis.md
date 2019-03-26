---
title: 第 6 课：在 SSIS 中对项目部署模型使用参数 | Microsoft Docs
ms.custom: ''
ms.date: 01/11/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 9216f18c-1762-4f2d-8c22-bd0ab7107555
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b9ebfb17a69abbaf8482999d3435bbdea11e0822
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/20/2019
ms.locfileid: "58289893"
---
# <a name="lesson-6-use-parameters-with-the-project-deployment-model-in-ssis"></a>第 6 课：在 SSIS 中对项目部署模型使用参数

SQL Server 2012 引入了一个新的部署模型，可在其中将项目部署到 Integration Services 服务器。 通过 Integration Services 服务器，您可以管理和运行包，以及为包配置运行时值。  
  
在本课中，将修改在[第 5 课：为包部署模型添加 SSIS 包配置](../integration-services/lesson-5-add-ssis-package-configurations-for-the-package-deployment-model.md)中创建的包，以使用项目部署模型。 您将使用一个参数替换该配置值，以便指定示例数据位置。 还可以复制本教程附带的已完成的 Lesson 5 包。  
  
使用 Integration Services 项目配置向导，可将项目转换为项目部署模型。 此模型使用参数而非配置值来设置 Directory 属性。 本课部分介绍了您将现有 SSIS 包转换为新的项目部署模型时要遵循的步骤。  
  
再次运行包时，[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务器使用参数来填充变量的值。 该变量转而会更新 Directory 属性。 包循环访问新参数指定的数据文件夹中的文件。  
  
> [!NOTE]
> 如果尚不具备必备条件，请参阅[第 1 课必备条件](../integration-services/lesson-1-create-a-project-and-basic-package-with-ssis.md#prerequisites)。
    
## <a name="lesson-tasks"></a>课程任务  
本课程包含以下任务：  
  
1.  [第 1 步：复制第 5 课包](../integration-services/lesson-6-1-copying-the-lesson-5-package.md)  
  
2.  [步骤 2：将项目转换为项目部署模型](../integration-services/lesson-6-2-converting-the-project-to-the-project-deployment-model.md)  
  
3.  [步骤 3：测试第 6 课包](../integration-services/lesson-6-3-testing-the-lesson-6-package.md)  
  
4.  [步骤 4：部署第 6 课包](../integration-services/lesson-6-4-deploying-the-lesson-6-package.md)  
  
## <a name="start-the-lesson"></a>开始课程  
[第 1 步：复制第 5 课包](../integration-services/lesson-6-1-copying-the-lesson-5-package.md)  
  
