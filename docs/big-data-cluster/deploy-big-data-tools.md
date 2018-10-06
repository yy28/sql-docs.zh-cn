---
title: 连接到大数据群集使用 Azure Data Studio 的 SQL Server |Microsoft Docs
description: 了解如何连接到 SQL Server 2019 大数据群集使用 Azure Data Studio。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/05/2018
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: 971fc2f8e8a77b00f3d2c5cd6390fec351ffc0f3
ms.sourcegitcommit: c7d3a903eb7f410db3a0230101d24de0af17621a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2018
ms.locfileid: "48827298"
---
# <a name="connect-to-a-sql-server-big-data-cluster-with-azure-data-studio"></a>连接到 SQL Server 大数据群集使用 Azure Data Studio

本文介绍如何安装 Azure Data Studio，SQL Server 2019 扩展 （预览版），然后连接到的大数据群集。 新的 SQL Server 2019 扩展包括支持预览版[SQL Server 2019 大数据群集](big-data-cluster-overview.md)，一个集成[笔记本体验](notebooks-guidance.md)，和 PolyBase [Create External Table 向导](../relational-databases/polybase/data-virtualization.md?toc=%2fsql%2fbig-data-cluster%2ftoc.json).

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="install-azure-data-studio"></a>安装 Azure 数据 Studio

若要安装 Azure Data Studio，请参阅[下载并安装最新版本的 Azure Data Studio](../azure-data-studio/download.md)。

## <a name="install-the-sql-server-2019-extension-preview"></a>安装 SQL Server 2019 扩展 （预览版）

若要安装扩展，请参阅[安装 SQL Server 2019 扩展 （预览版）](../azure-data-studio/sql-server-2019-extension.md)。

## <a name="connect-to-the-cluster"></a>连接到群集

当连接到的大数据群集时，可以选择要连接到 SQL Server[主实例](concept-master-instance.md)或 HDFS/Spark 网关。 以下部分说明如何连接到每个。

## <a name="master-instance"></a>主实例

1. 在 Azure Data Studio，按**F1** > **新连接**。
1. 在中**连接类型**，选择**Microsoft SQL Server**。
1. 键入 SQL Server 主实例中的 IP 地址**服务器名称**(例如：  **\<IP 地址\>、 31433**)。
1. 更改**数据库名称**到**high_value_data**数据库。

   ![连接到主实例](./media/deploy-big-data-tools/connect-to-cluster.png)

1. 按**Connect**，并**Server 仪表板**应显示。

## <a name="hdfsspark-gateway"></a>HDFS/Spark 网关

1. 在 Azure Data Studio，按**F1** > **新连接**。
1. 在中**连接类型**，选择**SQL Server 大数据群集**。
1. 键入中的大数据群集的 IP 地址**服务器名称**。

   ![连接到 HDFS/Spark 网关](./media/deploy-big-data-tools/connect-to-cluster-hdfs-spark.png)

1. 按**Connect**，并**Server 仪表板**应显示。

## <a name="next-steps"></a>后续步骤

若要在 Azure Data Studio 中运行 notebook，请参阅[如何在 SQL Server 2019 预览版中使用笔记本](notebooks-guidance.md)。
