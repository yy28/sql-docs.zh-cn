---
title: "第 5 课：添加包部署模型的 SSIS 包配置 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: integration-services
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to: SQL Server 2016
ms.assetid: 1c10dd54-67cb-4b63-9e4d-aa6ff0452ecb
caps.latest.revision: "28"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: ca7f828ee5ade6114887f261b51b9086f17c40d9
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="lesson-5-add-ssis-package-configurations-for-the-package-deployment-model"></a>第 5 课：添加包部署模型的 SSIS 包配置
包配置允许您从开发环境的外部设置运行时属性和变量。 配置允许您开发灵活且易于部署和分发的包。 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 提供了以下配置类型：  
  
-   XML 配置文件  
  
-   环境变量  
  
-   注册表项  
  
-   父包变量  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 表  
  
在本课中，将修改在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 第 4 课：使用 SSIS 添加错误流重定向 [中创建的简单](../integration-services/lesson-4-add-error-flow-redirection-with-ssis.md) 包，以便使用包部署模型并利用包配置。 还可以复制本教程中附带的已完成的 Lesson 4 包。 使用包配置向导创建一个 XML 配置，该配置通过使用映射到 Directory 属性的包级别变量来更新 Foreach 循环容器的 **Directory** 属性。 在创建配置文件之后，将从开发环境的外部修改该变量的值，并将修改后的属性指向新的示例数据文件夹。 再次运行包时，配置文件将填充变量值，而变量将更新 **Directory**属性。 结果，包将迭代遍历新数据文件夹中的文件，而不是迭代遍历在该包中硬编码的原始文件夹中的文件。  
  
> [!IMPORTANT]  
> 本教程需要 **AdventureWorksDW2012** 示例数据库。 有关如何安装和部署 **AdventureWorksDW2012**的详细信息，请参阅 [CodePlex 上的 Reporting Services 产品示例](http://go.microsoft.com/fwlink/p/?LinkID=526910)。  
  
## <a name="lesson-tasks"></a>课程任务  
本课程包含以下任务：  
  
-   [步骤 1：复制 Lesson 4 包](../integration-services/lesson-5-1-copying-the-lesson-4-package.md)  
  
-   [步骤 2：启用和配置包配置](../integration-services/lesson-5-2-enabling-and-configuring-package-configurations.md)  
  
-   [步骤 3：修改目录属性配置值](../integration-services/lesson-5-3-modifying-the-directory-property-configuration-value.md)  
  
-   [步骤 4：测试第 5 课教程包](../integration-services/lesson-5-4-testing-the-lesson-5-tutorial-package.md)  
  
## <a name="start-the-lesson"></a>开始课程  
  
-   [步骤 1：复制 Lesson 4 包](../integration-services/lesson-5-1-copying-the-lesson-4-package.md)  
  
  
  
