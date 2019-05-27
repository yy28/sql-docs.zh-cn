---
title: 在 Linux 上安装 SQL Server 语言扩展 (Java) |Microsoft Docs
description: 了解如何安装 SQL Server 语言扩展 (Java) 在 Red Hat、 Ubuntu 和 SUSE。
author: dphansen
ms.author: davidph
manager: cgronlun
ms.date: 05/22/2019
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: language-extensions
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: b694cde8784a1607c85ed9ab7dfcc4d770a6d938
ms.sourcegitcommit: 3b266dc0fdf1431fdca6b2ad34ae5fd38abe9f69
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/24/2019
ms.locfileid: "66186804"
---
# <a name="install-sql-server-2019-language-extensions-java-on-linux"></a>在 Linux 上安装 SQL Server 2019 语言扩展 (Java)

语言扩展是到数据库引擎外的接程序。 尽管你可以[同时安装数据库引擎和语言扩展](#install-all)，它是安装和配置 SQL Server 数据库引擎第一次，以便可以添加更多的组件之前解决任何问题的最佳做法。 

按照这篇文章来安装 Java 语言扩展中的步骤。

Java 扩展包位置是在 SQL Server Linux 源存储库中。 如果你已配置的数据库引擎安装源代码存储库，则可以运行**mssql server 扩展性 java**包使用相同的存储库注册的安装命令。

Linux 容器还支持语言扩展。 包含语言扩展，我们不会提供预建的容器，但您可以创建一个从使用 SQL Server 容器[可在 GitHub 上的示例模板](https://github.com/Microsoft/mssql-docker/tree/master/linux/preview/examples/mssql-mlservices)。

## <a name="uninstall-previous-ctp"></a>卸载以前的 CTP

在过去几个 CTP 版本中，从而导致较少的包已更改的包列表。 我们建议卸载 CTP 2.x 安装 CTP 3.0 之前删除所有以前的包。 不支持通过并行安装多个版本。

### <a name="1-confirm-package-installation"></a>1.确认包安装

你可能想要检查存在以前安装的第一步。 以下文件针对的是现有的安装： checkinstallextensibility.sh、 exthost、 快速启动板。

```bash
ls /opt/microsoft/mssql/bin
```

### <a name="2-uninstall-previous-ctp-2x-packages"></a>2.卸载以前的 CTP 2.x 包

卸载包最低级别。 会自动卸载依赖于较低级别程序包任何上游包。

  + 对于 Java 集成删除**mssql server 扩展性 java**

有关删除包的命令也显示在下表中。

| 平台  | 包删除命令 | 
|-----------|----------------------------|
| RHEL  | `sudo yum remove msssql-server-extensibility-java` |
| SLES  | `sudo zypper remove msssql-server-extensibility-java` |
| Ubuntu    | `sudo apt-get remove msssql-server-extensibility-java`|

### <a name="3-proceed-with-ctp-30-install"></a>3.继续 CTP 3.0 安装

安装的最高级别包为操作系统在本文中使用的说明。

为每个特定于操作系统的集的安装说明*最高的包级别*可以是**示例 1-完整安装**一系列完整的包，或**示例 2-最小安装**的最小的可行安装所需的包的数字。

1. 运行安装命令使用的 Linux 分发版的程序包管理器和语法： 

   + [RedHat](#RHEL)
   + [Ubuntu](#ubuntu)
   + [SUSE](#suse)

## <a name="prerequisites"></a>先决条件

+ Linux 版本必须是[SQL Server 支持的](sql-server-linux-release-notes-2019.md#supported-platforms)，但不包括 Docker 引擎。 支持的版本包括：

   + [Red Hat Enterprise Linux (RHEL)](quickstart-install-connect-red-hat.md)

   + [SUSE Enterprise Linux Server](quickstart-install-connect-suse.md)

   + [Ubuntu](quickstart-install-connect-ubuntu.md)

+ 应具有用于运行 T-SQL 命令的工具。 查询编辑器是必需的安装后配置和验证。 我们建议[Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/download?view=sql-server-2017#get-azure-data-studio-for-linux)，在 Linux 运行的免费下载。

## <a name="package-list"></a>包列表

在与 internet 连接的设备，包下载并安装独立于数据库引擎的每个操作系统使用包安装程序。 下表描述了所有可用的包。

| 包名称 | Applies-to | Description |
|--------------|----------|-------------|
|mssql-server-extensibility  | 所有语言 | 用于运行 Java 代码的可扩展性框架。 |
|mssql-server-extensibility-java | Java | 用于加载的 Java 执行环境的 Java 扩展。 没有任何其他库或用于 Java 的包。 |

<a name="RHEL"></a>

## <a name="install-language-extensions"></a>安装语言扩展

你可以安装的语言扩展和 Java 在 Linux 上安装**mssql server 扩展性 java**。 当你安装**mssql server 扩展性 java**，如果尚未安装包将自动安装 JRE 8。 它还将添加到名为 JRE_HOME 环境变量的 JVM 路径。

> [!Note]
> 在连接 internet 的服务器上，包依赖项下载和安装作为主包安装的一部分。 如果你的服务器未连接到 internet，请参阅中的更多详细信息[脱机安装程序](#offline-install)。

### <a name="redhat-install-command"></a>RedHat 安装命令

可以在使用以下命令的 RedHat 上安装适用于 Java 的语言扩展。

> [!Tip]
> 如果可能，运行`yum clean all`刷新之前安装系统上的包。

```bash
# Install as root or sudo
sudo yum install mssql-server-extensibility-java
```

<a name="ubuntu"></a>

### <a name="ubuntu-install-command"></a>Ubuntu 安装命令

可以使用以下命令在 Ubuntu 上安装适用于 Java 的语言扩展。

> [!Tip]
> 如果可能，运行`apt-get update`刷新之前安装系统上的包。 此外，Ubuntu 某些 docker 映像可能没有 https apt 传输选项。 若要安装它，请使用`apt-get install apt-transport-https`。

```bash
# Install as root or sudo
sudo apt-get install mssql-server-extensibility-java
```

<a name="suse"></a>

### <a name="suse-install-command"></a>SUSE 安装命令

可以使用以下命令的 SUSE 上安装适用于 Java 的语言扩展。

```bash
# Install as root or sudo
sudo zypper install mssql-server-extensibility-java
```

## <a name="post-install-config-required"></a>安装后配置 （必需）

1. Linux 上的授予权限

    不需要执行此步骤中，如果您使用的外部库。 工作的推荐的方法使用外部库。 从 jar 文件创建外部库的帮助，请参阅[创建外部库](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql)

    如果不使用外部库，您需要向 SQL Server 提供有权在 jar 中执行的 Java 类。

    若要授予读取和执行到 jar 文件的访问权限，请运行以下**chmod**命令上的 jar 文件。 我们建议始终将类文件放在一个 jar，当您使用 SQL Server 时。 创建一个 jar 的帮助，请参阅[如何创建一个 jar 文件](https://docs.microsoft.com/sql/language-extensions/how-to/create-a-java-jar-file-from-class-files)。

    ```cmd
    chmod ug+rx <MyJarFile.jar>
    ```

    此外需要为要读取/执行的 jar 文件提供 mssql_satellite 权限。

    ```cmd
    chown mssql_satellite:mssql_satellite <MyJarFile.jar>
    ```

    其他配置是主要通过[mssql-conf 工具](sql-server-linux-configure-mssql-conf.md)。

2. 添加用于运行 SQL Server 服务 mssql 用户帐户。 如果还没有以前运行安装程序，这是必需的。

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

3. 启用出站网络访问。 默认情况下，出站网络访问处于禁用状态。 若要启用出站请求，请使用 mssql-conf 工具的布尔属性设置"outboundnetworkaccess"。 有关详细信息，请参阅[在 Linux 上使用 mssql conf 配置 SQL Server](sql-server-linux-configure-mssql-conf.md#mlservices-outbound-access)。

   ```bash
   # Run as SUDO or root
   # Enable outbound requests over the network
   sudo /opt/mssql/bin/mssql-conf set extensibility outboundnetworkaccess 1
   ```

4. 重新启动 SQL Server Launchpad 服务和数据库引擎实例读取 INI 文件的更新的值。 重新启动消息提醒您在每当修改扩展性相关的设置。  

   ```bash
   systemctl restart mssql-launchpadd

   systemctl restart mssql-server.service
   ```

5. 启用外部脚本执行，使用 Azure Data Studio 或 SQL Server Management Studio (仅 Windows) 等其他工具运行 Transact SQL。

   ```bash
   EXEC sp_configure 'external scripts enabled', 1
   RECONFIGURE WITH OVERRIDE
   ```

6. 重新启动`mssql-launchpadd`再次服务。

7. 对于想要使用中的语言扩展每个数据库，你需要注册的外部语言[创建的外部语言](https://docs.microsoft.com/sql/t-sql/statements/create-external-language-transact-sql)。

## <a name="verify-installation"></a>验证安装

Java 功能集成不包括库，但你可以运行`grep -r JRE_HOME /etc`以确认创建 JAVA_HOME 环境变量。

若要验证安装，请运行 T-SQL 脚本执行系统存储过程调用 Java。 此任务需要查询工具。 Azure Data Studio 是一个不错的选择。 其他常用工具如 SQL Server Management Studio 或 PowerShell 也仅限 Windows 的。 如果必须使用这些工具的 Windows 计算机，使用它连接到数据库引擎的 Linux 安装。

<a name="install-all"></a>

## <a name="full-install-of-sql-server-and-language-extensions"></a>完整安装的 SQL Server 和语言扩展

可以安装和配置数据库引擎和语言扩展，一个过程中，通过附加的 Java 包和上安装数据库引擎的命令的参数。

1. 提供的命令行，包含数据库引擎和语言扩展功能。

  您可以添加到数据库引擎的可扩展性安装的 Java。

  ```bash
  sudo yum install -y mssql-server mssql-server-extensibility-java 
  ```

3. 接受许可协议并完成安装后配置。 使用**mssql conf**此任务的工具。

  ```bash
  sudo /opt/mssql/bin/mssql-conf setup
  ```

  系统将提示您接受数据库引擎的许可协议，选择版本，以及设置管理员密码。 

4. 如果系统提示你执行此操作，重新启动该服务。

  ```bash
  sudo systemctl restart mssql-server.service
  ```

## <a name="unattended-installation"></a>无人参与的安装

使用[无人参与的安装](https://docs.microsoft.com/sql/linux/sql-server-linux-setup#unattended)数据库引擎中，将添加为 mssql server 扩展性 java 包。

<a name="offline-install"></a>


## <a name="offline-installation"></a>脱机安装

请按照[脱机安装](sql-server-linux-setup.md#offline)步骤包的安装说明进行操作。 查找您的下载站点，然后下载特定包使用以下包列表。

> [!Tip]
> 多个包管理工具提供可帮助你的命令确定包的依赖项。 对于 yum，使用`sudo yum deplist [package]`。 对于 Ubuntu，请使用`sudo apt-get install --reinstall --download-only [package name]`跟`dpkg -I [package name].deb`。

#### <a name="download-site"></a>下载站点

您可以从程序包下载[ https://packages.microsoft.com/ ](https://packages.microsoft.com/)。 所有适用于 Java 的包都是与数据库引擎包共置。 

#### <a name="redhat7-paths"></a>RedHat/7 路径

|||
|--|----|
| mssql/可扩展性的 java 包 | [https://packages.microsoft.com/rhel/7/mssql-server-preview/](https://packages.microsoft.com/rhel/7/mssql-server-preview/) |

#### <a name="ubuntu1604-paths"></a>Ubuntu/16.04 路径

|||
|--|----|
| mssql/可扩展性的 java 包 | [https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/) |

#### <a name="suse12-paths"></a>SUSE/12 路径

|||
|--|----|
| mssql/可扩展性的 java 包 | [https://packages.microsoft.com/sles/12/mssql-server-preview/](https://packages.microsoft.com/sles/12/mssql-server-preview/) |

#### <a name="package-list"></a>包列表

具体取决于哪些扩展，你想要使用，请下载所需的特定语言包。 确切的文件名中使用后缀，包括平台的信息，但以下文件名称应足够接近，从而确定要获取的文件。

```
# Core packages 
mssql-server-15.0.1000
mssql-server-extensibility-15.0.1000

# Java
mssql-server-extensibility-java-15.0.1000
```

## <a name="limitations-in-ctp-releases"></a>在 CTP 版本中的限制

Linux 上的语言扩展和 Java 可扩展性是仍处于积极开发阶段。 以下功能尚未启用的预览版本中。

+ 隐式身份验证目前不可以在 Linux 上在此时，这意味着不能从正在 Java 来访问数据或其他资源连接到服务器。


### <a name="resource-governance"></a>资源调控

没有 Linux 和 Windows 的之间的奇偶校验[资源调控](../t-sql/statements/create-external-resource-pool-transact-sql.md)外部资源池，但的统计信息[sys.dm_resource_governor_external_resource_pools](../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pools.md)当前具有Linux 上的不同单位。 在将来的 ctp 版本中将对齐单元。
 
| 列名   | Description | Linux 上的值 | 
|---------------|--------------|---------------|
|peak_memory_kb | 最大资源池使用的内存量。 | 在 Linux 上，此统计信息来源于 CGroups 内存子系统，其中的值是 memory.max_usage_in_bytes |
|write_io_count | 写入自重置资源调控器统计信息以来发出的 Io 总数。 | 在 Linux 上，此统计信息来源于其中的值写入行是 blkio.throttle.io_serviced 的 CGroups blkio 子系统 | 
|read_io_count | 读取自重置资源调控器统计信息以来发出的 Io 总数。 | 在 Linux 上，此统计信息来源于 CGroups blkio 子系统，其中读取的行的值是 blkio.throttle.io_serviced | 
|total_cpu_kernel_ms | 累计 CPU 用户内核时间以毫秒为单位由于自重置资源调控器统计信息。 | 在 Linux 上，此统计信息来源于 CGroups cpuacct 子系统，其中用户行上的值是 cpuacct.stat |  
|total_cpu_user_ms | 以毫秒为单位自重置资源调控器统计信息以来累积 CPU 用户时间。| 在 Linux 上，此统计信息来源于 CGroups cpuacct 子系统，其中系统行值的值是 cpuacct.stat | 
|active_processes_count | 在请求的时间点运行的外部进程数。| 在 Linux 上，此统计信息来源于其中的值是 pids.current GGroups pid 子系统 | 

## <a name="next-steps"></a>后续步骤

Java 开发人员可以开始使用一些简单的示例，并学习与 SQL Server 的 Java 工作原理的基础知识。 下一步，请参阅以下链接：

+ [教程：与 Java 配合使用的正则表达式](../language-extensions/tutorials/search-for-string-using-regular-expressions-in-java.md)