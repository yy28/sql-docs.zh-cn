---
title: 数据库实验助手概述
description: 数据库实验助手概述
ms.custom: seo-lt-2019
ms.date: 11/05/2019
ms.prod: sql
ms.prod_service: dea
ms.suite: sql
ms.technology: dea
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: HJToland3
ms.author: jtoland
ms.reviewer: mathoma
ms.openlocfilehash: 7180656f8a4779c43f4c691f583aaaf5fcbf86d0
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056584"
---
# <a name="overview-of-database-experimentation-assistant"></a>数据库实验助手概述

数据库实验助手（DEA）是一种试验解决方案，用于 SQL Server 升级。 DEA 可帮助你评估特定工作负载的 SQL Server 目标版本。 从早期 SQL Server 版本（从2005开始）升级到较新版本的 SQL Server 的客户可以使用该工具提供的分析指标。

DEA 分析指标包括：

- 具有兼容性错误的查询
- 降级的查询和查询计划
- 其他工作负荷比较数据

比较数据可能会导致更高的置信度和成功的升级体验。

## <a name="get-dea"></a>获取 DEA

若要安装 DEA，请[下载](https://www.microsoft.com/download/details.aspx?id=54090)最新版本的工具。 然后，运行**DatabaseExperimentationAssistant**文件。

## <a name="solution-architecture-for-comparing-workloads"></a>用于比较工作负载的解决方案体系结构

下图显示了用于工作负载比较的解决方案体系结构。 在从 SQL Server 2008 升级到 SQL Server 2016 期间，工作负载比较使用 DEA 和 Distributed Replay。

![工作负载比较解决方案体系结构](./media/database-experimentation-assistant-overview/dea-overview-compare-solution-architecture.png)

## <a name="dea-prerequisites"></a>DEA 先决条件

下面是运行 DEA 的一些先决条件：

- 最低硬件要求：具有 3.5 GB RAM 的单核计算机。
- 理想硬件要求：8核 CPU （具有 3.5 GB 或更大的 RAM）。 具有8个以上内核的处理器不会提高 DEA 运行时。
- 存储、B 和报表分析数据库需要额外33% 的性能跟踪大小。

## <a name="configure-dea"></a>配置 DEA

在必备的环境体系结构中，我们建议在*Distributed Replay 控制器所在的同一台计算机上*安装 DEA。 这种做法可以避免跨计算机调用并简化配置。

### <a name="required-configuration-for-workload-comparison-by-using-dea"></a>使用 DEA 进行工作负荷比较所需的配置

DEA 使用 Windows 身份验证连接到数据库服务器。 确保运行 DEA 的用户可以使用 Windows 身份验证连接到数据库服务器（源、目标和分析）。

**捕获配置要求**：

- 运行 DEA 的用户可以通过使用 Windows 身份验证连接到源数据库服务器。
- 运行 DEA 的用户在源数据库服务器上具有 sysadmin 权限。
- 运行源数据库服务器的服务帐户具有对跟踪文件夹路径的写访问权限。

有关详细信息，请参阅[捕获常见问题解答](database-experimentation-assistant-capture-trace.md#frequently-asked-questions-about-trace-capture)

**重播配置要求**： 

- 运行 DEA 的用户可以通过使用 Windows 身份验证连接到目标数据库服务器。
- 运行 DEA 的用户在目标数据库服务器上具有 sysadmin 权限。
- 运行目标数据库服务器的服务帐户具有对跟踪文件夹路径的写访问权限。
- 运行 Distributed Replay 客户端的服务帐户可以使用 Windows 身份验证连接到目标数据库服务器。
- DEA 使用 COM 接口与 Distributed Replay 控制器通信。 请确保在 Distributed Replay 控制器上的传入请求中打开 TCP 端口。

有关详细信息，请参阅[重播常见问题解答](database-experimentation-assistant-replay-trace.md#frequently-asked-questions-about-trace-replay)

**分析配置要求**：

- 运行 DEA 的用户可以通过使用 Windows 身份验证连接到分析数据库服务器。
- 运行 DEA 的用户在源数据库服务器上具有 sysadmin 权限。

有关详细信息，请参阅[分析常见问题解答](database-experimentation-assistant-create-report.md#frequently-asked-questions-about-analysis-reports)

## <a name="set-up-telemetry"></a>设置遥测

DEA 具有支持 internet 的功能，可将遥测信息发送给 Microsoft。 Microsoft 收集遥测数据以增强产品体验。 遥测是可选的。 收集的信息也保存在您的计算机上以进行本地审核。 始终可以查看收集的内容。 DEA 中的所有日志文件都保存在% temp%\\DEA 文件夹中。

您可以决定收集哪些事件。 你还决定是否向 Microsoft 发送收集的事件。 有四种类型的事件：

- **TraceEvent**：应用程序的使用情况事件（例如，"触发停止捕获"）。
- **异常**：应用程序使用期间引发了异常。
- **DiagnosticEvent**：一种事件日志，用于在出现问题时帮助诊断（*不*发送给 Microsoft）。
- **FeedbackEvent**：通过应用程序提交的用户反馈。

以下步骤演示如何选择要收集的事件以及是否将事件发送到 Microsoft：

1. 中转到安装 DEA 的位置（例如，C：\\Program Files （x86）\\Microsoft Corporation\\数据库实验助手）。
2. 打开两个 .config 文件： DEA （适用于应用程序）和 DEACmd （适用于 CLI）。
3. 若要停止收集事件类型，请将*事件*（例如， **TraceEvent**）的值设置为**false**。 若要再次开始收集事件，请将值设置为**true**。
4. 若要停止保存事件的本地副本，请将**TraceLoggerEnabled**的值设置为**false**。 若要再次开始保存本地副本，请将值设置为**true**。
5. 若要停止向 Microsoft 发送事件，请将**AppInsightsLoggerEnabled**的值设置为**false**。 若要再次开始向 Microsoft 发送事件，请将值设置为**true**。

DEA 由[Microsoft 隐私声明](https://aka.ms/dea-privacy)控制。

## <a name="next-steps"></a>后续步骤

[入门](database-experimentation-assistant-get-started.md)指导完成捕获、重播和分析跟踪所需的步骤。
