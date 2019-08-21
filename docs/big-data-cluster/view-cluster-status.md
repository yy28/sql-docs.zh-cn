---
title: 查看群集状态
titleSuffix: SQL Server big data clusters
description: 本文介绍如何使用 Azure Data Studio、笔记本和 azdata 命令查看大数据群集的状态。
author: yualan
ms.author: alayu
ms.reviewer: mikeray
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 028864712658e35913fa04fb1a85e4ca960ad573
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2019
ms.locfileid: "69653275"
---
# <a name="how-to-view-the-status-of-a-big-data-cluster"></a>如何查看大数据群集的状态

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文介绍如何访问服务终结点，以及如何查看 SQL Server 大数据群集的状态（预览）。 可以同时使用 Azure Data Studio 和 azdata，本文会介绍这两种方法。

## <a id="datastudio"></a> 使用 Azure Data Studio

下载 [Azure Data Studio](https://aka.ms/azdata-insiders) 的最新**预览体验内部版本**后，可以使用 SQL Server 大数据群集仪表板查看服务终结点以及大数据群集的状态。 请注意，下面的某些功能仅在 Azure Data Studio 的预览体验内部版本中可用。

1. 首先，在 Azure Data Studio 中创建到大数据群集的连接。 有关详细信息，请参阅[使用 Azure Data Studio 连接到 SQL Server 大数据群集](connect-to-big-data-cluster.md)。

1. 右键单击大数据群集终结点，然后单击“管理”。

   ![右键单击管理](media/view-cluster-status/right-click-manage.png)

1. 选择“SQL Server 大数据群集”选项卡访问大数据群集仪表板。

   ![大数据群集仪表板](media/view-cluster-status/bdc-dashboard.png)

### <a name="service-endpoints"></a>服务终结点

能够轻松访问大数据群集中的各项服务很重要。 大数据群集仪表板提供了一个服务终结点表，可用于查看和复制服务终结点。

![服务终结点](media/view-cluster-status/service-endpoints.png)

前几行公开了以下服务：

- 应用程序代理
- 群集管理服务
- HDFS 和 Spark
- 管理代理

当需要可用于连接这些服务的终结点时，这些服务会列出可以复制和粘贴的终结点。 例如，可以单击终结点右侧的复制图标，然后将其粘贴到请求该终结点的文本窗口中。 要运行[群集状态笔记本](#notebook)，群集管理服务终结点是必需的。

### <a name="dashboards"></a>仪表板

服务终结点表还公开多个用于监视的仪表板：

- 度量值 (Grafana)
- 日志 (Kibana)
- Spark 作业监视
- Spark 资源管理

可以直接单击这些链接。 在连接到服务之前，系统会两次提示提供用户名和密码。

### <a id="notebook"></a> 群集状态笔记本

1. 还可以通过启动群集状态笔记本来查看大数据群集的群集状态。 若要启动笔记本，请单击“群集状态”任务。

    ![启动](media/view-cluster-status/cluster-status-launch.png)

2. 在开始之前，需要以下内容：

    - 大数据群集名称
    - 控制器用户名
    - 控制器密码
    - 控制器终结点

    除非在部署过程中进行了自定义，否则大数据群集名称默认为 mssql-cluster。 可以在服务终结点表的大数据群集仪表板中找到控制器终结点。 此终结点作为“群集管理服务”列出。 如果不知道凭据，请向部署群集的管理员询问。

3. 单击顶部工具栏中的“运行单元”。

4. 按照提示输入凭据。 分别为大数据群集名称、控制器用户名和控制器密码键入凭据后，按 ENTER。

    > [!Note]
    > 如果没有通过大数据设置的配置文件，系统会要求提供控制器终结点。 键入或粘贴它，然后按 ENTER 继续。

5. 如果成功连接，则笔记本的其余部分将显示大数据群集的每个组件的输出。 如果要重新运行某个代码单元，请将鼠标悬停在代码单元上，并单击“运行”图标。

## <a name="use-azdata"></a>使用 azdata

还可以使用 [azdata](deploy-install-azdata.md) 命令来查看终结点和群集状态。

### <a name="service-endpoints"></a>服务终结点

可以使用以下步骤获取大数据群集的外部终结点的 IP 地址。

1. 通过查看以下 kubectl 命令的 EXTERNAL-IP 输出，查找控制器终结点的 IP 地址：

   ```bash
   kubectl get svc controller-svc-external -n <your-big-data-cluster-name>
   ```

   > [!TIP]
   > 如果在部署过程中未更改默认名称，请在上一个命令中使用 `-n mssql-cluster`。 mssql-cluster 是大数据群集的默认名称。

1. 使用 [azdata login](reference-azdata.md) 登录大数据群集。 将 --controller-endpoint 参数设置为控制器终结点的外部 IP 地址。

   ```bash
   azdata login --controller-endpoint https://<ip-address-of-controller-svc-external>:30080 --controller-username <user-name>
   ```

   指定在部署过程中为控制器配置的用户名和密码（CONTROLLER_USERNAME 和 CONTROLLER_PASSWORD）。

1. 运行 [azdata bdc endpoint list](reference-azdata-bdc-endpoint.md) 以获取一个列表，其中包含每个终结点的描述及其对应的 IP 地址和端口值。 

   ```bash
   azdata bdc endpoint list -o table
   ```

   以下列表显示了此命令的示例输出：

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

可以通过 [azdata bdc status show](reference-azdata-bdc-status.md) 命令查看群集的状态。

```bash
azdata bdc status show -o table
```

> [!TIP]
> 若要运行状态命令，必须先用前面的终结点部分中所示的 azdata login 命令登录。

以下显示了此命令的示例输出：

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

可通过 [azdata bdc pool status show](reference-azdata-bdc-pool-status.md) 命令查看群集中池的状态。 若要使用此命令，请使用 `--kind` 参数指定池的类型。 池类型为：

- 计算
- data
- master
- Spark
- 存储

例如，以下命令显示存储池的池状态：

```bash
azdata bdc pool status show --kind storage
```

将看到类似以下输出的文本：

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

`logsUrl` 值链接到具有日志信息的 kibana 仪表板：

![Kibana 仪表板](./media/view-cluster-status/kibana-dashboard.png)

`nodeMetricsUrl` 和 `sqlMetricsUrl` 值链接到用于监视节点运行状况和 SQL 指标的 grafana 仪表板：

![Grafana 仪表板](./media/view-cluster-status/grafana-dashboard.png)

![SQL](./media/view-cluster-status/grafana-sql-status.png)

### <a name="view-controller-status"></a>查看控制器状态

可以通过 [azdata bdc status show](reference-azdata-bdc-control-status.md) 命令查看群集的状态。 它提供类似链接，链接到与大数据群集的控制器节点相关的监视仪表板。

## <a name="next-steps"></a>后续步骤

有关大数据群集的详细信息, 请参阅[什么[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]是](big-data-cluster-overview.md)。
