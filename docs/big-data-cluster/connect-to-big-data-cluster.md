---
title: 连接到主实例和 HDFS
titleSuffix: SQL Server big data clusters
description: 了解如何连接 SQL Server 主实例和 SQL Server 2019 大数据群集（预览版）的 HDFS/Spark 网关。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 05/22/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 1f09763b210427c84efe75d693fee302d7048db7
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/25/2019
ms.locfileid: "67958647"
---
# <a name="connect-to-a-sql-server-big-data-cluster-with-azure-data-studio"></a>使用 Azure Data Studio 连接到 SQL Server 大数据群集

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文介绍如何从 Azure Data Studio 连接到 SQL Server 2019 大数据群集（预览版）。

## <a name="prerequisites"></a>必备条件

- 已部署的 [SQL Server 2019 大数据群集](deployment-guidance.md)。
- [SQL Server 2019 大数据工具](deploy-big-data-tools.md)：
   - **Azure Data Studio**
   - **SQL Server 2019 扩展**
   - **kubectl**

## <a id="master"></a> 连接到群集

若要使用 Azure Data Studio 连接到大数据群集，请与群集中的 SQL Server 主实例建立新的连接。 以下步骤介绍如何使用 Azure Data Studio 连接到主实例。

1. 在命令行中，使用以下命令查找主实例的 IP：

   ```
   kubectl get svc master-svc-external -n <your-big-data-cluster-name>
   ```

   > [!TIP]
   > 除非在部署配置文件中自定义了名称，否则大数据群集名称默认为 **mssql-cluster**。 有关详细信息，请参阅[配置大数据群集的部署设置](deployment-custom-configuration.md#clustername)。

1. 在 Azure Data Studio 中，按“F1” > “新建连接”   。

1. 在“连接类型”中，选择“Microsoft SQL Server”   。

1. 在“服务器名称”中键入 SQL Server 主实例的 IP 地址（例如  ： **\<IP Address\>、31433**）。

1. 输入 SQL 登录“用户名”和“密码”   。

   > [!TIP]
   > 默认情况下，用户名为“SA”，且除非更改，否则密码对应于部署期间使用的 **MSSQL_SA_PASSWORD** 环境变量  。

1. 将目标“数据库名称”更改为你的关系数据库之一  。

   ![连接到主实例](./media/connect-to-big-data-cluster/connect-to-cluster.png)

1. 按“连接”，此时应显示“服务器仪表板”   。

借助 Azure Data Studio 2019 年 2 月版，连接到 SQL Server 主实例还使你可以与 HDFS/Spark 网关交互。 这意味着无需为下一部分介绍的 HDFS 和 Spark 使用单独的连接。

- 对象资源管理器现在包含一个新的“数据服务”节点，其为大数据群集任务提供右键单击支持，例如新建笔记本或提交 spark 作业  。 
- “数据服务”节点还包含一个“HDFS”文件夹，可用于 HDFS 探索和执行“创建外部表”或“在笔记本中进行分析”等操作   。
- 安装扩展时，连接的“服务器仪表板”还包含“SQL Server 大数据群集”和“SQL Server 2019（预览版）”选项卡    。

   ![Azure Data Studio 数据服务节点](./media/connect-to-big-data-cluster/connect-data-services-node.png)

## <a name="next-steps"></a>后续步骤

有关 SQL Server 2019 大数据群集的详细信息，请参阅[什么是 SQL Server 2019 大数据群集](big-data-cluster-overview.md)。