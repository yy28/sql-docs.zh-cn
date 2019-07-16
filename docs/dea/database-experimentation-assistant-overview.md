---
title: 升级 SQL Server 数据库实验助手解决方案概述
description: 数据库实验助手的概述
ms.custom: ''
ms.date: 01/08/2019
ms.prod: sql
ms.prod_service: dea
ms.suite: sql
ms.technology: dea
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: HJToland3
ms.author: ajaykar
ms.reviewer: mathoma
ms.openlocfilehash: 1183c6a443406f6031453b876f9165257db82c07
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68058900"
---
# <a name="overview-of-database-experimentation-assistant"></a>数据库实验助手的概述

数据库实验助手 (DEA) 是用于 SQL Server 升级的试验解决方案。 DEA 可以帮助您评估特定的工作负荷的目标的 SQL Server 版本。 从 SQL Server 早期版本 （从 2005年开始） 升级到较新版本的 SQL Server 的客户可以使用该工具将提供的分析度量值。 

DEA 分析指标包括：
- 具有兼容性错误的查询
- 降级的查询和查询计划
- 其他工作负荷的比较数据

比较数据可能会导致更高置信度和成功的升级体验。

DEA 和演示的 19 分钟介绍，请观看以下视频：

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-Database-Experimentation-Assistant/player]

## <a name="get-dea"></a>获取 DEA

若要安装 DEA，[下载](https://www.microsoft.com/download/details.aspx?id=54090)工具的最新版本。 然后，运行**DatabaseExperimentationAssistant.exe**文件。

## <a name="solution-architecture-for-comparing-workloads"></a>用于比较工作负荷的解决方案体系结构

下图显示了工作负荷比较的解决方案体系结构。 工作负荷比较期间从 SQL Server 2008 升级到 SQL Server 2016 使用 DEA 和分布式重播。

![工作负荷比较解决方案体系结构](./media/database-experimentation-assistant-overview/dea-overview-compare-solution-architecture.png)

## <a name="dea-prerequisites"></a>DEA 先决条件

以下是用于运行 DEA 某些必备组件：
- 最低硬件要求：3.5 gb 的 RAM 在单核计算机。
- 理想的硬件要求：（使用 3.5 GB 的 RAM 或更多) 八核 CPU。 有八个以上内核的处理器不提高 DEA 运行时。
- A、 B 和报表分析数据库到需要的性能跟踪大小增加 33%。

## <a name="configure-dea"></a>配置 DEA

在先决条件环境体系结构中，我们建议安装 DEA *Distributed Replay 控制器所在的同一计算机上*。 这种做法可以避免跨计算机调用并简化了配置。

### <a name="required-configuration-for-workload-comparison-by-using-dea"></a>通过使用 DEA 工作负荷比较所需的配置

DEA 使用 Windows 身份验证连接到数据库服务器。 请确保运行 DEA 的用户可以连接到数据库服务器 （源、 目标和分析） 通过使用 Windows 身份验证。

**捕获配置要求**:

*   运行 DEA 用户可以使用 Windows 身份验证连接到源数据库服务器。
*   运行 DEA 用户具有源数据库服务器上的 sysadmin 权限。
*   运行源数据库服务器的服务帐户具有到跟踪文件夹路径的写访问权限。

有关详细信息，请参阅[捕获常见问题](database-experimentation-assistant-capture-trace.md#frequently-asked-questions-about-trace-capture)

**重播配置要求**: 

*   运行 DEA 用户可以使用 Windows 身份验证连接到目标数据库服务器。
*   运行 DEA 用户具有目标数据库服务器上的 sysadmin 权限。
*   运行目标数据库服务器的服务帐户具有到跟踪文件夹路径的写访问权限。
*   服务帐户运行 Distributed Replay 客户端可以使用 Windows 身份验证连接到目标数据库服务器。
*   DEA 使用 COM 接口与分布式重播控制器进行通信。 请确保打开 TCP 端口，以便在分布式重播控制器上的传入请求。

有关详细信息，请参阅[重播常见问题](database-experimentation-assistant-replay-trace.md#frequently-asked-questions-about-trace-replay)

**分析配置要求**: 

*   运行 DEA 用户可以使用 Windows 身份验证连接到分析数据库服务器。
*   运行 DEA 用户具有源数据库服务器上的 sysadmin 权限。

有关详细信息，请参阅[分析常见问题解答](database-experimentation-assistant-create-report.md#frequently-asked-questions-about-analysis-reports)

## <a name="set-up-telemetry"></a>设置遥测

DEA 有一项支持 internet 的功能，可以将遥测信息发送给 Microsoft。 Microsoft 收集遥测数据来增强产品体验。 遥测是可选的。 本地审核在计算机上还保存收集的信息。 您始终可以看到收集哪些信息。 DEA 中的所有日志文件都保存在 %temp%\\DEA 文件夹。

您可以决定收集哪些事件。 您还可以决定是否向 Microsoft 发送收集的事件。 有四种类型的事件：

*   **TraceEvent**:应用程序 （例如，"触发的停止捕获"） 的使用情况事件。
*   **异常**:在应用程序使用情况期间引发的异常。
*   **DiagnosticEvent**:要在出现问题时帮助诊断的事件日志 (*不*发送给 Microsoft)。
*   **FeedbackEvent**:用户通过应用程序提交的反馈。

以下步骤显示如何选择收集哪些事件，是否将事件发送给 Microsoft:

1.  转到安装 DEA 的位置 (例如，c:\\Program Files (x86)\\Microsoft Corporation\\数据库实验助手)。
2.  打开两个.config 文件：DEA.exe.config （适用于应用程序） 和 DEACmd.exe.config （适用于 CLI)。
3.  若要停止收集事件的类型，请设置的值*事件*(例如， **TraceEvent**) 到**false**。 若要开始再次收集事件，请将值设置为 **，则返回 true**。
4.  若要停止保存事件的本地副本，请将值设置**TraceLoggerEnabled**到**false**。 若要开始再次保存本地副本，请将值设置为 **，则返回 true**。
5.  若要停止将事件发送到 Microsoft，设置的值**AppInsightsLoggerEnabled**到**false**。 若要开始再次将事件发送到 Microsoft，请将值设置为 **，则返回 true**。

DEA 受到[Microsoft 隐私声明](https://aka.ms/dea-privacy)。

## <a name="next-steps"></a>后续步骤

[开始](database-experimentation-assistant-get-started.md)将指导你完成捕获、 重播，并分析跟踪所需的步骤。
