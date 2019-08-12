---
title: 在 Kubernetes 上为 SQL Server Always On 可用性组创建部署脚本
description: 本文介绍如何在 Kubernetes 上为 SQL Server Always On 可用性组创建部署脚本
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 09/24/2018
ms.topic: article
ms.prod: sql
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 181773a19e87c34a1931cae05f5a329aedbc1239
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/25/2019
ms.locfileid: "68000139"
---
# <a name="create-deployment-script-for-sql-server-always-on-availability-group"></a>为 SQL Server Always On 可用性组创建部署脚本

本文使用示例部署脚本介绍如何通过单个命令在 Kubernetes 群集上部署可用性组。 `deploy-ag.py` 是 Python 脚本，可为群集创建 `.yaml` 文件并将它们应用于 Kubernetes 群集。

从 [sql-server-samples](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-deployment-script) 下载文件。

## <a name="before-you-start"></a>开始之前

在工作站上安装以下工具。

* [Python](https://www.python.org/downloads/)（3.5 或 3.6）
* [PyYAML](https://pyyaml.org/) - Python 包
* [Kubernetes 客户端](https://github.com/kubernetes-client/python) - Python 包

将 python 路径添加到环境变量（适用于 Windows）。

### <a name="install-the-required-components"></a>安装所需的组件

以下示例安装适用于 Python 的 PyYAML 和 Kubernetes 客户端包。

安装 Python 后，下载并提取示例文件夹。 

若要配置所需的文件，请运行以下命令。 将 `<path>` 替换为提取的示例文件的位置。

```cmd
pip install --user -r "C:\<path>\requirements.txt"
```

## <a name="create-cluster-and-download-config-file"></a>创建群集并下载配置文件

以下示例在 Azure Kubernetes 服务 (AKS) 中创建群集。

运行脚本前，更新尖括号中的值 - `<>`。

```azcli
az aks create  --resource-group <GroupName> --name <ClusterName> --generate-ssh-keys --node-count 4 --kubernetes-version 1.11.1

az aks get-credentials --resource-group=<GroupName> --name=<ClusterName>
```

>[!NOTE]
>可用性组需要 Kubernetes 1.11.0 版或更高版本。 该示例指定 1.11.1。

## <a name="run-the-deployment-script"></a>运行部署脚本

以下示例演示如何运行 `deploy-ag.py`。

### <a name="help"></a>帮助

```cmd
python ./deploy-ag.py --help
```

* **用法**：`deploy-ag.py [-h] {deploy | failover} ...`
* **可选参数**：
  * `-h, --help` 显示此帮助消息并退出
* **子命令**：
  * k8s 代理上的操作{部署 | 故障转移}

  `deploy`

   在可用性组中部署一组 SQL Server

  `failover`

   故障转移到目标副本。

### <a name="deploy-help"></a>部署帮助

```cmd
python ./deploy-ag.py deploy --help
```

* **用法**：

  ```
  python ./deploy-ag.py deploy [-h] [--verbose] [--ag AG] [-n NAMESPACE]
    [--dry-run] [-s SQL_SERVERS [SQL_SERVERS ...]]
    [-p SA_PASSWORD] [-e {ON_PREM,AKS}]
    [--skip-create-namespace]
  ```

  在命名空间（AG 名称）中部署 SQL Server 和 k8s 代理

* **可选参数**：
  
  `-h, --help`
  
  显示此帮助消息并退出
  
  `--verbose, -v`
  
  输出详细程度
  
  `--ag AG`
  
  可用性组的名称。 默认值 = ag1
  
  `-n NAMESPACE, --namespace NAMESPACE`
  
  k8s 命名空间的名称。 如果未指定，则默认为 AG 名称。

  `--dry-run`
  
  创建清单，但不要应用它们。
  
  `-s SQL_SERVERS [SQL_SERVERS ...], --sql-servers SQL_SERVERS [SQL_SERVERS ...]`

  SQL Server 实例的名称（最多 5 个，以空格分隔）默认 = ['mssql1', 'mssql2', 'mssql3']
  
  `-p SA_PASSWORD, --sa-password SA_PASSWORD`
  
  SA 密码。 默认 = 'SAPassword2018'
  
  `-e {ON_PREM,AKS}, --env {ON_PREM,AKS}`
  
  `--skip-create-namespace`
  
  跳过命名空间创建。

### <a name="failover-help"></a>故障转移帮助

```cmd
python ./deploy-ag.py failover --help
```
* **用法**： 

  ```cmd
  python deploy-ag.py failover [-h] [--verbose] [--ag AG]
    [--namespace NAMESPACE] [--dry-run]
    target_replica
  ```

  手动故障转移

* **位置参数**：`target_replica`

  用于故障转移的目标 SQL Server 副本的名称

* **可选参数**：

  `-h, --help`
  
  显示此帮助消息并退出

  `--verbose, -v`
  
  输出详细程度

  `--ag AG`
  
  可用性组的名称。 默认值 = ag1

  `--namespace NAMESPACE`

  k8s 命名空间的名称。 如果未指定，则默认为 AG 名称

  `--dry-run`
  
  创建清单，但不要应用。

### <a name="create-the-manifests---dont-apply"></a>创建清单 - 不应用

以下脚本创建清单文件但不应用它们。

```cmd
python ./deploy-ag.py deploy --dry-run
```

以下示例为包含三个副本的命名空间 `AG1` 下的可用性组创建清单。 运行脚本前，请将 `<MyC0m91exP@55w0r!>` 替换为复杂密码。

```cmd
python ./deploy-ag.py deploy --ag ag1 --namespace AG1 --sa-password '<MyC0m91exP@55w0r!>' --env AKS --dry-run
```

上一个命令生成示例 yaml 文件目录。

在这种情况下，命令输出显示清单文件的创建位置。

![脚本输出](./media/sql-server-linux-kubernetes-create-deployment/scriptbuild-out.png)
    
### <a name="create-the-manifests-and-apply"></a>创建清单并应用

以下示例为包含三个副本的命名空间 `ag1` 下的可用性组创建清单，并将其应用于 Kubernetes 群集。 群集随后将创建可用性组。 运行脚本前，请将 `<MyC0m91exP@55w0r!>` 替换为复杂密码。

```
python ./deploy-ag.py deploy --ag ag1 --namespace ag1 --sa-password '<MyC0m91exP@55w0r!>' --env AKS --verbose
```

脚本完成后，Kubernetes 运算符会创建存储、SQL Server 实例和负载均衡器服务。 可使用 [Kubernetes 仪表板](https://docs.microsoft.com/azure/aks/kubernetes-dashboard)监视部署。

在 Kubernetes 创建 SQL Server 容器后：

1. [连接](sql-server-linux-kubernetes-connect.md)到群集中的 SQL Server 实例。

1. 创建数据库。

1. 对数据库执行完整备份以启动日志链。

1. 将数据库添加到可用性组。

可用性组通过自动种子设定进行创建，以便 SQL Server 在相应的副本上自动创建辅助数据库。

### <a name="manually-failover"></a>手动故障转移

以下示例对主副本进行故障转移。

```cmd
python ./deploy-ag.py failover --ag ag1 --namespace ag1 --verbose mssql1-0
```

## <a name="next-steps"></a>后续步骤

[Kubernetes 群集上的 SQL Server 可用性组](sql-server-ag-kubernetes.md)
