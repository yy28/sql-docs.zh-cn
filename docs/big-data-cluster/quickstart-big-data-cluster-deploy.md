---
title: 部署脚本
titleSuffix: SQL Server big data clusters
description: 演练的 SQL Server 2019 大数据群集 （预览版） 在 Azure Kubernetes 服务 (AKS) 的部署。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
manager: jroth
ms.date: 05/22/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 0254b76b0845ff5f913d2d0ab69324ddd0072923
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/10/2019
ms.locfileid: "67728780"
---
# <a name="deploy-sql-server-big-data-cluster-on-azure-kubernetes-service-aks"></a>部署 SQL Server 大数据群集在 Azure Kubernetes 服务 (AKS)

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

在本教程中，使用的示例部署脚本部署到 Azure Kubernetes 服务 (AKS) 的 SQL Server 2019 大数据群集 （预览版）。 

> [!TIP]
> AKS 是适用于大数据群集的托管 Kubernetes 的只有一个选项。 若要了解有关其他部署选项以及如何自定义部署选项，请参阅[如何部署 SQL Server 大数据群集在 Kubernetes 上](deployment-guidance.md)。

此处使用默认大数据群集部署由 SQL 主实例、 一个计算池实例、 两个数据池实例和两个存储池实例组成。 数据将保留使用使用 AKS 默认存储类的 Kubernetes 永久性卷。 在本教程中使用的默认配置是适用于开发/测试环境。

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="prerequisites"></a>先决条件

- 一个 Azure 订阅。
- [大数据工具](deploy-big-data-tools.md):
   - **mssqlctl**
   - **kubectl**
   - **Azure Data Studio**
   - **SQL Server 2019 扩展**
   - **Azure CLI**

## <a name="log-in-to-your-azure-account"></a>登录到你的 Azure 帐户

该脚本使用 Azure CLI 自动执行创建 AKS 群集。 之前运行脚本后，你必须登录到 Azure 帐户和 Azure CLI 在至少一次。 从命令提示符处运行以下命令。

```
az login
```

## <a name="download-the-deployment-script"></a>下载部署脚本

本教程会自动创建的大数据群集上使用 python 脚本的 AKS**部署的 sql-大的数据-aks.py**。 如果已安装的 python **mssqlctl**，可以在本教程中成功运行该脚本。 

在 Windows PowerShell 或 Linux bash 提示符处，运行以下命令以从 GitHub 下载部署脚本。

```
curl -o deploy-sql-big-data-aks.py "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/deployment/aks/deploy-sql-big-data-aks.py"
```

## <a name="run-the-deployment-script"></a>运行部署脚本

使用以下步骤来运行部署脚本。 此脚本将在 Azure 中创建的 AKS 服务，然后将 SQL Server 2019 大数据群集部署到 AKS。 此外可以修改与其他脚本[环境变量](deployment-guidance.md#configfile)若要创建自定义部署。

1. 使用以下命令运行脚本：

   ```
   python deploy-sql-big-data-aks.py
   ```

   > [!NOTE]
   > 如果您有 python3 和 python2 在客户端计算机且位于该路径，则必须使用 python3 运行命令： `python3 deploy-sql-big-data-aks.py`。

1. 出现提示时，输入以下信息：

   | ReplTest1 | 描述 |
   |---|---|
   | **Azure 订阅 ID** | 要用于 AKS 的 Azure 订阅 ID。 可通过运行列出的所有订阅和其 Id`az account list`从另一个命令行。 |
   | **Azure 资源组** | 要创建 AKS 群集的 Azure 资源组名称。 |
   | **Docker 用户名** | 向你的有限公共预览版的一部分提供的 Docker 用户名。 |
   | **Docker 密码** | Docker 密码提供给你的有限公共预览版的一部分。 |
   | **Azure 区域** | 新的 AKS 群集的 Azure 区域 (默认**westus**)。 |
   | **机大小** | [虚拟机大小](https://docs.microsoft.com/azure/virtual-machines/windows/sizes)要用于 AKS 群集中的节点 (默认**Standard_L8s**)。 |
   | **辅助角色节点** | 在 AKS 群集中的辅助角色节点数 (默认**1**)。 |
   | **群集名称** | 在 AKS 群集和大数据群集的名称。 大数据群集的名称必须仅小写字母数字字符，不留空格。 (默认**sqlbigdata**)。 |
   | **密码** | 有关控制器、 HDFS/Spark 网关和主实例密码 (默认**MySQLBigData2019**)。 |
   | **控制器用户** | 控制器用户的用户名 (默认值：**管理员**)。 |

   > [!IMPORTANT]
   > 默认值**Standard_L8s**机大小不一定在每个 Azure 区域中可用。 如果您选择不同的计算机大小，请确保在群集中节点之间可以附加的磁盘总数大于或等于 24。 在群集中的每个永久性卷声明需要附加的磁盘。 目前，大数据群集需要 24 永久性卷声明。 例如， [Standard_L8s](https://docs.microsoft.com/azure/virtual-machines/windows/sizes-storage#lsv2-series)计算机大小支持 32 个附加的磁盘，以便您可以评估此计算机大小的单个节点的大数据群集。

   > [!NOTE]
   > `sa`帐户是在安装过程中创建的 SQL Server 主实例上的系统管理员。 创建部署之后,`MSSQL_SA_PASSWORD`环境变量是可发现通过运行`echo $MSSQL_SA_PASSWORD`主实例容器中。 出于安全考虑，更改你`sa`部署后的主实例上的密码。 有关详细信息，请参阅[更改 SA 密码](../linux/quickstart-install-connect-docker.md#sapassword)。

1. 该脚本将首先创建 AKS 群集使用您指定的参数。 此步骤需要几分钟的时间。

   <img src="./media/quickstart-big-data-cluster-deploy/script-parameters.png" width="800px" alt="Script parameters and AKS cluster creation"/>

## <a name="monitor-the-status"></a>监视状态

该脚本会创建 AKS 群集后，将设置必需的环境变量前面指定的设置。 然后，它调用**mssqlctl**部署 AKS 上的大数据群集。

客户端命令窗口将输出的部署状态。 在部署过程中，您应看到一系列消息，它正在等待控制器 pod:

```output
2018-11-15 15:42:02.0209 UTC | INFO | Waiting for controller pod to be up...
```

10 到 20 分钟后，您应会收到通知，正在运行的控制器 pod:

```output
2018-11-15 15:50:50.0300 UTC | INFO | Controller pod is running.
2018-11-15 15:50:50.0585 UTC | INFO | Controller Endpoint: https://111.111.111.111:30080
```

> [!IMPORTANT]
> 整个部署可能需要很长时间由于下载的大数据群集组件的容器映像所需的时间。 但是，也不会花费几个小时。 如果遇到你的部署的问题，请参阅[监视和故障排除 SQL Server 大数据群集](cluster-troubleshooting-commands.md)。

## <a name="inspect-the-cluster"></a>检查群集

在部署期间任何时候，可以使用**kubectl**或**mssqlctl**要检查的状态和运行大数据群集有关的详细信息。

### <a name="use-kubectl"></a>使用 kubectl

打开一个新的命令窗口以使用**kubectl**在部署过程。

1. 运行以下命令以获取整个群集的状态摘要：

   ```
   kubectl get all -n <your-big-data-cluster-name>
   ```

   > [!TIP]
   > 如果未更改的大数据群集名称，该脚本将默认为**sqlbigdata**。

1. 检查 kubernetes 服务和以下及其内部和外部终结点**kubectl**命令：

   ```
   kubectl get svc -n <your-big-data-cluster-name>
   ```

1. 此外可以检查状态的 kubernetes pod 使用以下命令：

   ```
   kubectl get pods -n <your-big-data-cluster-name>
   ```

1. 了解有关使用以下命令特定 pod 的详细信息：

   ```
   kubectl describe pod <pod name> -n <your-big-data-cluster-name>
   ```

> [!TIP]
> 有关如何监视和排查部署问题的更多详细信息，请参阅[监视和故障排除 SQL Server 大数据群集](cluster-troubleshooting-commands.md)。

## <a name="connect-to-the-cluster"></a>连接到群集

部署脚本完成后，输出会通知您成功：

```output
2018-11-15 16:10:25.0583 UTC | INFO | Cluster state: Ready
2018-11-15 16:10:25.0583 UTC | INFO | Cluster deployed successfully.
```

大数据群集现在部署在 AKS 的 SQL 服务器。 你现在可以使用 Azure Data Studio 连接到群集。 有关详细信息，请参阅[连接到 SQL Server 大数据群集使用 Azure Data Studio](connect-to-big-data-cluster.md)。

## <a name="clean-up"></a>清理

如果要在 Azure 中测试 SQL Server 大数据群集，则应删除 AKS 群集时已完成，以避免产生意外的费用。 如果你想要继续使用它，则不要删除群集。

> [!WARNING]
> 以下步骤停止 SQL Server 大数据群集中删除 AKS 群集。 如果您有任何数据库或你想要保留的 HDFS 数据，这些数据之前备份在删除该群集。

运行以下 Azure CLI 命令在 Azure 中删除大数据群集和 AKS 服务 (替换`<resource group name>`与**Azure 资源组**部署脚本中指定):

```azurecli
az group delete -n <resource group name>
```

## <a name="next-steps"></a>后续步骤

部署脚本 Azure Kubernetes 服务配置，并且还部署了 SQL Server 2019 大数据群集。 您还可以选择自定义进行手动安装以后进行部署。 若要了解更多有关如何大数据群集部署以及如何自定义部署，请参阅[如何部署 SQL Server 大数据群集在 Kubernetes 上](deployment-guidance.md)。

现在，已部署 SQL Server 大数据群集，可以加载示例数据并浏览的教程：

> [!div class="nextstepaction"]
> [教程：将示例数据加载到 SQL Server 2019 大数据群集](tutorial-load-sample-data.md)