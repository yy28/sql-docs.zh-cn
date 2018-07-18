---
title: 在 Linux 上安装 SQL Server Integration Services |Microsoft 文档
description: 本文介绍如何在 Linux 上安装 SQL Server Integration Services (SSIS)。
author: leolimsft
ms.author: lle
ms.reviewer: douglasl
manager: craigg
ms.date: 01/09/2018
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.openlocfilehash: d2e72c77ad5f200c07a6e71025a3461d6397032a
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2018
ms.locfileid: "34323388"
---
# <a name="install-sql-server-integration-services-ssis-on-linux"></a>在 Linux 上安装 SQL Server Integration Services (SSIS)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

按照本文章来安装 SQL Server Integration Services 中的步骤 (`mssql-server-is`) 在 Linux 上。 在此版本的适用于 Linux Integration Services 支持的功能的信息，请参阅[发行说明](sql-server-linux-release-notes.md)。

你为平台安装 SQL Server 集成服务器：

- [Ubuntu](#ubuntu)
- [Red Hat Enterprise Linux](#RHEL)

## <a name="ubuntu"></a> 在 Ubuntu 上安装 SSIS
若要安装`mssql-server-is`打包在 Ubuntu 上，执行以下步骤：

1. 导入公共存储库 GPG 密钥。

   ```bash
   curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

2. 注册 Microsoft SQL Server Ubuntu 存储库。

   ```bash
   sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017.list)"
   ```

3. 运行以下命令以安装 SQL Server Integration Services。

   ```bash
   sudo apt-get update
   sudo apt-get install -y mssql-server-is
   ```

4. 安装 Integration Services 以后, 运行`ssis-conf`。 有关详细信息，请参阅[与 ssis conf Linux 上配置 SSIS](sql-server-linux-configure-ssis.md)。

   ```bash
   sudo /opt/ssis/bin/ssis-conf setup
   ```

5. 完成配置后，设置的路径。

   ```bash
   export PATH=/opt/ssis/bin:$PATH
   ```

### <a name="update-ssis"></a>更新 SSIS
如果你已有`mssql-server-is`安装，你可以更新到最新版本使用以下命令：

```bash
sudo apt-get install mssql-server-is
```

### <a name="remove-ssis"></a>删除 SSIS
若要删除`mssql-server-is`，可以运行以下命令：
```bash
sudo apt-get remove mssql-server-is
```

## <a name="RHEL"></a> 在 RHEL 上安装 SSIS
若要安装`mssql-server-is`打包在 RHEL 上，执行以下步骤：

1. 下载 Microsoft SQL Server Red Hat 存储库配置文件。

   ```bash
   sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017.repo
   ```

1. 运行以下命令以安装 SQL Server Integration Services。

   ```bash
   sudo yum install -y mssql-server-is
   ```


1. 安装完成后，运行`ssis-conf`。 有关详细信息，请参阅[与 ssis conf Linux 上配置 SSIS](sql-server-linux-configure-ssis.md)。

   ```bash
   sudo /opt/ssis/bin/ssis-conf setup
   ```

1. 完成配置后，将路径设置。

   ```bash
   export PATH=/opt/ssis/bin:$PATH
   ```

### <a name="update-ssis"></a>更新 SSIS
如果你已有`mssql-server-is`安装，你可以更新到最新版本使用以下命令：

```bash
sudo yum update mssql-server-is
```

### <a name="remove-ssis"></a>删除 SSIS
若要删除`mssql-server-is`，可以运行以下命令：
```bash
sudo yum remove mssql-server-is
```

## <a name="unattended-installation"></a>无人参与的安装
若要在运行时运行无人参与的安装`ssis-conf setup`，执行以下操作：
1.  指定`-n`（无提示） 选项。
2.  通过设置环境变量来提供所需的值。

下面的示例将执行以下操作：
-   安装 SSIS。
-   通过提供的值指定开发人员版`SSIS_PID`环境变量。
-   通过提供的值接受 EULA`ACCEPT_EULA`环境变量。
-   通过指定运行无人参与的安装`-n`（无提示） 选项。

```
sudo SSIS_PID=Developer ACCEPT_EULA=Y /opt/ssis/bin/ssis-conf -n setup 
```

### <a name="environment-variables-for-unattended-installation"></a>无人参与安装的环境变量

| 环境变量 | Description |
|---|---|
| **ACCEPT_EULA** | 接受 SQL Server 许可协议时设置为任何值 (例如， `Y`)。|
| **SSIS_PID** | 设置 SQL Server 版本或产品密钥。 下面是可能的值：<br/>Evaluation<br/>开发人员<br/>Express <br/>Web <br/>Standard<br/>Enterprise <br/>产品密钥<br/><br/>如果指定的产品密钥，产品密钥必须是形式`#####-#####-#####-#####-#####`，其中`#`是字母或数字。  |
| | |

## <a name="next-steps"></a>后续步骤

若要在 Linux 上运行 SSIS 包，请参阅[提取、 转换和加载数据使用 SSIS 的 Linux 上的 SQL Server](sql-server-linux-migrate-ssis.md)。

若要在 Linux 上配置其他 SSIS 设置，请参阅[配置与 ssis conf Linux 上 SQL Server Integration Services](sql-server-linux-configure-ssis.md)。

## <a name="related-content-about-ssis-on-linux"></a>有关在 Linux 上的 SSIS 的相关的内容
-   [提取、 转换和加载使用 SSIS 的 Linux 上的数据](sql-server-linux-migrate-ssis.md)
-   [使用 ssis conf 在 Linux 上配置 SQL Server Integration Services](sql-server-linux-configure-ssis.md)
-   [限制和 Linux 上的 SSIS 的已知的问题](sql-server-linux-ssis-known-issues.md)
-   [计划 SQL Server Integration Services 包执行在 Linux 上的使用 cron](sql-server-linux-schedule-ssis-packages.md)
