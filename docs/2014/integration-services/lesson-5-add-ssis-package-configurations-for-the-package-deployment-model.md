---
title: 第 5 课：添加包部署模型的包配置 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 1c10dd54-67cb-4b63-9e4d-aa6ff0452ecb
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 25922725e202bc7b38e2c6141a097df1af119ed2
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/22/2019
ms.locfileid: "58378825"
---
# <a name="lesson-5-adding-package-configurations-for-the-package-deployment-model"></a>第 5 课：添加包部署模型的包配置
  包配置允许您从开发环境的外部设置运行时属性和变量。 配置允许您开发灵活且易于部署和分发的包。 [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 提供了以下配置类型：  
  
-   XML 配置文件  
  
-   环境变量  
  
-   注册表项  
  
-   父包变量  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 表  
  
 在本课程中，您将修改简单[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]中创建的包[第 4 课：添加错误流重定向](lesson-4-add-error-flow-redirection-with-ssis.md)以便使用包部署模型并利用包配置。 还可以复制本教程中附带的已完成的 Lesson 4 包。 使用包配置向导，将创建一个 XML 配置，以便通过使用映射到 Directory 属性的包级别变量来更新 Foreach 循环容器的 `Directory` 属性。 在创建配置文件之后，将从开发环境的外部修改该变量的值，并将修改后的属性指向新的示例数据文件夹。 当再次运行包、 配置文件将填充变量的值和变量又会更新`Directory`属性。 结果，包将迭代遍历新数据文件夹中的文件，而不是迭代遍历在该包中硬编码的原始文件夹中的文件。  
  
> [!IMPORTANT]  
>  本教程需要 **AdventureWorksDW2012** 示例数据库。 有关如何安装和部署 **AdventureWorksDW2012**的详细信息，请参阅 [CodePlex 上的 Reporting Services 产品示例](https://go.microsoft.com/fwlink/?LinkID=526910)。  
  
## <a name="lesson-tasks"></a>课程任务  
 本课程包含以下任务：  
  
-   [第 1 步：复制第 4 课包](lesson-5-1-copying-the-lesson-4-package.md)  
  
-   [步骤 2：启用和配置包配置](lesson-5-2-enabling-and-configuring-package-configurations.md)  
  
-   [步骤 3：修改目录属性配置值](lesson-5-3-modifying-the-directory-property-configuration-value.md)  
  
-   [步骤 4：测试第 5 课教程包](lesson-5-4-testing-the-lesson-5-tutorial-package.md)  
  
## <a name="start-the-lesson"></a>开始课程  
  
-   [第 1 步：复制第 4 课包](lesson-5-1-copying-the-lesson-4-package.md)  
  
  
