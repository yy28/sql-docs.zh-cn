---
title: 在 Linux 上安装 SQL Server 语言扩展 (Java)
description: 了解如何在 Red Hat、Ubuntu 和 SUSE 上安装 SQL Server 语言扩展 (Java)。
author: dphansen
ms.author: davidph
ms.reviewer: vanto
manager: cgronlun
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: language-extensions
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 3e86da652231a06cd28318096ada3ae3aed7526e
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/04/2019
ms.locfileid: "73531233"
---
# <a name="install-sql-server-2019-language-extensions-java-on-linux"></a>在 Linux 上安装 SQL Server 2019 语言扩展 (Java)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

语言扩展是数据库引擎的附加产品。 尽管可以[同时安装数据库引擎和语言扩展](#install-all)，但最好先安装并配置 SQL Server 数据库引擎，以便在添加更多组件之前解决所有问题。 

按照本文中的步骤安装 Java 语言扩展。

Java 扩展包位于 SQL Server Linux 源存储库中。 如果已为数据库引擎安装配置了源存储库，则可以使用相同的存储库注册运行 **mssql-server-extensibility-java** 包安装命令。

Linux 容器也支持语言扩展。 我们不提供带有语言扩展的预生成容器，但你可以使用 [GitHub 中提供的示例模板](https://github.com/Microsoft/mssql-docker/tree/master/linux/preview/examples/mssql-mlservices)通过 SQL Server 容器创建一个。

默认情况下，语言扩展和[机器学习服务](../advanced-analytics/index.yml)安装在 SQL Server 大数据群集上。 如果使用大数据群集，则无需按照本文中的步骤进行操作。 有关详细信息，请参阅[在大数据群集上使用机器学习服务（Python 和 R）](../big-data-cluster/machine-learning-services.md)。

## <a name="uninstall-preview-version"></a>卸载预览版

如果安装了预览版本（社区技术预览版 (CTP) 或候选发布 (RC)），建议先卸载此版本以删除以前的所有包，然后再安装 SQL Server 2019。 不支持并行安装多个版本，并且包列表在最后几个预览版 (CTP/RC) 中进行了更改。

### <a name="1-confirm-package-installation"></a>1.确认包安装

首先可能需要检查是否存在以前的安装。 以下文件指示现有安装：checkinstallextensibility.sh、exthost、launchpad。

```bash
ls /opt/microsoft/mssql/bin
```

### <a name="2-uninstall-previous-ctprc-packages"></a>2.卸载以前的 CTP/RC 包

在最低包级别进行卸载。 依赖于较低级别包的所有上游包都会自动卸载。

  + 对于 Java 集成，删除 **mssql-server-extensibility-java**

下表显示了用于删除包的命令。

| 平台  | 包删除命令 | 
|-----------|----------------------------|
| RHEL  | `sudo yum remove msssql-server-extensibility-java` |
| SLES  | `sudo zypper remove msssql-server-extensibility-java` |
| Ubuntu    | `sudo apt-get remove msssql-server-extensibility-java`|

### <a name="3-install-sql-server-2019"></a>3.安装 SQL Server 2019

使用本文中针对操作系统的说明在最高包级别进行安装。

对于每组特定于操作系统的安装说明，*最高包级别*为**示例 1 - 完全安装**（一组完整的包）或**示例 2 - 最小安装**（可行安装所需的最少包数）。

1. 使用 Linux 分发版的包管理器和语法运行安装命令： 

   + [RedHat](#RHEL)
   + [Ubuntu](#ubuntu)
   + [SUSE](#suse)

## <a name="prerequisites"></a>必备条件

+ Linux 版本必须[受 SQL Server 支持](sql-server-linux-release-notes-2019.md#supported-platforms)，但不包括 Docker 引擎。 受支持的版本包括：

   + [Red Hat Enterprise Linux (RHEL)](quickstart-install-connect-red-hat.md)

   + [SUSE Enterprise Linux Server](quickstart-install-connect-suse.md)

   + [Ubuntu](quickstart-install-connect-ubuntu.md)

+ 应安装用于运行 T-SQL 命令的工具。 需要使用查询编辑器进行安装后配置和验证。 我们建议使用 [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/download?view=sql-server-2017#get-azure-data-studio-for-linux)，它是在 Linux 上运行的免费下载。

## <a name="package-list"></a>包列表

在已连接 Internet 的设备上，将使用针对每个操作系统的包安装程序独立于数据库引擎下载和安装相应的包。 下表列出了所有可用的包。

| 包名称 | 适用对象 | 描述 |
|--------------|----------|-------------|
|mssql-server-extensibility  | 所有语言 | 用于 Java 语言扩展的扩展性框架 |
|mssql-server-extensibility-java | Java | 用于 Java 语言扩展的扩展性框架，包括支持的 Java 运行时 |

<a name="RHEL"></a>

## <a name="install-language-extensions"></a>安装语言扩展

可通过安装 **mssql-server-extensibility-java** 在 Linux 上安装语言扩展和 Java。 当你安装 mssql-server-extensibility-java  时，包会自动安装 JRE 11（如果尚未安装的话）。 它还会将 JVM 路径添加到名为 JRE_HOME 的环境变量中。

> [!Note]
> 在已连接 Internet 的服务器上，将在主包安装过程中下载并安装包依赖项。 如果服务器未连接到 Internet，请参阅[脱机设置](#offline-install)了解更多详细信息。

### <a name="redhat-install-command"></a>RedHat 安装命令

可使用以下命令在 RedHat 上安装适用于 Java 的语言扩展。

> [!Tip]
> 如果可以，请在安装之前运行 `yum clean all` 以刷新系统中的包。

```bash
# Install as root or sudo
sudo yum install mssql-server-extensibility-java
```

<a name="ubuntu"></a>

### <a name="ubuntu-install-command"></a>Ubuntu 安装命令

可使用以下命令在 Ubuntu 上安装适用于 Java 的语言扩展。

> [!Tip]
> 如果可以，请在安装之前运行 `apt-get update` 以刷新系统中的包。 此外，Ubuntu 的一些 docker 映像可能没有 https apt 传输选项。 若要进行安装，请使用 `apt-get install apt-transport-https`。

```bash
# Install as root or sudo
sudo apt-get install mssql-server-extensibility-java
```

<a name="suse"></a>

### <a name="suse-install-command"></a>SUSE 安装命令

可使用以下命令在 SUSE 上安装适用于 Java 的语言扩展。

```bash
# Install as root or sudo
sudo zypper install mssql-server-extensibility-java
```

## <a name="post-install-config-required"></a>安装后配置（必需）

1. 授予对 Linux 的权限

    如果使用外部库，则无需执行此步骤。 建议的工作方式为使用外部库。 有关通过 jar 文件创建外部库的帮助，请参阅 [CREATE EXTERNAL LIBRARY](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql)

    如果不使用外部库，则需要为 SQL Server 提供在 jar 中执行 Java 类的权限。

    若要授予对 jar 文件的读取和执行访问权限，请在 jar 文件上运行以下 **chmod** 命令。 我们建议在使用 SQL Server 时始终将类文件放在 jar 中。 有关创建 jar 的帮助，请参阅[如何创建 jar 文件](https://docs.microsoft.com/sql/language-extensions/how-to/create-a-java-jar-file-from-class-files)。

    ```cmd
    chmod ug+rx <MyJarFile.jar>
    ```

    还需要提供对要读取/执行的 jar 文件的 mssql_satellite 权限。

    ```cmd
    chown mssql_satellite:mssql_satellite <MyJarFile.jar>
    ```

    其他配置主要通过 [mssql-conf 工具](sql-server-linux-configure-mssql-conf.md)完成。

2. 添加用于运行 SQL Server 服务的 mssql 用户帐户。 如果之前未运行过该安装程序，则必须这样做。

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

3. 启用出站网络访问。 默认情况下，出站网络访问处于禁用状态。 若要启用出站请求，请使用 mssql-conf 工具设置“outboundnetworkaccess”布尔属性。 有关详细信息，请参阅[使用 mssql-conf 配置 Linux 上的 SQL Server](sql-server-linux-configure-mssql-conf.md#mlservices-outbound-access)。

   ```bash
   # Run as SUDO or root
   # Enable outbound requests over the network
   sudo /opt/mssql/bin/mssql-conf set extensibility outboundnetworkaccess 1
   ```

4. 重启 SQL Server Launchpad 服务和数据库引擎实例，以从 INI 文件中读取更新后的值。 每当修改与扩展性相关的设置时，都会收到重启消息提醒。  

   ```bash
   systemctl restart mssql-launchpadd

   systemctl restart mssql-server.service
   ```

5. 使用 Azure Data Studio 或使用运行 Transact-SQL 的其他工具（如 SQL Server Management Studio，仅限 Windows）来启用外部脚本执行。

   ```bash
   EXEC sp_configure 'external scripts enabled', 1
   RECONFIGURE WITH OVERRIDE
   ```

6. 再次重启 `mssql-launchpadd` 服务。

7. 对于想要在其中使用语言扩展的每个数据库，需要使用 [CREATE EXTERNAL LANGUAGE](https://docs.microsoft.com/sql/t-sql/statements/create-external-language-transact-sql) 注册外部语言。

## <a name="register-external-language"></a>注册外部语言

对于想要在其中使用语言扩展的每个数据库，需要使用 [CREATE EXTERNAL LANGUAGE](https://docs.microsoft.com/sql/t-sql/statements/create-external-language-transact-sql) 注册外部语言。

以下示例将名为 Java 的外部语言添加到 Linux 上的 SQL Server 的数据库中。

```SQL
CREATE EXTERNAL LANGUAGE Java
FROM (CONTENT = N'<path-to-tar.gz>', FILE_NAME = 'javaextension.so');
GO
```

有关详细信息，请参阅 [CREATE EXTERNAL LANGUAGE](https://docs.microsoft.com/sql/t-sql/statements/create-external-language-transact-sql)。

## <a name="verify-installation"></a>验证安装

Java 功能集成不包含库，但可以运行 `grep -r JRE_HOME /etc` 来确认创建 JAVA_HOME 环境变量。

若要验证安装，请运行执行调用 Java 的系统存储过程的 T-SQL 脚本。 需要使用查询工具来完成此任务。 Azure Data Studio 就是不错的选择。 其他常用工具（如 SQL Server Management Studio 或 PowerShell）仅适用于 Windows。 如果 Windows 计算机上安装了这些工具，请使用其连接到数据库引擎的 Linux 安装。

<a name="install-all"></a>

## <a name="full-install-of-sql-server-and-language-extensions"></a>完整安装 SQL Server 和语言扩展

通过在安装数据库引擎的命令上附加 Java 包和参数，可在一个过程中安装和配置数据库引擎及语言扩展。

1. 提供包含数据库引擎的命令行以及语言扩展功能。

  可将 Java 扩展性添加到数据库引擎安装中。

  ```bash
  sudo yum install -y mssql-server mssql-server-extensibility-java 
  ```

3. 接受许可协议并完成安装后配置。 使用 **mssql-conf** 工具完成此任务。

  ```bash
  sudo /opt/mssql/bin/mssql-conf setup
  ```

  系统将提示接受数据库引擎的许可协议、选择版本以及设置管理员密码。 

4. 如果系统出现重启提示，请重启服务。

  ```bash
  sudo systemctl restart mssql-server.service
  ```

## <a name="unattended-installation"></a>无人参与安装

对数据库引擎使用[无人参与安装](https://docs.microsoft.com/sql/linux/sql-server-linux-setup#unattended)，添加 mssql-server-extensibility-java 包。

<a name="offline-install"></a>


## <a name="offline-installation"></a>脱机安装

有关安装包的步骤，请按照[脱机安装](sql-server-linux-setup.md#offline)说明进行操作。 找到下载网站，然后使用下面的包列表下载特定的包。

> [!Tip]
> 一些包管理工具提供可帮助确定包依赖项的命令。 对于 yum，请使用 `sudo yum deplist [package]`。 对于 Ubuntu，请在使用 `sudo apt-get install --reinstall --download-only [package name]` 之后使用 `dpkg -I [package name].deb`。

#### <a name="download-site"></a>下载站点

可以从 [https://packages.microsoft.com/](https://packages.microsoft.com/) 下载包。 Java 的所有包都与数据库引擎包位于同一位置。 

#### <a name="redhat7-paths"></a>RedHat/7 路径

|||
|--|----|
| mssql/extensibility-java 包 | [https://packages.microsoft.com/rhel/7/mssql-server-preview/](https://packages.microsoft.com/rhel/7/mssql-server-preview/) |

#### <a name="ubuntu1604-paths"></a>Ubuntu/16.04 路径

|||
|--|----|
| mssql/extensibility-java 包 | [https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/) |

#### <a name="suse12-paths"></a>SUSE/12 路径

|||
|--|----|
| mssql/extensibility-java 包 | [https://packages.microsoft.com/sles/12/mssql-server-preview/](https://packages.microsoft.com/sles/12/mssql-server-preview/) |

#### <a name="package-list"></a>包列表

根据想要使用的扩展，下载特定语言所需的包。 精确的文件名在后缀中包含平台信息，但以下文件名应足够接近，可用于确定要获取的文件。

```
# Core packages 
mssql-server-15.0.1000
mssql-server-extensibility-15.0.1000

# Java
mssql-server-extensibility-java-15.0.1000
```

## <a name="limitations"></a>限制

+ 目前，Linux 中不提供隐式身份验证，这意味着无法从正在执行的 Java 连接回服务器来访问数据或其他资源。

### <a name="resource-governance"></a>资源调控

Linux 和 Windows 之间存在供外部资源池进行[资源调控](../t-sql/statements/create-external-resource-pool-transact-sql.md)的奇偶校验，但 [sys.dm_resource_governor_external_resource_pools](../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pools.md) 的统计信息目前在 Linux 上具有不同的单位。 
 
| 列名   | 描述 | Linux 上的值 | 
|---------------|--------------|---------------|
|peak_memory_kb | 资源池使用的最大内存量。 | 在 Linux 上，此统计信息来自 CGroups 内存子系统，其值为 memory.max_usage_in_bytes |
|write_io_count | 自重置 Resource Governor 统计信息以来发出的写入 IO 总数。 | 在 Linux 上，此统计信息来自 CGroups blkio 子系统，其中写入行上的值为 blkio.throttle.io_serviced | 
|read_io_count | 自重置 Resource Governor 统计信息以来发出的读取 IO 总数。 | 在 Linux 上，此统计信息来自 CGroups blkio 子系统，其中读取行上的值为 blkio.throttle.io_serviced | 
|total_cpu_kernel_ms | 自重置 Resource Governor 统计信息以来的累计 CPU 用户内核时间（以毫秒为单位）。 | 在 Linux 上，此统计信息来自 CGroups cpuacct 子系统，其中用户行上的值为 cpuacct.stat |  
|total_cpu_user_ms | 自重置 Resource Governor 统计信息以来的累计 CPU 用户时间（以毫秒为单位）。| 在 Linux 上，此统计信息来自 CGroups cpuacct 子系统，其中系统行值上的值为 cpuacct.stat | 
|active_processes_count | 请求时运行的外部进程数。| 在 Linux 上，此统计信息来自 GGroups pids 子系统，其值为 pids.current | 

## <a name="next-steps"></a>后续步骤

Java 开发人员可以开始体验一些简单的示例，并了解 Java 如何与 SQL Server 配合工作的基础知识。 有关下一步，请参阅以下链接：

+ [教程：正则表达式与 Java](../language-extensions/tutorials/search-for-string-using-regular-expressions-in-java.md)