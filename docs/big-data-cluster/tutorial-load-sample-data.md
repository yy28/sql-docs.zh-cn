---
title: 加载示例数据
titleSuffix: SQL Server big data clusters
description: 本教程演示如何将示例数据加载到 SQL Server 大数据群集。 示例数据包括 SQL Server 主实例中的关系数据。 它还在存储池中包含 HDFS 数据。 此数据支持本部分中的其他教程。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: tutorial
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 5b35eccece4df47cb483932386cf6a38e45d2dc8
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419275"
---
# <a name="tutorial-load-sample-data-into-a-sql-server-big-data-cluster"></a>教程：将示例数据加载到 SQL Server 大数据群集

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本教程介绍如何使用脚本将示例数据加载到 SQL Server 2019 大数据群集 (预览版) 中。 文档中的许多其他教程使用此示例数据。

> [!TIP]
> 可在[SQL Server 示例](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster)GitHub 存储库中找到 SQL Server 2019 大数据群集 (预览版) 的其他示例。 它们位于 " **sql-服务器-示例/示例/功能/sql-大数据-群集/** 路径" 中。

## <a name="prerequisites"></a>先决条件

- [部署的大数据群集](deployment-guidance.md)
- [大数据工具](deploy-big-data-tools.md)
   - **azdata**
   - **kubectl**
   - **sqlcmd**
   - **curl**

## <a id="sampledata"></a>加载示例数据

以下步骤使用启动脚本下载 SQL Server 数据库备份, 并将数据加载到大数据群集。 为了便于使用, 这些步骤已划分为[Windows](#windows)和[Linux](#linux)部分。

## <a id="windows"></a> Windows

以下步骤介绍如何使用 Windows 客户端将示例数据加载到大数据群集。

1. 打开新的 Windows 命令提示符。

   > [!IMPORTANT]
   > 请勿使用 Windows PowerShell 执行这些步骤。 在 PowerShell 中, 脚本将失败, 因为它将使用**卷**的 PowerShell 版本。

1. 使用 "**卷**" 可下载示例数据的启动脚本。

   ```cmd
   curl -o bootstrap-sample-db.cmd "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.cmd"
   ```

1. 下载**bootstrap-sample-db** sql 脚本。 此脚本由启动脚本调用。

   ```cmd
   curl -o bootstrap-sample-db.sql "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.sql"
   ```

1. 启动脚本需要适用于大数据分类的以下位置参数:

   | 参数 | 描述 |
   |---|---|
   | <CLUSTER_NAMESPACE> | 你为大数据群集提供的名称。 |
   | <SQL_MASTER_IP> | 主实例的 IP 地址。 |
   | <SQL_MASTER_SA_PASSWORD> | 主实例的 SA 密码。 |
   | <KNOX_IP> | HDFS/Spark 网关的 IP 地址。 |
   | <KNOX_PASSWORD> | HDFS/Spark 网关的密码。 |

   > [!TIP]
   > 使用[kubectl](cluster-troubleshooting-commands.md)查找 SQL Server master 实例和 KNOX 的 IP 地址。 运行`kubectl get svc -n <your-big-data-cluster-name>`并查看主实例的外部 IP 地址 (**主-svc-外部**) 和 Knox (**网关-svc-外部**)。 群集的默认名称为 " **mssql-群集**"。

1. 运行启动脚本。

   ```cmd
   .\bootstrap-sample-db.cmd <CLUSTER_NAMESPACE> <SQL_MASTER_IP> <SQL_MASTER_SA_PASSWORD> <KNOX_IP> <KNOX_PASSWORD>
   ```

## <a id="linux"></a> Linux

以下步骤介绍如何使用 Linux 客户端将示例数据加载到大数据群集。

1. 下载并向其分配可执行文件的权限。

   ```bash
   curl -o bootstrap-sample-db.sh "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.sh"
   chmod +x bootstrap-sample-db.sh
   ```

1. 下载**bootstrap-sample-db** sql 脚本。 此脚本由启动脚本调用。

   ```bash
   curl -o bootstrap-sample-db.sql "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.sql"
   ```

1. 启动脚本需要适用于大数据分类的以下位置参数:

   | 参数 | 描述 |
   |---|---|
   | <CLUSTER_NAMESPACE> | 你为大数据群集提供的名称。 |
   | <SQL_MASTER_IP> | 主实例的 IP 地址。 |
   | <SQL_MASTER_SA_PASSWORD> | 主实例的 SA 密码。 |
   | <KNOX_IP> | HDFS/Spark 网关的 IP 地址。 |
   | <KNOX_PASSWORD> | HDFS/Spark 网关的密码。 |

   > [!TIP]
   > 使用[kubectl](cluster-troubleshooting-commands.md)查找 SQL Server master 实例和 KNOX 的 IP 地址。 运行`kubectl get svc -n <your-big-data-cluster-name>`并查看主实例的外部 IP 地址 (**主-svc-外部**) 和 Knox (**网关-svc-外部**)。 群集的默认名称为 " **mssql-群集**"。

1. 运行启动脚本。

   ```bash
   sudo env "PATH=$PATH" ./bootstrap-sample-db.sh <CLUSTER_NAMESPACE> <SQL_MASTER_IP> <SQL_MASTER_SA_PASSWORD> <KNOX_IP> <KNOX_PASSWORD>
   ```

## <a name="next-steps"></a>后续步骤

在启动脚本运行后, 大数据群集将包含示例数据库和 HDFS 数据。 以下教程使用示例数据来演示大数据群集功能:

数据虚拟化:

- [教程：在 SQL Server 大数据群集中查询 HDFS](tutorial-query-hdfs-storage-pool.md)
- [教程：从 SQL Server 大数据群集查询 Oracle](tutorial-query-oracle.md)

数据引入:

- [教程：使用 Transact-sql 将数据引入 SQL Server 数据池](tutorial-data-pool-ingest-sql.md)
- [教程：使用 Spark 作业将数据引入到 SQL Server 的数据池中](tutorial-data-pool-ingest-spark.md)

记事本

- [教程：在 SQL Server 2019 大数据群集上运行示例笔记本](tutorial-notebook-spark.md)