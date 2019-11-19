---
title: 工作负载比较过程概述
description: 数据库实验助手（DEA）是一种用于在 SQL Server 环境中进行更改的 A/B 测试解决方案，如升级或新索引。
ms.date: 11/16/2019
ms.prod: sql
ms.prod_service: dea
ms.suite: sql
ms.technology: dea
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: HJToland3
ms.author: jtoland
ms.reviewer: mathoma
ms.custom: seo-lt-2019
ms.openlocfilehash: 18cba7abf0d73197c248a62283d52126873169a3
ms.sourcegitcommit: f018eb3caedabfcde553f9a5fc9c3e381c563f1a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/18/2019
ms.locfileid: "74165747"
---
# <a name="overview-of-the-workload-comparison-process"></a>工作负载比较过程概述

数据库实验助手（DEA）可帮助你评估源服务器上的工作负荷（在当前环境中）在你的新环境中将如何执行。 DEA 指导你完成三个阶段，以运行 A/B 测试：

- 正在捕获源服务器上的工作负荷跟踪。
- 在目标1和目标2上重播捕获的工作负载跟踪。
- 分析从目标1和目标2收集的重播工作负载跟踪。

本文提供此过程的概述。

## <a name="capturing-a-workload-trace"></a>捕获工作负载跟踪

SQL Server A/B 测试的第一阶段是捕获源服务器上的跟踪。 源服务器通常是生产服务器。 跟踪文件将捕获该服务器上的整个查询工作负荷，包括时间戳。

注意事项：

- 在开始捕获工作负荷跟踪之前，请务必备份要从中捕获跟踪的数据库。
- DEA 用户必须配置为使用 Windows 身份验证连接到数据库。
- SQL Server 服务帐户需要访问源跟踪文件路径。
- 要使 DEA 能够确定查询的性能是否有所提高或是否降级，该查询必须在捕获期间至少执行15次。

## <a name="replaying-a-workload-trace"></a>重播工作负载跟踪

SQL Server A/B 测试的第二个阶段是重播在两个目标服务器上捕获的跟踪文件：

目标1，它模拟你的源服务器目标2，它模拟你的建议目标环境。

目标1和目标2的硬件配置应尽可能相似，因此 SQL Server 可以准确地分析所建议更改的性能影响。

注意事项：

- 若要重播工作负载跟踪，你的计算机必须设置为运行 Distributed Replay （DReplay）跟踪。
- 请确保通过使用源服务器的备份来还原目标服务器上的数据库。
- 建议在服务应用程序中重新启动 SQL Server 服务（MSSQLSERVER）以提高评估结果的一致性。 SQL Server 中的查询缓存可能会影响评估结果。

## <a name="analyzing-the-replayed-workload-traces"></a>分析重播的工作负载跟踪

此过程的最后阶段是使用重播跟踪生成分析报告。 然后，可以查看分析报告，获取有关建议更改的潜在性能影响的见解。

注意事项：

- 如果缺少一个或多个组件，则当你尝试生成新的分析报表（需要 internet 连接）时，会显示包含下载链接的 "先决条件" 页面。
- 若要查看在工具的早期版本中生成的报表，必须先更新该架构。

## <a name="see-also"></a>另请参阅

- 若要了解如何生成跟踪文件以及服务器上发生的事件日志，请参阅[捕获跟踪](database-experimentation-assistant-capture-trace.md)。
