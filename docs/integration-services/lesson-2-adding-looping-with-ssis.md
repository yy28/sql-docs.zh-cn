---
title: 第 2 课：使用 SSIS 添加循环 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 01f2ed61-1e5a-4ec6-b6a6-2bd070c64077
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 5b26f7b7a36d024ec18de617b08fdefe2d352083
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47686195"
---
# <a name="lesson-2-adding-looping-with-ssis"></a>第 2 课：使用 SSIS 添加循环
在 [第 1 课：使用 SSIS 创建项目包和基础包](../integration-services/lesson-1-create-a-project-and-basic-package-with-ssis.md)中，创建了从单个平面文件源中提取数据的包，然后使用查找转换功能对数据进行了转换，最后将数据加载到 **AdventureWorksDW2012** 示例数据库的 **FactCurrency** 事实数据表中。  
  
但是，提取、转换和加载 (ETL) 过程很少使用单个平面文件。 典型的 ETL 过程从多个平面文件源提取数据。 从多个源提取数据需要采用迭代控制流。 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 最可能出现的功能之一是可以方便快捷地向包中添加迭代或循环。  
  
[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 为循环遍历包提供了两种容器类型：Foreach 循环容器和 For 循环容器。 Foreach 循环容器使用枚举器执行循环，而 For 循环容器则通常使用变量表达式。 本课使用 Foreach 循环容器。  
  
Foreach 循环容器使包能够对指定枚举器的每个成员重复执行控制流。 使用 Foreach 循环容器，可以枚举：  
  
-   ADO 记录集行  
  
-   ADO .Net 架构信息  
  
-   文件和目录结构  
  
-   系统、包和用户变量  
  
-   在变量中包含的可枚举对象  
  
-   集合中的项  
  
-   XML Path 语言 (XPath) 表达式中的节点  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 管理对象 (SMO)  
  
在本课中，您将修改在第 1 课中创建的简单 ETL 包，以便利用 Foreach 循环容器。 还将设置用户定义的包变量，以便使该教程包能够迭代遍历文件夹中的所有平面文件。 如果您尚未完成上一课，则也可以复制本教程中附带的已完成的 Lesson 1 包。  
  
在本课中，将不修改数据流，而只修改控制流。  
  
> [!IMPORTANT]  
> 本教程需要 **AdventureWorksDW2012** 示例数据库。 有关如何安装和部署 **AdventureWorksDW2012**的详细信息，请参阅 [CodePlex 上的 Reporting Services 产品示例](http://go.microsoft.com/fwlink/p/?LinkID=526910)。  
  
## <a name="lesson-tasks"></a>课程任务  
本课程包含以下任务：  
  
-   [步骤 1：复制第 1 课包](../integration-services/lesson-2-1-copying-the-lesson-1-package.md)  
  
-   [步骤 2：添加和配置 Foreach 循环容器](../integration-services/lesson-2-2-adding-and-configuring-the-foreach-loop-container.md)  
  
-   [步骤 3：修改平面文件连接管理器](../integration-services/lesson-2-3-modifying-the-flat-file-connection-manager.md)  
  
-   [步骤 4：测试第 2 课教程包](../integration-services/lesson-2-4-testing-the-lesson-2-tutorial-package.md)  
  
## <a name="start-the-lesson"></a>开始课程  
[步骤 1：复制 Lesson 1 包](../integration-services/lesson-2-1-copying-the-lesson-1-package.md)  
  
## <a name="see-also"></a>另请参阅  
[For 循环容器](../integration-services/control-flow/for-loop-container.md)  
  
  
  
