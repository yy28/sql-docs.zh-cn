---
title: 在 Linux 上配置使用情况和适用于 SQL Server 的诊断数据收集 |Microsoft Docs
description: 描述如何收集和配置 Linux 上 SQL Server 客户的使用情况和诊断数据。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 03/27/2019
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
ms.openlocfilehash: c94023e89dbdfb784f2b1bc8db8c9842c4455fb1
ms.sourcegitcommit: aa4f594ec6d3e85d0a1da6e69fa0c2070d42e1d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2019
ms.locfileid: "59243601"
---
# <a name="configure-usage-and-diagnostic-data-collection-for-sql-server-on-linux"></a>在 Linux 上配置使用情况和适用于 SQL Server 的诊断数据收集

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

默认情况下，Microsoft SQL Server 收集有关其客户如何使用应用程序的信息。 具体来说，SQL Server 收集有关安装体验、使用情况和性能的信息。 此信息有助于 Microsoft 改进产品以更好地满足客户需求。 例如，Microsoft 收集有关客户遇到的错误代码类型信息，这样我们就可以修复相关 bug，改进关于如何使用 SQL Server 的文档，并确定是否应将功能添加到产品中以更好地为客户服务。

本文档提供了有关收集哪些类型的信息以及有关如何发送，收集在 Linux 上配置 Microsoft SQL Server 详细信息到 Microsoft 的信息。 SQL Server 2017 包含隐私声明，其中介绍了我们执行操作并不会从用户收集哪些信息。 有关详细信息，请参阅[隐私声明](https://go.microsoft.com/fwlink/?LinkID=868444)。

具体而言，Microsoft 不会通过这种机制发送以下任何类型的信息：

- 用户表中的任何值
- 任何登录凭据或其他身份验证信息
- 个人身份信息 (PII)

SQL Server 2017 始终收集和发送从安装过程开始的安装体验相关信息，方便我们快速查找并修复客户遇到的任何安装问题。 可以配置 SQL Server 2017 不将发送到 Microsoft 通过 （根据每个服务器实例） 的信息**mssql conf**。 mssql conf 是 Red Hat Enterprise Linux、 SUSE Linux Enterprise Server 和 Ubuntu 安装了 SQL Server 2017 的配置脚本。

> [!NOTE]
> 只能在付费版本的 SQL Server 中禁用向 Microsoft 发送信息的功能。

## <a name="disable-usage-and-diagnostic-data-collection"></a>禁用使用情况和诊断数据收集

此选项可以根据 SQL Server 将发送使用情况和诊断数据收集到 Microsoft 或不更改。 默认情况下，此值设置为 true。 若要更改的值，运行以下命令：

> [!IMPORTANT]
> 您可以将关闭使用情况和诊断数据收集免费版本的 SQL Server、 Express 和开发人员。

### <a name="on-red-hat-suse-and-ubuntu"></a>在 Red Hat、 SUSE 和 Ubuntu

1. 作为与根运行 mssql-conf 脚本**设置**命令，以进行**telemetry.customerfeedback**。 下面的示例将禁用使用情况和诊断数据收集通过指定**false**。

   ```bash
   sudo /opt/mssql/bin/mssql-conf set telemetry.customerfeedback false
   ```

1. 重新启动 SQL Server 服务：

   ```bash
   sudo systemctl restart mssql-server
   ```
   
### <a name="on-docker"></a>Docker 上
若要禁用使用情况和 docker 上的诊断数据收集，必须具有 Docker[持久保存数据](sql-server-linux-configure-docker.md)。 

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

1. 添加`mssql.conf`行的文件`[telemetry]`和`customerfeedback = false`主机目录中：
 
   ```bash
   echo '[telemetry]' >> <host directory>/mssql.conf
   ```

   ```bash
   echo 'customerfeedback = false' >> <host directory>/mssql.conf
   ```

2. 运行容器映像

   ```bash
   docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2017-latest
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2017-latest
   ```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

1. 添加`mssql.conf`行的文件`[telemetry]`和`customerfeedback = false`主机目录中：

   ```bash
   echo '[telemetry]' >> <host directory>/mssql.conf
   ```

   ```bash
   echo 'customerfeedback = false' >> <host directory>/mssql.conf
   ```

2. 运行容器映像

   ```bash
   docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-CTP2.4-ubuntu
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-CTP2.4-ubuntu
   ```

::: moniker-end

## <a name="local-audit-for-sql-server-on-linux-usage-and-diagnostic-data-collection"></a>Linux 使用情况和诊断数据集合上的 SQL Server 的本地审核

Microsoft SQL Server 2017 包含了一些支持 Internet 的功能，可收集并向 Microsoft 发送有关你的计算机或设备 （"标准计算机信息"） 的信息。 SQL Server 使用情况和诊断数据收集的本地审核组件可以写入到指定的文件夹，它表示将发送给 Microsoft 的数据 （日志） 本服务收集的数据。 本地审核的用途是使客户可以出于合规性、监管或隐私验证原因而查看 Microsoft 使用此功能收集的所有数据。

在 Linux 上的 SQL Server，本地审核可以在实例级别针对 SQL Server 数据库引擎是可配置。 其他 SQL Server 组件和 SQL Server Tools 没有使用情况和诊断数据收集的本地审核功能。

### <a name="enable-local-audit"></a>启用本地审核

此选项后，本地审核并将目录设置在其中创建本地审核日志。

1. 创建新的本地审核日志的目标目录。 下面的示例创建一个新 **/tmp/审核**目录：

   ```bash
   sudo mkdir /tmp/audit
   ```

2. 更改所有者和组的目录**mssql**用户：

   ```bash
   sudo chown mssql /tmp/audit
   sudo chgrp mssql /tmp/audit
   ```

3. 作为与根运行 mssql-conf 脚本**设置**命令，以进行**telemetry.userrequestedlocalauditdirectory**:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set telemetry.userrequestedlocalauditdirectory /tmp/audit
   ```

4. 重新启动 SQL Server 服务：

   ```bash
   sudo systemctl restart mssql-server
   ```
   
### <a name="on-docker"></a>Docker 上
若要在 docker 上启用本地审核，必须具有 Docker[持久保存数据](sql-server-linux-configure-docker.md)。 

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

1. 在容器中将新的本地审核日志的目标目录。 在你的计算机上的主机目录中创建新的本地审核日志的目标目录。 下面的示例创建一个新 **/审核**目录：

   ```bash
   sudo mkdir <host directory>/audit
   ```

1. 添加`mssql.conf`行的文件`[telemetry]`和`userrequestedlocalauditdirectory = <host directory>/audit`主机目录中：
 
   ```bash
   echo '[telemetry]' >> <host directory>/mssql.conf
   ```

   ```bash
   echo 'userrequestedlocalauditdirectory = <host directory>/audit' >> <host directory>/mssql.conf
   ```

1. 运行容器映像

   ```bash
   docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2017-latest
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2017-latest
   ```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

1. 在容器中将新的本地审核日志的目标目录。 在你的计算机上的主机目录中创建新的本地审核日志的目标目录。 下面的示例创建一个新 **/审核**目录：

   ```bash
   sudo mkdir <host directory>/audit
   ```

1. 添加`mssql.conf`行的文件`[telemetry]`和`userrequestedlocalauditdirectory = <host directory>/audit`主机目录中：
 
   ```bash
   echo '[telemetry]' >> <host directory>/mssql.conf
   ```

   ```bash
   echo 'userrequestedlocalauditdirectory = <host directory>/audit' >> <host directory>/mssql.conf
   ```

1. 运行容器映像

   ```bash
   docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-CTP2.4-ubuntu
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-CTP2.4-ubuntu
   ```

::: moniker-end

## <a name="next-steps"></a>后续步骤

Linux 上 SQL Server 的详细信息，请参阅[概述的 SQL Server Linux 上](sql-server-linux-overview.md)。
