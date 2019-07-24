---
title: 部署指南
titleSuffix: SQL Server big data clusters
description: 了解如何在 Kubernetes 上部署 SQL Server 2019 大数据群集 (预览版)。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: e6f2eefd37c45753e3051722448b80d88712df26
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419418"
---
# <a name="how-to-deploy-sql-server-big-data-clusters-on-kubernetes"></a>如何在 Kubernetes 上部署 SQL Server 大数据群集

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

SQL Server 大数据群集在 Kubernetes 群集上部署为 docker 容器。 下面概述了设置和配置步骤:

- 在单个 VM、Vm 群集或 Azure Kubernetes 服务 (AKS) 中设置 Kubernetes 群集。
- 在客户端计算机上安装群集配置工具**azdata** 。
- 在 Kubernetes 群集中部署 SQL Server 大数据群集。

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="install-sql-server-2019-big-data-tools"></a>安装 SQL Server 2019 大数据工具

在部署 SQL Server 2019 大数据群集之前, 请先[安装大数据工具](deploy-big-data-tools.md):

- **azdata**
- **kubectl**
- **Azure Data Studio**
- **SQL Server 2019 扩展**

## <a id="prereqs"></a>Kubernetes 先决条件

SQL Server 大数据群集要求服务器和客户端 (kubectl) 至少具有5v 的 Kubernetes 版本。

> [!NOTE]
> 请注意, 客户端和服务器 Kubernetes 版本应在 + 1 或-1 次版本内。 有关详细信息, 请参阅[Kubernetes 发行说明和版本歪斜 SKU 策略)](https://github.com/kubernetes/community/blob/master/contributors/design-proposals/release/versioning.md#supported-releases-and-component-skew)。

### <a id="kubernetes"></a>Kubernetes 群集设置

如果已具有满足上述先决条件的 Kubernetes 群集, 则可以直接跳到[部署步骤](#deploy)。 本部分假定你基本了解 Kubernetes 的概念。  有关 Kubernetes 的详细信息, 请参阅[Kubernetes 文档](https://kubernetes.io/docs/home)。

可以通过以下三种方式之一选择部署 Kubernetes:

| 部署 Kubernetes: | 描述 | 链接 |
|---|---|---|
| **Azure Kubernetes Services (AKS)** | Azure 中的托管 Kubernetes 容器服务。 | [说明](deploy-on-aks.md) |
| **多台计算机 (kubeadm)** | 使用**kubeadm**部署在物理计算机或虚拟机上的 Kubernetes 群集 | [说明](deploy-with-kubeadm.md) |
| **Minikube** | VM 中的单节点 Kubernetes 群集。 | [说明](deploy-on-minikube.md) |

> [!TIP]
> 有关同时部署 AKS 和 SQL Server 大数据群集的示例 python 脚本, 请参阅[快速入门:在 Azure Kubernetes 服务 (AKS)](quickstart-big-data-cluster-deploy.md)上部署 SQL Server 大数据群集。

### <a name="verify-kubernetes-configuration"></a>验证 Kubernetes 配置

运行**kubectl**命令以查看群集配置。 确保 kubectl 指向正确的群集上下文。

```bash
kubectl config view
```

配置 Kubernetes 群集后, 可以继续部署新的 SQL Server 大数据群集。 如果要从以前的版本升级, 请参阅[如何升级 SQL Server 大数据群集](deployment-upgrade.md)。

## <a id="deploy"></a>部署概述

大多数大数据群集设置都是在 JSON 部署配置文件中定义的。 可以将默认部署配置文件用于 AKS、 `kubeadm`或`minikube` , 也可以自定义你自己的部署配置文件以在安装过程中使用。 出于安全原因, 通过环境变量传递身份验证设置。

以下各节提供了有关如何配置大数据群集部署以及常见自定义的示例的更多详细信息。 此外, 您始终可以使用 VS Code 例如, 使用编辑器编辑自定义部署配置文件。

## <a id="configfile"></a>默认配置

大数据群集部署选项是在 JSON 配置文件中定义的。 有三个标准部署配置文件, 其默认设置适用于开发/测试环境:

| 部署配置文件 | Kubernetes 环境 |
|---|---|
| **aks-dev-test** | Azure Kubernetes 服务 (AKS) |
| **kubeadm-dev-test** | 多台计算机 (kubeadm) |
| **minikube-dev-test** | Minikube |

可以通过运行**azdata bdc create**来部署大数据群集。 这会提示您选择一个默认配置, 然后指导您完成部署。

首次运行`azdata`时, 必须包括`--accept-eula`接受最终用户许可协议 (EULA)。

```bash
azdata bdc create --accept-eula
```

在这种情况下, 系统将提示你输入不属于默认配置 (如密码) 的任何设置。 

> [!NOTE]
> 从 SQL Server 2019 CTP 3.2 开始, 你不再有权使用 SQL Server 2019[早期采用计划](https://aka.ms/eapsignup)来体验大数据群集的预览版本。

> [!IMPORTANT]
> 大数据群集的默认名称为 " **mssql-群集**"。 若要运行用`-n`参数指定 Kubernetes 命名空间的任何**kubectl**命令, 必须了解这一点。

## <a id="customconfig"></a>自定义配置

还可以自定义你自己的部署配置文件。 可以执行以下步骤:

1. 从与 Kubernetes 环境匹配的标准部署配置文件中启动。 可以使用**azdata bdc config list**命令列出它们:

   ```bash
   azdata bdc config list
   ```

1. 若要自定义部署, 请使用**azdata bdc config init**命令创建部署配置文件的副本。 例如, 下面的命令在名为`custom`的目标目录中创建**aks**部署配置文件的副本:

   ```bash
   azdata bdc config init --source aks-dev-test --target custom
   ```

   azdata
   > 指定一个目录, 其中包含基于`--source`参数的配置文件、**群集**和**控件 json**。 `--target`

1. 若要自定义部署配置文件中的设置, 可以在适用于编辑 JSON 文件的工具 (如 VS Code) 中编辑部署配置文件。 对于脚本化自动化, 还可以使用**azdata bdc config**命令编辑自定义部署配置文件。 例如, 以下命令将更改自定义部署配置文件, 以将部署的群集的名称从默认 (**mssql 群集**) 更改为**测试群集**:  

   ```bash
   azdata bdc config replace --config-file custom/cluster.json --json-values "metadata.name=test-cluster"
   ```

   > 用于查找 JSON 路径的有用工具是[JSONPath Online 计算器](https://jsonpath.com/)。

   除了传递键值对外, 还可以提供内联 JSON 值或传递 JSON 修补文件。 有关详细信息, 请参阅为[大数据群集配置部署设置](deployment-custom-configuration.md)。

1. 然后将自定义配置文件传递到**azdata bdc create**。 请注意, 你必须设置所需的[环境变量](#env), 否则系统将提示你输入值:

   ```bash
   azdata bdc create --config-profile custom --accept-eula yes
   ```

> 有关部署配置文件的结构的详细信息, 请参阅[部署配置文件参考](reference-deployment-config.md)。 有关更多配置示例, 请参阅为[大数据群集配置部署设置](deployment-custom-configuration.md)。

## <a id="env"></a>环境变量

以下环境变量用于未存储在部署配置文件中的安全设置。 请注意, 可以在配置文件中设置除凭据之外的 Docker 设置。

| 环境变量 | 要求 |描述 |
|---|---|---|
| **CONTROLLER_USERNAME** | Required |群集管理员的用户名。 |
| **CONTROLLER_PASSWORD** | Required |群集管理员的密码。 |
| **MSSQL_SA_PASSWORD** | Required |SQL 主实例的 SA 用户的密码。 |
| **KNOX_PASSWORD** | 必填 |Knox 用户的密码。 |
| **ACCEPT_EULA**| 首次使用时需要`azdata`| 不需要任何值。 当设置为环境变量时, 它将 EULA 同时应用到 SQL Server `azdata`和。 如果未设置为环境变量, 则可以在`--accept-eula`第一次`azdata`使用命令时包括。|
| **DOCKER_USERNAME** | 可选 | 在存储在专用存储库中时访问容器映像的用户名。 请参阅[脱机部署](deploy-offline.md)主题, 了解有关如何使用专用 Docker 存储库进行大数据群集部署的更多详细信息。|
| **DOCKER_PASSWORD** | 可选 |用于访问上述专用存储库的密码。 |

在调用**azdata bdc create**之前, 必须设置这些环境变量。 如果未设置任何变量, 则系统会提示您输入。

下面的示例演示如何设置适用于 Linux (bash) 和 Windows (PowerShell) 的环境变量:

```bash
export CONTROLLER_USERNAME=admin
export CONTROLLER_PASSWORD=<password>
export MSSQL_SA_PASSWORD=<password>
export KNOX_PASSWORD=<password>
```

```PowerShell
SET CONTROLLER_USERNAME=admin
SET CONTROLLER_PASSWORD=<password>
SET MSSQL_SA_PASSWORD=<password>
SET KNOX_PASSWORD=<password>
```

设置环境变量后, 必须运行`azdata bdc create`以触发部署。 此示例使用上面创建的群集配置文件:

```bash
azdata bdc create --config-profile custom --accept-eula yes
```

请注意以下准则:

- 如果密码包含任何特殊字符, 请确保用双引号将其括起来。 可以将**MSSQL_SA_PASSWORD**设置为所需的任何内容, 但请确保密码非常复杂且不使用`!` `&`或`'`字符。 请注意, 双引号分隔符仅适用于 bash 命令。
- **SA**登录名是在安装过程中创建的 SQL Server 主实例上的系统管理员。 创建 SQL Server 容器后, 可通过在容器中运行`echo $MSSQL_SA_PASSWORD`来发现你指定的 MSSQL_SA_PASSWORD 环境变量。 出于安全目的, 请根据[此处](../linux/quickstart-install-connect-docker.md#sapassword)所述的最佳做法更改 SA 密码。

## <a id="unattended"></a>无人参与安装

对于无人参与的部署, 必须设置所有必需的`azdata bdc create` `--accept-eula yes`环境变量, 使用配置文件, 并使用参数调用命令。 上一部分中的示例演示了无人参与安装的语法。

## <a id="monitor"></a>监视部署

在群集启动过程中, 客户端命令窗口将输出部署状态。 在部署过程中, 应会看到一系列消息正在等待控制器 pod:

```output
Waiting for cluster controller to start.
```

15到30分钟后, 应通知控制器 pod 正在运行:

```output
Cluster controller endpoint is available at 11.111.111.11:30080.
Cluster control plane is ready.
```

> [!IMPORTANT]
> 由于下载大数据群集组件的容器映像所需的时间, 整个部署可能需要较长时间。 但是, 这不会花几个小时。 如果你的部署遇到问题, 请参阅[SQL Server 大数据群集的监视和故障排除](cluster-troubleshooting-commands.md)。

部署完成后, 输出会通知你成功:

```output
Cluster deployed successfully.
```

> [!TIP]
> 部署的大数据群集的默认名称为, `mssql-cluster`除非由自定义配置进行修改。

## <a id="endpoints"></a>检索终结点

部署脚本成功完成后, 可以使用以下步骤获取大数据群集的外部终结点的 IP 地址。

1. 部署完成后, 从部署标准输出中查找控制器终结点的 IP 地址, 或查看以下**kubectl**命令的外部 IP 输出:

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

还可以通过运行以下**kubectl**命令获取为群集部署的所有服务终结点:

```bash
kubectl get svc -n <your-big-data-cluster-name>
```

### <a name="minikube"></a>Minikube

如果使用的是 minikube, 则需要运行以下命令以获取连接到所需的 IP 地址。 除了 IP 外, 还需为需要连接到的终结点指定端口。

```bash
minikube ip
```

## <a id="status"></a>验证群集状态

部署后, 可以通过 " [azdata bdc status show](reference-azdata-bdc-status.md) " 命令检查群集的状态。

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

在此摘要状态下, 还可以通过以下命令获取更详细的状态:

- [azdata bdc 控件状态](reference-azdata-bdc-control-status.md)
- [azdata bdc 池状态](reference-azdata-bdc-pool-status.md)

这些命令的输出包含 Kibana 和 Grafana 仪表板的 Url, 以便进行更详细的分析。

除了使用**azdata**, 还可以使用 Azure Data Studio 来查找终结点和状态信息。 有关使用**azdata**和 Azure Data Studio 查看群集状态的详细信息, 请参阅[如何查看大数据群集的状态](view-cluster-status.md)。

## <a id="connect"></a>连接到群集

有关如何连接到大数据群集的详细信息, 请参阅[使用 Azure Data Studio 连接到 SQL Server 大数据群集](connect-to-big-data-cluster.md)。

## <a name="next-steps"></a>后续步骤

若要详细了解大数据群集部署, 请参阅以下资源:

- [为大数据群集配置部署设置](deployment-custom-configuration.md)
- [执行 SQL Server 大数据群集的脱机部署](deploy-offline.md)
- [此次Microsoft SQL Server 大数据群集体系结构](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
