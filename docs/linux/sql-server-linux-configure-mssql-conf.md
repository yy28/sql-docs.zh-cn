---
title: 在 Linux 上配置 SQL Server 设置
description: 本文介绍如何使用 mssql-conf 工具配置 Linux 上的 SQL Server 设置。
author: VanMSFT
ms.author: vanto
manager: jroth
ms.date: 02/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 06798dff-65c7-43e0-9ab3-ffb23374b322
ms.openlocfilehash: 57e43f3afd9c46e3b49e4f1f07ab3038359c8c50
ms.sourcegitcommit: 93d1566b9fe0c092c9f0f8c84435b0eede07019f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2019
ms.locfileid: "67834012"
---
# <a name="configure-sql-server-on-linux-with-the-mssql-conf-tool"></a>使用 mssql-conf 工具配置 Linux 上的 SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

**mssql conf**是 Red Hat Enterprise Linux、 SUSE Linux Enterprise Server 和 Ubuntu 安装了 SQL Server 2017 的配置脚本。 可以使用此实用工具设置以下参数：

|||
|---|---|
| [代理](#agent) | 启用 SQL Server 代理 |
| [排序规则](#collation) | 在 Linux 上为 SQL Server 设置新的排序规则。 |
| [客户反馈](#customerfeedback) | 选择 SQL Server 将反馈发送给 Microsoft。 |
| [数据库邮件配置文件](#dbmail) | 设置 SQL Server 的 Linux 上的默认数据库邮件配置文件。 |
| [默认数据目录](#datadir) | 更改默认目录的新 SQL Server 数据库数据文件 (.mdf)。 |
| [默认日志目录](#datadir) | 更改新的 SQL Server 数据库日志 (.ldf) 文件的默认目录。 |
| [默认 master 数据库目录](#masterdatabasedir) | 更改主数据库和日志文件的默认目录。|
| [默认 master 数据库文件名称](#masterdatabasename) | 更改 master 数据库文件的名称。 |
| [默认转储目录](#dumpdir) | 更改新的内存转储和其他故障排除的文件的默认目录。 |
| [默认错误日志目录](#errorlogdir) | 更改 SQL Server 错误日志、 默认 Profiler 跟踪、 系统运行状况会话 XE 和 Hekaton 会话 XE 的新文件的默认目录。 |
| [默认备份目录](#backupdir) | 更改新的备份文件的默认目录。 |
| [转储类型](#coredump) | 选择要收集的转储内存转储文件的类型。 |
| [高可用性](#hadr) | 启用可用性组。 |
| [本地审核目录](#localaudit) | 设置要添加本地审核文件的目录。 |
| [区域设置](#lcid) | 设置 SQL Server 使用的区域设置。 |
| [内存限制](#memorylimit) | 设置 SQL Server 的内存限制。 |
| [TCP 端口](#tcpport) | 更改 SQL Server 侦听的连接的端口。 |
| [TLS](#tls) | 配置传输级安全。 |
| [跟踪标志](#traceflags) | 设置服务要使用的跟踪标志。 |

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

**mssql conf**一起安装的配置脚本[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)]Red Hat Enterprise Linux、 SUSE Linux Enterprise Server 和 Ubuntu。 可以使用此实用工具设置以下参数：

|||
|---|---|
| [代理](#agent) | 启用 SQL Server 代理 |
| [排序规则](#collation) | 在 Linux 上为 SQL Server 设置新的排序规则。 |
| [客户反馈](#customerfeedback) | 选择 SQL Server 将反馈发送给 Microsoft。 |
| [数据库邮件配置文件](#dbmail) | 设置 SQL Server 的 Linux 上的默认数据库邮件配置文件。 |
| [默认数据目录](#datadir) | 更改默认目录的新 SQL Server 数据库数据文件 (.mdf)。 |
| [默认日志目录](#datadir) | 更改新的 SQL Server 数据库日志 (.ldf) 文件的默认目录。 |
| [默认 master 数据库文件目录](#masterdatabasedir) | 更改现有的 SQL 安装上的 master 数据库文件的默认目录。|
| [默认 master 数据库文件名称](#masterdatabasename) | 更改 master 数据库文件的名称。 |
| [默认转储目录](#dumpdir) | 更改新的内存转储和其他故障排除的文件的默认目录。 |
| [默认错误日志目录](#errorlogdir) | 更改 SQL Server 错误日志、 默认 Profiler 跟踪、 系统运行状况会话 XE 和 Hekaton 会话 XE 的新文件的默认目录。 |
| [默认备份目录](#backupdir) | 更改新的备份文件的默认目录。 |
| [转储类型](#coredump) | 选择要收集的转储内存转储文件的类型。 |
| [高可用性](#hadr) | 启用可用性组。 |
| [本地审核目录](#localaudit) | 设置要添加本地审核文件的目录。 |
| [区域设置](#lcid) | 设置 SQL Server 使用的区域设置。 |
| [内存限制](#memorylimit) | 设置 SQL Server 的内存限制。 |
| [Microsoft 分布式事务处理协调器](#msdtc) | 配置和故障排除 Linux 上的 MSDTC。 |
| [MLServices Eula](#mlservices-eula) | R 和 Python Eula 接受 mlservices 包。 适用于仅 SQL Server 2019。|
| [outboundnetworkaccess](#mlservices-outbound-access) |启用出站网络访问权限[mlservices](sql-server-linux-setup-machine-learning.md) R、 Python 和 Java 扩展。|
| [TCP 端口](#tcpport) | 更改 SQL Server 侦听的连接的端口。 |
| [TLS](#tls) | 配置传输级安全。 |
| [跟踪标志](#traceflags) | 设置服务要使用的跟踪标志。 |

::: moniker-end

> [!TIP]
> 此外可以使用环境变量配置其中的某些设置。 有关详细信息，请参阅[使用环境变量配置 SQL Server 设置](sql-server-linux-configure-environment-variables.md)。

## <a name="usage-tips"></a>使用提示

* 有关 Always On 可用性组和共享的磁盘群集，始终在每个节点上进行相同的配置更改。

* 为共享的磁盘群集方案中，不要尝试重新启动**mssql server**服务以应用更改。 SQL Server 正在运行的应用程序。 相反，使资源离线，然后回到联机状态。

* 这些示例通过指定完整路径运行 mssql-conf: **/opt/mssql/bin/mssql-conf**。 如果您选择改为导航到该路径，在当前目录的上下文中运行 mssql-conf: **。 / mssql conf**。

## <a id="agent"></a> 启用 SQL Server 代理

**Sqlagent.enabled**设置可让[SQL Server 代理](sql-server-linux-run-sql-server-agent-job.md)。 默认情况下会禁用 SQL Server 代理。 如果**sqlagent.enabled**中不存在 mssql.conf 设置文件，然后在内部 SQL Server 将认为 SQL Server 代理已禁用。

若要更改此设置，请使用以下步骤：

1. 启用 SQL Server 代理：

   ```bash
   sudo /opt/mssql/bin/mssql-conf set sqlagent.enabled true 
   ```

2. 重新启动 SQL Server 服务：

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a id="collation"></a> 更改 SQL Server 排序规则

**集排序规则**选项排序规则的值更改为任何支持的排序规则。

1. 第一个[备份任何用户数据库](sql-server-linux-backup-and-restore-database.md)在服务器上。

1. 然后，使用[sp_detach_db](../relational-databases/system-stored-procedures/sp-detach-db-transact-sql.md)存储过程来分离用户数据库。

1. 运行**集排序规则**选项，并按照提示进行操作：

   ```bash
   sudo /opt/mssql/bin/mssql-conf set-collation
   ```

1. Mssql-conf 实用工具将尝试将更改为指定的排序规则值并重新启动服务。 如果有任何错误，它将回滚排序规则到以前的值。

1. 还原用户数据库备份。

有关支持的排序规则的列表，运行[sys.fn_helpcollations](../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md)函数： `SELECT Name from sys.fn_helpcollations()`。

## <a id="customerfeedback"></a> 配置客户反馈

**Telemetry.customerfeedback**是否 SQL Server 将反馈发送给 Microsoft 或不设置更改。 默认情况下，此值设置为 **，则返回 true**适用于所有版本。 若要更改的值，运行以下命令：

> [!IMPORTANT]
> 您可以将关闭客户反馈免费版本的 SQL Server、 Express 和开发人员。

1. 作为与根运行 mssql-conf 脚本**设置**命令，以进行**telemetry.customerfeedback**。 下面的示例通过指定关闭客户反馈**false**。

   ```bash
   sudo /opt/mssql/bin/mssql-conf set telemetry.customerfeedback false
   ```

1. 重新启动 SQL Server 服务：

   ```bash
   sudo systemctl restart mssql-server
   ```

有关详细信息，请参阅[Linux 上的 SQL Server 客户反馈](sql-server-linux-customer-feedback.md)并[SQL Server 隐私声明](https://go.microsoft.com/fwlink/?LinkID=868444)。

## <a id="datadir"></a> 更改默认数据或日志目录位置

**Filelocation.defaultdatadir**并**filelocation.defaultlogdir**设置更改在其中创建新的数据库和日志文件的位置。 默认情况下，此位置为 /var/opt/mssql/data。 若要更改这些设置，请使用以下步骤：

1. 创建新的数据库的目标目录数据和日志文件。 下面的示例创建一个新 **/tmp/数据**目录：

   ```bash
   sudo mkdir /tmp/data
   ```

1. 更改所有者和组的目录**mssql**用户：

   ```bash
   sudo chown mssql /tmp/data
   sudo chgrp mssql /tmp/data
   ```

1. 使用 mssql conf 更改使用的默认数据目录**设置**命令：

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.defaultdatadir /tmp/data
   ```

1. 重新启动 SQL Server 服务：

   ```bash
   sudo systemctl restart mssql-server
   ```

1. 现在，已创建的新数据库的所有数据库文件都将存储在此新位置。 如果要更改新数据库的日志文件 (.ldf) 位置，可以使用下面的“set”命令：

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.defaultlogdir /tmp/log
   ```

1. 此命令还假定/tmp/日志目录存在，并且它是在用户和组下**mssql**。


## <a id="masterdatabasedir"></a> 更改默认 master 数据库文件目录位置

**Filelocation.masterdatafile**并**filelocation.masterlogfile**设置 SQL Server 引擎中查找的 master 数据库文件的位置的更改。 默认情况下，此位置为 /var/opt/mssql/data。

若要更改这些设置，请使用以下步骤：

1. 创建新的错误日志文件的目标目录。 下面的示例创建一个新 **/tmp/masterdatabasedir**目录：

   ```bash
   sudo mkdir /tmp/masterdatabasedir
   ```

1. 更改所有者和组的目录**mssql**用户：

   ```bash
   sudo chown mssql /tmp/masterdatabasedir
   sudo chgrp mssql /tmp/masterdatabasedir
   ```

1. 使用 mssql conf 来更改与 master 数据和日志文件的默认 master 数据库目录**设置**命令：

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.masterdatafile /tmp/masterdatabasedir/master.mdf
   sudo /opt/mssql/bin/mssql-conf set filelocation.masterlogfile /tmp/masterdatabasedir/mastlog.ldf
   ```

   > [!NOTE]
   > 除了移动 master 数据和日志文件，这也会移动所有其他系统数据库的默认位置。

1. 停止 SQL Server 服务：

   ```bash
   sudo systemctl stop mssql-server
   ```

1. 将 master.mdf 和 masterlog.ldf 移动：

   ```bash
   sudo mv /var/opt/mssql/data/master.mdf /tmp/masterdatabasedir/master.mdf 
   sudo mv /var/opt/mssql/data/mastlog.ldf /tmp/masterdatabasedir/mastlog.ldf
   ```

1. 启动 SQL Server 服务：

   ```bash
   sudo systemctl start mssql-server
   ```

   > [!NOTE]
   > 如果 SQL Server 无法在指定的目录中找到 master.mdf 和 mastlog.ldf 文件，将在指定的目录中，自动创建模板化副本的系统数据库和 SQL Server 已成功启动。 但是，不会在新的 master 数据库中更新元数据，例如用户数据库、 服务器登录名、 服务器证书、 加密密钥、 SQL 代理作业或旧的 SA 登录名密码。 你将需要停止 SQL Server 并将你的旧 master.mdf 和 mastlog.ldf 移动到新的指定位置并启动 SQL Server 以继续使用现有的元数据。
 
## <a id="masterdatabasename"></a> 更改 master 数据库文件的名称

**Filelocation.masterdatafile**并**filelocation.masterlogfile**设置 SQL Server 引擎中查找的 master 数据库文件的位置的更改。 此外可以使用此更改的主数据库和日志文件的名称。 

若要更改这些设置，请使用以下步骤：

1. 停止 SQL Server 服务：

   ```bash
   sudo systemctl stop mssql-server
   ```

1. 使用 mssql-conf 更改与 master 数据和日志文件的主数据库的预期的名称**设置**命令：

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.masterdatafile /var/opt/mssql/data/masternew.mdf
   sudo /opt/mssql/bin/mssql-conf set filelocation.mastlogfile /var/opt/mssql/data/mastlognew.ldf
   ```

   > [!IMPORTANT]
   > 只能更改 master 数据库的名称和 SQL Server 已成功启动后的日志文件。 之前在首次运行 SQL Server 需要 master.mdf 和 mastlog.ldf 命名的文件。

1. 更改 master 数据库数据和日志文件的名称 

   ```bash
   sudo mv /var/opt/mssql/data/master.mdf /var/opt/mssql/data/masternew.mdf
   sudo mv /var/opt/mssql/data/mastlog.ldf /var/opt/mssql/data/mastlognew.ldf
   ```

1. 启动 SQL Server 服务：

   ```bash
   sudo systemctl start mssql-server
   ```

## <a id="dumpdir"></a> 更改默认转储目录位置

**Filelocation.defaultdumpdir**设置的内存和 SQL 转储生成系统崩溃时的默认位置的更改。 默认情况下，这些文件在 /var/opt/mssql/log 中生成。

若要设置此新位置，请使用以下命令：

1. 创建新的转储文件的目标目录。 下面的示例创建一个新 **/tmp/转储**目录：

   ```bash
   sudo mkdir /tmp/dump
   ```

1. 更改所有者和组的目录**mssql**用户：

   ```bash
   sudo chown mssql /tmp/dump
   sudo chgrp mssql /tmp/dump
   ```

1. 使用 mssql conf 更改使用的默认数据目录**设置**命令：

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.defaultdumpdir /tmp/dump
   ```

1. 重新启动 SQL Server 服务：

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a id="errorlogdir"></a> 更改默认错误日志文件目录位置

**Filelocation.errorlogfile**设置创建新的错误日志、 默认探查器跟踪、 系统运行状况会话 XE 和 Hekaton XE 会话文件的位置的更改。 默认情况下，此位置为 /var/opt/mssql/log。 在其中设置 SQL 错误日志文件的目录将成为其他日志的默认日志目录。

若要更改这些设置：

1. 创建新的错误日志文件的目标目录。 下面的示例创建一个新 **/tmp/logs**目录：

   ```bash
   sudo mkdir /tmp/logs
   ```

1. 更改所有者和组的目录**mssql**用户：

   ```bash
   sudo chown mssql /tmp/logs
   sudo chgrp mssql /tmp/logs
   ```

1. 使用 mssql conf 更改的默认错误日志文件名**设置**命令：

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.errorlogfile /tmp/logs/errorlog
   ```

1. 重新启动 SQL Server 服务：

   ```bash
   sudo systemctl restart mssql-server
   ```


## <a id="backupdir"></a> 更改默认备份目录位置

**Filelocation.defaultbackupdir**设置其中生成备份文件的默认位置的更改。 默认情况下，这些文件在 /var/opt/mssql/data 中生成。

若要设置此新位置，请使用以下命令：

1. 创建新的备份文件的目标目录。 下面的示例创建一个新 **/tmp/备份**目录：

   ```bash
   sudo mkdir /tmp/backup
   ```

1. 更改所有者和组的目录**mssql**用户：

   ```bash
   sudo chown mssql /tmp/backup
   sudo chgrp mssql /tmp/backup
   ```

1. 使用 mssql-conf 通过“set”命令更改默认备份目录：

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.defaultbackupdir /tmp/backup
   ```

1. 重新启动 SQL Server 服务：

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a id="coredump"></a> 指定核心转储设置

如果一个 SQL Server 进程中发生异常，SQL Server 会创建内存转储。

有两个选项控制的类型的内存转储，收集 SQL Server: **coredump.coredumptype**并**coredump.captureminiandfull**。 这两个选项与核心转储捕获的两个阶段相关。 

第一阶段捕获受**coredump.coredumptype**设置，它确定异常期间生成的转储文件的类型。 当启用了第二个阶段**coredump.captureminiandfull**设置。 如果**coredump.captureminiandfull**设置为 true，转储所指定的文件**coredump.coredumptype**生成，还生成第二个的小型转储。 设置**coredump.captureminiandfull**为 false 会禁止第二次捕获尝试。

1. 决定是否要捕获与小型转储和完全转储**coredump.captureminiandfull**设置。

    ```bash
    sudo /opt/mssql/bin/mssql-conf set coredump.captureminiandfull <true or false>
    ```

    默认值： **false**

1. 指定的转储文件类型**coredump.coredumptype**设置。

    ```bash
    sudo /opt/mssql/bin/mssql-conf set coredump.coredumptype <dump_type>
    ```

    默认值： **miniplus**

    下表列出了可能**coredump.coredumptype**值。

    | type | 描述 |
    |-----|-----|
    | **mini** | mini 是最小的转储文件类型。 它使用 Linux 系统信息确定进程中的线程和模块。 转储仅包含主机环境线程堆栈和模块。 不包含间接内存引用或全局变量。 |
    | **miniplus** | MiniPlus 与 mini 相似，但它包括更多内存。 它理解 SQLPAL 和主机环境中，将下面的内存区域添加到转储的内部：</br></br> -各种全局变量</br> 的超过 64tb 所有内存</br> -所有命名区域中找到 **/proc/$ pid/maps**</br> 的来自线程和堆栈间接内存</br> 线程信息</br> -相关 Teb 和 Peb 的</br> 模块信息</br> VMM 和 VAD 树 |
    | **filtered** | filtered 采用基于减法的设计，包括进程中的所有内存，除非专门排除某些内存。 此设计理解 SQLPAL 的内部机制和宿主环境，从转储中排除某些区域。
    | **full** | 完全位于中包括所有区域的完整过程转储 **/proc/$ pid/maps**。 这不受**coredump.captureminiandfull**设置。 |

## <a id="dbmail"></a> 设置在 Linux 上的 SQL Server 的默认数据库邮件配置文件

**Sqlpagent.databasemailprofile** ，可以设置电子邮件警报的默认数据库邮件配置文件。

```bash
sudo /opt/mssq/bin/mssql-conf set sqlagent.databasemailprofile <profile_name>
```
## <a id="hadr"></a> 高可用性

**Hadr.hadrenabled**选项使您的 SQL Server 实例上的可用性组。 以下命令通过设置可使可用性组**hadr.hadrenabled**为 1。 必须重启 SQL Server，该设置才能生效。

```bash
sudo /opt/mssql/bin/mssql-conf set hadr.hadrenabled  1
sudo systemctl restart mssql-server
```

有关如何使用此方法与可用性组的信息，请参阅以下两个主题。

- [配置 Always On 可用性组为 Linux 上的 SQL Server](sql-server-linux-availability-group-configure-ha.md)
- [Linux 上的 SQL Server 配置读取缩放可用性组](sql-server-linux-availability-group-configure-rs.md)


## <a id="localaudit"></a> 设置本地审核目录

**Telemetry.userrequestedlocalauditdirectory**设置启用本地审核，以及在创建可让你设置目录，其中的本地审核日志。

1. 创建新的本地审核日志的目标目录。 下面的示例创建一个新 **/tmp/审核**目录：

   ```bash
   sudo mkdir /tmp/audit
   ```

1. 更改所有者和组的目录**mssql**用户：

   ```bash
   sudo chown mssql /tmp/audit
   sudo chgrp mssql /tmp/audit
   ```

1. 作为与根运行 mssql-conf 脚本**设置**命令，以进行**telemetry.userrequestedlocalauditdirectory**:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set telemetry.userrequestedlocalauditdirectory /tmp/audit
   ```

1. 重新启动 SQL Server 服务：

   ```bash
   sudo systemctl restart mssql-server
   ```

有关详细信息，请参阅[Linux 上的 SQL Server 客户反馈](sql-server-linux-customer-feedback.md)。

## <a id="lcid"></a> 更改 SQL Server 区域设置

**Language.lcid**将更改 SQL Server 区域设置设置为任何受支持的语言标识符 (LCID)。 

1. 下面的示例更改为法语区域设置 (1036):

   ```bash
   sudo /opt/mssql/bin/mssql-conf set language.lcid 1036
   ```

1. 重新启动 SQL Server 服务以应用所做的更改：

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a id="memorylimit"></a> 设置内存限制

**Memory.memorylimitmb**到 SQL Server 设置控制量可用物理内存 （以 mb 为单位）。 默认值为 80%的物理内存。

1. 作为与根运行 mssql-conf 脚本**设置**命令，以进行**memory.memorylimitmb**。 下面的示例更改为 SQL Server 到 3.25 GB (3328 MB) 的可用内存。

   ```bash
   sudo /opt/mssql/bin/mssql-conf set memory.memorylimitmb 3328
   ```

1. 重新启动 SQL Server 服务以应用所做的更改：

   ```bash
   sudo systemctl restart mssql-server
   ```

::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

## <a id="msdtc"></a> 配置 MSDTC

**Network.rpcport**并**distributedtransaction.servertcpport**设置用于配置 Microsoft 分布式事务处理协调器 (MSDTC)。 若要更改这些设置，请运行以下命令：

1. 作为与根运行 mssql-conf 脚本**设置**"network.rpcport"命令：

   ```bash
   sudo /opt/mssql/bin/mssql-conf set network.rpcport <rcp_port>
   ```

2. 然后将"distributedtransaction.servertcpport"设置：

   ```bash
   sudo /opt/mssql/bin/mssql-conf set distributedtransaction.servertcpport <servertcpport_port>
   ```

除了设置这些值，还必须配置路由并更新防火墙以允许端口 135。 有关如何执行此操作的详细信息，请参阅[如何在 Linux 上配置 MSDTC](sql-server-linux-configure-msdtc.md)。

有几个可用于监视和故障排除 MSDTC 的 mssql conf 其他设置。 下表简要介绍这些设置。 有关其用法的详细信息，请参阅 Windows 支持文章中的详细信息[如何对 MS DTC 中启用诊断跟踪](https://support.microsoft.com/help/926099/how-to-enable-diagnostic-tracing-for-ms-dtc-on-a-windows-based-compute)。

| mssql-conf 设置 | 描述 |
|---|---|
| distributedtransaction.allowonlysecurerpccalls | 配置安全的分布式事务的唯一 RPC 调用 |
| distributedtransaction.fallbacktounsecurerpcifnecessary | 为分布式配置安全仅 RPC 调用 |事务
| distributedtransaction.maxlogsize | 以 mb 为单位，DTC 事务日志文件大小。 默认值为 64 MB |
| distributedtransaction.memorybuffersize | 循环缓冲区跟踪存储大小。 此大小是以 mb 为单位，默认值为 10 MB |
| distributedtransaction.servertcpport | MSDTC rpc 服务器端口 |
| distributedtransaction.trace_cm | 连接管理器中的跟踪 |
| distributedtransaction.trace_contact | 跟踪的联系人的池和联系人 |
| distributedtransaction.trace_gateway | 跟踪网关源 |
| distributedtransaction.trace_log | 日志跟踪 |
| distributedtransaction.trace_misc | 不能归入其他类别分类的跟踪 |
| distributedtransaction.trace_proxy | MSDTC 代理中生成的跟踪 |
| distributedtransaction.trace_svc | 跟踪服务和.exe 文件启动 |
| distributedtransaction.trace_trace | 跟踪基础结构本身 |
| distributedtransaction.trace_util | 从多个位置调用的跟踪实用程序例程 |
| distributedtransaction.trace_xa | XA 事务管理器 (XATM) 跟踪源 |
| distributedtransaction.tracefilepath | 文件应存储在跟踪中的文件夹 |
| distributedtransaction.turnoffrpcsecurity | 启用或禁用 RPC 安全性为分布式事务 |

::: moniker-end
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

## <a id="mlservices-eula"></a> 接受 MLServices Eula

添加[机器学习 R 或 Python 程序包](sql-server-linux-setup-machine-learning.md)到数据库引擎需要接受的 R 和 Python 开源分发版的许可条款。 下表枚举了所有可用的命令或 mlservices Eula 与相关的选项。 相同的最终用户许可协议参数用于 R 和 Python，具体取决于您的安装。

```bash
# For all packages: database engine and mlservices
# Setup prompts for mlservices EULAs, which you need to accept
sudo /opt/mssql/bin/mssql-conf setup

# Add R or Python to an existing installation
sudo /opt/mssql/bin/mssql-conf setup accept-eula-ml

# Alternative valid syntax
# Adds the EULA section to the INI and sets acceptulam to yes
sudo /opt/mssql/bin/mssql-conf set EULA accepteulaml Y

# Rescind EULA acceptance and removes the setting
sudo /opt/mssql/bin/mssql-conf unset EULA accepteulaml
```

您还可以直接添加的 EULA 接受[mssql.conf 文件](#mssql-conf-format):

```ini
[EULA]
accepteula = Y
accepteulaml = Y
```
:::moniker-end
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

## <a id="mlservices-outbound-access"></a> 启用出站网络访问

R、 Python 和 Java 中的扩展的出站网络访问[SQL Server 机器学习服务](sql-server-linux-setup-machine-learning.md)功能默认处于禁用状态。 若要启用出站请求，请将"outboundnetworkaccess"布尔属性使用 mssql-conf

设置属性之后, 重新启动 SQL Server Launchpad 服务读取 INI 文件的更新的值。 重新启动消息提醒您在每当修改扩展性相关的设置。

```bash
# Adds the extensibility section and property.
# Sets "outboundnetworkaccess" to true.
# This setting is required if you want to access data or operations off the server.
sudo /opt/mssql/bin/mssql-conf set extensibility outboundnetworkaccess 1

# Turns off network access but preserves the setting
/opt/mssql/bin/mssql-conf set extensibility outboundnetworkaccess 0

# Removes the setting and rescinds network access
sudo /opt/mssql/bin/mssql-conf unset extensibility.outboundnetworkaccess
```

您还可以添加"outboundnetworkaccess"直接[mssql.conf 文件](#mssql-conf-format):

```ini
[extensibility]
outboundnetworkaccess = 1
```
:::moniker-end

## <a id="tcpport"></a> 更改 TCP 端口

**Network.tcpport**设置 SQL Server 侦听的连接的 TCP 端口的更改。 默认情况下，此端口设置为 1433。 若要更改端口，请运行以下命令：

1. 使用“network.tcpport”的“set”命令以根用户身份运行 mssql-conf 脚本：

   ```bash
   sudo /opt/mssql/bin/mssql-conf set network.tcpport <new_tcp_port>
   ```

2. 重新启动 SQL Server 服务：

   ```bash
   sudo systemctl restart mssql-server
   ```

3. 时现在连接到 SQL Server，必须在主机名或 IP 地址之后使用逗号 （，） 指定自定义端口。 例如，要使用 SQLCMD 进行连接，则需使用以下命令：

   ```bash
   sqlcmd -S localhost,<new_tcp_port> -U test -P test
   ```

## <a id="tls"></a> 指定 TLS 设置

以下选项在 Linux 上运行的 SQL Server 实例配置 TLS。

|Option |描述 |
|--- |--- |
|**network.forceencryption** |如果为 1，然后[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]强制所有连接进行加密。 默认情况下，此选项为 0。 |
|**network.tlscert** |证书的绝对路径文件[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]使用 TLS。 例如： `/etc/ssl/certs/mssql.pem`  证书文件必须是可由 mssql 帐户访问。 Microsoft 建议将访问限制文件使用到`chown mssql:mssql <file>; chmod 400 <file>`。 |
|**network.tlskey** |私钥的绝对路径文件[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]使用 TLS。 例如：`/etc/ssl/private/mssql.key`  证书文件必须是可由 mssql 帐户访问。 Microsoft 建议将访问限制文件使用到`chown mssql:mssql <file>; chmod 400 <file>`。 |
|**network.tlsprotocols** |允许通过 SQL Server 的哪个 TLS 协议以逗号分隔列表。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 始终会尝试协商的最强的允许的协议。 如果客户端不支持任何允许的协议，[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]拒绝连接尝试。  对于兼容性，默认情况下，（1.2、 1.1 和 1.0） 允许所有支持的协议。  如果你的客户端支持 TLS 1.2，Microsoft 建议允许仅 TLS 1.2。 |
|**network.tlsciphers** |指定允许哪些密码[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]TLS 的。 此字符串的格式必须每[OpenSSL 的密码列表格式](https://www.openssl.org/docs/man1.0.2/apps/ciphers.html)。 一般情况下，不需要更改此选项。 <br /> 默认情况下，允许以下密码： <br /> `ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES128-SHA256:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES128-SHA256:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA:ECDHE-RSA-AES128-SHA:AES256-GCM-SHA384:AES128-GCM-SHA256:AES256-SHA256:AES128-SHA256:AES256-SHA:AES128-SHA` |
| **network.kerberoskeytabfile** |Kerberos keytab 文件的路径 |

使用 TLS 设置的示例，请参阅[加密的连接到 Linux 上的 SQL Server](sql-server-linux-encrypted-connections.md)。

## <a id="traceflags"></a> 启用/禁用跟踪标志

这**跟踪标志**选项启用或禁用跟踪标志启动的 SQL Server 服务。 若要启用/禁用跟踪标志，请使用以下命令：

1. 启用跟踪标志使用以下命令。 例如，对于跟踪标志 1234：

   ```bash
   sudo /opt/mssql/bin/mssql-conf traceflag 1234 on
   ```

1. 可以通过单独指定跟踪标志来启用多个跟踪标志：

   ```bash
   sudo /opt/mssql/bin/mssql-conf traceflag 2345 3456 on
   ```

1. 在类似的方式，您可以通过指定它们，并添加禁用一个或多个启用的跟踪标志**关闭**参数：

   ```bash
   sudo /opt/mssql/bin/mssql-conf traceflag 1234 2345 3456 off
   ```

1. 重新启动 SQL Server 服务以应用所做的更改：

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a name="remove-a-setting"></a>删除设置

取消设置的任何设置进行`mssql-conf set`，调用**mssql conf**与`unset`选项和设置的名称。 这将清除该设置，有效地将其返回到其默认值。

1. 以下示例清除**network.tcpport**选项。

   ```bash
   sudo /opt/mssql/bin/mssql-conf unset network.tcpport
   ```

1. 重启 SQL Server 服务。

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a name="view-current-settings"></a>查看当前设置

若要查看任何配置设置，请运行以下命令输出的内容**mssql.conf**文件：

```bash
sudo cat /var/opt/mssql/mssql.conf
```

请注意，未在此文件中显示的所有设置均使用其默认值。 下一节提供了一个示例**mssql.conf**文件。


## <a id="mssql-conf-format"></a> mssql.conf format

以下 **/var/opt/mssql/mssql.conf**文件提供每个设置的示例。 可以使用此格式才能手动更改**mssql.conf**文件根据需要。 如果手动更改该文件，必须重新启动 SQL Server 之前应用所做的更改。 若要使用**mssql.conf**文件使用 Docker，你必须具有 Docker[持久保存数据](sql-server-linux-configure-docker.md)。 首先添加整个**mssql.conf**文件到你的主机目录，然后运行该容器。 没有出现在这种[客户反馈](sql-server-linux-customer-feedback.md)。

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

```ini
[EULA]
accepteula = Y

[coredump]
captureminiandfull = true
coredumptype = full

[filelocation]
defaultbackupdir = /var/opt/mssql/data/
defaultdatadir = /var/opt/mssql/data/
defaultdumpdir = /var/opt/mssql/data/
defaultlogdir = /var/opt/mssql/data/

[hadr]
hadrenabled = 0

[language]
lcid = 1033

[memory]
memorylimitmb = 4096

[network]
forceencryption = 0
ipaddress = 10.192.0.0
kerberoskeytabfile = /var/opt/mssql/secrets/mssql.keytab
tcpport = 1401
tlscert = /etc/ssl/certs/mssql.pem
tlsciphers = ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES128-SHA256:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES128-SHA256:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA:ECDHE-RSA-AES128-SHA:AES256-GCM-SHA384:AES128-GCM-SHA256:AES256-SHA256:AES128-SHA256:AES256-SHA:AES128-SHA
tlskey = /etc/ssl/private/mssql.key
tlsprotocols = 1.2,1.1,1.0

[sqlagent]
databasemailprofile = default
errorlogfile = /var/opt/mssql/log/sqlagentlog.log
errorlogginglevel = 7

[telemetry]
customerfeedback = true
userrequestedlocalauditdirectory = /tmp/audit

[traceflag]
traceflag0 = 1204
traceflag1 = 2345
traceflag = 3456
```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

```ini
[EULA]
accepteula = Y
accepteulaml = Y

[coredump]
captureminiandfull = true
coredumptype = full

[distributedtransaction]
servertcpport = 51999

[filelocation]
defaultbackupdir = /var/opt/mssql/data/
defaultdatadir = /var/opt/mssql/data/
defaultdumpdir = /var/opt/mssql/data/
defaultlogdir = /var/opt/mssql/data/

[hadr]
hadrenabled = 0

[language]
lcid = 1033

[memory]
memorylimitmb = 4096

[network]
forceencryption = 0
ipaddress = 10.192.0.0
kerberoskeytabfile = /var/opt/mssql/secrets/mssql.keytab
rpcport = 13500
tcpport = 1401
tlscert = /etc/ssl/certs/mssql.pem
tlsciphers = ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES128-SHA256:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES128-SHA256:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA:ECDHE-RSA-AES128-SHA:AES256-GCM-SHA384:AES128-GCM-SHA256:AES256-SHA256:AES128-SHA256:AES256-SHA:AES128-SHA
tlskey = /etc/ssl/private/mssql.key
tlsprotocols = 1.2,1.1,1.0

[sqlagent]
databasemailprofile = default
errorlogfile = /var/opt/mssql/log/sqlagentlog.log
errorlogginglevel = 7

[telemetry]
customerfeedback = true
userrequestedlocalauditdirectory = /tmp/audit

[traceflag]
traceflag0 = 1204
traceflag1 = 2345
traceflag = 3456
```

::: moniker-end

## <a name="next-steps"></a>后续步骤

若要改为使用环境变量使一些这些配置更改，请参阅[使用环境变量配置 SQL Server 设置](sql-server-linux-configure-environment-variables.md)。

有关其他管理工具和方案，请参阅[管理 Linux 上的 SQL Server](sql-server-linux-management-overview.md)。
