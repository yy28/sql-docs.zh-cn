---
title: 有关 SQL Server 中的机器学习的安全注意事项 |Microsoft 文档
ms.date: 02/01/2018
ms.reviewer: ''
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.author: heidist
author: HeidiSteen
manager: cgronlun
ms.workload: Inactive
ms.openlocfilehash: bd695d866479b88f139011ff4f7760b4c0565734
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/04/2018
---
# <a name="security-considerations-for-machine-learning-in-sql-server"></a>有关 SQL Server 中的机器学习的安全注意事项
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文列出了管理员或架构师应牢记使用机器学习服务时的安全注意事项。

**适用于：** SQL Server 2016 R Services、 SQL Server 自 2017 年 1 机器学习服务

## <a name="use-a-firewall-to-restrict-network-access"></a>使用防火墙限制网络访问权限

在默认安装中，Windows 防火墙规则用于阻止从外部运行时进程的所有出站网络访问权限。 应创建防火墙规则，以防止外部运行时进程下载程序包或进行其他可能有恶意的网络调用。

如果你使用的是其他防火墙程序，你还可以创建规则以阻止通过设置为本地用户帐户或用户帐户池所表示的组的规则的外部运行时，出站网络连接。

我们强烈建议您开启 Windows 防火墙 （或你选择的另一个防火墙） 以防止的 R 或 Python 运行时不受限制的网络访问权限。

## <a name="authentication-methods-supported-for-remote-compute-contexts"></a>支持远程计算上下文的身份验证方法

[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 支持 Windows 集成身份验证和 SQL 登录名创建之间的连接时[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和远程数据科学客户端。

例如，假设你在您的笔记本电脑上进行开发 R 解决方案并想要在 SQL Server 计算机上执行计算。 你将使用在 R，创建 SQL Server 数据源**rx**函数和定义连接字符串基于您的 Windows 凭据。

当你更改_计算上下文_从 SQL Server 计算机便携式计算机，所有 R 代码都执行的 SQL Server 计算机上，如果你的 Windows 帐户具有所需的权限。 此外，在你的凭据以及下运行的 R 代码的一部分执行的任何 SQL 查询。

在此方案还支持使用 SQL 登录名。 但是，这需要 SQL Server 实例将配置为允许混合的模式身份验证。

### <a name="implied-authentication"></a>隐式身份验证

 一般情况下，[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]启动外部脚本运行时并执行其自己的帐户下的脚本。 但是，如果外部运行时发出的 ODBC 调用，[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]模拟发送命令以确保不会无法通过 ODBC 调用用户的凭据。 这称为*隐式身份验证*。
 
 > [!IMPORTANT]
 > 默示的身份验证成功，包含辅助帐户的 Windows 用户组 (默认情况下， **SQLRUserGroup**) 必须具有 master 数据库中的帐户的实例，并且此帐户必须会获得对权限连接到的实例。
 > 
 > 组**SQLRUserGroup**运行 Python 脚本时，还使用。 

通常情况下，我们建议你将大型数据集移入 SQL Server 事先，而不是尝试读取数据使用 RODBC 或另一个库。 此外，使用 SQL Server 查询或视图作为您的主数据源，以提高性能。 

例如，你可能从 SQL Server 中获取定型数据 （通常的最大数据），并从外部源获取的因素列表。 你可以定义一个链接的服务器以便从大多数 ODBC 数据源获取数据。 有关详细信息，请参阅[创建链接的服务器](https://docs.microsoft.com/sql/relational-databases/linked-servers/create-linked-servers-sql-server-database-engine)。

若要尽量减少在 ODBC 调用外部数据源的依赖项，你还可能执行数据工程作为单独的进程，并将结果保存在表中，或使用 T-SQL 的。 请参阅本教程针对 SQL vs 中的数据工程一个很好示例。:[创建数据功能使用 T-SQL](../tutorials/sqldev-create-data-features-using-t-sql.md)。

## <a name="no-support-for-encryption-at-rest"></a>不支持静态加密

[透明数据加密 (TDE)](https://docs.microsoft.com/sql/relational-databases/security/encryption/transparent-data-encryption)的数据发送到或接收来自外部脚本运行时不支持。 原因是，R （或 Python） 外部运行的 SQL Server 进程;因此，使用的外部运行时数据不受数据库引擎的加密功能。  此行为是从数据库读取数据并使副本的 SQL Server 计算机上运行的任何其他客户端没有什么不同。

因此，TDE**不**应用到 R 或 Python 脚本中使用的任何数据或任何数据保存到磁盘，或任何持久的中间结果。 但是，其他类型的加密，如 Windows BitLocker 加密或第三方加密在文件或文件夹级别应用，仍适用。

情况下[始终加密](https://docs.microsoft.com/sql/relational-databases/security/encryption/overview-of-key-management-for-always-encrypted)，外部运行时不能访问的加密密钥; 因此，无法将数据发送到脚本。

## <a name="resources"></a>Resources

有关管理服务，以及如何设置用于执行机器学习脚本的用户帐户的详细信息，请参阅[配置和管理高级分析扩展](../../advanced-analytics/r/configure-and-manage-advanced-analytics-extensions.md)。

常规安全体系结构的说明，请参阅：

+ [R 的安全性概述](security-overview-sql-server-r.md)
+ [Python 的安全性概述](../python/security-overview-sql-server-python-services.md)
