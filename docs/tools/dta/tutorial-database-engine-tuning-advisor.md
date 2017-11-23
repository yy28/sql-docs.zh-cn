---
title: "教程： 数据库引擎优化顾问 |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
helpviewer_keywords:
- Database Engine Tuning Advisor [SQL Server], tutorials
- tutorials [Database Engine Tuning Advisor]
ms.assetid: 3b54cbbe-d8c6-424d-92f1-aa58179f4da8
caps.latest.revision: "38"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 07bd2070758bd17ac110d91179da621198373146
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="tutorial-database-engine-tuning-advisor"></a>教程：数据库引擎优化顾问
欢迎使用数据库引擎优化顾问教程。 数据库引擎优化顾问检查指定数据库中处理查询的方式，然后建议如何通过修改数据库结构（例如索引、索引视图和分区）来改善查询处理性能。  
  
数据库引擎优化顾问提供两个用户界面：图形用户界面 (GUI) 和 **dta** 命令提示实用工具。 使用 GUI 可以方便快捷地查看优化会话结果，而使用 **dta** 实用工具则可以轻松地将数据库引擎优化顾问功能并入脚本中，从而实现自动优化。 此外，数据库引擎优化顾问可以接受 XML 输入，该输入可对优化过程进行更多控制。  
  
## <a name="what-you-will-learn"></a>学习内容  
本教程将讲述如何定位数据库引擎优化顾问 GUI，以及如何通过 GUI 和 **dta** 实用工具执行一些基本任务。 本教程包含以下几课：  
  
[第 1 课：数据库引擎优化顾问中的基本导航](../../tools/dta/lesson-1-basic-navigation-in-database-engine-tuning-advisor.md)  
在本课程中，您将熟悉新的数据库引擎优化顾问 GUI，并学习如何设置显示选项和布局。  
  
[第 2 课：使用数据库引擎优化顾问](../../tools/dta/lesson-2-using-database-engine-tuning-advisor.md)  
在本课中，您将学习如何通过数据库引擎优化顾问 GUI 执行基本的优化任务。  
  
[第 3 课：使用 dta 命令提示实用工具](../../tools/dta/lesson-3-using-the-dta-command-prompt-utility.md)  
在本课程中，将学习如何启动 **dta** 命令提示实用工具以及如何运行一些简单的优化命令。  
  
## <a name="requirements"></a>要求  
本教程面向符合以下条件的数据库管理员：不熟悉数据库引擎优化顾问 GUI 或 **dta** 命令提示实用工具，但对于数据库概念和结构（如索引和索引视图）经验丰富。  
  
必须使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 示例数据库安装 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] （或更高版本）。 为了增强安全性，默认情况下不会安装示例数据库。 若要安装示例数据库，请参阅 [安装 SQL Server 示例和示例数据库](http://sqlserversamples.codeplex.com)。  
  
## <a name="after-you-finish-this-tutorial"></a>学完本教程后  
学完本教程中的课程后，请参考以下主题来了解有关数据库引擎优化顾问的详细信息：  
  
-   [数据库引擎优化顾问](../../relational-databases/performance/database-engine-tuning-advisor.md) 提供有关如何使用此工具执行任务的说明。  
  
-   [dta 实用工具](../../tools/dta/dta-utility.md) 提供有关此命令提示实用工具的参考材料和可用于控制此实用工具的操作的可选 XML 文件。  
  
## <a name="next-lesson"></a>下一课  
[第 1 课：数据库引擎优化顾问中的基本导航](../../tools/dta/lesson-1-basic-navigation-in-database-engine-tuning-advisor.md)  
  
  
  
