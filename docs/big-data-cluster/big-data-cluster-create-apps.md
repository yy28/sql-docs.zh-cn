---
title: 如何将应用部署
titleSuffix: SQL Server 2019 big data clusters
description: 将 Python 或 R 脚本部署为 SQL Server 2019 大数据群集 （预览版） 上的应用程序。
author: TheBharath
ms.author: bharaths
manager: craigg
ms.date: 12/11/2018
ms.topic: conceptual
ms.prod: sql
ms.custom: seodec18
ms.openlocfilehash: cca0ac5e7b81318d95fbb133758fca83e1a0742e
ms.sourcegitcommit: edf7372cb674179f03a330de5e674824a8b4118f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/11/2018
ms.locfileid: "53246400"
---
# <a name="how-to-deploy-an-app-on-sql-server-2019-big-data-cluster-preview"></a>如何部署 SQL Server 2019 大数据群集 （预览版） 上的应用程序

本文介绍如何部署和管理 R 和 Python 脚本为 SQL Server 2019 大数据群集 （预览版） 内的应用程序。

R 和 Python 应用程序部署和管理与**mssqlctl-pre** CTP 2.2 中的命令行实用程序。 本文提供有关如何将这些 R 和 Python 脚本部署为从命令行应用程序的示例。

## <a name="prerequisites"></a>先决条件

您必须具有配置的 SQL Server 2019 大数据群集。 有关详细信息，请参阅[如何部署大数据群集在 Kubernetes 的 SQL Server](deployment-guidance.md)。 

## <a name="installation"></a>安装

**Mssqlctl-pre**命令行实用工具提供预览的 Python 和 R 的应用程序部署功能。 使用以下命令安装实用程序：

```cmd
pip install -r https://private-repo.microsoft.com/python/ctp-2.2/mssqlctlpre/mssqlctlpre.txt --trusted-host https://private-repo.microsoft.com
```

## <a name="capabilities"></a>功能

CTP 2.2 中可以创建、 删除、 列出和运行 R 或 Python 应用程序。 下表描述了可用于应用程序部署命令**mssqlctl-pre**。

| Command | Description |
|---|---|
| `mssqlctl-pre login` | 登录到 SQL Server 大数据群集 |
| `mssqlctl-pre app create` | 创建应用 |
| `mssqlctl-pre app list` | 列出已部署的应用 |
| `mssqlctl-pre app delete` | 删除应用 |
| `mssqlctl-pre app run` | 列出正在运行的应用 |

可以获取帮助`--help`参数，如以下示例所示：

```bash
mssqlctl-pre app create --help
```

以下部分介绍这些命令的更多详细信息。

## <a name="log-in"></a>登录

在配置之前 R 和 Python 应用程序，首先登录到 SQL Server 使用的大数据群集`mssqlctl-pre login`命令。 指定的外部 IP 地址`service-proxy-lb`或`service-proxy-nodeport`服务 (例如： `https://ip-address:30777`) 以及用户名和密码向群集。

可以获取的 IP 地址**服务代理 lb**或**服务代理 nodeport**服务通过在 bash 或 cmd 窗口中运行以下命令：

```bash 
kubectl get svc service-proxy-lb -n <name of your cluster>
```

```bash
mssqlctl-pre login -e https://<ip-address-of-service-proxy-lb>:30777 -u <user-name> -p <password>
```

## <a name="create-an-app"></a>创建应用

若要创建的应用程序，可以传递到 Python 或 R 代码文件**mssqlctl-pre**与`app create`命令。 这些文件创建从应用的计算机上驻留在本地。

使用以下语法在大数据群集中创建新的应用：

```bash
mssqlctl-pre app create -n <app_name> -v <version_number> -r <runtime> -i <path_to_code_init> -c <path_to_code> --inputs <input_params> --outputs <output_params> 
```

以下命令显示了此命令可能如下所示的示例：

```py
#add.py
def add(x,y):
        result = x+y
        return result;
result=add(x,y)
```
若要尝试此操作，将上面的代码行保存到本地目录作为`add.py`并运行以下命令

```bash
mssqlctl-pre app create --name add-app --version v1 --runtime Python --code ./add.py  --inputs x=int,y=int --outputs result=int 
```

你可以检查是否使用列表命令部署应用：

```bash
mssqlctl-pre app list
```

如果部署未完成您应该看到显示"创建""状态": 

```
[
  {
    "name": "add-app",
    "state": "Creating",
    "version": "v1"
  }
]
```

部署成功后应看到"状态"更改为"就绪"状态：

```
[
  {
    "name": "add-app",
    "state": "Ready",
    "version": "v1"
  }
]
```

## <a name="list-an-app"></a>列出应用

可以列出已成功创建了与任何应用`app list`命令。

以下命令列出了大数据群集中所有可用的应用程序：

```bash
mssqlctl-pre app list
```

如果指定的名称和版本，它将列出该特定应用程序和其状态 （创建或就绪）：

```bash
mssqlctl-pre app list --name <app_name> --version <app_version>
```

下面的示例演示了此命令：

```bash
mssqlctl-pre app list --name add-app --version v1
```

应看到类似于下面的示例输出：

```
[
  {
    "name": "add-app",
    "state": "Ready",
    "version": "v1"
  }
]
```

## <a name="run-an-app"></a>运行应用

如果应用程序处于"就绪"状态，可以使用它通过运行具有指定的输入参数。 使用以下语法来运行应用：

```bash
mssqlctl-pre app run --name <app_name> --version <app_version> --inputs <inputs_params>
```

以下示例命令演示如何运行的命令：

```bash
mssqlctl-pre app run --name add-app --version v1 --inputs x=1,y=2
```

如果成功运行，您应看到在输出与创建该应用程序时指定。 下面是一个示例。

```
{
  "changedFiles": [],
  "consoleOutput": "",
  "errorMessage": "",
  "outputFiles": {},
  "outputParameters": {
    "result": 3
  },
  "success": true
}
```

## <a name="delete-an-app"></a>删除应用

若要从大数据群集中删除应用，使用以下语法：

```bash
mssqlctl-pre app delete --name add-app --version v1
```

## <a name="next-steps"></a>后续步骤

您还可以查看其他示例位于[ https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster ](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster)。 

有关 SQL Server 大数据群集的详细信息，请参阅[什么是 SQL Server 2019 大数据群集？](big-data-cluster-overview.md)。
