---
title: azdata 引用
titleSuffix: SQL Server big data clusters
description: Azdata 命令的参考文章。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: a8136c85f8c32e08423f3d199a021d4f60353b39
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/23/2019
ms.locfileid: "68425987"
---
# <a name="azdata"></a>azdata

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

以下文章提供了有关[SQL Server 2019 大数据群集 (预览版)](big-data-cluster-overview.md)的**azdata**工具的参考。 有关如何安装**azdata**工具的详细信息, 请参阅[安装 azdata 以管理 SQL Server 2019 大数据群集](deploy-install-azdata.md)。

## <a name="commands"></a>命令
|     |     |
| --- | --- |
|[azdata 应用](reference-azdata-app.md) | 创建、删除、运行和管理应用程序。 |
|[azdata bdc](reference-azdata-bdc.md) | 选择、管理和操作 SQL Server 大数据群集。 |
|[azdata 笔记本](reference-azdata-notebook.md) | 用于从终端查看、运行和管理笔记本的命令。 |
[azdata 登录](#azdata-login) | 登录到群集的控制器终结点。
[azdata 注销](#azdata-logout) | 注销群集。
|[azdata sql](reference-azdata-sql.md) | SQL DB CLI 允许用户通过 T-sql 与 SQL Server 进行交互。 |
## <a name="azdata-login"></a>azdata 登录
部署群集后, 它将在部署期间列出控制器终结点, 你应该使用该终结点登录。  如果你不知道控制器终结点, 则可以通过在系统上将群集的 kube config 置于<user home>/.kube/config 的默认位置登录, 或使用 KUBECONFIG env var, 如 export KUBECONFIG = path/to/. kube/config。
```bash
azdata login [--cluster-name -n] 
             [--controller-username -u]  
             [--controller-endpoint -e]  
             [--accept-eula -a]
```
### <a name="examples"></a>示例
以交互方式登录。 如果未指定为参数, 将始终提示群集名称。 如果系统上设置了 CONTROLLER_USERNAME、CONTROLLER_PASSWORD 和 ACCEPT_EULA 环境变量, 则不会提示这些变量。 如果系统上有 kube config, 或使用 KUBECONFIG env var 指定配置的路径, 则交互式体验将首先尝试使用该配置, 然后在配置失败时提示你。
```bash
azdata login
```
登录 (非交互)。 登录时, 将群集名称、控制器用户名、控制器终结点和 EULA 接受设置为参数。 必须设置环境变量 CONTROLLER_PASSWORD。  如果你不想指定控制器终结点, 请在计算机上的默认位置<user home>"/.kube/config" 中安装 kube 配置, 或使用 KUBECONFIG env var, 即 export KUBECONFIG = path/to/kube/config。
```bash
azdata login --cluster-name ClusterName --controller-user johndoe@contoso.com  --controller-endpoint https://<ip>:30080 --accept-eula yes
```
在计算机上用 kube config 登录, 并为 CONTROLLER_USERNAME、CONTROLLER_PASSWORD 和 ACCEPT_EULA 设置 env var。
```bash
azdata login -n ClusterName
```
### <a name="optional-parameters"></a>可选参数
#### `--cluster-name -n`
群集名称。
#### `--controller-username -u`
帐户用户。 如果不想使用此 arg, 可以设置环境变量 CONTROLLER_USERNAME。
#### `--controller-endpoint -e`
群集控制器终结点 https://host:port ""。 如果不想使用此 arg, 可以在计算机上使用 kube config。 请确保配置位于<user home>/.kube/config 的默认位置, 或使用 KUBECONFIG env var。
#### `--accept-eula -a`
接受许可条款吗？ [是/否]。 如果不想使用此参数, 则可以将环境变量 ACCEPT_EULA 设置为 "yes"。 可以在 https://aka.ms/azdata-eula 中查看此产品的许可条款。
### <a name="global-arguments"></a>全局参数
#### `--debug`
提高日志记录详细程度以显示所有调试日志。
#### `--help -h`
显示此帮助消息并退出。
#### `--output -o`
输出格式。  允许的值: json、jsonc、table、tsv。  默认值: json。
#### `--query -q`
JMESPath 查询字符串。 有关[http://jmespath.org/](http://jmespath.org/])详细信息和示例, 请参阅。
#### `--verbose`
提高日志记录详细程度。 使用--debug 获取完整的调试日志。
## <a name="azdata-logout"></a>azdata 注销
注销群集。
```bash
azdata logout 
```
### <a name="examples"></a>示例
注销此用户。
```bash
azdata logout
```
### <a name="global-arguments"></a>全局参数
#### `--debug`
提高日志记录详细程度以显示所有调试日志。
#### `--help -h`
显示此帮助消息并退出。
#### `--output -o`
输出格式。  允许的值: json、jsonc、table、tsv。  默认值: json。
#### `--query -q`
JMESPath 查询字符串。 有关[http://jmespath.org/](http://jmespath.org/])详细信息和示例, 请参阅。
#### `--verbose`
提高日志记录详细程度。 使用--debug 获取完整的调试日志。

## <a name="next-steps"></a>后续步骤

有关如何安装**azdata**工具的详细信息, 请参阅[安装 azdata 以管理 SQL Server 2019 大数据群集](deploy-install-azdata.md)。
