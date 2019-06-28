---
title: 查看群集状态
titleSuffix: SQL Server big data clusters
description: 本文介绍如何查看使用 Azure Data Studio、 笔记本电脑和 mssqlctl 命令的大数据群集的状态。
author: yualan
ms.author: alayu
manager: jroth
ms.date: 06/27/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 2edd49c37655d420cf8022677c0d0287028a0b93
ms.sourcegitcommit: 0a4879dad09c6c42ad1ff717e4512cfea46820e9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2019
ms.locfileid: "67413964"
---
# <a name="how-to-view-the-status-of-a-big-data-cluster"></a>如何查看的大数据群集状态

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文介绍如何访问服务终结点和查看 SQL Server 大数据群集 （预览版） 的状态。 可以使用这两个 Azure Data Studio 和**mssqlctl**，和这篇文章介绍这两种技术。

## <a id="datastudio"></a> 使用 Azure 数据 Studio

下载最新版本后**预览体验成员版本**的[Azure Data Studio](https://aka.ms/azdata-insiders)，可以查看服务终结点和状态的大数据群集与 SQL Server 大数据群集仪表板。 请注意，以下功能的一些仅首次在 Azure Data Studio 的预览体验成员版本中可用。

1. 首先，在 Azure Data Studio 中创建与大数据群集的连接。 有关详细信息，请参阅[连接到 SQL Server 大数据群集使用 Azure Data Studio](connect-to-big-data-cluster.md)。

1. 大数据群集终结点，右键单击，然后单击**管理**。

   ![右键单击管理](media/view-cluster-status/right-click-manage.png)

1. 选择**SQL Server 大数据群集**选项卡可访问大数据群集仪表板。

   ![大数据群集仪表板](media/view-cluster-status/bdc-dashboard.png)

### <a name="service-endpoints"></a>服务终结点

务必要能够轻松地访问大数据群集内的各种服务。 大数据群集仪表板提供，可查看和复制服务终结点的服务终结点表。

![服务终结点](media/view-cluster-status/service-endpoints.png)

前几个行公开以下服务：

- 应用程序代理
- 群集管理服务
- HDFS 和 Spark
- 管理代理

这些服务列出了可以进行复制和粘贴时用于连接到这些服务需要终结点的终结点。 例如，您可以单击复制图标右侧的终结点，然后将其粘贴在文本窗口中请求该终结点。 群集管理服务终结点是运行所需[群集状态 notebook](#notebook)。

### <a name="dashboards"></a>仪表板

服务终结点表还公开多个仪表板进行监视：

- 度量值 (Grafana)
- 日志 (Kibana)
- Spark 作业监视
- Spark 资源管理

您可以直接单击下面的链接。 需要两次连接到服务之前提供用户名和密码。

### <a id="notebook"></a> 群集状态 notebook

1. 此外可以通过启动群集状态笔记本来查看群集状态的大数据群集。 若要启动笔记本，请单击**群集状态**任务。

    ![启动](media/view-cluster-status/cluster-status-launch.png)

2. 在开始之前，你将需要以下项：

    - 大数据群集名称
    - 控制器用户名
    - 控制器密码
    - 控制器终结点

    默认的大数据群集名称是**mssql 群集**除非自它定义在部署期间。 服务终结点表中，可以找到在大数据群集仪表板的控制器终结点。 终结点被列为**群集管理服务**。 如果不知道凭据，要求部署群集的管理员。

3. 单击**运行的单元格**在顶部工具栏中。

4. 按照你的凭据的提示。 按按 ENTER 键后的键入每个大数据群集名称、 控制器用户名和控制器的密码的凭据。

    > [!Note]
    > 如果您没有与你的大数据配置文件设置，您将要求为控制器终结点。 键入或粘贴，，然后按 ENTER 以继续。

5. 如果连接成功以后，该 notebook 的其余部分将显示大数据群集的每个组件的输出。 当你想要重新运行代码单元时，将鼠标悬停在代码单元格，然后单击**运行**图标。

## <a name="use-mssqlctl"></a>使用 mssqlctl

此外可以使用[mssqlctl](deploy-install-mssqlctl.md)命令以查看终结点和群集状态。

### <a name="service-endpoints"></a>服务终结点

你可以获取使用以下步骤在大数据群集的外部终结点的 IP 地址。

1. 通过查看以下的外部 IP 输出中查找控制器终结点的 IP 地址**kubectl**命令：

   ```bash
   kubectl get svc controller-svc-external -n <your-big-data-cluster-name>
   ```

   > [!TIP]
   > 如果在部署期间未更改默认名称，使用`-n mssql-cluster`在前一命令中。 **mssql 群集**是大数据群集的默认名称。

1. 登录到大数据群集[mssqlctl 登录](reference-mssqlctl.md)。 设置 **-控制器终结点**控制器终结点的外部 IP 地址的参数。

   ```bash
   mssqlctl login --controller-endpoint https://<ip-address-of-controller-svc-external>:30080 --controller-username <user-name>
   ```

   在部署过程中指定的用户名和密码配置为控制器 （CONTROLLER_USERNAME 和 CONTROLLER_PASSWORD）。

1. 运行[mssqlctl bdc 终结点列表](reference-mssqlctl-bdc-endpoint.md)以获取每个终结点和其对应的 IP 地址和端口值的说明的列表。 

   ```bash
   mssqlctl bdc endpoint list -o table
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

您可以查看与群集的状态[mssqlctl bdc 状态显示](reference-mssqlctl-bdc-status.md)命令。

```bash
mssqlctl bdc status show -o table
```

> [!TIP]
> 若要运行的状态命令，你必须首先登录**mssqlctl 登录**命令，在上一终结点节中所示。

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

您可以查看与群集中的池的状态[mssqlctl bdc 池状态显示](reference-mssqlctl-bdc-pool-status.md)命令。 若要使用此命令，指定包含池类型`--kind`参数。 池类型包括：

- 计算
- data
- master
- Spark
- 存储

例如，下面的命令显示存储池的池状态：

```bash
mssqlctl bdc pool status show --kind storage
```

应看到类似于以下输出的文本：

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

`logsUrl`值 kibana 仪表板的日志信息的链接：

![kibana 仪表板](./media/view-cluster-status/kibana-dashboard.png)

`nodeMetricsUrl`和`sqlMetricsUrl`值链接到 grafana 仪表板用于监视节点运行状况和 SQL 指标：

![Grafana 仪表板](./media/view-cluster-status/grafana-dashboard.png)

![SQL](./media/view-cluster-status/grafana-sql-status.png)

### <a name="view-controller-status"></a>查看控制器状态

您可以查看与控制器状态[mssqlctl bdc 控件状态显示](reference-mssqlctl-bdc-control-status.md)命令。 它提供了类似的大数据群集的控制器节点与相关的监视仪表板的链接。

## <a name="next-steps"></a>后续步骤

有关大数据群集的详细信息，请参阅[什么是 SQL Server 大数据群集](big-data-cluster-overview.md)。
