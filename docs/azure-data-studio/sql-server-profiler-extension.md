---
title: SQL Server Profiler 扩展
titleSuffix: Azure Data Studio
description: 安装和使用适用于 Azure Data Studio SQL Server Profiler 扩展 （预览版）
ms.custom: seodec18
ms.date: 09/24/2018
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
manager: jroth
ms.openlocfilehash: 92c662a05334731d66891e85e7501e38da438e03
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66798003"
---
# <a name="sql-server-profiler-extension-preview"></a>SQL Server Profiler 扩展 （预览版）

SQL Server Profiler 扩展 （预览版） 提供了简单的 SQL Server 跟踪解决方案类似于 SQL Server Management Studio (SSMS) 除外的 Profiler 使用 XEvents 生成。 SQL Server Profiler 是非常易于使用，具有很好的默认值的最常见的跟踪配置。 用户体验进行优化事件通过浏览和查看关联的 TRANSACT-SQL (T-SQL) 文本。 Azure Data Studio SQL Server Profiler 还假定很好的默认值，用于收集 T-SQL 执行活动，与易于使用的用户体验。 此扩展当前处于预览状态。

**常见 SQL Profiler 用例：**

- 逐步分析有问题的查询以找到问题的原因。
- 查找并诊断运行慢的查询。
- 捕获导致某个问题的 TRANSACT-SQL 语句的一系列。
- 监视 SQL Server，以优化工作负荷的性能。
- 使性能计数器与诊断问题关联。


## <a name="install-the-sql-server-profiler-extension"></a>安装 SQL Server Profiler 扩展

1. 若要開啟擴充管理員及存取可用的擴充功能，選取 [擴充功能] 圖示，或選取**檢視**功能表中的**擴充功能**。
2. 选择要查看其详细信息的可用扩展。

   ![探查器扩展管理器](media/extensions/sql-server-profiler-extension/profiler-extension.png)

1. 选择所需的扩展并**安装**它。
2. 選取**重新載入**啟用該擴充功能 （只有第一次安裝擴充功能時需要）。

## <a name="start-profiler"></a>启动 Profiler

1. 若要启动 Profiler，请首先在服务器选项卡中请连接到服务器。
2. 建立连接后，键入**Alt + P**启动 Profiler。
3. 若要启动 Profiler，请键入**Alt + s。** 现在可以开始查看扩展事件。
    ![探查器扩展管理器](media/extensions/sql-server-profiler-extension/view-profiler.png)    
1. 若要停止 Profiler，请键入**Alt + s。** 此热键是一个触发器。

## <a name="next-steps"></a>后续步骤

若要了解有关 Profiler 和扩展的事件的详细信息，请参阅[扩展事件](https://docs.microsoft.com/sql/relational-databases/extended-events/extended-events)。





