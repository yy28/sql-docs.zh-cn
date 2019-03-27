---
title: 安装 SQL Server 机器学习在 Linux 上的服务 (R、 Python、 Java) |Microsoft Docs
description: 在 Red Hat 和 Ubuntu 上了解如何安装 SQL Server 机器学习服务 （R、 Python、 Java）。
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.date: 03/27/2018
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: machine-learning
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: f1ca66c5e376704737a092f21fd25401d20bbdbb
ms.sourcegitcommit: 2db83830514d23691b914466a314dfeb49094b3c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "58493869"
---
# <a name="install-sql-server-2019-machine-learning-services-r-python-java-on-linux"></a>安装 SQL Server 2019 机器学习服务 (R、 Python、 Java) 在 Linux 上

[SQL Server 机器学习服务](../advanced-analytics/what-is-sql-server-machine-learning.md)启动 SQL Server 2019 此预览版本中的 Linux 操作系统上运行。 按照这篇文章来安装 Java 编程扩展或机器学习对 R 和 Python 的扩展中的步骤。 

机器学习和编程扩展插件是到数据库引擎外的接程序。 尽管你可以[同时安装数据库引擎和机器学习服务](#install-all)，它是安装和配置 SQL Server 数据库引擎第一次，以便可以添加更多之前解决任何问题的最佳做法组件。 

R、 Python 和 Java 扩展包位置是在 SQL Server Linux 源存储库中。 如果你已配置的数据库引擎安装源代码存储库，则可以运行**mssql mlservices**包使用相同的存储库注册的安装命令。

机器学习服务还支持在 Linux 容器上。 使用机器学习服务，我们不会提供预建的容器，但您可以创建一个从使用 SQL Server 容器[可在 GitHub 上的示例模板](https://github.com/Microsoft/mssql-docker/tree/master/linux/preview/examples/mssql-mlservices)。

## <a name="uninstall-previous-ctp"></a>卸载以前的 CTP

在过去几个 CTP 版本中，从而导致较少的包已更改的包列表。 我们建议卸载 CTP 2.x 安装 CTP 2.4 之前删除所有以前的包。 不支持通过并行安装多个版本。

### <a name="1-confirm-package-installation"></a>1.确认包安装

你可能想要检查存在以前安装的第一步。 以下文件针对的是现有的安装： checkinstallextensibility.sh、 exthost、 快速启动板。

```bash
ls /opt/microsoft/mssql/bin
```

### <a name="2-uninstall-previous-ctp-2x-packages"></a>2.卸载以前的 CTP 2.x 包

卸载包最低级别。 会自动卸载依赖于较低级别程序包任何上游包。

  + 对于 R 集成删除**microsoft r open***
  + 对于 Python 集成删除**mssql mlservices python**
  + 对于 Java 集成删除**mssql server 扩展性 java**

有关删除包的命令也显示在下表中。

| 平台  | 包删除命令 | 
|-----------|----------------------------|
| RHEL  | `sudo yum remove microsoft-r-open-mro-3.4.4`<br/>`sudo yum remove msssql-mlservices-python`<br/>`sudo yum remove msssql-server-extensibility-java` |
| SLES  | `sudo zypper remove microsoft-r-open-mro-3.4.4`<br/>`sudo zypper remove msssql-mlservices-python`<br/>`sudo zypper remove msssql-server-extensibility-java` |
| Ubuntu    | `sudo apt-get remove microsoft-r-open-mro-3.4.4`<br/>`sudo apt-get remove msssql-mlservices-python`<br/>`sudo apt-get remove msssql-server-extensibility-java`|

> [!Note]
> Microsoft R Open 三个包组成。 如果任何这些包保留删除 microsoft-r-打开-mro-3.4.4 后，你应分别将其删除。
> ```
> microsoft-r-open-foreachiterators-3.4.4
> microsoft-r-open-mkl-3.4.4
> microsoft-r-open-mro-3.4.4
> ```

### <a name="3-proceed-with-ctp-24-install"></a>3.继续 CTP 2.4 安装

安装的最高级别包为操作系统在本文中使用的说明。

为每个特定于操作系统的集的安装说明*最高的包级别*可以是**示例 1-完整安装**一系列完整的包，或**示例 2-最小安装**的最小的可行安装所需的包的数字。

1. 对于 R 集成开始[MRO](#mro)因为它是一项必备条件。 如果没有它，不会安装 R 集成。

2. 运行安装命令使用你的操作系统的程序包管理器和语法： 

   + [RedHat](#RHEL)
   + [Ubuntu](#ubuntu)
   + [SUSE](#suse)

## <a name="prerequisites"></a>先决条件

+ Linux 版本必须是[SQL Server 支持的](sql-server-linux-release-notes-2019.md#supported-platforms)，但不包括 Docker 引擎。 支持的版本包括：

   + [Red Hat Enterprise Linux (RHEL)](quickstart-install-connect-red-hat.md)

   + [SUSE Enterprise Linux Server](quickstart-install-connect-suse.md)

   + [Ubuntu](quickstart-install-connect-ubuntu.md)

+ (仅适用于 R)[Microsoft R Open](#mro)提供基础 R 发行版的 SQL Server 中 R 功能

+ 应具有用于运行 T-SQL 命令的工具。 查询编辑器是必需的安装后配置和验证。 我们建议[Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/download?view=sql-server-2017#get-azure-data-studio-for-linux)，在 Linux 运行的免费下载。

<a name="mro"></a>

### <a name="microsoft-r-open-mro-installation"></a>Microsoft R Open (MRO) 安装

Microsoft 的 R 基础分发是使用 RevoScaleR、 MicrosoftML 和使用机器学习服务安装其他 R 包的先决条件。

所需的版本是 MRO 3.4.4。

选择从以下两种方法安装 MRO:

+ 从 MRAN 下载 MRO tarball，解压缩它，并运行其 install.sh 脚本。 可以按照[MRAN 的安装说明](https://mran.microsoft.com/releases/3.4.4)如果希望此方法。

+ 或者，注册**packages.microsoft.com**如下所述安装三个包组成 MRO 分发存储库： microsoft r open mro、 microsoft-r-打开-mkl，和microsoft-r-打开-foreachiterators。 

以下命令注册存储库提供 MRO。 注册后，用于安装其他 R 包，例如 mssql-mlservices-mml-r，命令将作为包依赖项中自动包括 MRO。

#### <a name="mro-on-ubuntu"></a>在 Ubuntu 上 MRO

```bash
# Install as root
sudo su

# Optionally, if your system does not have the https apt transport option
apt-get install apt-transport-https

# Add the **azure-cli** repo to your apt sources list
AZ_REPO=$(lsb_release -cs)

echo "deb [arch=amd64] https://packages.microsoft.com/repos/azure-cli/ $AZ_REPO main" | sudo tee /etc/apt/sources.list.d/azure-cli.list

# Set the location of the package repo the "prod" directory containing the distribution.
# This example specifies 16.04. Replace with 14.04 if you want that version
wget https://packages.microsoft.com/config/ubuntu/16.04/packages-microsoft-prod.deb

# Register the repo
dpkg -i packages-microsoft-prod.deb

# Update packages on your system (required), including MRO installation
sudo apt-get update
```

#### <a name="mro-on-rhel"></a>在 RHEL 上 MRO

```bash
# Import the Microsoft repository key
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc

# Create local `azure-cli` repository
sudo sh -c 'echo -e "[azure-cli]\nname=Azure CLI\nbaseurl=https://packages.microsoft.com/yumrepos/azure-cli\nenabled=1\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/yum.repos.d/azure-cli.repo'

# Set the location of the package repo at the "prod" directory
# The following command is for version 7.x
# For 6.x, replace 7 with 6 to get that version
rpm -Uvh https://packages.microsoft.com/config/rhel/7/packages-microsoft-prod.rpm

# Update packages on your system (optional)
yum update
```
#### <a name="mro-on-suse"></a>在 SUSE 上 MRO

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

在与 internet 连接的设备，包下载并安装独立于数据库引擎的每个操作系统使用包安装程序。 下表描述了所有可用的包，但对 R 和 Python，指定提供完整功能安装或最小功能安装的包。

| 包名称 | Applies-to | Description |
|--------------|----------|-------------|
|mssql-server-extensibility  | All | 用于运行 R、 Python 或 Java 代码的可扩展性框架。 |
|mssql-server-extensibility-java | Java | 用于加载的 Java 执行环境的 Java 扩展。 没有任何其他库或用于 Java 的包。 |
| microsoft-openmpi  | Python, R | 消息传递接口 Revo * 库用于 Linux 上的并行化。 |
| mssql-mlservices-python | Python | 开放源代码分发 Anaconda 和 Python。 |
|mssql-mlservices-mlm-py  | Python | *完整安装*。 提供了 revoscalepy，microsoftml，预先训练的图像特征化和文本情绪分析的模型。| 
|mssql-mlservices-packages-py  | Python | *最小安装*。 提供了 revoscalepy 和 microsoftml。 <br/>不包括预先训练的模型。 | 
| [microsoft-r-open*](#mro) | R | 开放源代码 R 分发版中，三个包组成。 |
|mssql-mlservices-mlm-r  | R | *完整安装*。 提供了第 sqlRUtils RevoScaleR，MicrosoftML、 olapR，预先训练的图像特征化和文本情绪分析的模型。| 
|mssql-mlservices-packages-r  | R | *最小安装*。 提供了 RevoScaleR，sqlRUtils，MicrosoftML、 olapR。 <br/>不包括预先训练的模型。 | 
|mssql-mlservices-mml-py  | 仅 CTP 2.0 2.1 | 由于 Python 包整合到 mssql mslservices python，在 CTP 2.2 中已过时。 提供了 revoscalepy。 不包括预先训练的模型和 microsoftml。| 
|mssql-mlservices-mml-r  | 仅 CTP 2.0 2.1 | 由于 R 包整合到 mssql mslservices python，在 CTP 2.2 中已过时。 提供 RevoScaleR、 sqlRUtils、 olapR。 不包括预先训练的模型和 MicrosoftML。  |

<a name="RHEL"></a>

## <a name="rhel-commands"></a>RHEL 命令

可以安装语言支持任何组合中需要 （一个或多个语言）。 对 R 和 Python，有两个包可供选择。 一个提供了所有可用的功能，分为*完全安装*。 其他选项不包括预先训练的机器学习模型，并被视为*最小安装*。

> [!Tip]
> 如果可能，运行`yum clean all`刷新之前安装系统上的包。

### <a name="example-1----full-installation"></a>示例 1-完整安装 

包括开放源代码 R 和 Python，可扩展性框架，microsoft openmpi，扩展插件 （R、 Python、 Java），使用机器学习库和预先训练的模型对 R 和 Python。 

```bash
# Install as root or sudo
# Add everything (all R, Python, Java)
# Be sure to include -9.4.6* in mlsservices package names
sudo yum install mssql-mlservices-mlm-py-9.4.6*
sudo yum install mssql-mlservices-mlm-r-9.4.6* 
sudo yum install mssql-server-extensibility-java
```

### <a name="example-2---minimum-installation"></a>示例 2-最小安装 

R 和 Python 和 Java 扩展包括开放源代码 R 和 Python，extensibility framework、 microsoft openmpi、 core Revo * 库和机器学习库。 不包括预先训练的模型。

```bash
# Install as root or sudo
# Minimum install of R, Python, Java extensions
# Be sure to include -9.4.6* in mlsservices package names
sudo yum install mssql-mlservices-packages-py-9.4.6*
sudo yum install mssql-mlservices-packages-r-9.4.6*
sudo yum install mssql-server-extensibility-java
```

<a name="ubuntu"></a>

## <a name="ubuntu-commands"></a>Ubuntu 命令

可以安装语言支持任何组合中需要 （一个或多个语言）。 对 R 和 Python，有两个包可供选择。 一个提供了所有可用的功能，分为*完全安装*。 其他选项不包括预先训练的机器学习模型，并被视为*最小安装*。

> [!Tip]
> 如果可能，运行`apt-get update`刷新之前安装系统上的包。 此外，Ubuntu 某些 docker 映像可能没有 https apt 传输选项。 若要安装它，请使用`apt-get install apt-transport-https`。

<!---
### Prerequisite for 18.04

Running mssql-mlservices R libraries on Ubuntu 18.04 requires **libpng12** from the Linux Kernel archives. This package is no longer included in the standard distribution and must be installed manually. To get this library, run the following commands:

```bash
wget https://mirrors.kernel.org/ubuntu/pool/main/libp/libpng/libpng12-0_1.2.54-1ubuntu1_amd64.deb
dpkg -i libpng12-0_1.2.54-1ubuntu1_amd64.deb
```--->

### <a name="example-1----full-installation"></a>示例 1-完整安装 

包括开放源代码 R 和 Python，可扩展性框架，microsoft openmpi，扩展插件 （R、 Python、 Java），使用机器学习库和预先训练的模型对 R 和 Python。 

```bash
# Install as root or sudo
# Add everything (all R, Python, Java)
# There is no asterisk in this full install
sudo apt-get install mssql-mlservices-mlm-py 
sudo apt-get install mssql-mlservices-mlm-r 
sudo apt-get install mssql-server-extensibility-java
```

### <a name="example-2---minimum-installation"></a>示例 2-最小安装 

R 和 Python 和 Java 扩展包括开放源代码 R 和 Python，extensibility framework、 microsoft openmpi、 core Revo * 库和机器学习库。 不包括预先训练的模型。 

```bash
# Install as root or sudo
# Minimum install of R, Python, Java
# No aasterisk
sudo apt-get install mssql-mlservices-packages-py
sudo apt-get install mssql-mlservices-packages-r
sudo apt-get install mssql-server-extensibility-java
```

<a name="suse"></a>

## <a name="suse-commands"></a>SUSE 命令

可以安装语言支持任何组合中需要 （一个或多个语言）。 对 R 和 Python，有两个包可供选择。 一个提供了所有可用的功能，分为*完全安装*。 其他选项不包括预先训练的机器学习模型，并被视为*最小安装*。

### <a name="example-1----full-installation"></a>示例 1-完整安装 

包括开放源代码 R 和 Python，可扩展性框架，microsoft openmpi，扩展插件 （R、 Python、 Java），使用机器学习库和预先训练的模型对 R 和 Python。 

```bash
# Install as root or sudo
# Add everything (all R, Python, Java)
# Be sure to include -9.4.6* in mlsservices package names
sudo zypper install mssql-mlservices-mlm-py-9.4.6*
sudo zypper install mssql-mlservices-mlm-r-9.4.6* 
sudo zypper install mssql-server-extensibility-java
```

### <a name="example-2---minimum-installation"></a>示例 2-最小安装 

R 和 Python 和 Java 扩展包括开放源代码 R 和 Python，extensibility framework、 microsoft openmpi、 core Revo * 库和机器学习库。 不包括预先训练的模型。 

```bash
# Install as root or sudo
# Minimum install of R, Python, Java extensions
# Be sure to include -9.4.6* in mlsservices package names
sudo zypper install mssql-mlservices-packages-py-9.4.6*
sudo zypper install mssql-mlservices-packages-r-9.4.6*
sudo zypper install mssql-server-extensibility-java
```

## <a name="post-install-config-required"></a>安装后配置 （必需）

其他配置是主要通过[mssql-conf 工具](sql-server-linux-configure-mssql-conf.md)。


1. 添加用于运行 SQL Server 服务 mssql 用户帐户。 如果还没有以前运行安装程序，这是必需的。

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

2. 接受许可协议对开放源代码 R 和 Python。 有几种方法来执行此操作。 如果以前接受的 SQL Server 许可，并且现在要添加的 R 或 Python 的扩展，以下命令将为您的同意条款：

   ```bash
   # Run as SUDO or root
   # Use set + EULA 
   sudo /opt/mssql/bin/mssql-conf set EULA accepteulaml Y
   ```

   备用的工作流是如果你未接受许可协议的 SQL Server 数据库引擎，安装程序检测 mssql mlservices 包并会提示你输入的 EULA 接受时`mssql-conf setup`运行。 有关最终用户许可协议参数的详细信息，请参阅[使用 mssql-conf 工具配置 SQL Server](sql-server-linux-configure-mssql-conf.md#mlservices-eula)。

3. 启用出站网络访问。 默认情况下，出站网络访问处于禁用状态。 若要启用出站请求，请使用 mssql-conf 工具的布尔属性设置"outboundnetworkaccess"。 有关详细信息，请参阅[在 Linux 上使用 mssql conf 配置 SQL Server](sql-server-linux-configure-mssql-conf.md#mlservices-outbound-access)。

   ```bash
   # Run as SUDO or root
   # Enable outbound requests over the network
   sudo /opt/mssql/bin/mssql-conf set extensibility outboundnetworkaccess 1
   ```

4. 适用于 R 功能集成唯一，将**MKL_CBWR**环境变量[确保一致的输出](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr)从 Intel Math Kernel Library (MKL) 的计算。

   + 编辑或创建名为的文件 **.bash_profile**用户主目录中添加的代码行`export MKL_CBWR="AUTO"`的文件。

   + 通过键入来执行此文件`source .bash_profile`bash 命令提示符处。

5. 重新启动 SQL Server Launchpad 服务和数据库引擎实例读取 INI 文件的更新的值。 重新启动消息提醒您在每当修改扩展性相关的设置。  

   ```bash
   systemctl restart mssql-launchpadd

   systemctl restart mssql-server.service
   ```

6. 启用外部脚本执行，使用 Azure Data Studio 或 SQL Server Management Studio (仅 Windows) 等其他工具运行 Transact SQL。 

   ```bash
   EXEC sp_configure 'external scripts enabled', 1 
   RECONFIGURE WITH OVERRIDE 
   ```

7. 再次重新启动 Launchpad 服务。

## <a name="verify-installation"></a>验证安装

R 库 （MicrosoftML、 RevoScaleR，等），请参阅`/opt/mssql/mlservices/libraries/RServer`。

Python 库 （microsoftml 并 revoscalepy），请参阅`/opt/mssql/mlservices/libraries/PythonServer`。

Java 功能集成不包括库，但你可以运行`grep -r JAVA_HOME /etc`以确认创建 JAVA_HOME 环境变量。

若要验证安装，请运行执行系统存储过程调用 R 或 Python 的 T-SQL 脚本。 此任务需要查询工具。 Azure Data Studio 是一个不错的选择。 其他常用工具如 SQL Server Management Studio 或 PowerShell 也仅限 Windows 的。 如果必须使用这些工具的 Windows 计算机，使用它连接到数据库引擎的 Linux 安装。

执行以下的 SQL 命令，以测试 SQL Server 中 R 执行。 如果脚本未运行，请尝试重新启动服务， `sudo systemctl restart mssql-server.service`。

```r
EXEC sp_execute_external_script   
@language =N'R', 
@script=N' 
OutputDataSet <- InputDataSet', 
@input_data_1 =N'SELECT 1 AS hello' 
WITH RESULT SETS (([hello] int not null)); 
GO 
```
 
执行测试 Python 执行 SQL Server 中的以下 SQL 命令。 
 
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

## <a name="chained-combo-install"></a>链接"组合"安装

可以安装并通过追加 R、 Python 或 Java 包和参数的命令将安装数据库引擎上一个过程中配置的数据库引擎和机器学习服务。 

1. 对于 R 集成安装[Microsoft R Open](#mro)作为必备组件。 如果您未安装 R 功能，请跳过此步骤。

2. 提供的命令行，包含数据库引擎和语言扩展功能。

  您可以添加单个功能，例如 Java 集成到数据库引擎安装。

  ```bash
  sudo yum install -y mssql-server mssql-server-extensibility-java 
  ```

  或者，添加所有扩展 (Java、 R、 Python)。

  ```bash
  sudo yum install -y mssql-server mssql-server-extensibility-java mssql-mlservices-packages-r-9.4.6* mssql-mlservices-packages-py-9.4.6*
  ```

3. 接受许可协议并完成安装后配置。 使用**mssql conf**此任务的工具。

  ```bash
  sudo /opt/mssql/bin/mssql-conf setup
  ```

  系统将提示您接受数据库引擎的许可协议，选择版本，以及设置管理员密码。 系统会提示接受许可证协议的机器学习服务。

4. 如果系统提示你执行此操作，重新启动该服务。

  ```bash
  sudo systemctl restart mssql-server.service
  ```

## <a name="unattended-installation"></a>无人参与的安装

使用[无人参与的安装](https://docs.microsoft.com/sql/linux/sql-server-linux-setup?view=sql-server-2017#unattended)数据库引擎中，将添加 mssql mlservices 和 Eula 的包。

回想一下，安装程序或者 mssql-conf 工具将提示提供接受许可协议。 如果已配置 SQL Server 数据库引擎并接受其最终用户许可协议，使用特定于 mlservices 的最终用户许可协议参数之一的开放源代码 R 和 Python 分发版：

```bash
sudo /opt/mssql/bin/mssql-conf setup accept-eula-ml
```

中记录了所有可能排列的 EULA 接受[在 Linux 上使用 mssql-conf 工具配置 SQL Server](sql-server-linux-configure-mssql-conf.md#mlservices-eula)。

## <a name="offline-installation"></a>脱机安装

请按照[脱机安装](sql-server-linux-setup.md#offline)步骤包的安装说明进行操作。 查找您的下载站点，然后下载特定包使用以下包列表。

> [!Tip]
> 多个包管理工具提供可帮助你的命令确定包的依赖项。 对于 yum，使用`sudo yum deplist [package]`。 对于 Ubuntu，请使用`sudo apt-get install --reinstall --download-only [package name]`跟`dpkg -I [package name].deb`。


#### <a name="download-site"></a>下载站点

您可以从程序包下载[ https://packages.microsoft.com/ ](https://packages.microsoft.com/)。 所有 R、 Python 和 Java 的 mlservices 包都是与数据库引擎包共存。 基 mlservices 包版本是 （适用于 CTP 2.0) 9.4.5 9.4.6 （CTP 2.1 和更高版本）。 回想一下，microsoft r open 包位于[不同的存储库](#mro)。

#### <a name="rhel7-paths"></a>RHEL/7 路径

|||
|--|----|
| mssql/mlservices 包 | [https://packages.microsoft.com/rhel/7/mssql-server-preview/](https://packages.microsoft.com/rhel/7/mssql-server-preview/) |
| microsoft-r-open packages | [https://packages.microsoft.com/rhel/7/prod/](https://packages.microsoft.com/rhel/7/prod/) | 


#### <a name="ubuntu1604-paths"></a>Ubuntu/16.04 路径

|||
|--|----|
| mssql/mlservices 包 | [https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/) |
| microsoft-r-open packages | [https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/](https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/) | 

#### <a name="sles12-paths"></a>SLES/12 路径

|||
|--|----|
| mssql/mlservices 包 | [https://packages.microsoft.com/sles/12/mssql-server-preview/](https://packages.microsoft.com/sles/12/mssql-server-preview/) |
| microsoft-r-open packages | [https://packages.microsoft.com/sles/12/prod/](https://packages.microsoft.com/sles/12/prod/) | 

#### <a name="package-list"></a>包列表

具体取决于哪些扩展，你想要使用，请下载所需的特定语言包。 确切的文件名中使用后缀，包括平台的信息，但以下文件名称应足够接近，从而确定要获取的文件。

```
# Core packages 
mssql-server-15.0.1000
mssql-server-extensibility-15.0.1000

# Java
mssql-server-extensibility-java-15.0.1000

# R
microsoft-openmpi-3.0.0
microsoft-r-open-foreachiterators-3.4.4
microsoft-r-open-mkl-3.4.4
microsoft-r-open-mro-3.4.4
mssql-mlservices-packages-r-9.4.6.523
mssql-mlservices-mlm-r-9.4.6.523
mssql-mlservices-mml-r-9.4.6.523

# Python
microsoft-openmpi-3.0.0
mssql-mlservices-python-9.4.6.523
mssql-mlservices-packages-py-9.4.6.523
mssql-mlservices-mlm-py-9.4.6.523
mssql-mlservices-mml-py-9.4.6.523
```

#### <a name="package-list-for-original-ctp-20-and-21"></a>原始 CTP 2.0 和 2.1 的包列表

CTP 2.2 中移除**mssql mlservices mlm py**并**mssql mlservices mlm r**通过包合并到**mssql mlservices 包 py**和**mssql mlservices 包 r**分别。

如果您特别需要原始 CTP 2.0 或 2.1 包，下载以下包：

* 有关 CTP 2.0 中，下载包版本 9.4.5

* 对于 CTP 2.1，下载包版本 9.4.6.237


## <a name="add-more-rpython-packages"></a>添加更多 R/Python 包 
 
可以安装其他 R 和 Python 包，并在 SQL Server 2019 执行的脚本中使用它们。

### <a name="r-packages"></a>R 包 
 
1. 启动 R 会话。

   ```r
   # sudo /opt/mssql/mlservices/bin/R/R 
   ```

2. 安装 R 包名为[粘附](https://mran.microsoft.com/package/glue)以测试包的安装。

   ```r
   # install.packages("glue",lib="/opt/mssql/mlservices/libraries/RServer") 
   ```
   或者，可以从命令行安装 R 包 

   ```r
   # sudo /opt/mssql/mlservices/bin/R/R CMD INSTALL -l /opt/mssql/mlservices/libraries/RServer glue_1.1.1.tar.gz 
   ```

3. 导入中的 R 包[sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。

   ```r
   EXEC sp_execute_external_script  
   @language = N'R', 
   @script = N'library(glue)' 
   ```

### <a name="python-packages"></a>Python 包 
 
1. 安装名为的 Python 包[httpie](https://httpie.org/)使用 pip。 

   ```python
   # sudo /opt/mssql/mlservices/bin/python/python -m pip install httpie 
   ``` 

2. 导入中的 Python 包[sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。
 
   ```python
   EXEC sp_execute_external_script  
   @language = N'Python',  
   @script = N'import httpie' 
   ```

## <a name="limitations-in-ctp-releases"></a>在 CTP 版本中的限制

Linux 上的 R、 Python 和 Java 集成仍处于活跃开发阶段。 以下功能尚未启用的预览版本中。

+ 隐式身份验证目前不在 Linux 上的机器学习服务在此期间，这意味着您无法重新连接到服务器中访问数据或其他资源的进行中的 R 或 Python 脚本。 

+ [CREATE EXTERNAL LIBRARY](../t-sql/statements/create-external-library-transact-sql.md) （适用于在数据库中存储的 R 包） 目前不可以在 Linux 上，不支持 Python。  

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

R 开发人员可以开始使用一些简单的示例，并了解 R 如何与 SQL Server 配合工作的基础知识。 下一步，请参阅以下链接：

+ [教程：在 T-SQL 中运行 R](../advanced-analytics/tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [教程：R 开发人员的数据库内分析](../advanced-analytics/tutorials/sqldev-in-database-r-for-sql-developers.md)

Python 开发人员可以了解如何将 Python 与 SQL Server 使用按照这些教程：

+ [教程：在 T-SQL 中运行 Python](../advanced-analytics/tutorials/run-python-using-t-sql.md)
+ [教程：面向 Python 开发人员的数据库内分析](../advanced-analytics/tutorials/sqldev-in-database-python-for-sql-developers.md)

若要查看基于实际场景的机器学习示例，请参阅[机器学习教程](../advanced-analytics/tutorials/machine-learning-services-tutorials.md)。
