---
title: 加载示例数据
titleSuffix: SQL Server 2019 big data clusters
description: 本教程演示如何将示例数据加载到 SQL Server 大数据群集。 示例数据在 SQL Server 主实例中包括关系数据。 它还包括在存储池中的 HDFS 数据。 在本部分中，此数据支持的其他教程。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 01/17/2019
ms.topic: tutorial
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 207d2d01278d96456bcec44814efe76fdae70fdf
ms.sourcegitcommit: e3f5b70bbb4c66294df8c7b2c70186bdf2365af9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/18/2019
ms.locfileid: "54397506"
---
# <a name="tutorial-load-sample-data-into-a-sql-server-2019-big-data-cluster"></a>教程：将示例数据加载到 SQL Server 2019 大数据群集

本教程介绍如何使用脚本将示例数据加载到 SQL Server 2019 大数据群集 （预览版）。 许多其他教程文档中使用此示例数据。

> [!TIP]
> 可以在 SQL Server 2019 大数据群集 （预览版） 的其他示例中找到[sql server 示例](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster)GitHub 存储库。 这些文件位于**sql-server-samples/samples/features/sql-big-data-cluster/** 路径。

## <a name="prerequisites"></a>先决条件

- [已部署的大数据群集](deployment-guidance.md)
- [大数据工具](deploy-big-data-tools.md)
   - **mssqlctl**
   - **kubectl**
   - **sqlcmd**
   - **curl**

## <a id="sampledata"></a> 加载示例数据

以下步骤使用启动脚本下载 SQL Server 数据库备份，并将数据加载到你的大数据群集。 为了方便使用，这些步骤的部分具有已分解到[Windows](#windows)并[Linux](#linux)部分。

## <a id="windows"></a> Windows

以下步骤介绍如何使用 Windows 客户端将示例数据加载到你的大数据群集。

1. 打开新的 Windows 命令提示符。

   > [!IMPORTANT]
   > 对于这些步骤不使用 Windows PowerShell。 在 PowerShell 中，该脚本将失败，因为它将使用的 PowerShell 版本**curl**。

1. 使用**curl**若要下载示例数据的启动脚本。

   ```cmd
   curl -o bootstrap-sample-db.cmd "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.cmd"
   ```

1. 下载**bootstrap 示例 db.sql** Transact SQL 脚本。 启动脚本通过调用此脚本。

   ```cmd
   curl -o bootstrap-sample-db.sql "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.sql"
   ```

1. 启动脚本需要大数据群集的以下位置参数：

   | 参数 | Description |
   |---|---|
   | <CLUSTER_NAMESPACE> | 提供你的大数据群集的名称。 |
   | <SQL_MASTER_IP> | 主实例的 IP 地址。 |
   | <SQL_MASTER_SA_PASSWORD> | 主实例 SA 密码。 |
   | <KNOX_IP> | HDFS/Spark 网关的 IP 地址。 |
   | <KNOX_PASSWORD> | HDFS/Spark 网关的密码。 |

   > [!TIP]
   > 使用[kubectl](cluster-troubleshooting-commands.md)以查找 SQL Server 主实例和 Knox 的 IP 地址。 运行`kubectl get svc -n <your-cluster-name>`并查看主实例的外部 IP 地址 (**终结点的主池**) 和 Knox (**服务-安全性-l b**或**服务-安全性-nodeport**).

1. 运行启动脚本。

   ```cmd
   .\bootstrap-sample-db.cmd <CLUSTER_NAMESPACE> <SQL_MASTER_IP> <SQL_MASTER_SA_PASSWORD> <KNOX_IP> <KNOX_PASSWORD>
   ```

## <a id="linux"></a> Linux

以下步骤介绍如何使用 Linux 客户端将示例数据加载到你的大数据群集。

1. 下载该启动脚本，并为其分配可执行文件的权限。

   ```bash
   curl -o bootstrap-sample-db.sh "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.sh"
   chmod +x bootstrap-sample-db.sh
   ```

1. 下载**bootstrap 示例 db.sql** Transact SQL 脚本。 启动脚本通过调用此脚本。

   ```bash
   curl -o bootstrap-sample-db.sql "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.sql"
   ```

1. 启动脚本需要大数据群集的以下位置参数：

   | 参数 | Description |
   |---|---|
   | <CLUSTER_NAMESPACE> | 提供你的大数据群集的名称。 |
   | <SQL_MASTER_IP> | 主实例的 IP 地址。 |
   | <SQL_MASTER_SA_PASSWORD> | 主实例 SA 密码。 |
   | <KNOX_IP> | HDFS/Spark 网关的 IP 地址。 |
   | <KNOX_PASSWORD> | HDFS/Spark 网关的密码。 |

   > [!TIP]
   > 使用[kubectl](cluster-troubleshooting-commands.md)以查找 SQL Server 主实例和 Knox 的 IP 地址。 运行`kubectl get svc -n <your-cluster-name>`并查看主实例的外部 IP 地址 (**终结点的主池**) 和 Knox (**服务-安全性-l b**或**服务-安全性-nodeport**).

1. 运行启动脚本。

   ```bash
   sudo env "PATH=$PATH" ./bootstrap-sample-db.sh <CLUSTER_NAMESPACE> <SQL_MASTER_IP> <SQL_MASTER_SA_PASSWORD> <KNOX_IP> <KNOX_PASSWORD>
   ```

## <a name="next-steps"></a>后续步骤

启动脚本运行大数据群集后，示例数据库和 HDFS 的数据。 若要开始浏览此数据和大数据群集，请参阅[教程](tutorial-query-hdfs-storage-pool.md)在本部分中。
