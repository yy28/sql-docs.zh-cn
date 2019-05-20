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
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f4d8fdf2a714f47e40e4c2afe12bb7357068fa9d
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/16/2019
ms.locfileid: "65722079"
---
# <a name="lesson-3-add-logging-with-ssis"></a>第 3 课：使用 SSIS 添加日志记录

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



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
  
-   [步骤 1：复制第 2 课包](../integration-services/lesson-3-1-copying-the-lesson-2-package.md)  
  
-   [步骤 2：添加和配置日志记录](../integration-services/lesson-3-2-adding-and-configuring-logging.md)  
  
-   [步骤 3：测试第 3 课包](../integration-services/lesson-3-3-testing-the-lesson-3-tutorial-package.md)  
  
## <a name="start-the-lesson"></a>开始课程  
[步骤 1：复制第 2 课包](../integration-services/lesson-3-1-copying-the-lesson-2-package.md)  
  
