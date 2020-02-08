---
title: SQL Server Profiler 扩展
titleSuffix: Azure Data Studio
description: 安装和使用 Azure Data Studio 的 SQL Server Profiler 扩展（预览版）
ms.custom: seodec18
ms.date: 09/24/2018
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.openlocfilehash: 4fcb16d2ec3c267dc2927f22a029709a434416c9
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "75776508"
---
# <a name="sql-server-profiler-extension-preview"></a>SQL Server Profiler 扩展（预览版）

SQL Server Profiler 扩展（预览版）提供类似于 SQL Server Management Studio (SSMS) Profiler 的简单 SQL Server 跟踪解决方案，但前者是使用扩展事件构建的。 SQL Server Profiler 非常易于使用，为最常见的跟踪配置设置了很合适的默认值。 UX 针对事件浏览和关联 Transact-SQL (T-SQL) 文本的查看性能进行了优化。 Azure Data Studio 的 SQL Server Profiler 还为实现后列操作设置了很合适的默认值：通过易于使用的 UX 收集 T-SQL 执行活动。 此扩展当前处于预览状态。

**常见的 SQL Profiler 用例：**

- 逐步分析有问题的查询以找到问题的原因。
- 查找并诊断运行慢的查询。
- 捕获导致问题的一系列 Transact-SQL 语句。
- 监视 SQL Server 的性能以优化工作负荷。
- 使性能计数器与诊断问题关联。


## <a name="install-the-sql-server-profiler-extension"></a>安装 SQL Server Profiler 扩展

1. 若要打开扩展管理器并访问可用扩展，请选择扩展图标，或在“视图”菜单中选择“扩展”   。
2. 选择某个可用扩展以查看其详细信息。

   ![Profiler 扩展管理器](media/extensions/sql-server-profiler-extension/profiler-extension.png)

1. 选择所需的扩展并“安装”它  。
2. 选择“重新加载”以启用扩展（仅在第一次安装扩展时是必需的）  。

## <a name="start-profiler"></a>启动 Profiler

1. 要启动 Profiler，需先在“服务器”选项卡中建立与服务器的连接。
2. 建立连接后，键入“Alt + P”启动 Profiler  。
3. 要启动 Profiler，请键入“Alt + S”  现在可以开始查看扩展事件。
    ![Profiler 扩展管理器](media/extensions/sql-server-profiler-extension/view-profiler.png)    
1. 要停止 Profiler，请键入“Alt + S”  。此热键是一个开关。

## <a name="next-steps"></a>后续步骤

要了解有关 Profiler 和扩展事件的详细信息，请参阅[扩展事件](https://docs.microsoft.com/sql/relational-databases/extended-events/extended-events)。





