---
title: 在 Linux 上安装 SQL Server 机器学习服务（Python、R）
description: 了解如何在 Linux 上安装 SQL Server 机器学习服务（Python 和 R）：Red Hat、Ubuntu 和 SUSE。
author: dphansen
ms.author: davidph
ms.reviewer: vanto
manager: cgronlun
ms.date: 09/23/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: machine-learning
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: b3d2fb6c05a078e222a68e8de8998d4edff3c1a8
ms.sourcegitcommit: 2f56848ec422845ee81fb84ed321a716c677aa0e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/25/2019
ms.locfileid: "71271967"
---
# <a name="install-sql-server-machine-learning-services-python-and-r-on-linux"></a>在 Linux 上安装 SQL Server 机器学习服务（Python 和 R）

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本文介绍如何在 Linux 上安装 [SQL Server 机器学习服务](../advanced-analytics/index.yml)。 可使用机器学习服务在数据库中执行 Python 和 R 脚本。

支持以下 Linux 分发版：

- Red Hat Enterprise Linux (RHEL)
- SUSE Linux Enterprise Server (SLES)
- Ubuntu

机器学习服务是数据库引擎的一项附加功能。 虽然可以[同时安装数据库引擎和机器学习服务](#install-all)，但最好先安装并配置 SQL Server 数据库引擎，以便在添加更多组件之前解决所有问题。 

Python 和 R 扩展的包位于 SQL Server Linux 源存储库中。 如果已为数据库引擎安装配置了源存储库，则可以使用相同的存储库注册运行 mssql-mlservices 包安装命令  。

Linux 容器也支持机器学习服务。 我们不提供带有机器学习服务的预构建容器，但你可以使用 [GitHub 中的示例模板](https://github.com/Microsoft/mssql-docker/tree/master/linux/preview/examples/mssql-mlservices)在 SQL Server 容器中创建一个容器。

## <a name="uninstall-previous-ctp"></a>卸载以前的 CTP

包列表在最近几个 CTP 版本中发生了更改，因而包的数量有所减少。 我们建议先卸载 CTP 2.x 以删除所有以前的包，然后再安装 CTP 3.2。 不支持并行安装多个版本。

### <a name="1-confirm-package-installation"></a>1.确认包安装

首先可能需要检查是否存在以前的安装。 以下文件指示现有安装：checkinstallextensibility.sh、exthost、launchpad。

```bash
ls /opt/microsoft/mssql/bin
```

### <a name="2-uninstall-previous-ctp-2x-packages"></a>2.卸载以前的 CTP 2.x 包

在最低包级别进行卸载。 依赖于较低级别包的所有上游包都会自动卸载。

  + 对于 R 集成，请删除 **microsoft-r-open***
  + 对于 Python 集成，请删除 **mssql-mlservices-python**

下表显示了用于删除包的命令。

| 平台  | 包删除命令 | 
|-----------|----------------------------|
| Red Hat   | `sudo yum remove microsoft-r-open-mro-3.4.4`<br/>`sudo yum remove msssql-mlservices-python` |
| SUSE  | `sudo zypper remove microsoft-r-open-mro-3.4.4`<br/>`sudo zypper remove msssql-mlservices-python` |
| Ubuntu    | `sudo apt-get remove microsoft-r-open-mro-3.4.4`<br/>`sudo apt-get remove msssql-mlservices-python`|

> [!Note]
> Microsoft R Open 3.4.4 由两个或三个包组成，具体取决于之前安装的 CTP 版本。 （foreachiterators 包已合并到 CTP 2.2 中的主 mro 包中。）如果在删除 microsoft-r-open-mro-3.4.4 后，这些包中的任何包仍然存在，则应单独删除它们。
> ```
> microsoft-r-open-foreachiterators-3.4.4
> microsoft-r-open-mkl-3.4.4
> microsoft-r-open-mro-3.4.4
> ```

### <a name="3-proceed-with-ctp-32-install"></a>3.继续进行 CTP 3.2 安装

使用本文中针对操作系统的说明在最高包级别进行安装。

对于每个特定于 OS 的安装说明集，“最高包级别”是“示例 1 - 完全安装”（完整的包集）或“示例 2 - 最小安装”（可行安装所需的最少的包数量）    。

1. 对于 R 集成，请从 [MRO](#mro) 开始，因为它是必备组件。 如果没有该组件，则无法安装 R 集成。

2. 使用操作系统的包管理器和语法运行安装命令： 

   + [Red Hat](#RHEL)
   + [Ubuntu](#ubuntu)
   + [SUSE](#suse)

## <a name="prerequisites"></a>必备条件

+ Linux 版本必须[受 SQL Server 支持](sql-server-linux-release-notes-2019.md#supported-platforms)，但不包括 Docker 引擎。 受支持的版本包括：

   + [Red Hat Enterprise Linux (RHEL)](quickstart-install-connect-red-hat.md)

   + [SUSE Enterprise Linux Server](quickstart-install-connect-suse.md)

   + [Ubuntu](quickstart-install-connect-ubuntu.md)

+ （仅限 R）[Microsoft R Open](#mro) 为 SQL Server 中的 R 功能提供基本 R 发行版

+ 应安装用于运行 T-SQL 命令的工具。 需要使用查询编辑器进行安装后配置和验证。 我们建议使用 [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/download?view=sql-server-2017#get-azure-data-studio-for-linux)，它是在 Linux 上运行的免费下载。

<a name="mro"></a>

### <a name="microsoft-r-open-mro-installation"></a>Microsoft R Open (MRO) 安装

要使用通过机器学习服务安装的 RevoScaleR、MicrosoftML 和其他 R 包，Microsoft 的 R 基础发行版是先决条件。

所需版本为 MRO 3.5.2。

从以下两种安装 MRO 的方法中进行选择：

+ 从 MRAN 下载 MRO tarball，解压缩并运行其 install.sh 脚本。 如果要使用此方法，可以按照 [MRAN 上的安装说明](https://mran.microsoft.com/releases/3.5.2)进行操作。

+ 或者，如下所述注册 **packages.microsoft.com** 存储库以安装包含 MRO 发行版的两个软件包：microsoft-r-open-mro 和 microsoft-r-open-mkl。 

以下命令可注册提供 MRO 的存储库。 注册后，用于安装其他 R 包的命令（如 mssql-mlservices-mml-r）将自动包含作为包依赖项的 MRO。

#### <a name="mro-on-ubuntu"></a>Ubuntu 上的 MRO

```bash
# Install as root
sudo su

# Optionally, if your system does not have the https apt transport option
apt-get install apt-transport-https

# Set the location of the package repo the "prod" directory containing the distribution.
# This example specifies 16.04. Replace with 14.04 if you want that version
wget https://packages.microsoft.com/config/ubuntu/16.04/packages-microsoft-prod.deb

# Register the repo
dpkg -i packages-microsoft-prod.deb

# Update packages on your system (required), including MRO installation
sudo apt-get update
```

#### <a name="mro-on-red-hat"></a>Red Hat 上的 MRO

```bash
# Import the Microsoft repository key
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc


# Set the location of the package repo at the "prod" directory
# The following command is for version 7.x
# For 6.x, replace 7 with 6 to get that version
rpm -Uvh https://packages.microsoft.com/config/rhel/7/packages-microsoft-prod.rpm

# Update packages on your system (optional)
yum update
```

#### <a name="mro-on-suse"></a>SUSE 上的 MRO

```bash
# Install as root
sudo su

# Set the location of the package repo at the "prod" directory containing the distribution
# This example is for SLES12, the only supported version of SUSE in Machine Learning Server
zypper ar -f https://packages.microsoft.com/sles/12/prod packages-microsoft-com

# Update packages on your system (optional)
zypper update
```

## <a name="package-list"></a>包列表

在已连接 Internet 的设备上，将使用每个操作系统的包安装程序来独立于数据库引擎下载和安装包。 下表介绍了所有可用包，但对于 R 和 Python，需要指定提供完整功能安装或最小功能安装的包。

| 包名称 | 适用对象 | 描述 |
|--------------|----------|-------------|
|mssql-server-extensibility  | All | 用于运行 R 和 Python 代码的可扩展性框架。 |
| microsoft-openmpi  | Python、R | Revo* 库在 Linux 上进行并行化所使用的消息传递接口。 |
| mssql-mlservices-python | Python | Anaconda 和 Python 的开放源代码发行版。 |
|mssql-mlservices-mlm-py  | Python | 完全安装  。 提供用于图像特征化和文本情绪分析的 revoscalepy、microsoftml、预先训练的模型。| 
|mssql-mlservices-packages-py  | Python | 最小安装  。 提供 revoscalepy 和 microsoftml。 <br/>不包括预先训练的模型。 | 
| [microsoft-r-open*](#mro) | R | 由三个包组成的 R 的开放源代码发行版。 |
|mssql-mlservices-mlm-r  | R | 完全安装  。 提供用于图像特征化和文本情绪分析的 RevoScaleR、MicrosoftML、sqlRUtils、olapR、预先训练的模型。| 
|mssql-mlservices-packages-r  | R | 最小安装  。 提供 RevoScaleR、sqlRUtils、MicrosoftML、olapR。 <br/>不包括预先训练的模型。 | 
|mssql-mlservices-mml-py  | 仅限 CTP 2.0-2.1 | 由于 Python 包合并到 mssql-mslservices-python 中，因此在 CTP 2.2 中已过时。 提供 revoscalepy。 不包括预先训练的模型和 microsoftml。| 
|mssql-mlservices-mml-r  | 仅限 CTP 2.0-2.1 | 由于 R 包合并到 mssql-mslservices-python 中，因此在 CTP 2.2 中已过时。 提供 RevoScaleR、sqlRUtils、olapR。 不包括预先训练的模型和 MicrosoftML。  |

<a name="RHEL"></a>

## <a name="redhat-commands"></a>RedHat 命令

可以安装所需的任何语言支持组合（一种或多种语言）。 对于 R 和 Python，有两个包可供选择。 其中一个包提供所有可用功能，其特征为完全安装  。 替代选项不包括预先训练的机器学习模型，被认为是最小安装  。

> [!Tip]
> 如果可以，请在安装之前运行 `yum clean all` 以刷新系统中的包。

### <a name="example-1----full-installation"></a>示例 1 - 完全安装 

包括开放源代码 R 和 Python、扩展性框架、microsoft-openmpi、扩展（R、Python）以及机器学习库和 R 和 Python 的预先训练模型。 

```bash
# Install as root or sudo
# Add everything (all R, Python)
# Be sure to include -9.4.7* in mlsservices package names
sudo yum install mssql-mlservices-mlm-py-9.4.7*
sudo yum install mssql-mlservices-mlm-r-9.4.7* 
```

### <a name="example-2---minimum-installation"></a>示例 2 - 最小安装 

包括开放源代码 R 和 Python、扩展性框架、microsoft-openmpi、核心 Revo * 库以及 R 和 Python 的机器学习库。 不包括预先训练的模型。

```bash
# Install as root or sudo
# Minimum install of R, Python extensions
# Be sure to include -9.4.6* in mlsservices package names
sudo yum install mssql-mlservices-packages-py-9.4.7*
sudo yum install mssql-mlservices-packages-r-9.4.7*
```

<a name="ubuntu"></a>

## <a name="ubuntu-commands"></a>Ubuntu 命令

可以安装所需的任何语言支持组合（一种或多种语言）。 对于 R 和 Python，有两个包可供选择。 其中一个包提供所有可用功能，其特征为完全安装  。 替代选项不包括预先训练的机器学习模型，被认为是最小安装  。

> [!Tip]
> 如果可以，请在安装之前运行 `apt-get update` 以刷新系统中的包。 此外，Ubuntu 的一些 docker 映像可能没有 https apt 传输选项。 若要进行安装，请使用 `apt-get install apt-transport-https`。

### <a name="example-1----full-installation"></a>示例 1 - 完全安装 

包括开放源代码 R 和 Python、扩展性框架、microsoft-openmpi、扩展（R、Python）以及机器学习库和 R 和 Python 的预先训练模型。 

```bash
# Install as root or sudo
# Add everything (all R, Python)
# There is no asterisk in this full install
sudo apt-get install mssql-mlservices-mlm-py 
sudo apt-get install mssql-mlservices-mlm-r 
```

### <a name="example-2---minimum-installation"></a>示例 2 - 最小安装 

包括开放源代码 R 和 Python、扩展性框架、microsoft-openmpi、核心 Revo * 库以及 R 和 Python 的机器学习库。 不包括预先训练的模型。 

```bash
# Install as root or sudo
# Minimum install of R, Python
# No aasterisk
sudo apt-get install mssql-mlservices-packages-py
sudo apt-get install mssql-mlservices-packages-r
```

<a name="suse"></a>

## <a name="suse-commands"></a>SUSE 命令

可以安装所需的任何语言支持组合（一种或多种语言）。 对于 R 和 Python，有两个包可供选择。 其中一个包提供所有可用功能，其特征为完全安装  。 替代选项不包括预先训练的机器学习模型，被认为是最小安装  。

### <a name="example-1----full-installation"></a>示例 1 - 完全安装 

包括开放源代码 R 和 Python、扩展性框架、microsoft-openmpi、扩展（R、Python）以及机器学习库和 R 和 Python 的预先训练模型。 

```bash
# Install as root or sudo
# Add everything (all R, Python)
# Be sure to include -9.4.7* in mlsservices package names
sudo zypper install mssql-mlservices-mlm-py-9.4.7*
sudo zypper install mssql-mlservices-mlm-r-9.4.7* 
```

### <a name="example-2---minimum-installation"></a>示例 2 - 最小安装 

包括开放源代码 R 和 Python、扩展性框架、microsoft-openmpi、核心 Revo * 库以及 R 和 Python 的机器学习库。 不包括预先训练的模型。 

```bash
# Install as root or sudo
# Minimum install of R, Python extensions
# Be sure to include -9.4.6* in mlsservices package names
sudo zypper install mssql-mlservices-packages-py-9.4.7*
sudo zypper install mssql-mlservices-packages-r-9.4.7*
```

## <a name="post-install-config-required"></a>安装后配置（必需）

其他配置主要通过 [mssql-conf 工具](sql-server-linux-configure-mssql-conf.md)来完成。


1. 添加用于运行 SQL Server 服务的 mssql 用户帐户。 如果之前未运行过该安装程序，则必须这样做。

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

2. 接受开放源代码 R 和 Python 的许可协议。 可以通过多种方式来完成此项工作。 如果之前已接受 SQL Server 许可并且现将添加 R 或 Python 扩展，则以下命令可表示你同意其条款：

   ```bash
   # Run as SUDO or root
   # Use set + EULA 
   sudo /opt/mssql/bin/mssql-conf set EULA accepteulaml Y
   ```

   另一种工作流是，如果未接受过 SQL Server 数据库引擎许可协议，则在运行 `mssql-conf setup` 时，安装程序会检测 mssql-mlservices 包，并提示你接受 EULA。 有关 EULA 参数的详细信息，请参阅[使用 mssql-conf 工具配置 SQL Server](sql-server-linux-configure-mssql-conf.md#mlservices-eula)。

3. 启用出站网络访问。 默认情况下，出站网络访问处于禁用状态。 若要启用出站请求，请使用 mssql-conf 工具设置“outboundnetworkaccess”布尔属性。 有关详细信息，请参阅[使用 mssql-conf 配置 Linux 上的 SQL Server](sql-server-linux-configure-mssql-conf.md#mlservices-outbound-access)。

   ```bash
   # Run as SUDO or root
   # Enable outbound requests over the network
   sudo /opt/mssql/bin/mssql-conf set extensibility outboundnetworkaccess 1
   ```

4. （仅适用于 R 功能集成）请设置“MKL_CBWR”环境变量，以确保从 Intel 数学核心函数库 (MKL) 计算得到[一致的输出结果](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr)  。

   + 在用户主目录中编辑或创建名为 .bash_profile 的文件，并将行 `export MKL_CBWR="AUTO"` 添加到该文件中  。

   + 通过在 bash 命令提示符处键入 `source .bash_profile` 来执行此文件。

5. 重启 SQL Server Launchpad 服务和数据库引擎实例，以从 INI 文件中读取更新后的值。 每当修改与扩展性相关的设置时，都会收到重启消息提醒。  

   ```bash
   systemctl restart mssql-launchpadd

   systemctl restart mssql-server.service
   ```

6. 使用 Azure Data Studio 或使用运行 Transact-SQL 的其他工具（如 SQL Server Management Studio，仅限 Windows）来启用外部脚本执行。 

   ```bash
   EXEC sp_configure 'external scripts enabled', 1 
   RECONFIGURE WITH OVERRIDE 
   ```

7. 再次重启 Launchpad 服务。

## <a name="verify-installation"></a>验证安装

可在 `/opt/mssql/mlservices/libraries/RServer` 中找到 R 库（MicrosoftML、RevoScaleR 及其他库）。

可在 `/opt/mssql/mlservices/libraries/PythonServer` 中找到 Python 库（microsoftml 和 revoscalepy）。

若要验证安装，请运行可执行调用 R 或 Python 的系统存储过程的 T-SQL 脚本。 需要使用查询工具来完成此任务。 Azure Data Studio 就是不错的选择。 其他常用工具（如 SQL Server Management Studio 或 PowerShell）仅适用于 Windows。 如果 Windows 计算机上安装了这些工具，请使用其连接到数据库引擎的 Linux 安装。

请执行以下 SQL 命令以测试 SQL Server 中的 R 执行。 如果脚本未运行，则尝试重启服务，`sudo systemctl restart mssql-server.service`。

```r
EXEC sp_execute_external_script   
@language =N'R', 
@script=N' 
OutputDataSet <- InputDataSet', 
@input_data_1 =N'SELECT 1 AS hello' 
WITH RESULT SETS (([hello] int not null)); 
GO 
```
 
请执行以下 SQL 命令以测试 SQL Server 中的 Python 执行。 
 
```python
EXEC sp_execute_external_script  
@language =N'Python', 
@script=N' 
OutputDataSet = InputDataSet; 
', 
@input_data_1 =N'SELECT 1 AS hello' 
WITH RESULT SETS (([hello] int not null)); 
GO 
```

<a name="install-all"></a>

## <a name="chained-combo-install"></a>链式“组合”安装

通过在安装数据库引擎的命令上附加 R 或 Python 包和参数，可在一个过程中安装和配置数据库引擎和机器学习服务。 

1. 对于 R 集成，请安装 [Microsoft R Open](#mro)，将其作为必备组件。 如果没有安装 R 功能，请跳过此步骤。

2. 提供包含数据库引擎的命令行以及语言扩展功能。

  可以将单项功能（如 Python 集成）添加到数据库引擎安装中。

  ```bash
  sudo yum install -y mssql-server mssql-mlservices-packages-r-9.4.7* 
  ```

  或者，同时添加两项扩展（R、Python）。

  ```bash
  sudo yum install -y mssql-server mssql-mlservices-packages-r-9.4.7* mssql-mlservices-packages-py-9.4.7*
  ```

3. 接受许可协议并完成安装后的配置。 使用 **mssql-conf** 工具完成此任务。

  ```bash
  sudo /opt/mssql/bin/mssql-conf setup
  ```

  系统将提示你接受数据库引擎的许可协议，选择版本，以及设置管理员密码。 系统还会提示你接受机器学习服务的许可协议。

4. 如果系统出现重启提示，请重启服务。

  ```bash
  sudo systemctl restart mssql-server.service
  ```

## <a name="unattended-installation"></a>无人参与安装

对数据库引擎使用[无人参与安装](https://docs.microsoft.com/sql/linux/sql-server-linux-setup?view=sql-server-2017#unattended)，添加 mssql-mlservices 和 EULA 的包。

回想一下，安装程序或 mssql-conf 工具会提示接受许可协议。 如果已配置 SQL Server 数据库引擎且已接受其 EULA，请使用开放源代码 R 和 Python 发行版的某个特定于 mlservices 的 EULA 参数：

```bash
sudo /opt/mssql/bin/mssql-conf setup accept-eula-ml
```

EULA 接受的所有可能的排列方式都记录在[使用 mssql-conf 工具配置 Linux 上的 SQL Server](sql-server-linux-configure-mssql-conf.md#mlservices-eula) 中。

## <a name="offline-installation"></a>脱机安装

有关安装包的步骤，请按照[脱机安装](sql-server-linux-setup.md#offline)说明进行操作。 找到下载网站，然后使用下面的包列表下载特定的包。

> [!Tip]
> 一些包管理工具提供可帮助确定包依赖项的命令。 对于 yum，请使用 `sudo yum deplist [package]`。 对于 Ubuntu，请在使用 `sudo apt-get install --reinstall --download-only [package name]` 之后使用 `dpkg -I [package name].deb`。


#### <a name="download-site"></a>下载站点

可以从 [https://packages.microsoft.com/](https://packages.microsoft.com/) 下载包。 R 和 Python 的所有 mlservices 包都与数据库引擎包位于相同位置。 mlservices 包的基本版本为 9.4.5（适用于 CTP 2.0）、9.4.6（适用于 CTP 2.1 及更高版本）。 回想一下，microsoft-r-open 包位于[其他存储库](#mro)中。

#### <a name="rhel7-paths"></a>RHEL/7 路径

|||
|--|----|
| mssql/mlservices 包 | [https://packages.microsoft.com/rhel/7/mssql-server-preview/](https://packages.microsoft.com/rhel/7/mssql-server-preview/) |
| microsoft-r-open 包 | [https://packages.microsoft.com/rhel/7/prod/](https://packages.microsoft.com/rhel/7/prod/) | 


#### <a name="ubuntu1604-paths"></a>Ubuntu/16.04 路径

|||
|--|----|
| mssql/mlservices 包 | [https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/) |
| microsoft-r-open 包 | [https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/](https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/) | 

#### <a name="sles12-paths"></a>SLES/12 路径

|||
|--|----|
| mssql/mlservices 包 | [https://packages.microsoft.com/sles/12/mssql-server-preview/](https://packages.microsoft.com/sles/12/mssql-server-preview/) |
| microsoft-r-open 包 | [https://packages.microsoft.com/sles/12/prod/](https://packages.microsoft.com/sles/12/prod/) | 

#### <a name="package-list"></a>包列表

根据想要使用的扩展，下载特定语言所需的包。 确切文件名的后缀中包含平台信息，但下面的文件名应足够接近以确定要获取的文件。

```
# Core packages 
mssql-server-15.0.1000
mssql-server-extensibility-15.0.1000

# R
microsoft-openmpi-3.0.0
microsoft-r-open-mkl-3.5.2
microsoft-r-open-mro-3.5.2
mssql-mlservices-packages-r-9.4.7.64
mssql-mlservices-mlm-r-9.4.7.64


# Python
microsoft-openmpi-3.0.0
mssql-mlservices-python-9.4.7.64
mssql-mlservices-packages-py-9.4.7.64
mssql-mlservices-mlm-py-9.4.7.64
```

## <a name="add-more-rpython-packages"></a>添加更多 R/Python 包 
 
可以安装其他 R 和 Python 包，并在从 SQL Server 2019 上执行的脚本中使用它们。

### <a name="r-packages"></a>R 包 
 
1. 启动 R 会话。

   ```r
   # sudo /opt/mssql/mlservices/bin/R/R 
   ```

2. 安装名为 [glue](https://mran.microsoft.com/package/glue) 的 R 包以测试包安装。

   ```r
   # install.packages("glue",lib="/opt/mssql/mlservices/libraries/RServer") 
   ```
   也可以从命令行安装 R 包 

   ```r
   # sudo /opt/mssql/mlservices/bin/R/R CMD INSTALL -l /opt/mssql/mlservices/libraries/RServer glue_1.1.1.tar.gz 
   ```

3. 在 [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 中导入 R 包。

   ```r
   EXEC sp_execute_external_script  
   @language = N'R', 
   @script = N'library(glue)' 
   ```

### <a name="python-packages"></a>Python 包 
 
1. 使用 pip 安装名为 [httpie](https://httpie.org/) 的 Python 包。 

   ```python
   # sudo /opt/mssql/mlservices/bin/python/python -m pip install httpie 
   ``` 

2. 在 [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 中导入 Python 包。
 
   ```python
   EXEC sp_execute_external_script  
   @language = N'Python',  
   @script = N'import httpie' 
   ```

## <a name="limitations-in-ctp-releases"></a>CTP 版本的限制

Linux 上的 R 和 Python 集成仍处于积极开发阶段。 预览版本中尚未启用以下功能。

+ 目前，Linux 上的机器学习服务中不提供隐式身份验证，这意味着无法从进程中的 R 或 Python 脚本连接回服务器以访问数据或其他资源。 

### <a name="resource-governance"></a>资源调控

Linux 和 Windows 之间存在供外部资源池进行[资源调控](../t-sql/statements/create-external-resource-pool-transact-sql.md)的奇偶校验，但 [sys.dm_resource_governor_external_resource_pools](../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pools.md) 的统计信息目前在 Linux 上具有不同的单位。 单位将在即将推出的 CTP 中保持一致。
 
| 列名   | 描述 | Linux 上的值 | 
|---------------|--------------|---------------|
|peak_memory_kb | 资源池使用的最大内存量。 | 在 Linux 上，此统计信息来自 CGroups 内存子系统，其值为 memory.max_usage_in_bytes |
|write_io_count | 自重置 Resource Governor 统计信息以来发出的写入 IO 总数。 | 在 Linux 上，此统计信息来自 CGroups blkio 子系统，其中写入行上的值为 blkio.throttle.io_serviced | 
|read_io_count | 自重置 Resource Governor 统计信息以来发出的读取 IO 总数。 | 在 Linux 上，此统计信息来自 CGroups blkio 子系统，其中读取行上的值为 blkio.throttle.io_serviced | 
|total_cpu_kernel_ms | 自重置 Resource Governor 统计信息以来的累计 CPU 用户内核时间（以毫秒为单位）。 | 在 Linux 上，此统计信息来自 CGroups cpuacct 子系统，其中用户行上的值为 cpuacct.stat |  
|total_cpu_user_ms | 自重置 Resource Governor 统计信息以来的累计 CPU 用户时间（以毫秒为单位）。| 在 Linux 上，此统计信息来自 CGroups cpuacct 子系统，其中系统行值上的值为 cpuacct.stat | 
|active_processes_count | 请求时运行的外部进程数。| 在 Linux 上，此统计信息来自 GGroups pids 子系统，其值为 pids.current | 

## <a name="next-steps"></a>后续步骤

R 开发人员可以开始使用一些简单的示例，并了解 R 如何与 SQL Server 协同工作的基础知识。 有关下一步，请参阅以下链接：

+ [教程：在 T-SQL 中运行 R](../advanced-analytics/tutorials/quickstart-r-create-script.md)
+ [教程：适用于 R 开发人员的数据库内分析](../advanced-analytics/tutorials/sqldev-in-database-r-for-sql-developers.md)

Python 开发人员可以通过以下教程了解如何将 Python 与 SQL Server 一起使用：

+ [教程：在 T-SQL 中运行 Python](../advanced-analytics/tutorials/run-python-using-t-sql.md)
+ [教程：适用于 Python 开发人员的数据库内分析](../advanced-analytics/tutorials/sqldev-in-database-python-for-sql-developers.md)

若要查看基于真实场景的机器学习示例，请参阅[机器学习教程](../advanced-analytics/tutorials/machine-learning-services-tutorials.md)。
