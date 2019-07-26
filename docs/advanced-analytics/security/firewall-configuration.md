---
title: 防火墙配置
description: 如何为 SQL Server 机器学习服务中的出站连接配置防火墙。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/17/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 754e243f45965801b9295d2b40a920d52bd2c95c
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/24/2019
ms.locfileid: "68469856"
---
# <a name="firewall-configuration-for-sql-server-machine-learning-services"></a>SQL Server 机器学习服务的防火墙配置
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本文列出了管理员或架构师在使用机器学习服务时应牢记的防火墙配置注意事项。

## <a name="default-firewall-rules"></a>默认防火墙规则

默认情况下, SQL Server 安装程序通过创建防火墙规则来禁用出站连接。

在 SQL Server 2016 和2017中, 这些规则基于本地用户帐户, 其中, 安装程序为拒绝对其成员的网络访问的**SQLRUserGroup**创建了一个出站规则 (每个辅助角色帐户作为规则的本地原则列出。 有关 SQLRUserGroup 的详细信息, 请参阅[SQL Server 机器学习服务中扩展性框架的安全性概述](../../advanced-analytics/concepts/security.md#sqlrusergroup)。

作为 AppContainers 的一部分, 在 2019 SQL Server 中, 有新的防火墙规则基于 AppContainer Sid: SQL Server 安装程序创建的20个 AppContainers 中的一个。 防火墙规则名称的命名约定会**阻止 SQL Server 实例 MSSQLSERVER 中的 appcontainer-00 的网络访问**, 其中00是 appcontainer 的编号 (默认值为 00-20), 而 MSSQLSERVER 是 SQL Server 实例的名称。

> [!Note]
> 如果需要网络调用, 你可以在 Windows 防火墙中禁用出站规则。

## <a name="restrict-network-access"></a>限制网络访问

在默认安装中, 使用 Windows 防火墙规则来阻止来自外部运行时进程的所有出站网络访问。 应创建防火墙规则, 以防止外部运行时进程下载程序包或进行其他可能是恶意的网络调用。

如果你使用的是其他防火墙程序, 还可以通过为本地用户帐户或用户帐户池所代表的组设置规则来创建规则, 以阻止外部运行时的出站网络连接。

我们强烈建议你启用 Windows 防火墙 (或你选择的另一防火墙) 以阻止 R 或 Python 运行时进行不受限制的网络访问。

## <a name="next-steps"></a>后续步骤

[为入站连接配置 Windows 防火墙](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)