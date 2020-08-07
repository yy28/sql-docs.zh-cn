---
title: 工作负载比较过程概述
description: 数据库实验助手 (DEA) 是一个 A/B 测试解决方案，适用于 SQL Server 环境中的更改，例如升级或新索引。
ms.date: 12/12/2019
ms.prod: sql
ms.prod_service: dea
ms.suite: sql
ms.technology: dea
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: pochiraju
ms.author: rajpo
ms.reviewer: mathoma
ms.custom: seo-lt-2019
ms.openlocfilehash: a5a508a31d510d4004ece8d82c01615352739dce
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2020
ms.locfileid: "87951212"
---
# <a name="overview-of-the-workload-comparison-process"></a>工作负载比较过程概述

数据库实验助手 (DEA) 可帮助你评估源服务器上的工作负荷在当前环境中的 (，) 将在你的新环境中执行。 DEA 指导你完成三个阶段，以运行 A/B 测试：

- 正在捕获源服务器上的工作负荷跟踪。
- 在目标1和目标2上重播捕获的工作负载跟踪。
- 分析从目标1和目标2收集的重播工作负载跟踪。

本文提供此过程的概述。

## <a name="capturing-a-workload-trace"></a>捕获工作负载跟踪

SQL Server A/B 测试的第一阶段是捕获源服务器上的跟踪。 源服务器通常是生产服务器。 跟踪文件将捕获该服务器上的整个查询工作负荷，包括时间戳。

注意事项：

- 在开始之前，请确保备份要从中捕获跟踪的数据库。
- DEA 用户必须能够通过使用 Windows 身份验证连接到数据库。
- SQL Server 的服务帐户必须能够访问源跟踪文件路径。
- 要使 DEA 能够确定查询的性能是否有所提高或是否降级，该查询必须在捕获期间至少执行15次。

## <a name="replaying-a-workload-trace"></a>重播工作负载跟踪

SQL Server A/B 测试的第二个阶段是重播在两个目标服务器上捕获的跟踪文件：

目标1，它模拟你的源服务器目标2，它模拟你的建议目标环境。

目标1和目标2的硬件配置应尽可能相似，以便 SQL Server 能够准确地分析所建议更改的性能影响。

注意事项：

- 若要重播工作负载跟踪，你的计算机必须设置为 (DReplay) 跟踪运行 Distributed Replay。
- 请确保通过使用源服务器的备份来还原目标服务器上的数据库。
- 建议在服务应用程序中重新启动 SQL Server 服务 (MSSQLSERVER) ，以提高评估结果的一致性。 SQL Server 中的查询缓存可能会影响评估结果。

## <a name="analyzing-the-replayed-workload-traces"></a>分析重播的工作负载跟踪

此过程的最后一步是使用重播跟踪生成分析报告，并查看报告，以了解有关建议更改的潜在性能影响的信息。

注意事项：

- 如果缺少一个或多个组件，则当你尝试生成新的分析报表时，将会显示 "先决条件" 页面，其中包含用于下载的链接， (需要) Internet 连接。
- 若要查看在工具的早期版本中生成的报表，必须先更新该架构。

## <a name="see-also"></a>请参阅

- 若要了解如何生成跟踪文件以及服务器上发生的事件日志，请参阅文章[在数据库实验助手中捕获跟踪](database-experimentation-assistant-capture-trace.md)。