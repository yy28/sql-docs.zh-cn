---
title: "在 Linux 上的 SQL Server 的客户反馈 |Microsoft 文档"
description: "描述如何收集和 Linux 上配置 SQL Server 客户反馈。"
author: annashres
ms.author: anshrest
manager: jhubbard
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: b2736223d2a333738ca17b3b3307034c6744512d
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="customer-feedback-for-sql-server-on-linux"></a>在 Linux 上的 SQL Server 的客户反馈

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

默认情况下，Microsoft SQL Server 收集有关其客户如何使用应用程序的信息。 具体来说，SQL Server 收集有关安装体验、使用情况和性能的信息。 此信息有助于 Microsoft 改进产品以更好地满足客户需求。 例如，Microsoft 收集有关客户遇到的错误代码类型信息，这样我们就可以修复相关 bug，改进关于如何使用 SQL Server 的文档，并确定是否应将功能添加到产品中以更好地为客户服务。

本文档提供有关收集哪些类型的信息以及如何在发送，它收集的 linux 操作系统上配置 Microsoft SQL Server 的详细信息向 Microsoft 的信息。 SQL Server 2017 包括说明我们执行操作并不会从用户收集哪些信息的隐私声明。 请阅读隐私声明 》。

具体而言，Microsoft 不会通过这种机制发送以下任何类型的信息：

- 用户表中的任何值
- 任何登录凭据或其他身份验证信息
- 个人身份信息 (PII)

SQL Server 2017 始终收集和发送从安装过程开始的安装体验相关信息，方便我们快速查找并修复客户遇到的任何安装问题。 可以配置 SQL Server 2017 不为 （针对每个服务器实例进行） 的信息发送给 Microsoft 通过**mssql conf**。 mssql conf 是将与 SQL Server 2017 为 Red Hat Enterprise Linux、 SUSE Linux 企业服务器和 Ubuntu 安装的配置脚本。

> [!NOTE]
> 只能在付费版本的 SQL Server 中禁用向 Microsoft 发送信息的功能。

## <a name="disable-customer-feedback"></a>禁用客户反馈

此选项允许你根据 SQL Server 向 Microsoft 发送反馈，或未更改。 默认情况下，此值设置为 true。 若要更改的值，请运行以下命令：

### <a name="on-red-hat-suse-and-ubuntu"></a>在 Red Hat、 SUSE 和 Ubuntu

1. Mssql conf 脚本作为根与运行**设置**命令**telemetry.customerfeedback**。 下面的示例通过指定关闭客户反馈**false**。

   ```bash
   sudo /opt/mssql/bin/mssql-conf set telemetry.customerfeedback false
   ```

1. 重新启动 SQL Server 服务：

   ```bash
   sudo systemctl restart mssql-server
   ```
   
### <a name="on-docker"></a>在 Docker 上
若要在 docker 上禁用客户反馈必须 Docker[保存数据](sql-server-linux-configure-docker.md)。 

1. 添加`mssql.conf`文件替换为行`[telemetry]`和`customerfeedback = false`主机目录中：
 
   ```bash
   echo '[telemetry]' >> <host directory>/mssql.conf
   ```

   ```bash
   echo 'customerfeedback = false' >> <host directory>/mssql.conf
   ```
2. 运行容器映像
   ```bash
   docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v <host directory>:/var/opt/mssql -d microsoft/mssql-server-linux:2017-latest
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>:/var/opt/mssql -d microsoft/mssql-server-linux:2017-latest
   ```
   
## <a name="local-audit-for-sql-server-on-linux-usage-feedback-collection"></a>有关 Linux 用法反馈集合上的 SQL Server 的本地审核

Microsoft SQL Server 2017 包含 Internet 启用的功能，可以收集并向 Microsoft 发送有关你的计算机或设备 （"标准计算机信息"） 的信息。 SQL Server 使用情况反馈集合的本地审核组件可以写入到指定的文件夹，表示将发送给 Microsoft 的数据 （日志） 服务收集的数据。 本地审核的用途是使客户可以出于合规性、监管或隐私验证原因而查看 Microsoft 使用此功能收集的所有数据。

在 Linux 上的 SQL Server，本地审核可以在 SQL Server 数据库引擎的实例级别上是可配置。 其他 SQL Server 组件和 SQL Server 工具没有使用情况反馈收集本地审核功能。

### <a name="enable-local-audit"></a>启用本地审核

此选项允许本地审核，并且允许你设置在其中创建本地审核日志的目录。

1. 创建新的本地审核日志的目标目录。 下面的示例创建一个新**/tmp/审核**目录：

   ```bash
   sudo mkdir /tmp/audit
   ```

1. 更改所有者和到的目录组**mssql**用户：

   ```bash
   sudo chown mssql /tmp/audit
   sudo chgrp mssql /tmp/audit
   ```

1. Mssql conf 脚本作为根与运行**设置**命令**telemetry.userrequestedlocalauditdirectory**:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set telemetry.userrequestedlocalauditdirectory /tmp/audit
   ```

1. 重新启动 SQL Server 服务：

   ```bash
   sudo systemctl restart mssql-server
   ```
   
### <a name="on-docker"></a>在 Docker 上
若要在 docker 上启用本地审核必须 Docker[保存数据](sql-server-linux-configure-docker.md)。 

1. 新的本地审核日志的目标目录将容器中。 在您的计算机上的主机目录中创建新的本地审核日志的目标目录。 下面的示例创建一个新**/审核**目录：

   ```bash
   sudo mkdir <host directory>/audit
   ```

   
1. 添加`mssql.conf`文件替换为行`[telemetry]`和`userrequestedlocalauditdirectory = <host directory>/audit`主机目录中：
 
   ```bash
   echo '[telemetry]' >> <host directory>/mssql.conf
   ```

   ```bash
   echo 'userrequestedlocalauditdirectory = <host directory>/audit' >> <host directory>/mssql.conf
   ```
2. 运行容器映像
   ```bash
   docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v <host directory>:/var/opt/mssql -d microsoft/mssql-server-linux:2017-latest
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>:/var/opt/mssql -d microsoft/mssql-server-linux:2017-latest
   ```
   
## <a name="next-steps"></a>后续步骤

在 Linux 上 SQL Server 的详细信息，请参阅[概述的 SQL Server on Linux](sql-server-linux-overview.md)。

