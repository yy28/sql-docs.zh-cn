---
title: 为 SQL Server Always On 可用性组在 Kubernetes 上创建部署脚本
description: 此文章介绍了如何为 SQL Server Always On 可用性组在 Kubernetes 上创建部署脚本
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 09/24/2018
ms.topic: article
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 2bc5acc2ee6f81dbdf1ce16a98fb7f75bbf6f121
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47594555"
---
# <a name="create-deployment-script-for-sql-server-always-on-availability-group"></a>为 SQL Server Always On 可用性组创建部署脚本

本文介绍如何部署使用的示例部署脚本的单个命令中的 Kubernetes 群集上的可用性组。 `deploy-ag.py` 创建一个 Python 脚本`.yaml`群集的文件，并可以将它们应用于 Kubernetes 群集。

从文件的文件的下载[sql server 示例](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-deployment-script)。

## <a name="before-you-start"></a>开始之前

在工作站上安装以下工具。

* [Python](https://www.python.org/downloads/) （3.5 或 3.6）
* [PyYAML](https://pyyaml.org/) -Python 包
* [Kubernetes 客户端](https://github.com/kubernetes-client/python)-Python 包

将 python 路径添加到环境变量 （适用于 Windows)。

### <a name="install-the-required-components"></a>安装所需的组件

下面的示例更高版本的 Python 安装的 PyYAML 和 Kubernetes 客户端包。

安装 Python 后，下载并解压缩示例文件夹。 

若要配置所需的文件，请运行以下命令。 替换为`<path>`解压缩后的示例文件的位置。

```cmd
pip install --user -r "C:\<path>\requirements.txt"
```

## <a name="create-cluster-and-download-config-file"></a>创建群集并下载配置文件

以下示例创建群集在 Azure Kubernetes 服务 (AKS)。

运行该脚本之前，更新在尖括号内的值`<>`。

```azcli
az aks create  --resource-group <GroupName> --name <ClusterName> --generate-ssh-keys --node-count 4 --kubernetes-version 1.11.1

az aks get-credentials --resource-group=<GroupName> --name=<ClusterName>
```

>[!NOTE]
>可用性组需要 Kubernetes 1.11.0 版本或更高版本。 该示例指定 1.11.1。

## <a name="run-the-deployment-script"></a>运行部署脚本

下面的示例演示如何运行`deploy-ag.py`。

### <a name="help"></a>帮助

```cmd
python ./deploy-ag.py --help
```

* **使用情况**: `deploy-ag.py [-h] {deploy | failover} ...`
* **可选参数**:
  * `-h, --help` 显示此帮助消息并退出
* **子命令**:
  * K8s 代理上的操作 {部署 | 故障转移}

  `deploy`

   部署 SQL Server 可用性组中的一组

  `failover`

   故障转移到目标副本。

### <a name="deploy-help"></a>部署帮助

```cmd
python ./deploy-ag.py deploy --help
```

* **使用情况**:

  ```
  python ./deploy-ag.py deploy [-h] [--verbose] [--ag AG] [-n NAMESPACE]
    [--dry-run] [-s SQL_SERVERS [SQL_SERVERS ...]]
    [-p SA_PASSWORD] [-e {ON_PREM,AKS}]
    [--skip-create-namespace]
  ```

  部署 SQL Server 和中 namespace(AG name) k8s 代理

* **可选参数**:
  
  `-h, --help`
  
  显示此帮助消息并退出
  
  `--verbose, -v`
  
  输出的详细级别
  
  `--ag AG`
  
  可用性组的名称。 默认值 = ag1
  
  `-n NAMESPACE, --namespace NAMESPACE`
  
  k8s 命名空间名称。 如果未指定，则默认为可用性组名称。

  `--dry-run`
  
  创建清单，但不是应用它们。
  
  `-s SQL_SERVERS [SQL_SERVERS ...], --sql-servers SQL_SERVERS [SQL_SERVERS ...]`

  SQL Server 实例的名称 （最多为 5，由空格分隔) 默认值 = [mssql1、 mssql2、 mssql3']
  
  `-p SA_PASSWORD, --sa-password SA_PASSWORD`
  
  SA 密码。 默认值 = SAPassword2018
  
  `-e {ON_PREM,AKS}, --env {ON_PREM,AKS}`
  
  `--skip-create-namespace`
  
  跳过创建命名空间。

### <a name="failover-help"></a>故障转移帮助

```cmd
python ./deploy-ag.py failover --help
```
* **使用情况**: 

  ```cmd
  python deploy-ag.py failover [-h] [--verbose] [--ag AG]
    [--namespace NAMESPACE] [--dry-run]
    target_replica
  ```

  手动故障转移

* **位置参数**: `target_replica`

  故障转移的目标 SQL Server 副本名称

* **可选参数**:

  `-h, --help`
  
  显示此帮助消息并退出

  `--verbose, -v`
  
  输出的详细级别

  `--ag AG`
  
  可用性组的名称。 默认值 = ag1

  `--namespace NAMESPACE`

  k8s 命名空间名称。 如果未指定的 AG 名称到默认值

  `--dry-run`
  
  创建，但不适用于为清单。

### <a name="create-the-manifests---dont-apply"></a>创建清单-不适用

以下脚本创建的清单文件，但不适用于它们。

```cmd
python ./deploy-ag.py deploy --dry-run
```

下面的示例创建命名空间下的可用性组的清单`AG1`具有三个副本。 在运行该脚本之前，替换`<MyC0m91exP@55w0r!>`使用复杂密码。

```cmd
python ./deploy-ag.py deploy --ag ag1 --namespace AG1 --sa-password '<MyC0m91exP@55w0r!>' --env AKS --dry-run
```

前一命令生成示例 yaml 文件目录。

在这种情况下，命令输出显示其中创建清单文件。

![脚本输出](./media/sql-server-linux-kubernetes-create-deployment/scriptbuild-out.png)
    
### <a name="create-the-manifests-and-apply"></a>创建清单和应用

下面的示例创建命名空间下的可用性组的清单`ag1`具有三个副本并将其应用到 Kubernetes 群集。 该群集然后将创建可用性组。 在运行该脚本之前，替换`<MyC0m91exP@55w0r!>`使用复杂密码。

```
python ./deploy-ag.py deploy --ag ag1 --namespace ag1 --sa-password '<MyC0m91exP@55w0r!>' --env AKS --verbose
```

在脚本完成后，Kubernetes 运算符来创建存储、 SQL Server 实例、 负载均衡器服务。 你可以监视与部署[Kubernetes 仪表板](http://docs.microsoft.com/azure/aks/kubernetes-dashboard)。

在 Kubernetes 后会创建 SQL Server 容器：

1. [连接](sql-server-linux-kubernetes-connect.md)到群集中的 SQL Server 实例。

1. 创建数据库。

1. 执行完整备份的数据库，以启动日志链。

1. 将数据库添加到可用性组。

使用自动种子设定使 SQL Server 将相应的副本上自动创建辅助数据库创建可用性组。

### <a name="manually-failover"></a>手动故障转移

下面的示例将故障转移主副本。

```cmd
python ./deploy-ag.py failover --ag ag1 --namespace ag1 --verbose mssql1-0
```

## <a name="next-steps"></a>后续步骤

[Kubernetes 群集上的 SQL Server 可用性组](sql-server-ag-kubernetes.md)
