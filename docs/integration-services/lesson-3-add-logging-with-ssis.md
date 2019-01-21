---
title: 第 3 课：使用 SSIS 添加日志记录 | Microsoft Docs
ms.custom: ''
ms.date: 01/04/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 64cd24cc-ba8e-4bd7-b10b-6b80d8b04af6
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 790738d3c66d4b973d2f6934e89caa77af6ffde0
ms.sourcegitcommit: dd794633466b1da8ead9889f5e633bdf4b3389cd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/09/2019
ms.locfileid: "54142997"
---
# <a name="lesson-3-add-logging-with-ssis"></a>第 3 课：使用 SSIS 添加日志记录

[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 包含日志记录功能，可通过提供任务和容器事件跟踪监控包执行情况以及进行故障排除。 日志记录功能非常灵活。 可以在包级别或包中的单个任务或容器上启用日志记录。 选择要记录的事件，也可以对单个包创建多个日志。  
  
日志提供程序创建日志。 每个日志提供程序可以将日志记录信息写入不同的格式和目标类型。 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 提供以下日志提供程序：  
  
-   文本文件  
  
-   [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)]  
  
-   Windows 事件日志  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  
  
-   XML 文件  
  
在本课中，将为[第 2 课中创建的包创建副本：使用 SSIS 添加循环](../integration-services/lesson-2-adding-looping-with-ssis.md)。 然后使用该新包添加和配置日志记录，以在包执行过程中监控特定事件。 如果尚未完成前面的任何课程，也可以复制本教程附带的已完成的第 2 课包。  

> [!NOTE]
> 如果尚不具备必备条件，请参阅[第 1 课必备条件](../integration-services/lesson-1-create-a-project-and-basic-package-with-ssis.md#prerequisites)。

## <a name="lesson-tasks"></a>课程任务  
本课程包含以下任务：  
  
-   [第 1 步：复制第 2 课包](../integration-services/lesson-3-1-copying-the-lesson-2-package.md)  
  
-   [步骤 2：添加和配置日志记录](../integration-services/lesson-3-2-adding-and-configuring-logging.md)  
  
-   [步骤 3：测试第 3 课包](../integration-services/lesson-3-3-testing-the-lesson-3-tutorial-package.md)  
  
## <a name="start-the-lesson"></a>开始课程  
[第 1 步：复制第 2 课包](../integration-services/lesson-3-1-copying-the-lesson-2-package.md)  
  
