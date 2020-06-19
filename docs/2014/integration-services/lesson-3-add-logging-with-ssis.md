---
title: 第3课：添加日志记录 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 64cd24cc-ba8e-4bd7-b10b-6b80d8b04af6
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 22f08b13232b7ae90c7b1eacfe55a98a1f1ca283
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84965203"
---
# <a name="lesson-3-adding-logging"></a>第 3 课：添加日志记录
  [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 包含日志记录功能，可通过提供任务和容器事件跟踪监控包执行情况以及进行故障排除。 日志记录功能非常灵活，可以在包级别或在包中的各个任务和容器上启用。 可以选择要记录的事件，也可以对单个包创建多个日志。  
  
 日志记录由日志提供程序提供。 每个日志提供程序可以将日志记录信息写入不同的格式和目标类型。 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 提供以下日志提供程序：  
  
-   文本文件  
  
-   [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)]  
  
-   Windows 事件日志  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  
  
-   XML 文件  
  
 在本课中，您将为 [Lesson 2: Adding Looping](lesson-2-adding-looping-with-ssis.md)中创建的包创建副本。 使用这个新包，您将添加并配置日志记录，以在包执行过程中监控特定事件。 如果您尚未完成前面的任何课程，也可以复制本教程附带的已完成的 Lesson 2 包。  
  
> [!IMPORTANT]  
>  本教程需要 **AdventureWorksDW2012** 示例数据库。 有关如何安装和部署**AdventureWorksDW2012**的详细信息，请[Reporting Services GitHub 上的产品示例](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks)。  
  
## <a name="lesson-tasks"></a>课程任务  
 本课程包含以下任务：  
  
-   [步骤 1：复制第 2 课包](lesson-3-1-copying-the-lesson-2-package.md)  
  
-   [步骤 2：添加并配置日志记录](lesson-3-2-adding-and-configuring-logging.md)  
  
-   [步骤 3：测试第 3 课教程包](../integration-services/lesson-3-3-testing-the-lesson-3-tutorial-package.md)  
  
## <a name="start-the-lesson"></a>开始课程  
 [步骤 1：复制第 2 课包](lesson-3-1-copying-the-lesson-2-package.md)  
  
  
