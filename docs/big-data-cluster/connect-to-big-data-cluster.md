---
title: 连接到主实例和 HDFS 大数据群集
description: 了解如何连接到 SQL Server 主实例和 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] 的 HDFS/Spark 网关。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 0717226ee785df568d4cea75511e65acb728c592
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/04/2019
ms.locfileid: "73532242"
---
# <a name="connect-to-a-sql-server-big-data-cluster-with-azure-data-studio"></a>使用 Azure Data Studio 连接到 SQL Server 大数据群集

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文介绍如何从 Azure Data Studio 连接到 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]。

## <a name="prerequisites"></a>必备条件

- 已部署的 [SQL Server 2019 大数据群集](deployment-guidance.md)。
- [SQL Server 2019 大数据工具](deploy-big-data-tools.md)：
   - **Azure Data Studio**
   - **SQL Server 2019 扩展**
   - **kubectl**
   - **azdata**

## <a id="master"></a> 连接到群集

若要使用 Azure Data Studio 连接到大数据群集，请与群集中的 SQL Server 主实例建立新的连接。 以下步骤介绍如何使用 Azure Data Studio 连接到主实例。

1. 查找 SQL Server 主实例终结点：

   ```
   azdata bdc endpoint list -e sql-server-master
   ```

   > [!TIP]
   > 有关如何检索终结点的详细信息，请参阅[检索终结点](deployment-guidance.md#endpoints)。

1. 在 Azure Data Studio 中，按“F1” > “新建连接”   。

1. 在“连接类型”中，选择“Microsoft SQL Server”   。

1. 在“服务器名称”文本框中键入为 SQL Server 主实例找到的终结点名称（例如  ： **\<IP_Address\>31433**。 

1. 选择身份验证类型。 对于在大数据群集中运行的 SQL Server 主实例，仅支持 Windows 身份验证和 SQL 登录   。 

1. 输入 SQL 登录用户名和密码   。 如果使用的是 Windows 身份验证，则不需要这样做。

   > [!TIP]
   > 默认情况下，用户名 SA 在大数据群集部署过程中处于禁用状态  。 在部署期间预配一个新的 sysadmin 用户，其名称对应于 AZDATA_USERNAME 环境变量，其密码对应于部署期间使用的 AZDATA_PASSWORD 环境变量   。

1. 将目标“数据库名称”更改为你的关系数据库之一  。

   ![连接到主实例](./media/connect-to-big-data-cluster/connect-to-cluster.png)

1. 按“连接”，此时应显示“服务器仪表板”   。

借助 Azure Data Studio 2019 年 2 月版，连接到 SQL Server 主实例还使你可以与 HDFS/Spark 网关交互。 这意味着无需为下一部分介绍的 HDFS 和 Spark 使用单独的连接。

- 对象资源管理器现在包含一个新的“数据服务”节点，其为大数据群集任务提供右键单击支持，例如新建笔记本或提交 spark 作业  。 
- “数据服务”节点还包含一个“HDFS”文件夹，可用于 HDFS 探索和执行“创建外部表”或“在笔记本中进行分析”等操作   。
- 安装扩展时，连接的“服务器仪表板”还包含“SQL Server 大数据群集”和“SQL Server 2019（预览版）”选项卡    。

   ![Azure Data Studio 数据服务节点](./media/connect-to-big-data-cluster/connect-data-services-node.png)

## <a name="next-steps"></a>后续步骤

有关 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] 的详细信息，请参阅[什么是 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]](big-data-cluster-overview.md)。
