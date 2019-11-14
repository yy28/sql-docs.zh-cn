---
title: 为 SQL Server 升级配置重播
description: 在数据库实验助手中配置重播
ms.custom: seo-lt-2019
ms.date: 10/22/2018
ms.prod: sql
ms.prod_service: dea
ms.suite: sql
ms.technology: dea
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: HJToland3
ms.author: ajaykar
ms.reviewer: mathoma
ms.openlocfilehash: b58233e40e27908f0bc8b03a95455216de2c119c
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056722"
---
# <a name="configure-replay-in-database-experimentation-assistant"></a>在数据库实验助手中配置重播

数据库实验助手（DEA）使用 SQL Server 安装中的 Distributed Replay 工具来针对升级后的测试环境重播捕获的跟踪。 建议在执行完整重播之前使用小型跟踪文件执行测试运行，以确保正确重播查询。

## <a name="distributed-replay-requirements"></a>Distributed Replay 要求

- 在 Distributed Replay 控制器计算机上创建 IRF 文件需要额外78% 的硬盘空间。
- 200 MB 或 512 MB 是用于捕获生产或性能跟踪的理想跟踪滚动更新大小。   
- Distributed Replay 控制器和客户端计算机的最小 CPU 和 RAM 要求是具有 3.5 GB RAM 的单核 CPU。
- 重播时间大约比捕获时间长1.55 倍，因为有一个控制器和四个子计算机用于重播生产跟踪。
- 如果你使用生产和性能跟踪定义文件的 "已发布" 版本，并且性能跟踪定义筛选出一个相关数据库的跟踪，则分析将显示**性能跟踪**大小约为大于**生产跟踪**大小的15倍。

## <a name="set-up-a-virtual-network-or-domain"></a>设置虚拟网络或域

Distributed Replay 要求在计算机之间使用公用帐户。 由于此要求，出于安全原因，我们建议在虚拟网络或域控制的网络上运行 Distributed Replay：

- 在环境中创建控制器和客户端计算机。
- 确保控制器和客户端计算机可以通过网络相互 ping。
- Distributed Replay 客户端计算机必须连接到运行 SQL Server 的重播目标计算机。

## <a name="set-up-the-controller-service"></a>设置控制器服务

设置控制器服务的步骤：

1. 使用 SQL Server 安装程序安装 Distributed Replay 控制器。 如果跳过了配置 Distributed Replay 控制器的 SQL Server 安装程序向导步骤，则可以通过配置文件配置控制器。 在典型安装中，配置文件位于 C:\Program Files （x86） \Microsoft SQL Server\<版本\>\Tools\DReplayController\DReplayController.config。
1. Distributed Replay 控制器日志位于 C:\Program Files （x86） \Microsoft SQL Server\<版本\>\Tools\DReplayController\Log。
1. 打开 services.msc 并中转到**SQL Server Distributed Replay 控制器**服务。
1. 右键单击该服务，然后选择 "**属性**"。 将服务帐户设置为在网络中对控制器和客户端计算机通用的帐户。
1. 选择 **"确定"** 以关闭 "**属性**" 窗口。
1. 从 services.msc 重新启动**SQL Server Distributed Replay 控制器**服务。 还可以在命令行中运行以下命令，以重新启动该服务：<br/>
   `NET STOP "SQL Server Distributed Replay Controller"`<br/>
   `NET START "SQL Server Distributed Replay Controller"`
1. 有关更多配置选项，请参阅[Configure Distributed Replay](https://docs.microsoft.com/sql/tools/distributed-replay/configure-distributed-replay)。

## <a name="configure-dcom"></a>配置 DCOM

此配置仅在控制器计算机上是必需的。

1. 打开 dcomcnfg.exe。
1. 展开 "**组件服务**" > **计算机**" > **我的电脑** > **DCOM 配置**"。
1. 在 " **DCOM 配置**" 下，右键单击**DReplayController**，然后选择 "**属性**"。
1. 选择 **“安全”** 选项卡。
1. 在 "**启动和激活权限**" 下，选择 "**自定义**"，然后选择 "**编辑**"。
1. 添加将开始重播的用户。 为用户授予本地启动和本地激活权限。 如果用户计划远程启动或激活，请向用户授予 "远程启动" 和 "远程激活" 权限。
1. 选择 **"确定"** 以提交更改并返回到 "**安全**" 选项卡。
1. 在 "**访问权限**" 下，选择 "**自定义**"，然后选择 "**编辑**"。
1. 添加将开始重播的用户。 向用户授予本地访问权限。 如果用户计划远程访问控制器服务，请为用户授予远程访问权限。
1. 选择 **"确定"** 以提交更改并返回到 "**安全**" 选项卡。
1. 选择 **"确定"** 以提交更改。
1. 从 services.msc 重新启动 SQL Server Distributed Replay 控制器服务。 还可以在命令行中运行以下命令，以重新启动该服务：<br/>
   `NET STOP "SQL Server Distributed Replay Controller"`<br/>
   `NET START "SQL Server Distributed Replay Controller"`

## <a name="set-up-the-client-service"></a>设置客户端服务

在设置客户端服务之前，请使用 ping 等网络工具来验证控制器和客户端计算机是否能够通信。

1. 使用 SQL Server 安装程序安装 Distributed Replay 客户端。
1. 打开 services.msc 并中转到 SQL Server Distributed Replay 客户端服务。
1. 右键单击该服务，然后选择 "**属性**"。 将服务帐户设置为网络中控制器和客户端计算机共用的帐户。
1. 选择 **"确定"** 以关闭 "**属性**" 窗口。 如果跳过 SQL Server 安装程序向导步骤来配置 Distributed Replay 客户端，则可以通过配置文件配置该客户端。 在典型安装中，配置文件位于 C:\Program Files （x86） \Microsoft SQL Server\<版本\>\Tools\DReplayClient\DReplayClient.config。
1. 确保 Dreplayclient.exe 文件包含控制器计算机的名称作为用于注册的控制器。
1.  从 services.msc 重新启动 SQL Server Distributed Replay 客户端服务。 还可以从命令行运行以下命令，以重新启动该服务：<br/>
    `NET STOP "SQL Server Distributed Replay Client"`<br/>
    `NET START "SQL Server Distributed Replay Client"`
1. Distributed Replay 控制器日志位于 C:\Program Files （x86） \Microsoft SQL Server\<版本\>\Tools\DReplayClient\Log。 日志指示客户端是否可以向控制器注册自身。
1. 如果配置成功，日志将显示 "向控制器注册 < 控制器名称\>" 消息。
1. 有关更多配置选项，请参阅[Configure Distributed Replay](https://docs.microsoft.com/sql/tools/distributed-replay/configure-distributed-replay)。

## <a name="set-up-distributed-replay-administration-tools"></a>设置 Distributed Replay 管理工具

您可以使用 Distributed Replay 管理工具快速测试 Distributed Replay 在环境中是否正常工作。 在向控制器注册多个客户端计算机的环境中，测试配置可能特别有用。 你可能需要安装 SQL Server Management Studio （SSMS）才能获取管理工具。

1. 请参阅 SSMS 安装位置，并查找 Distributed Replay 管理工具 dreplay 及其依赖组件。
1. 打开 "命令提示符" 窗口并运行 `dreplay.exe status -f 1`。
1. 如果前面的所有步骤都成功，则控制台输出表明控制器可以查看其客户端处于 `READY` 状态。

## <a name="configure-the-firewall-for-remote-distributed-replay-access"></a>为远程 Distributed Replay 访问配置防火墙

远程访问 Distributed Replay 需要打开可在域或虚拟网络中看到的端口。

1. 打开 "**高级安全** **Windows 防火墙**"。
1. 中转到 "**入站规则**"。
1. 为 program C:\Program Files （x86） \Microsoft SQL Server 创建新的入站防火墙规则\>\Tools\DReplayController\DReplayController.exe.\<版本
1. 允许 DReplayController 的所有端口的域级访问，以便能够远程与控制器服务进行通信。
1. 保存规则。

## <a name="set-up-target-computers"></a>设置目标计算机

若要运行 A/B 测试或实验，需要执行两次重播。 也就是说，对于迁移方案，可能需要两个单独的 SQL Server 安装实例。 

你还可以在同一台计算机上安装 SQL Server 实例的两个版本。 需要注意的是要确保在进行重播时完全隔离实例。

每次重播都必须执行以下步骤：

1. 还原数据库的备份。
1. 为客户端服务帐户用户提供访问 SQL Server 实例下的数据库的权限。 需要对 SQL Server 实例执行查询的权限。
1. 开始重播。

## <a name="next-steps"></a>后续步骤

- 若要了解如何在升级的测试环境中重播捕获的跟踪，请参阅[重播跟踪](database-experimentation-assistant-replay-trace.md)。

- 有关 DEA 和演示的19分钟简介，请观看以下视频：

  > [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-Database-Experimentation-Assistant/player]
