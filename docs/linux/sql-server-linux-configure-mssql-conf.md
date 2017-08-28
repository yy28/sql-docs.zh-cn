---
title: "在 Linux 上配置 SQL Server 设置 |Microsoft 文档"
description: "本主题介绍如何使用 mssql conf 工具在 Linux 上配置 SQL Server 2017 设置。"
author: luisbosquez
ms.author: lbosq
manager: jhubbard
ms.date: 08/24/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 06798dff-65c7-43e0-9ab3-ffb23374b322
ms.translationtype: MT
ms.sourcegitcommit: 21f0cfd102a6fcc44dfc9151750f1b3c936aa053
ms.openlocfilehash: 894a3756d9bffcaaf3347e0bfae92abb0f846a97
ms.contentlocale: zh-cn
ms.lasthandoff: 08/28/2017

---
# <a name="configure-sql-server-on-linux-with-the-mssql-conf-tool"></a>使用 mssql-conf 工具配置 Linux 上的 SQL Server

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

**mssql conf**是将与 SQL Server 自 2017 年 1 RC2 为 Red Hat Enterprise Linux、 SUSE Linux 企业服务器和 Ubuntu 安装的配置脚本。 可以使用此实用工具设置以下参数：

|||
|---|---|
| [排序规则](#collation) | 在 Linux 上，为 SQL Server 设置新的排序规则。 |
| [客户反馈](#customerfeedback) | 选择 SQL Server 向 Microsoft 发送反馈。 |
| [默认数据目录](#datadir) | 更改新的 SQL Server 数据库数据文件 (.mdf) 的默认目录。 |
| [默认日志目录](#datadir) | 更改新的 SQL Server 数据库日志 (.ldf) 文件的默认目录。 |
| [默认转储目录](#dumpdir) | 更改新内存转储和其他故障排除的文件的默认目录。 |
| [默认备份目录](#backupdir) | 更改新的备份文件的默认目录。 |
| [转储类型](#coredump) | 选择要收集的转储内存转储文件的类型。 |
| [高可用性](#hadr) | 启用可用性组。 |
| [本地审核目录](#localaudit) | 设置要添加本地审核文件的目录。 |
| [区域设置](#lcid) | 设置 SQL Server 以使用的区域设置。 |
| [内存限制](#memorylimit) | 设置 SQL Server 的内存限制。 |
| [TCP 端口](#tcpport) | 更改 SQL Server 侦听的连接的端口。 |
| [TLS](#tls) | 配置传输级安全。 |
| [跟踪标志](#traceflags) | 设置服务要使用这些跟踪标志。 |

> [!TIP]
> 其中某些设置还可以使用环境变量配置。 有关详细信息，请参阅[与环境变量配置 SQL Server 设置](sql-server-linux-configure-environment-variables.md)。

## <a name="usage-tips"></a>使用提示

* 有关 Alwayson 可用性组和共享的磁盘群集，始终在每个节点上进行相同的配置更改。

* 对于共享的磁盘群集方案，请不要尝试重新启动**mssql server**服务以应用更改。 SQL Server 正在运行为应用程序。 相反，使资源脱机再然后恢复联机。

* 运行 mssql-conf 通过这些示例指定完整路径： **/opt/mssql/bin/mssql-conf**。 如果你选择请改为导航到该路径，在当前目录的上下文中运行 mssql conf: **。 / mssql conf**。

## <a id="collation"></a>更改 SQL Server 排序规则

**集排序规则**选项的排序规则值更改为任何支持的排序规则：

1. 运行**集排序规则**选项并按照提示进行操作：

   ```bash
   sudo /opt/mssql/bin/mssql-conf set-collation
   ```

1. mssql-conf 实用工具将尝试使用指定的排序规则还原数据库并重新启动服务。 如果不存在任何错误，它将回滚排序规则到以前的值。

支持的排序列表，请运行[sys.fn_helpcollations](../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md)函数： `SELECT Name from sys.fn_helpcollations()`。

## <a id="customerfeedback"></a>配置客户反馈

**Telemetry.customerfeedback**是否 SQL Server 向 Microsoft 发送反馈，或不设置更改。 默认情况下，此值设置为**true**。 若要更改的值，请运行以下命令：

1. Mssql conf 脚本作为根与运行**设置**命令**telemetry.customerfeedback**。 下面的示例通过指定关闭客户反馈**false**。

   ```bash
   sudo /opt/mssql/bin/mssql-conf set telemetry.customerfeedback false
   ```

1. 重新启动 SQL Server 服务：

   ```bash
   sudo systemctl restart mssql-server
   ```

有关详细信息，请参阅[在 Linux 上的 SQL Server 的客户反馈](sql-server-linux-customer-feedback.md)。

## <a id="datadir"></a>默认数据或日志目录位置更改

**Filelocation.defaultdatadir**和**filelocation.defaultlogdir**设置更改其中创建新的数据库和日志文件的位置。 默认情况下，此位置为 /var/opt/mssql/data。 若要更改这些设置，请使用以下步骤：

1. 创建新数据库的目标目录数据和日志文件。 下面的示例创建一个新**/tmp/数据**目录：

   ```bash
   sudo mkdir /tmp/data
   ```

1. 更改所有者和到的目录组**mssql**用户：

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

1. 此命令还假定/tmp/日志目录存在，并且它位于用户和组**mssql**。

## <a id="dumpdir"></a>更改默认转储目录位置

**Filelocation.defaultdumpdir**设置的内存和 SQL 转储生成崩溃时的默认位置的更改。 默认情况下，这些文件在 /var/opt/mssql/log 中生成。

若要设置此新位置，请使用以下命令：

1. 创建新的转储文件的目标目录。 下面的示例创建一个新**/tmp/转储**目录：

   ```bash
   sudo mkdir /tmp/dump
   ```

1. 更改所有者和到的目录组**mssql**用户：

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

## <a id="backupdir"></a>更改默认备份目录位置

**Filelocation.defaultbackupdir**设置中生成的备份文件的默认位置的更改。 默认情况下，这些文件在 /var/opt/mssql/data 中生成。

若要设置此新位置，请使用以下命令：

1. 创建新的备份文件的目标目录。 下面的示例创建一个新**/tmp/备份**目录：

   ```bash
   sudo mkdir /tmp/backup
   ```

1. 更改所有者和到的目录组**mssql**用户：

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

## <a id="coredump"></a>指定核心转储设置

如果一个 SQL Server 进程中发生异常，SQL Server 会创建内存转储。

有两个选项的 SQL Server 收集控制的一种内存转储： **coredump.coredumptype**和**coredump.captureminiandfull**。 这两个选项与核心转储捕获的两个阶段相关。 

第一个阶段捕获受**coredump.coredumptype**设置，确定在异常过程中生成的转储文件的类型。 第二个阶段时，启用选项**coredump.captureminiandfull**设置。 如果**coredump.captureminiandfull**设置为 true，转储文件指定**coredump.coredumptype**生成，并且还生成第二个的小型转储。 设置**coredump.captureminiandfull**为 false 则禁止尝试第二个捕获。

1. 决定是否要捕获与微型和完整转储**coredump.captureminiandfull**设置。

    ```bash
    sudo /opt/mssql/bin/mssql-conf set coredump.captureminiandfull <true or false>
    ```

    默认值： **false**

1. 指定的转储文件的类型**coredump.coredumptype**设置。

    ```bash
    sudo /opt/mssql/bin/mssql-conf set coredump.coredumptype <dump_type>
    ```

    默认值： **miniplus**

    下表列出可能**coredump.coredumptype**值。

    | 类型 | Description |
    |-----|-----|
    | **迷你** | mini 是最小的转储文件类型。 它使用 Linux 系统信息确定进程中的线程和模块。 转储仅包含主机环境线程堆栈和模块。 不包含间接内存引用或全局变量。 |
    | **miniplus** | MiniPlus 与 mini 相似，但它包括更多内存。 它理解 SQLPAL 和主机环境中，将以下的内存区域添加到转储的内部结构：</br></br> -各种全局函数</br> 的所有内存超过 64 TB</br> -All 名为区域中找到**/proc/$ pid/映射**</br> 双向从线程和堆栈的间接内存</br> 线程信息</br> -关联 Teb 的和 Peb 的</br> 模块信息</br> VMM 和 VAD 树 |
    | **筛选** | filtered 采用基于减法的设计，包括进程中的所有内存，除非专门排除某些内存。 此设计理解 SQLPAL 的内部机制和宿主环境，从转储中排除某些区域。
    | **完整** | 完整的整个过程转储中包括所有区域位于**/proc/$ pid/映射**。 这不受**coredump.captureminiandfull**设置。 |

## <a id="hadr"></a>高可用性

**Hadr.hadrenabled**选项使您的 SQL Server 实例上的可用性组。 以下命令通过设置可使可用性组**hadr.hadrenabled**为 1。 必须重启 SQL Server，该设置才能生效。

```bash
sudo /opt/mssql/bin/mssql-conf set hadr.hadrenabled  1
sudo systemctl restart mssql-server
```

有关如何将此项用于可用性组的信息，请参阅以下两个主题。

- [配置 Always On 可用性组在 Linux 上的 SQL server](sql-server-linux-availability-group-configure-ha.md)
- [在 Linux 上的 SQL Server 配置读取缩放可用性组](sql-server-linux-availability-group-configure-rs.md)

## <a id="localaudit"></a>设置本地审核目录

**Telemetry.userrequestedlocalauditdirectory**设置启用本地审核和创建的允许你设置目录，其中本地的审核日志。

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

有关详细信息，请参阅[在 Linux 上的 SQL Server 的客户反馈](sql-server-linux-customer-feedback.md)。

## <a id="lcid"></a>更改 SQL Server 区域设置

**Language.lcid**将更改的 SQL Server 区域设置设置为任何受支持的语言标识符 (LCID)。 

1. 下面的示例更改为法语的区域设置 (1036):

   ```bash
   sudo /opt/mssql/bin/mssql-conf set language.lcid 1036
   ```

1. 重新启动 SQL Server 服务以应用所做的更改：

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a id="memorylimit"></a>设置内存限制

**Memory.memorylimitmb**将控件设置为 SQL Server 的物理内存量 （以 mb 为单位） 可用。 默认值为 80%的物理内存。

1. Mssql conf 脚本作为根与运行**设置**命令**memory.memorylimitmb**。 下面的示例更改为 SQL Server 到 3.25 GB (3328 MB) 的可用内存。

   ```bash
   sudo /opt/mssql/bin/mssql-conf set memory.memorylimitmb 3328
   ```

1. 重新启动 SQL Server 服务以应用所做的更改：

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a id="tcpport"></a>更改 TCP 端口

**Network.tcpport**设置 SQL Server 侦听的连接的 TCP 端口的更改。 默认情况下，此端口设置为 1433。 若要更改端口，请运行以下命令：

1. 使用“network.tcpport”的“set”命令以根用户身份运行 mssql-conf 脚本：

   ```bash
   sudo /opt/mssql/bin/mssql-conf set network.tcpport <new_tcp_port>
   ```

1. 重新启动 SQL Server 服务：

   ```bash
   sudo systemctl restart mssql-server
   ```

1. 现在连接到 SQL Server，你必须指定自定义端口逗号 （，） 后的主机名或 IP 地址。 例如，要使用 SQLCMD 进行连接，则需使用以下命令：

   ```bash
   sqlcmd -S localhost,<new_tcp_port> -U test -P test
   ```

## <a id="tls"></a>指定 TLS 设置

以下选项在 Linux 上运行的 SQL Server 实例配置 TLS。

|选项 |Description |
|--- |--- |
|**network.forceencryption** |如果为 1，然后[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]强制所有连接进行加密。 默认情况下，此选项为 0。 |
|**network.tlscert** |证书的绝对路径文件[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]用于 TLS。 示例：`/etc/ssl/certs/mssql.pem`证书文件必须是可由 mssql 帐户访问。 Microsoft 建议限制访问文件使用`chown mssql:mssql <file>; chmod 400 <file>`。 |
|**network.tlskey** |私钥的绝对路径文件[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]用于 TLS。 示例：`/etc/ssl/private/mssql.key`证书文件必须是可由 mssql 帐户访问。 Microsoft 建议限制访问文件使用`chown mssql:mssql <file>; chmod 400 <file>`。 |
|**network.tlsprotocols** |哪些 TLS 协议都允许 SQL Server 的逗号分隔的列表。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]始终尝试协商允许的最高协议。 如果客户端不支持任何允许的协议，[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]拒绝连接尝试。  为了实现兼容，默认情况下，（1.2、 1.1、 1.0） 允许所有支持的协议。  如果你的客户端支持 TLS 1.2，Microsoft 建议允许仅 TLS 1.2。 |
|**network.tlsciphers** |指定允许哪些密码[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]tls。 此字符串的格式必须设置每个[OpenSSL 的密码的列表格式](https://www.openssl.org/docs/man1.0.2/apps/ciphers.html)。 一般情况下，你应该不需要更改此选项。 <br /> 默认情况下，允许以下密码： <br /> `ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES128-SHA256:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES128-SHA256:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA:ECDHE-RSA-AES128-SHA:AES256-GCM-SHA384:AES128-GCM-SHA256:AES256-SHA256:AES128-SHA256:AES256-SHA:AES128-SHA` |
| **network.kerberoskeytabfile** |Kerberos keytab 文件路径 |

使用 TLS 设置的示例，请参阅[Encrypting connections to Linux 上的 SQL Server 连接](sql-server-linux-encrypted-connections.md)。

## <a id="traceflags"></a>启用/禁用跟踪标志

这**跟踪标志**选项启用或禁用跟踪标志为 SQL Server 服务启动。 若要启用/禁用跟踪标志，请使用以下命令：

1. 启用跟踪标志，使用以下命令。 例如，对于跟踪标志 1234：

   ```bash
   sudo /opt/mssql/bin/mssql-conf traceflag 1234 on
   ```

1. 可以通过单独指定跟踪标志来启用多个跟踪标志：

   ```bash
   sudo /opt/mssql/bin/mssql-conf traceflag 2345 3456 on
   ```

1. 在类似的方式，您可以通过指定它们并添加禁用一个或多个启用的跟踪标志**关闭**参数：

   ```bash
   sudo /opt/mssql/bin/mssql-conf traceflag 1234 2345 3456 off
   ```

1. 重新启动 SQL Server 服务以应用所做的更改：

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a name="remove-a-setting"></a>删除该设置

使用的任何设置进行以取消设置`mssql-conf set`，调用**mssql conf**与`unset`选项和设置的名称。 这将清除该设置，有效地将其返回到其默认值。

1. 下面的示例清除**network.tcpport**选项。

   ```bash
   sudo /opt/mssql/bin/mssql-conf unset network.tcpport
   ```

1. 重新启动 SQL Server 服务。

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a name="view-current-settings"></a>查看当前设置

若要查看任何配置设置，请运行以下命令以输出的内容**mssql.conf**文件：

```bash
sudo cat /var/opt/mssql/mssql.conf
```

请注意，未在此文件中显示的所有设置均使用其默认值。 下一节提供一个示例**mssql.conf**文件。

## <a name="mssqlconf-format"></a>mssql.conf 格式

以下**/var/opt/mssql/mssql.conf**文件提供了为每个设置的一个示例。 可以使用此格式可以手动更改到**mssql.conf**文件根据需要。 如果你手动更改此文件，必须重新启动 SQL Server，才能将应用所做的更改。 若要使用**mssql.conf**文件使用 Docker，你必须具有 Docker[保存数据](sql-server-linux-configure-docker.md)。 第一次添加整个**mssql.conf**到你的主机目录文件，然后运行容器。 没有在此示例[客户反馈](sql-server-linux-customer-feedback.md)。

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

## <a name="next-steps"></a>后续步骤

若要改为使用环境变量使这些配置更改的某些项目，请参阅[与环境变量配置 SQL Server 设置](sql-server-linux-configure-environment-variables.md)。

其他管理工具和方案，请参阅[管理在 Linux 上的 SQL Server](sql-server-linux-management-overview.md)。

