---
title: 在 Linux 上安装 PolyBase
titlesuffix: SQL Server
description: 了解如何在 Linux 上安装 SQL Server PolyBase。 PolyBase 允许针对远程数据源运行外部查询。
author: MikeRayMSFT
ms.author: mikeray
ms.date: 7/22/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
monikerRange: '>= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions'
ms.openlocfilehash: f886c1d1ae3b5054c6ca0f0159ca8202054ec375
ms.sourcegitcommit: 3ea082c778f6771b17d90fb597680ed334d3e0ec
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/11/2020
ms.locfileid: "88087345"
---
# <a name="install-polybase-on-linux"></a>在 Linux 上安装 PolyBase

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

以下步骤在 Linux 上安装 [PolyBase](../../relational-databases/search/full-text-search.md) (mssql-server-polybase)  。 PolyBase 允许针对远程数据源运行外部查询。 

>[!NOTE]
> 在安装 Polybase 前，请首先[安装 SQL Server 2019 预览版](../../linux/sql-server-linux-setup.md#platforms)。 这将配置安装 mssql-server-polybase 包时要用到的密钥和存储库  。
>
> SQL Server 2017 for Linux 不支持 PolyBase。
> 当前无法在 Linux 上对 PolyBase 进行横向扩展。

为操作系统安装 PolyBase：

- [Red Hat Enterprise Linux](#RHEL)
- [Ubuntu](#ubuntu)
- [SUSE Linux Enterprise Server](#SLES)



## <a name=""></a><a name="RHEL">在 RHEL 上安装</a>

通过下列命令在 Red Hat Enterprise Linux 上安装 mssql-server-polybase  。 

```bash
sudo yum install -y mssql-server-polybase
```

系统将提示你重启 SQL Server 实例。 使用以下命令来执行此操作。

```bash
sudo systemctl restart mssql-server
```

>[!NOTE]
>安装后，必须[启用 PolyBase 功能](#enable)。

如果需要脱机安装，请在[发行说明](../../linux/sql-server-linux-release-notes.md)中找到 PolyBase 包下载。 然后执行与文章[安装 SQL Server](../../linux/sql-server-linux-setup.md#offline) 所述相同的脱机安装步骤。

## <a name=""></a><a name="ubuntu">在 Ubuntu 上安装</a>

通过下列命令在 Ubuntu 上安装 mssql-server-polybase  。 

```bash
sudo apt-get install mssql-server-polybase
```

系统将提示你重启 SQL Server 实例。 使用以下命令来执行此操作。

```bash
sudo systemctl restart mssql-server
```

>[!NOTE]
>安装后，必须[启用 PolyBase 功能](#enable)。

如果需要脱机安装，请在[发行说明](../../linux/sql-server-linux-release-notes.md)中找到 PolyBase 包下载。 然后执行与文章[安装 SQL Server](../../linux/sql-server-linux-setup.md#offline) 所述相同的脱机安装步骤。

## <a name=""></a><a name="SLES">在 SLES 上安装</a>

通过下列命令在 SUSE Linux Enterprise Server 上安装 mssql-server-polybase  。 

```bash
sudo zypper install mssql-server-polybase
```

系统将提示你重启 SQL Server 实例。 使用以下命令来执行此操作。

```bash
sudo systemctl restart mssql-server
```

>[!NOTE]
>安装后，必须[启用 PolyBase 功能](#enable)。


如果需要脱机安装，请在[发行说明](../../linux/sql-server-linux-release-notes.md)中找到 PolyBase 包下载。 然后执行与文章[安装 SQL Server](../../linux/sql-server-linux-setup.md#offline) 所述相同的脱机安装步骤。


## <a name=""></a><a name="enable">启用 PolyBase</a> 

安装完成后，必须启用 PolyBase 来获取其功能。 连接到已安装的 SQL Server 实例并使用以下 Transact-SQL 命令进行启用。

```sql
exec sp_configure @configname = 'polybase enabled', @configvalue = 1;
RECONFIGURE WITH OVERRIDE;
```

## <a name="update-polybase"></a>更新 PolyBase

如果已安装 mssql-server-polybase，可使用下列命令将其更新至最新版本  ：

### <a name="rhel"></a>RHEL

```bash
sudo yum remove -y mssql-server-polybase
sudo yum check-update
sudo yum install -y mssql-server-polybase
```

系统将提示你重启 SQL Server 实例。 使用以下命令来执行此操作。

```
sudo systemctl restart mssql-server
```

### <a name="ubuntu"></a>Ubuntu

```bash
sudo apt-get remove mssql-server-polybase
sudo apt-get update 
sudo apt-get install mssql-server-polybase
```

系统将提示你重启 SQL Server 实例。 使用以下命令来执行此操作。

```
sudo systemctl restart mssql-server
```

### <a name="sles"></a>SLES

```bash
sudo zypper remove mssql-server-polybase
sudo zypper refresh
sudo zypper install mssql-server-polybase
```

系统将提示你重启 SQL Server 实例。 使用以下命令来执行此操作。

```
sudo systemctl restart mssql-server
```

>[!NOTE]
>安装后，必须[启用 PolyBase 功能](#enable)。

## <a name="next-steps"></a>后续步骤

Linux 上的 PolyBase 可以访问以下数据源。 遵循提供的链接，详细了解如何从已启用 PolyBase 的数据源创建外部表。 

- [SQL Server（以及 SQL 数据库、Azure SQL 数据仓库）](../../relational-databases/polybase/polybase-configure-sql-server.md)
- [Oracle](../../relational-databases/polybase/polybase-configure-oracle.md)
- [Teradata](../../relational-databases/polybase/polybase-configure-teradata.md)
- [MongoDB（和 Cosmos DB）](../../relational-databases/polybase/polybase-configure-mongodb.md)

有关如何使用它的更多信息，请参阅 [CREATE EXTERNAL TABLE](../../t-sql/statements/create-external-table-transact-sql.md) 的 Transact-SQL 参考文章。
