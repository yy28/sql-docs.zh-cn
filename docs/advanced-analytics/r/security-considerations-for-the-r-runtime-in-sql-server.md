---
title: "有关 SQL Server 中的机器学习的安全注意事项 |Microsoft 文档"
ms.custom:
- SQL2016_New_Updated
ms.date: 07/31/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d5065197-69e6-4fce-9654-00acaecc148b
caps.latest.revision: 15
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d9b5fba856cc40c11f218faf0a61f66ee5451aa4
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="security-considerations-for-machine-learning-in-sql-server"></a>有关 SQL Server 中的机器学习的安全注意事项

本文列出了管理员或架构师应牢记使用机器学习服务时的安全注意事项。

**适用于：** SQL Server 2016 R Services、 SQL Server 自 2017 年 1 机器学习服务

## <a name="use-a-firewall-to-restrict-network-access-by-r"></a>使用防火墙限制 R 的网络访问

在默认安装中，Windows 防火墙规则用于阻止从 R 运行时进程的所有出站网络访问权限。 应创建防火墙规则来防止 R 运行时进程下载程序包或进行其他可能有恶意目的的网络调用。

如果使用的是其他防火墙程序，还可以通过为本地用户帐户或用户帐户池所代表的组设置规则来创建规则，以阻止 R 运行时的出站网络连接。

我们强烈建议您开启 Windows 防火墙 （或你选择的另一个防火墙） 以防止的 R 或 Python 运行时的自由的网络访问权限。

## <a name="authentication-methods-supported-for-remote-compute-contexts"></a>支持远程计算上下文的身份验证方法

[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]支持 Windows 集成身份验证和 SQL 登录名创建之间的连接时[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和远程数据科学客户端。

例如，如果你要在笔记本电脑上开发 R 解决方案，并且想要在 SQL Server 计算机上执行计算，可通过使用 **rx** 函数基于 Windows 凭据定义连接字符串来在 R 中创建 SQL Server 数据源。

当你更改_计算上下文_从 SQL Server 计算机便携式计算机，如果你的 Windows 帐户具有必要的权限，所有 R 代码都执行 SQL Server 计算机上。 此外，在你的凭据以及下运行的 R 代码的一部分执行的任何 SQL 查询。

在此方案中，这需要 SQL Server 实例将配置为允许混合的模式身份验证还支持使用 SQL 登录名。

### <a name="implied-authentication"></a>隐式身份验证

 一般情况下，[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]启动外部脚本运行时并执行其自己的帐户下的脚本。 但是，如果外部运行时发出的 ODBC 调用，[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]模拟发送命令以确保不会无法通过 ODBC 调用用户的凭据。 这称为*隐式身份验证*。
 
 > [!IMPORTANT]
 >
 > 要使隐式身份验证成功，包含辅助角色帐户的 Windows 用户组（默认情况下，为 **SQLRUser**）必须在实例的 master 数据库中有帐户，并且此帐户必须有权连接到该实例。
 > 
 > 组**SQLRUser**运行 Python 脚本时，还使用。 

## <a name="no-support-for-encryption-at-rest"></a>不支持静态加密

数据发送到或接收来自外部脚本运行时不支持透明数据加密。 因此，静态加密**不**应用于在 R 或 Python 脚本中，任何数据保存到磁盘或任何持久的中间结果使用的任何数据。

## <a name="resources"></a>Resources

有关管理服务，以及如何设置用于执行 R 脚本的用户帐户的详细信息，请参阅[配置和管理高级分析扩展](../../advanced-analytics/r/configure-and-manage-advanced-analytics-extensions.md)。

安全体系结构的说明，请参阅：

+ [R 的安全性概述](security-overview-sql-server-r.md)
+ [Python 的安全性概述](../python/security-overview-sql-server-python-services.md)

