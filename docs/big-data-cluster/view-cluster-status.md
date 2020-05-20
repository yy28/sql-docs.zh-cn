---
title: 查看群集状态
titleSuffix: SQL Server big data clusters
description: 本文介绍如何使用 Azure Data Studio、笔记本和 azdata 命令查看大数据群集的状态。
author: yualan
ms.author: alayu
ms.reviewer: mikeray
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 45cf5461b9154d397ee5365fd275d2545a3cc376
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "73531591"
---
# <a name="how-to-view-the-status-of-a-big-data-cluster"></a>如何查看大数据群集的状态 

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文介绍如何访问服务终结点，以及如何查看 SQL Server 大数据群集组件的状态。 可以同时使用 Azure Data Studio 和 azdata  ，本文会介绍这两种方法。

## <a name="use-azure-data-studio"></a><a id="datastudio"></a> 使用 Azure Data Studio

下载 [Azure Data Studio](https://aka.ms/getazuredatastudio) 的最新**预览体验内部版本**后，可以使用 SQL Server 大数据群集仪表板查看服务终结点以及大数据群集的状态。 下面的某些功能仅在 Azure Data Studio 的预览体验内部版本中可用。

1. 首先，在 Azure Data Studio 中创建到大数据群集的连接。 有关详细信息，请参阅[使用 Azure Data Studio 连接到 SQL Server 大数据群集](connect-to-big-data-cluster.md)。

1. 右键单击大数据群集终结点，然后单击“管理”  。

   ![右键单击管理](media/view-cluster-status/right-click-manage.png)

1. 选择“SQL Server 大数据群集”选项卡访问大数据群集仪表板  。

   ![大数据群集仪表板](media/view-cluster-status/bdc-dashboard.png)

### <a name="service-endpoints"></a>服务终结点

能够轻松访问大数据群集中的各项服务很重要。 大数据群集仪表板提供了一个服务终结点表，可用于查看和复制服务终结点。

![服务终结点](media/view-cluster-status/service-endpoints.png)

当需要可用于连接这些服务的终结点时，这些服务会列出可以复制和粘贴的终结点。 例如，可以单击终结点右侧的复制图标，然后将其粘贴到请求该终结点的文本窗口中。 要运行[群集状态笔记本](#notebook)，群集管理服务终结点是必需的。

### <a name="dashboards"></a>仪表板

服务终结点表还公开多个用于监视的仪表板：

- 度量值 (Grafana)
- 日志 (Kibana)
- Spark 作业监视
- Spark 资源管理

可以直接单击这些链接。 在访问这些仪表板时，将需要进行身份验证。 对于指标和日志仪表板，请提供在部署时使用环境变量设置的控制器管理员凭据 AZDATA_USERNAME 和 AZDATA_PASSWORD   。 Spark 面板将使用网关 (Knox) 凭据：与 AD 集成的群集中的 AD 标识，或如果在群集中使用基本身份验证，则为用户 root 和 AZDATA_PASSWORD   。 

### <a name="cluster-status-notebook"></a><a id="notebook"></a> 群集状态笔记本

1. 还可以通过启动群集状态笔记本来查看大数据群集的群集状态。 若要启动笔记本，请单击“群集状态”任务  。

    ![启动](media/view-cluster-status/cluster-status-launch.png)

2. 在开始之前，需要以下内容：

    - 大数据群集名称
    - 控制器用户名
    - 控制器密码
    - 控制器终结点

    除非在部署过程中进行了自定义，否则大数据群集名称默认为 mssql-cluster  。 可以在服务终结点表的大数据群集仪表板中找到控制器终结点。 此终结点作为“群集管理服务”  列出。 如果不知道凭据，请向部署群集的管理员询问。

3. 单击顶部工具栏中的“运行单元”  。

4. 按照提示输入凭据。 分别为大数据群集名称、控制器用户名和控制器密码键入凭据后，按 ENTER。

    > [!Note]
    > 如果没有通过大数据设置的配置文件，系统会要求提供控制器终结点。 键入或粘贴它，然后按 ENTER 继续。

5. 如果成功连接，则笔记本的其余部分将显示大数据群集的每个组件的输出。 如果要重新运行某个代码单元，请将鼠标悬停在代码单元上，并单击“运行”图标  。

## <a name="use-azdata"></a>使用 azdata

还可以使用 [azdata](deploy-install-azdata.md) 命令来查看终结点和群集状态。

### <a name="service-endpoints"></a>服务终结点

1. 使用 [azdata login](reference-azdata.md) 登录大数据群集。 将 --controller-endpoint  参数设置为控制器终结点的外部 IP 地址。

   ```bash
   azdata login --endpoint https://<ip-address-of-controller-svc-external>:30080 --username <user-name>
   ```

   指定在部署过程中为控制器配置的用户名和密码（AZDATA_USERNAME 和 AZDATA_PASSWORD）。 
   对于 AD 身份验证，该命令为：

  ```bash
   azdata login --endpoint https://<control_domain_name>:30080 --auth ad
   ```

1. 运行 [`azdata bdc endpoint list`](reference-azdata-bdc-endpoint.md) 可获取一个列表，其中包含每个终结点的描述及其对应的 IP 地址和端口值。 

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

可以通过 [`azdata bdc status show`](reference-azdata-bdc-status.md) 命令查看群集的状态。

```bash
azdata bdc status show
```

> [!TIP]
> 若要运行状态命令，必须先用前面的终结点部分中所示的 azdata login  命令登录。

以下显示了此命令的示例输出：

```output
 Bdc: ready                                                                                                                                                                                                          Health Status:  healthy
 ===========================================================================================================================================================================================================================================
 Services: ready                                                                                                                                                                                                     Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Servicename    State    Healthstatus    Details

 spark          ready    healthy         -
 sql            ready    healthy         -
 hdfs           ready    healthy         -
 control        ready    healthy         -
 gateway        ready    healthy         -
 app            ready    healthy         -


 Spark Services: ready                                                                                                                                                                                               Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Resourcename    State    Healthstatus    Details

 sparkhead       ready    healthy         StatefulSet sparkhead is healthy
 storage-0       ready    healthy         StatefulSet storage-0 is healthy


 Sql Services: ready                                                                                                                                                                                                 Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Resourcename    State    Healthstatus    Details

 master          ready    healthy         StatefulSet master is healthy
 compute-0       ready    healthy         StatefulSet compute-0 is healthy
 data-0          ready    healthy         StatefulSet data-0 is healthy
 storage-0       ready    healthy         StatefulSet storage-0 is healthy


 Hdfs Services: ready                                                                                                                                                                                                Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Resourcename    State    Healthstatus    Details

 nmnode-0        ready    healthy         StatefulSet nmnode-0 is healthy
 zookeeper       ready    healthy         StatefulSet zookeeper is healthy
 storage-0       ready    healthy         StatefulSet storage-0 is healthy
 sparkhead       ready    healthy         StatefulSet sparkhead is healthy


 Control Services: ready                                                                                                                                                                                             Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Resourcename    State    Healthstatus    Details

 controldb       ready    healthy         StatefulSet controldb is healthy
 control         ready    healthy         ReplicaSet control is healthy
 metricsdc       ready    healthy         DaemonSet metricsdc is healthy
 metricsui       ready    healthy         ReplicaSet metricsui is healthy
 metricsdb       ready    healthy         StatefulSet metricsdb is healthy
 logsui          ready    healthy         ReplicaSet logsui is healthy
 logsdb          ready    healthy         StatefulSet logsdb is healthy
 mgmtproxy       ready    healthy         ReplicaSet mgmtproxy is healthy
 controlwd       ready    healthy         ReplicaSet controlwd is healthy


 Gateway Services: ready                                                                                                                                                                                             Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Resourcename    State    Healthstatus    Details

 gateway         ready    healthy         StatefulSet gateway is healthy


 App Services: ready                                                                                                                                                                                                 Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Resourcename    State    Healthstatus    Details

 appproxy        ready    healthy         ReplicaSet appproxy is healthy
```

### <a name="view-specific-resource-status"></a>查看特定资源的状态

可通过 [azdata bdc status show](reference-azdata-bdc-status.md) 命令查看群集中特定资源的状态。 使用此命令时，可以使用 `--resource` 参数进行筛选。 `--resource` 参数输入的几个示例包括：

- master
- 控制
- compute-0
- storage-0
- gateway

例如，以下命令显示存储池的状态：

```bash
azdata bdc status show --all --resource storage-0
```

若要查看运行特定服务的所有组件的状态，则必须使用相应的命令组 `azdata bdc <serviceName> status show`。 例如：

- azdata bdc sql status show --all
- azdata bdc hdfs status show --all
- azdata bdc spark status show --all

下面是示例输出：

```output
  Storage-0: ready                                                                                                                                                                                                    Health Status:  healthy
 ===========================================================================================================================================================================================================================================
 Instances: running                                                                                                                                                                                                  Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Instancename    State    Healthstatus    Details

 storage-0-0     running  healthy         Pod storage-0-0 is healthy
 storage-0-1     running  healthy         Pod storage-0-1 is healthy


 Dashboards
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Name            Url

 nodeMetricsUrl  https://13.91.50.9:30777/api/v1/bdc/instances/storage-0-1/status/nodemetrics/ui
 sqlMetricsUrl   https://13.91.50.9:30777/api/v1/bdc/instances/storage-0-1/status/sqlmetrics/ui
 logsUrl         https://13.91.50.9:30777/api/v1/bdc/instances/storage-0-1/status/logs/ui
 ```

> [!TIP]
> 运行包含 `--all` 参数的状态命令可获取其他运行状况详细信息，包括指向与特定实例相对应的指标和日志仪表板的链接。 下面是使用 `--all` 参数时的示例输出：

```output
 Spark: ready                                                                                                                                                                                                        Health Status:  healthy
 ===========================================================================================================================================================================================================================================
 Resources: ready                                                                                                                                                                                                    Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Resourcename    State    Healthstatus    Details

 sparkhead       ready    healthy         StatefulSet sparkhead is healthy
 storage-0       ready    healthy         StatefulSet storage-0 is healthy


 Sparkhead Resources: running                                                                                                                                                                                        Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Instancename    State    Healthstatus    Details

 sparkhead-0     running  healthy         Pod sparkhead-0 is healthy
 sparkhead-1     running  healthy         Pod sparkhead-1 is healthy


      Dashboards
      --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
      Name            Url

      nodeMetricsUrl  https://13.91.50.9:30777/api/v1/bdc/instances/sparkhead-1/status/nodemetrics/ui
      sqlMetricsUrl   https://13.91.50.9:30777/api/v1/bdc/instances/sparkhead-1/status/sqlmetrics/ui
      logsUrl         https://13.91.50.9:30777/api/v1/bdc/instances/sparkhead-1/status/logs/ui


 Storage-0 Resources: running                                                                                                                                                                                        Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Instancename    State    Healthstatus    Details

 storage-0-0     running  healthy         Pod storage-0-0 is healthy
 storage-0-1     running  healthy         Pod storage-0-1 is healthy


      Dashboards
      --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
      Name            Url

      nodeMetricsUrl  https://13.91.50.9:30777/api/v1/bdc/instances/storage-0-1/status/nodemetrics/ui
      sqlMetricsUrl   https://13.91.50.9:30777/api/v1/bdc/instances/storage-0-1/status/sqlmetrics/ui
      logsUrl         https://13.91.50.9:30777/api/v1/bdc/instances/storage-0-1/status/logs/ui
```

`logsUrl` 值链接到 Kibana 仪表板：

![Kibana 仪表板](./media/view-cluster-status/kibana-dashboard.png)

> [!NOTE]
> （旧版）Microsoft Edge 浏览器与 Kibana 不兼容，因此必须使用基于 chromium 的浏览器来正确显示仪表板。 使用不受支持的浏览器加载仪表板时，会看到一个空白页。 请参阅此处，了解 Kibana 支持的浏览器。

`nodeMetricsUrl` 和 `sqlMetricsUrl` 值链接到用于监视 Kubernetes 节点指标和大数据群集服务指标的 Grafana 仪表板：

![Grafana 仪表板](./media/view-cluster-status/grafana-dashboard.png)

![SQL](./media/view-cluster-status/grafana-sql-status.png)

### <a name="view-controller-status"></a>查看控制器状态

可以通过 [`azdata bdc control status show`](reference-azdata-bdc-control-status.md) 命令查看控制器状态。 它提供类似链接，可链接到与大数据群集的控制器组件相关的监视仪表板。

## <a name="next-steps"></a>后续步骤

有关大数据群集的详细信息，请参阅[什么是 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](big-data-cluster-overview.md)。
