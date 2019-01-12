---
title: 连接到主服务器和 HDFS
titleSuffix: SQL Server 2019 big data clusters
description: 了解如何连接到 SQL Server 主实例和 SQL Server 2019 大数据群集 （预览版） 的 HDFS/Spark 网关。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 12/10/2018
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: 4d3ca6a3e43781b35bfd24f04ee1cf0483b1eb05
ms.sourcegitcommit: 1f53b6a536ccffd701fc87e658ddac714f6da7a2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/10/2019
ms.locfileid: "54206263"
---
# <a name="connect-to-a-sql-server-big-data-cluster-with-azure-data-studio"></a>连接到 SQL Server 大数据群集使用 Azure Data Studio

本文介绍如何从 Azure Data Studio 连接到 SQL Server 2019 大数据群集 （预览版）。

## <a name="prerequisites"></a>先决条件

- 已部署[SQL Server 2019 大数据群集](deployment-guidance.md)。
- [SQL Server 2019 大数据工具](deploy-big-data-tools.md):
   - **Azure Data Studio**
   - **SQL Server 2019 扩展**
   - **Kubectl**

## <a name="connect-to-the-cluster"></a>连接到群集

当连接到的大数据群集时，可以选择要连接到 SQL Server 主实例或 HDFS/Spark 网关。 以下部分说明如何连接到每个。

## <a id="master"></a> 主实例

SQL Server 主实例是包含关系的 SQL Server 数据库的传统 SQL Server 实例。 以下步骤介绍如何连接到使用 Azure Data Studio 的主实例。

1. 从命令行中，查找使用以下命令在主实例的 IP:

   ```
   kubectl get svc endpoint-master-pool -n <your-cluster-name>
   ```

1. 在 Azure Data Studio，按**F1** > **新连接**。

1. 在中**连接类型**，选择**Microsoft SQL Server**。

1. 键入 SQL Server 主实例中的 IP 地址**服务器名称**(例如：**\<IP 地址\>、 31433**)。

1. 输入 SQL 登录名**用户名**并**密码**。

   > [!TIP]
   > 默认情况下，用户名称是**SA**和密码更改，除非对应于**MSSQL_SA_PASSWORD**部署过程中使用的环境变量。

1. 将目标更改**数据库名称**到一个关系数据库。

   ![连接到主实例](./media/connect-to-big-data-cluster/connect-to-cluster.png)

1. 按**Connect**，并**Server 仪表板**应显示。

## <a id="hdfs"></a> HDFS/Spark 网关

**HDFS/Spark 网关**使你能够连接才能与 HDFS 存储池和运行 Spark 作业。 以下步骤介绍如何使用 Azure Data Studio 进行连接。

1. 从命令行中，查找使用以下命令之一 HDFS/Spark 网关的 IP 地址。
   
   **AKS 部署：**

   ```
   kubectl get svc service-security-lb -n <your-cluster-name>
   ```

   **非 AKS 部署**:

   ```
   kubectl get svc service-security-nodeport -n <your-cluster-name>
   ```
 
1. 在 Azure Data Studio，按**F1** > **新连接**。

1. 在中**连接类型**，选择**SQL Server 大数据群集**。

   > [!TIP]
   > 如果没有看到**SQL Server 大数据群集**连接类型，请确保已安装[SQL Server 2019 扩展](../azure-data-studio/sql-server-2019-extension.md)和已完成的扩展后重启 Azure Data Studio正在安装。

1. 键入中的大数据群集的 IP 地址**服务器名称**（不指定端口）。

1. 输入`root`有关**用户**并指定**密码**到大数据群集。

   ![连接到 HDFS/Spark 网关](./media/connect-to-big-data-cluster/connect-to-cluster-hdfs-spark.png)

   > [!TIP]
   > 默认情况下，用户名称是**根**和密码对应于**KNOX_PASSWORD**部署过程中使用的环境变量。

1. 按**Connect**，并**Server 仪表板**应显示。

## <a name="next-steps"></a>后续步骤

有关 SQL Server 2019 大数据群集的详细信息，请参阅[什么是 SQL Server 2019 大数据群集](big-data-cluster-overview.md)。