---
title: "SSIS 如何创建 ETL 包 | Microsoft Docs"
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
helpviewer_keywords:
- SSIS, tutorials
- packages [Integration Services], tutorials
- Integration Services, tutorials
- SQL Server Integration Services, tutorials
- logs [Integration Services], tutorials
- walkthroughs [Integration Services]
ms.assetid: d6d5bb1f-4cb1-4605-9cd6-f60b858382c4
caps.latest.revision: "38"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: b14d05d686b26aaad7e6de24c9b445e0c4b1abf7
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="ssis-how-to-create-an-etl-package"></a>SSIS 如何创建 ETL 包

 > 如需与以前版本的 SQL Server 相关的内容，请参阅[教程：创建简单的 ETL 包](https://msdn.microsoft.com/en-US/library/ms169917(SQL.120).aspx)。

[!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] (SSIS) 是一个可用于生成高性能数据集成解决方案的平台，其中包括数据仓库的提取、转换和加载 (ETL) 包。 SSIS 包括生成并调试包的图形工具和向导；执行如 FTP 操作、执行 SQL 语句和发送电子邮件等工作流功能的任务；用于提取和加载数据的数据源和目标；用于清理、聚合、合并和复制数据的转换；管理服务，即用于管理包执行和存储的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务；以及用于对 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 对象模型编程的应用程序编程接口 (API)。  
  
在本教程中，您将学习如何使用 [!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器创建一个简单的 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 包。 所创建的包将从平面文件提取数据，重新设置数据的格式，然后将已重新设置格式的数据插入到事实数据表中。 在下列课程中，将扩展包以阐释循环、包配置、日志记录和错误流。  
  
在安装教程所用的示例数据的同时，也会安装将在教程的每一课中创建的完整的包版本。 使用完整的包，您可以按需要跳过前面几课而从后面的课程开始学习教程。 如果您是第一次使用包或新的开发环境，我们建议从第 1 课开始学习。  
  
## <a name="what-you-will-learn"></a>学习内容  
熟悉 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 的新工具、控件和功能的最好方法，就是使用它们。 本教程将引导您使用 [!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器创建一个简单的 ETL 包，其中包含循环、配置、错误流逻辑和日志记录。  
  
## <a name="requirements"></a>要求  
本教程适用于熟悉基本数据库操作，但对 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]中的新功能认识有限的用户。  
  
若要使用本教程，系统中必须安装下列组件：  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 数据库的 **数据库的** 。 为了增强安全性，默认情况下不会安装示例数据库。 要下载 **AdventureWorksDW2012** 数据库，请参阅 [Adventure Works for SQL Server 2012](http://go.microsoft.com/fwlink/?LinkId=275026)。  
  
    > [!IMPORTANT]  
    > 附加数据库 (\*.mdf file) 时，默认情况下 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 将搜索 .ldf 文件。 在 **“附加数据库”** 对话框中单击“确定”前，您必须手动删除 .ldf 文件。  
    >   
    > 有关附加数据库的详细信息，请参阅 [Attach a Database](../relational-databases/databases/attach-a-database.md)。  
  
-   示例数据。 示例数据与 [!INCLUDE[ssIS](../includes/ssis-md.md)] 课程包一起提供。 要下载示例数据和课程包，请执行以下操作：  
  
    1.  导航到 [Integration Services 产品示例](http://go.microsoft.com/fwlink/?LinkId=275027)  
  
    2.  单击 **“下载”** 选项卡。  
  
    3.  单击 SQL2012.Integration_Services.Create_Simple_ETL_Tutorial.Sample.zip 文件。  
  
## <a name="lessons-in-this-tutorial"></a>本教程中的课程  
[第 1 课：使用 SSIS 创建项目和基本包](../integration-services/lesson-1-create-a-project-and-basic-package-with-ssis.md)  
在本课中，将创建一个简单的 ETL 包，从单个平面文件中提取数据，再使用查找转换转换数据，最后将所得结果加载到目标事实数据表中。  
  
[第 2 课：使用 SSIS 添加循环](../integration-services/lesson-2-adding-looping-with-ssis.md)  
在本课中，将扩展第 1 课中创建的包，利用新增的循环功能，将多个平面文件提取到单个数据流进程中。  
  
[第 3 课：使用 SSIS 添加日志记录](../integration-services/lesson-3-add-logging-with-ssis.md)  
在本课中，将扩展第 2 课中创建的包，利用新增的日志记录功能。  
  
[第 4 课：使用 SSIS 添加错误流重定向](../integration-services/lesson-4-add-error-flow-redirection-with-ssis.md)  
在本课中，将扩展第 3 课中创建的包，以便利用新增的错误输出配置。  
  
[第 5 课：添加包部署模型的 SSIS 包配置](../integration-services/lesson-5-add-ssis-package-configurations-for-the-package-deployment-model.md)  
在本课中，将扩展第 4 课中创建的包，利用新增的包配置选项。  
  
[第 6 课：在 SSIS 中对项目部署模型使用参数](../integration-services/lesson-6-using-parameters-with-the-project-deployment-model-in-ssis.md)  
在本课中，将扩展第 5 课中创建的包，以将新参数用于项目部署模型。  
  
  
  
