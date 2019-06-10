---
title: 在数据库实验助手 for SQL Server 升级配置重播
description: 重播配置在数据库实验助手
ms.custom: ''
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
manager: jroth
ms.openlocfilehash: 8efef6f081395265f641197058b7920162cdde46
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2019
ms.locfileid: "66794490"
---
# <a name="configure-replay-in-database-experimentation-assistant"></a>重播配置在数据库实验助手

数据库实验助手 (DEA) 使用从 SQL Server 安装分布式重播工具来重播捕获的跟踪针对升级后的测试环境。 我们建议执行此测试运行执行完整重播之前使用小的跟踪文件，以确保正确重播的查询。

## <a name="distributed-replay-requirements"></a>分布式的重播要求

- 创建 IRF 文件 Distributed Replay 控制器计算机上的需要额外的硬盘空间 78%。
- 200 MB 或 512 MB 是理想之选跟踪滚动更新大小要用于捕获生产或性能跟踪。   
- Distributed Replay 控制器和客户端计算机的最小 CPU 和 RAM 要求为 3.5 gb RAM 的单核 CPU。
- 重播时间需要大约 1.55 更长时间比捕获时间因为使用一个控制器和四个子机重播生产跟踪。
- 如果感兴趣的一个数据库使用我们"published"版本的生产和性能跟踪定义文件和性能跟踪定义筛选出跟踪，分析表明： 通过**性能跟踪**大小大约 15 倍**生产跟踪**大小。

## <a name="set-up-a-virtual-network-or-domain"></a>设置虚拟网络或域

分布式的重播要求使用计算机之间的通用帐户。 鉴于此要求，并出于安全原因，我们建议在虚拟网络或域控制网络上运行 Distributed Replay:

- 在环境中创建的控制器和客户端计算机。
- 请确保该控制器和客户端计算机可以相互 ping 通过网络。
- 分布式的重播客户端计算机必须连接到运行 SQL Server 的重播目标计算机。

## <a name="set-up-the-controller-service"></a>设置控制器服务

若要设置控制器服务：

1. 使用 SQL Server 安装程序安装 Distributed Replay 控制器。 如果你跳过配置 Distributed Replay 控制器的 SQL Server 安装程序向导步骤，您可以通过配置文件配置控制器。 在典型安装中，配置文件位于 C:\Program Files (x86) \Microsoft SQL Server\<版本\>\Tools\DReplayController\DReplayController.config。
1. 分布式的重播控制器日志位于 C:\Program Files (x86) \Microsoft SQL Server\<版本\>\Tools\DReplayController\Log。
1. 打开 Services.msc 并转到**SQL Server 分布式重播控制器**服务。
1. 在服务上，右键单击，然后选择**属性**。 设置为普遍适用于在网络中的控制器和客户端计算机的帐户服务帐户。
1. 选择**确定**以关闭**属性**窗口。
1. 重新启动**SQL Server 分布式重播控制器**Services.msc 服务。 此外可以在要重新启动该服务的命令行运行以下命令：<br/>
   `NET STOP "SQL Server Distributed Replay Controller"`<br/>
   `NET START "SQL Server Distributed Replay Controller"`
1. 有关更多配置选项，请参阅[配置 Distributed Replay](https://docs.microsoft.com/sql/tools/distributed-replay/configure-distributed-replay)。

## <a name="configure-dcom"></a>配置 DCOM

仅在控制器计算机上需要此配置。

1. 打开 dcomcnfg.exe。
1. 展开**组件服务** > **计算机** > **我的计算机** > **DCOM 配置**。
1. 下**DCOM Config**，右键单击**DReplayController**，然后选择**属性**。
1. 选择 **“安全”** 选项卡。
1. 下**启动和激活权限**，选择**自定义**，然后选择**编辑**。
1. 添加用户，将启动重播。 为用户提供本地启动和本地激活权限。 如果用户计划启动或远程激活，为用户提供远程启动和远程激活权限。
1. 选择**确定**以提交更改并返回到**安全**选项卡。
1. 下**访问权限**，选择**自定义**，然后选择**编辑**。
1. 添加用户，将启动重播。 为用户提供本地访问权限。 如果用户计划远程访问控制器服务，为用户提供远程访问权限。
1. 选择**确定**以提交更改并返回到**安全**选项卡。
1. 选择**确定**提交所做的更改。
1. 重新启动 Services.msc 中的 SQL Server 分布式重播控制器服务。 此外可以在要重新启动该服务的命令行运行以下命令：<br/>
   `NET STOP "SQL Server Distributed Replay Controller"`<br/>
   `NET START "SQL Server Distributed Replay Controller"`

## <a name="set-up-the-client-service"></a>设置客户端服务

设置客户端服务之前，请使用 ping 等网络工具验证的控制器和客户端计算机可以进行通信。

1. 使用 SQL Server 安装程序安装 Distributed Replay 客户端。
1. 打开 Services.msc，并转到 SQL Server 分布式重播客户端服务。
1. 在服务上，右键单击，然后选择**属性**。 设置为普遍适用于网络中的控制器和客户端计算机的帐户服务帐户。
1. 选择**确定**以关闭**属性**窗口。 如果你跳过 SQL Server 安装程序向导步骤，若要配置 Distributed Replay 客户端，您可以通过配置文件配置。 在典型安装中，配置文件位于 C:\Program Files (x86) \Microsoft SQL Server\<版本\>\Tools\DReplayClient\DReplayClient.config。
1. 请确保 DReplayClient.config 文件作为注册其控制器包含在控制器计算机的名称。
1.  重新启动 SQL Server 分布式重播客户端服务通过 Services.msc。 此外可以从命令行重新启动服务来运行以下命令：<br/>
    `NET STOP "SQL Server Distributed Replay Client"`<br/>
    `NET START "SQL Server Distributed Replay Client"`
1. 分布式的重播控制器日志位于 C:\Program Files (x86) \Microsoft SQL Server\<版本\>\Tools\DReplayClient\Log。 日志指示是否在客户端可以注册其自身的控制器。
1. 如果配置是否成功，日志将显示消息"向控制器注册 < 控制器名称\>"。
1. 有关更多配置选项，请参阅[配置 Distributed Replay](https://docs.microsoft.com/sql/tools/distributed-replay/configure-distributed-replay)。

## <a name="set-up-distributed-replay-administration-tools"></a>安装 Distributed Replay 管理工具

Distributed Replay 管理工具可用于快速测试是否 Distributed Replay 环境中工作正常。 测试配置可以在其中可以向控制器中注册多个客户端计算机的环境中特别有用。 您可能需要安装 SQL Server Management Studio (SSMS) 以获取管理工具。

1. 请转到 SSMS 安装位置，并查找的 Distributed Replay 管理工具 dreplay.exe 和及其依赖的组件。
1. 打开命令提示符窗口并运行`dreplay.exe status -f 1`。
1. 如果上述所有步骤都都成功，控制台输出将指示控制器，可以看到在其客户端`READY`状态。

## <a name="configure-the-firewall-for-remote-distributed-replay-access"></a>为 Distributed Replay 的远程访问配置防火墙

远程访问 Distributed Replay 要求打开端口在域或虚拟网络可见的。

1. 打开**Windows 防火墙**与**高级安全**。
1. 转到**入站规则**。
1. 创建新的入站的防火墙规则的程序 C:\Program Files (x86) \Microsoft SQL Server\<版本\>\Tools\DReplayController\DReplayController.exe。
1. 允许对 DReplayController.exe 要能够远程通信与控制器服务的所有端口域级访问权限。
1. 保存规则。

## <a name="set-up-target-computers"></a>设置目标计算机

两个重播所需运行 A / B 测试或进行实验。 也就是说，您可能需要两个单独实例的 SQL Server 安装的迁移方案。 

此外可以在同一台计算机上安装 SQL Server 实例的两个版本。 需要注意的是以确保当重播正在进行时实例之间完全隔离。

为每个重播，必须执行以下步骤：

1. 还原数据库的备份。
1. 提供客户端服务帐户用户来访问 SQL Server 实例下的数据库的权限。 所需的 SQL Server 实例上执行的查询权限。
1. 启动重播。

## <a name="next-steps"></a>后续步骤

- 若要了解如何重播已升级的测试环境中捕获的跟踪，请参阅[重播的跟踪](database-experimentation-assistant-replay-trace.md)。

- DEA 和演示的 19 分钟介绍，请观看以下视频：

  > [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-Database-Experimentation-Assistant/player]
