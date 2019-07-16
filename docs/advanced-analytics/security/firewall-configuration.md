---
title: 防火墙配置的 SQL Server 机器学习服务
description: 如何配置防火墙以允许从 SQL Server 机器学习服务的出站连接。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/17/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: f62b42754b56ac07714eeade0d86e6c8ac582698
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962345"
---
# <a name="firewall-configuration-for-sql-server-machine-learning-services"></a>SQL Server 机器学习服务的防火墙配置
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文列出了管理员或架构师应记住使用机器学习服务时的防火墙配置注意事项。

## <a name="default-firewall-rules"></a>默认防火墙规则

默认情况下，SQL Server 安装程序通过创建防火墙规则禁用出站连接。

在 SQL Server 2016 和 2017年中，这些规则基于本地用户帐户，安装程序在其中创建一个出站规则**SQLRUserGroup** ，拒绝对其成员的网络访问 （每个辅助角色帐户被列为受本地原则该规则。 有关 SQLRUserGroup 的详细信息，请参阅[SQL Server 机器学习服务中的可扩展性框架的安全性概述](../../advanced-analytics/concepts/security.md#sqlrusergroup)。

在 SQL Server 2019 作为到 AppContainers，在移动过程中有基于 AppContainer Sid 的新防火墙规则： 一个用于 20 AppContainers 的每个创建的 SQL Server 安装程序。 防火墙规则名称的命名约定是**阻止 AppContainer 00 的 SQL Server 实例 MSSQLSERVER 中的网络访问**，其中 00 是 AppContainer (00-20 默认情况下)，数量，MSSQLSERVER 是 SQL 的名称服务器实例。

> [!Note]
> 如果网络调用是必需的则可以禁用 Windows 防火墙中的出站规则。

## <a name="restrict-network-access"></a>限制网络访问

在默认安装中，使用 Windows 防火墙规则以阻止从外部运行时进程的所有出站网络访问。 应创建防火墙规则，以防止外部运行时进程下载程序包或进行其他可能有恶意的网络调用。

如果使用其他防火墙程序，您还可以创建规则以阻止出站网络连接的外部运行时，通过设置为本地用户帐户或用户帐户池所表示的组的规则。

我们强烈建议开启 Windows 防火墙 （或所选的另一个防火墙） 以防止不受限制的网络访问的 R 或 Python 运行时。

## <a name="next-steps"></a>后续步骤

[配置 Windows 防火墙以允许入站连接](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)