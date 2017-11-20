---
title: "在 Linux 上安装 SQL Server Integration Services |Microsoft 文档"
description: "本主题介绍如何在 Linux 上安装 SQL Server Integration Services (SSIS)。"
author: leolimsft
ms.author: lle
ms.reviewer: douglasl
manager: craigg
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 29122bdf543e82c1f429cf401b5fe1d8383515fc
ms.openlocfilehash: cd81ffd71eb78a553703fc31650a0e60a8c513aa
ms.contentlocale: zh-cn
ms.lasthandoff: 10/10/2017

---
# <a name="install-sql-server-integration-services-ssis-on-linux"></a>在 Linux 上安装 SQL Server Integration Services (SSIS)

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

按照本文章来安装 SQL Server Integration Services 中的步骤 (`mssql-server-is`) 在 Linux 上。 在此版本的适用于 Linux Integration Services 支持的功能的信息，请参阅[发行说明](sql-server-linux-release-notes.md)。

你为平台安装 SQL Server 集成服务器：

- [Ubuntu](#ubuntu)
- [Red Hat Enterprise Linux](#RHEL)

## <a name="ubuntu"></a>在 Ubuntu 上安装 SSIS
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
sudo apt-get remove msssql-server-is
```

## <a name="RHEL"></a>在 RHEL 上安装 SSIS
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
sudo yum remove msssql-server-is
```




## <a name="run-a-package"></a>运行包
将 SSIS 包复制到 Linux 计算机。 然后使用以下命令运行包。

```bash
dtexec /F <package name> /DE <protection password>
```



## <a name="next-steps"></a>后续步骤

有关如何在 Linux 上使用 SSIS 来提取、 转换和加载数据的详细信息，请参阅[提取、 转换和加载数据使用 SSIS 的 Linux 上的 SQL Server](sql-server-linux-migrate-ssis.md)。

