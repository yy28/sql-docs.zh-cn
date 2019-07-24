---
title: 部署脚本
titleSuffix: SQL Server big data clusters
description: 演练 Azure Kubernetes Service (AKS) 上的 SQL Server 2019 大数据群集 (预览版) 的部署。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 7ff1ec3672fbcf101d98ad30913742186dea574d
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419399"
---
# <a name="deploy-sql-server-big-data-cluster-on-azure-kubernetes-service-aks"></a>在 Azure Kubernetes 服务 (AKS) 上部署 SQL Server 大数据群集

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本教程介绍如何使用示例部署脚本将 SQL Server 2019 大数据群集 (预览版) 部署到 Azure Kubernetes 服务 (AKS)。 

> [!TIP]
> AKS 只是一种为大数据群集托管 Kubernetes 的选项。 若要了解其他部署选项以及如何自定义部署选项, 请参阅[如何在 Kubernetes 上部署 SQL Server 大数据群集](deployment-guidance.md)。

此处使用的默认大数据群集部署包含一个 SQL 主实例、一个计算池实例、两个数据池实例和两个存储池实例。 使用 AKS 默认存储类的 Kubernetes 永久性卷来保存数据。 本教程中使用的默认配置适用于开发/测试环境。

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="prerequisites"></a>先决条件

- 一个 Azure 订阅。
- [大数据工具](deploy-big-data-tools.md):
   - **azdata**
   - **kubectl**
   - **Azure Data Studio**
   - **SQL Server 2019 扩展**
   - **Azure CLI**

## <a name="log-in-to-your-azure-account"></a>登录到 Azure 帐户

脚本使用 Azure CLI 来自动创建 AKS 群集。 在运行该脚本之前, 必须至少通过 Azure CLI 登录到 Azure 帐户。 在命令提示符下运行以下命令。

```
az login
```

## <a name="download-the-deployment-script"></a>下载部署脚本

本教程使用 python 脚本**deploy-sql-big-data-aks.py**在 AKS 上自动创建大数据群集。 如果已安装 python for **azdata**, 则应该能够在本教程中成功运行该脚本。 

在 Windows PowerShell 或 Linux bash 提示符下, 运行以下命令以从 GitHub 下载部署脚本。

```
curl -o deploy-sql-big-data-aks.py "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/deployment/aks/deploy-sql-big-data-aks.py"
```

## <a name="run-the-deployment-script"></a>运行部署脚本

使用以下步骤运行部署脚本。 此脚本会在 Azure 中创建 AKS 服务, 然后将 SQL Server 2019 大数据群集部署到 AKS。 你还可以使用其他[环境变量](deployment-guidance.md#configfile)修改该脚本, 以创建自定义部署。

1. 用以下命令运行该脚本:

   ```
   python deploy-sql-big-data-aks.py
   ```

   > [!NOTE]
   > 如果客户端计算机和路径中都有 python3 和 python2, 则必须使用 python3: `python3 deploy-sql-big-data-aks.py`运行该命令。

1. 出现提示时, 输入以下信息:

   | ReplTest1 | 描述 |
   |---|---|
   | **Azure 订阅 ID** | 要用于 AKS 的 Azure 订阅 ID。 可以通过从另一个命令行运行`az account list`来列出所有订阅及其 id。 |
   | **Azure 资源组** | 要为 AKS 群集创建的 Azure 资源组名称。 |
   | **Azure 区域** | 新 AKS 群集的 Azure 区域 (默认值为**westus**)。 |
   | **计算机大小** | 要用于 AKS 群集中的节点的[计算机大小](https://docs.microsoft.com/azure/virtual-machines/windows/sizes)(默认值为**Standard_L8s**)。 |
   | **辅助角色节点** | AKS 群集中的辅助角色节点数 (默认值为**1**)。 |
   | **群集名称** | AKS 群集和大数据群集的名称。 大数据群集名称只能包含小写字母数字字符, 且不能包含空格。 (默认值为**sqlbigdata**)。 |
   | **密码** | 控制器、HDFS/Spark 网关和 master 实例的密码 (默认值为**MySQLBigData2019**)。 |
   | **控制器用户** | 控制器用户的用户名 (默认值: **admin**)。 |

SQL Server 2019 大数据群集早期采用者计划中的参与者需要以下参数:**Docker 用户名**和**docker 密码**。 从 CTP 3.2, 不再需要它们。

   > [!IMPORTANT]
   > 默认的**Standard_L8s**计算机大小在每个 Azure 区域中可能不可用。 如果选择其他计算机大小, 请确保可在群集中的节点上附加的磁盘总数大于或等于24。 群集中的每个永久性卷声明都需要一个附加的磁盘。 目前, 大数据群集需要24个永久性卷声明。 例如, [Standard_L8s](https://docs.microsoft.com/azure/virtual-machines/windows/sizes-storage#lsv2-series)计算机大小支持32附加的磁盘, 因此你可以使用此计算机大小的单个节点评估大数据群集。

   > [!NOTE]
   > 此`sa`帐户是在安装过程中创建的 SQL Server 主实例上的系统管理员。 创建部署后, `MSSQL_SA_PASSWORD`可通过在主实例容器中运行`echo $MSSQL_SA_PASSWORD`来发现环境变量。 出于安全目的, 请在`sa`部署后在主实例上更改密码。 有关详细信息, 请参阅[更改 SA 密码](../linux/quickstart-install-connect-docker.md#sapassword)。

1. 脚本将首先使用指定的参数创建 AKS 群集。 此步骤花费几分钟时间。

   <img src="./media/quickstart-big-data-cluster-deploy/script-parameters.png" width="800px" alt="Script parameters and AKS cluster creation"/>

## <a name="monitor-the-status"></a>监视状态

此脚本在创建 AKS 群集后, 将继续设置所需的环境变量和前面指定的设置。 然后, 它调用**azdata**在 AKS 上部署大数据群集。

客户端命令窗口将输出部署状态。 在部署过程中, 应会看到一系列消息正在等待控制器 pod:

```output
2018-11-15 15:42:02.0209 UTC | INFO | Waiting for controller pod to be up...
```

10到20分钟后, 应通知控制器 pod 正在运行:

```output
2018-11-15 15:50:50.0300 UTC | INFO | Controller pod is running.
2018-11-15 15:50:50.0585 UTC | INFO | Controller Endpoint: https://111.111.111.111:30080
```

> [!IMPORTANT]
> 由于下载大数据群集组件的容器映像所需的时间, 整个部署可能需要较长时间。 但是, 这不会花几个小时。 如果你的部署遇到问题, 请参阅[SQL Server 大数据群集的监视和故障排除](cluster-troubleshooting-commands.md)。

## <a name="inspect-the-cluster"></a>检查群集

在部署过程中, 你可以使用**kubectl**或**azdata**来检查有关正在运行的大数据群集的状态和详细信息。

### <a name="use-kubectl"></a>使用 kubectl

在部署过程中, 打开新的命令窗口以使用**kubectl** 。

1. 运行以下命令以获取整个群集状态的摘要:

   ```
   kubectl get all -n <your-big-data-cluster-name>
   ```

   > [!TIP]
   > 如果未更改大数据群集名称, 则脚本默认为 " **sqlbigdata**"。

1. 用以下**kubectl**命令检查 kubernetes 服务及其内部和外部终结点:

   ```
   kubectl get svc -n <your-big-data-cluster-name>
   ```

1. 还可以通过以下命令检查 kubernetes pod 的状态:

   ```
   kubectl get pods -n <your-big-data-cluster-name>
   ```

1. 使用以下命令查找有关特定 pod 的详细信息:

   ```
   kubectl describe pod <pod name> -n <your-big-data-cluster-name>
   ```

> [!TIP]
> 有关如何监视和排查部署问题的详细信息, 请参阅[SQL Server 大数据群集的监视和故障排除](cluster-troubleshooting-commands.md)。

## <a name="connect-to-the-cluster"></a>连接到群集

部署脚本完成后, 输出会通知你成功:

```output
2018-11-15 16:10:25.0583 UTC | INFO | Cluster state: Ready
2018-11-15 16:10:25.0583 UTC | INFO | Cluster deployed successfully.
```

SQL Server 大数据群集现已部署在 AKS 上。 你现在可以使用 Azure Data Studio 连接到群集。 有关详细信息, 请参阅[使用 Azure Data Studio 连接到 SQL Server 大数据群集](connect-to-big-data-cluster.md)。

## <a name="clean-up"></a>清理

如果要在 Azure 中测试 SQL Server 大数据群集, 则应在完成时删除 AKS 群集以避免意外费用。 如果要继续使用群集, 请不要删除它。

> [!WARNING]
> 以下步骤将泪水删除 SQL Server 大数据群集的 AKS 群集。 如果你有想要保留的任何数据库或 HDFS 数据, 请在删除该群集之前备份该数据。

运行以下 Azure CLI 命令, 在 azure 中删除大数据群集和 AKS 服务 (将替换`<resource group name>`为在部署脚本中指定的**Azure 资源组**):

```azurecli
az group delete -n <resource group name>
```

## <a name="next-steps"></a>后续步骤

部署脚本已配置 Azure Kubernetes 服务, 还部署了 SQL Server 2019 大数据群集。 你还可以选择通过手动安装自定义将来的部署。 若要详细了解如何部署大数据群集以及如何自定义部署, 请参阅[如何在 Kubernetes 上部署 SQL Server 大数据群集](deployment-guidance.md)。

现在已部署 SQL Server 大数据群集, 可以加载示例数据并浏览教程:

> [!div class="nextstepaction"]
> [教程：将示例数据加载到 SQL Server 2019 大数据群集](tutorial-load-sample-data.md)