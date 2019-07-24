---
title: 查看群集状态
titleSuffix: SQL Server big data clusters
description: 本文介绍如何使用 Azure Data Studio、笔记本和 azdata 命令查看大数据群集的状态。
author: yualan
ms.author: alayu
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: c6dca94b8bd7547222394d7809cb003b9e936982
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419287"
---
# <a name="how-to-view-the-status-of-a-big-data-cluster"></a>如何查看大数据群集的状态

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文介绍如何访问服务终结点, 以及如何查看 SQL Server 大数据群集 (预览版) 的状态。 可以同时使用 Azure Data Studio 和**azdata**, 本文将介绍这两种方法。

## <a id="datastudio"></a>使用 Azure Data Studio

下载[Azure Data Studio](https://aka.ms/azdata-insiders)的最新内部**版本**后, 可以使用 SQL Server 大数据群集仪表板查看服务终结点以及大数据群集的状态。 请注意, 下面的某些功能仅在 Azure Data Studio 的预览体验内部版本中可用。

1. 首先, 在 Azure Data Studio 中创建到大数据群集的连接。 有关详细信息, 请参阅[使用 Azure Data Studio 连接到 SQL Server 大数据群集](connect-to-big-data-cluster.md)。

1. 右键单击大数据群集终结点, 然后单击 "**管理**"。

   ![右键单击 "管理"](media/view-cluster-status/right-click-manage.png)

1. 选择 " **SQL Server 大数据分类**" 选项卡以访问大数据群集仪表板。

   ![大数据群集仪表板](media/view-cluster-status/bdc-dashboard.png)

### <a name="service-endpoints"></a>服务终结点

很重要的一点是, 能够轻松访问大数据群集中的各种服务。 大数据群集仪表板提供了一个服务终结点表, 可用于查看和复制服务终结点。

![服务终结点](media/view-cluster-status/service-endpoints.png)

前几行公开了以下服务:

- 应用程序代理
- 群集管理服务
- HDFS 和 Spark
- 管理代理

当你需要用于连接到这些服务的终结点时, 这些服务会列出可以复制和粘贴的终结点。 例如, 可以单击终结点右侧的 "复制" 图标, 然后将其粘贴到请求该终结点的文本窗口中。 群集管理服务终结点对于运行[群集状态笔记本](#notebook)是必需的。

### <a name="dashboards"></a>仪表板

"服务终结点" 表还公开了多个仪表板用于监视:

- 度量值 (Grafana)
- 日志 (Kibana)
- Spark 作业监视
- Spark 资源管理

可以直接单击这些链接。 在连接到服务前, 系统会提示你提供用户名和密码两次。

### <a id="notebook"></a>群集状态笔记本

1. 你还可以通过启动群集状态笔记本来查看大数据群集的群集状态。 若要启动笔记本, 请单击 "**群集状态**" 任务。

    ![开始](media/view-cluster-status/cluster-status-launch.png)

2. 在开始之前, 你将需要以下项:

    - 大数据群集名称
    - 控制器用户名
    - 控制器密码
    - 控制器终结点

    除非在部署过程中对其进行了自定义, 否则默认大数据群集名称为**mssql 群集**名称。 可以在 "服务终结点" 表的 "大数据群集" 仪表板中找到控制器终结点。 此终结点作为**群集管理服务**列出。 如果你不知道凭据, 请要求管理员部署群集。

3. 单击顶部工具栏中的 "**运行单元**"。

4. 按照提示输入凭据。 为大数据群集名称、控制器用户名和控制器密码键入每个凭据后, 按 enter。

    > [!Note]
    > 如果你没有使用大数据的配置文件设置, 将要求你提供控制器终结点。 键入或粘贴它, 然后按 ENTER 继续。

5. 如果成功连接, 则笔记本的其余部分将显示大数据分类的每个组件的输出。 如果要重新运行某个代码单元格, 请将鼠标悬停在代码单元上, 并单击 "**运行**" 图标。

## <a name="use-azdata"></a>使用 azdata

你还可以使用[azdata](deploy-install-azdata.md)命令来查看终结点和群集状态。

### <a name="service-endpoints"></a>服务终结点

可以使用以下步骤获取大数据群集的外部终结点的 IP 地址。

1. 查看以下**kubectl**命令的外部 IP 输出, 查找控制器终结点的 IP 地址:

   ```bash
   kubectl get svc controller-svc-external -n <your-big-data-cluster-name>
   ```

   > [!TIP]
   > 如果在部署过程中没有更改默认名称, 请在`-n mssql-cluster`上一个命令中使用。 **mssql-群集**是大数据群集的默认名称。

1. 通过[azdata 登录名](reference-azdata.md)登录到大数据群集。 将 **--controller-endpoint**参数设置为控制器终结点的外部 IP 地址。

   ```bash
   azdata login --controller-endpoint https://<ip-address-of-controller-svc-external>:30080 --controller-username <user-name>
   ```

   指定在部署过程中为控制器配置的用户名和密码 (CONTROLLER_USERNAME 和 CONTROLLER_PASSWORD)。

1. 运行[azdata bdc endpoint list](reference-azdata-bdc-endpoint.md) , 以获取一个列表, 其中列出了每个终结点及其对应的 IP 地址和端口值。 

   ```bash
   azdata bdc endpoint list -o table
   ```

   以下列表显示了此命令的示例输出:

   ```output
   Description                                             Endpoint                                                   Ip              Name               Port    Protocol
   ------------------------------------------------------  ---------------------------------------------------------  --------------  -----------------  ------  ----------
   Gateway to access HDFS files, Spark                     https://11.111.111.111:30443                               11.111.111.111  gateway            30443   https
   Spark Jobs Management and Monitoring Dashboard          https://11.111.111.111:30443/gateway/default/sparkhistory  11.111.111.111  spark-history      30443   https
   Spark Diagnostics and Monitoring Dashboard              https://11.111.111.111:30443/gateway/default/yarn          11.111.111.111  yarn-ui            30443   https
   Application Proxy                                       https://11.111.111.111:30778                               11.111.111.111  app-proxy          30778   https
   Management Proxy                                        https://11.111.111.111:30777                               11.111.111.111  mgmtproxy          30777   https
   Log Search Dashboard                                    https://11.111.111.111:30777/kibana                        11.111.111.111  logsui             30777   https
   Metrics Dashboard                                       https://11.111.111.111:30777/grafana                       11.111.111.111  metricsui          30777   https
   Cluster Management Service                              https://11.111.111.111:30080                               11.111.111.111  controller         30080   https
   SQL Server Master Instance Front-End                    11.111.111.111,31433                                       11.111.111.111  sql-server-master  31433   tcp
   HDFS File System Proxy                                  https://11.111.111.111:30443/gateway/default/webhdfs/v1    11.111.111.111  webhdfs            30443   https
   Proxy for running Spark statements, jobs, applications  https://11.111.111.111:30443/gateway/default/livy/v1       11.111.111.111  livy               30443   https
   ```

### <a name="view-cluster-status"></a>查看群集状态

可以通过[azdata bdc status show](reference-azdata-bdc-status.md)命令查看群集的状态。

```bash
azdata bdc status show -o table
```

> [!TIP]
> 若要运行状态命令, 你必须先用 "前面的终结点" 部分中显示的**azdata login**命令登录。

下面显示了此命令的示例输出:

```output
Kind     Name           State
-------  -------------  -------
BDC      mssql-cluster  Ready
Control  default        Ready
Master   default        Ready
Compute  default        Ready
Data     default        Ready
Storage  default        Ready
```

### <a name="view-pool-status"></a>查看池状态

可以在群集中通过 " [azdata bdc 池状态显示](reference-azdata-bdc-pool-status.md)" 命令查看池的状态。 若要使用此命令, 请使用`--kind`参数指定池的类型。 池类型为:

- 计算
- data
- master
- 激发
- 储存

例如, 以下命令显示存储池的池状态:

```bash
azdata bdc pool status show --kind storage
```

应会看到类似于以下输出的文本:

```output
[
  {
    "kind": "Pod",
    "logsUrl": "https://11.111.111.111:30080/clusters/mssql-cluster/pods/storage-0-0/logs/ui",
    "name": "storage-0-0",
    "nodeMetricsUrl": "https://11.111.111.111:30080/clusters/mssql-cluster/pods/storage-0-0/nodemetrics/ui",
    "sqlMetricsUrl": "https://11.111.111.111:30080/clusters/mssql-cluster/pods/storage-0-0/sqlmetrics/ui",
    "state": "Running"
  },
  {
    "kind": "Pod",
    "logsUrl": "https://11.111.111.111:30080/clusters/mssql-cluster/pods/storage-0-1/logs/ui",
    "name": "storage-0-1",
    "nodeMetricsUrl": "https://11.111.111.111:30080/clusters/mssql-cluster/pods/storage-0-1/nodemetrics/ui",
    "sqlMetricsUrl": "https://11.111.111.111:30080/clusters/mssql-cluster/pods/storage-0-1/sqlmetrics/ui",
    "state": "Running"
  }
]
```

`logsUrl`值链接到具有日志信息的 kibana 仪表板:

![Kibana 仪表板](./media/view-cluster-status/kibana-dashboard.png)

`nodeMetricsUrl` 和`sqlMetricsUrl`值链接到用于监视节点运行状况和 SQL 指标的 grafana 仪表板:

![Grafana 仪表板](./media/view-cluster-status/grafana-dashboard.png)

![SQL](./media/view-cluster-status/grafana-sql-status.png)

### <a name="view-controller-status"></a>查看控制器状态

可以查看控制器状态并[显示 "azdata bdc control status show](reference-azdata-bdc-control-status.md) " 命令。 它提供与大数据群集的控制器节点相关的监视仪表板的链接。

## <a name="next-steps"></a>后续步骤

有关大数据群集的详细信息, 请参阅[什么是 SQL Server 大数据群集](big-data-cluster-overview.md)。
