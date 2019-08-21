---
title: azdata 参考
titleSuffix: SQL Server big data clusters
description: azdata 命令的参考文章。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 33cc3070647c58e6ae57c8bff3d587a76ae0a28d
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2019
ms.locfileid: "69653091"
---
# <a name="azdata"></a>azdata

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

以下文章提供了[ [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] (预览版)](big-data-cluster-overview.md)的**azdata**工具的参考。 有关如何安装**azdata**工具的详细信息, 请参阅[install [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]azdata to manage ](deploy-install-azdata.md)。

## <a name="commands"></a>命令
|     |     |
| --- | --- |
|[azdata app](reference-azdata-app.md) | 创建、删除、运行和管理应用程序。 |
|[azdata bdc](reference-azdata-bdc.md) | 选择、管理和操作 SQL Server 大数据群集。 |
|[azdata login](#azdata-login) | 登录到群集的控制器终结点。
|[azdata logout](#azdata-logout) | 注销群集。

## <a name="azdata-login"></a>azdata login
部署群集后, 它将在部署期间列出控制器终结点, 你应该使用该终结点登录。  如果你不知道控制器终结点, 则可以通过将群集的 kube config 置于<user home>/.kube/config 的默认位置来登录, 或使用 KUBECONFIG env var, 即 export KUBECONFIG = path/to/. kube/config。
```bash
azdata login [--cluster-name -n] 
             [--controller-username -u]  
             [--controller-endpoint -e]  
             [--accept-eula -a]
```
### <a name="examples"></a>示例
以交互方式登录。 如果未指定为参数，则系统会始终提示输入群集名称。 如果在系统上设置了 CONTROLLER_USERNAME、CONTROLLER_PASSWORD 和 ACCEPT_EULA 环境变量，则不会提示输入这些变量。 如果系统上设置了 kube 配置或正在使用 KUBECONFIG 环境变量来指定配置路径，则交互式体验将首先尝试使用该配置，然后在配置失败时进行提示。
```bash
azdata login
```
登录（非交互式）。 通过将群集名称、控制器用户名、控制器终结点和接受 EULA 设置为参数进行登录。 必须设置 CONTROLLER_PASSWORD 环境变量。  如果不想指定控制器终结点, 请在计算机上的默认位置<user home>/.kube/config 中安装 kube 配置, 或使用 KUBECONFIG env var, 即 export KUBECONFIG = path/to/. kube/config。
```bash
azdata login --cluster-name ClusterName --controller-user johndoe@contoso.com  --controller-endpoint https://<ip>:30080 --accept-eula yes
```
在计算机上使用 kube 配置登录，并设置 CONTROLLER_USERNAME、CONTROLLER_PASSWORD 和 ACCEPT_EULA 环境变量。
```bash
azdata login -n ClusterName
```
### <a name="optional-parameters"></a>可选参数
#### `--cluster-name -n`
群集名称。
#### `--controller-username -u`
帐户用户。 如果不想使用此参数，则可设置环境变量 CONTROLLER_USERNAME。
#### `--controller-endpoint -e`
群集控制器终结点“https://host:port”。 如果不想使用此参数，则可在计算机上使用 kube 配置。 确保配置位于<user home>/.kube/config 的默认位置, 或使用 KUBECONFIG env var。
#### `--accept-eula -a`
是否接受许可条款？ [是/否]。 如果不想使用此参数，可以将环境变量 ACCEPT_EULA 设置为“yes”。 
### <a name="global-arguments"></a>全局参数
#### `--debug`
提高日志记录详细程度以显示所有调试日志。
#### `--help -h`
显示此帮助消息并退出。
#### `--output -o`
输出格式。  允许的值：json、jsonc、table、tsv。  默认值：json。
#### `--query -q`
JMESPath 查询字符串。 有关详细信息, 请[http://jmespath.org/](http://jmespath.org/])参阅。
#### `--verbose`
提高日志记录详细程度。 使用 --debug 获取完整的调试日志。
## <a name="azdata-logout"></a>azdata logout
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
输出格式。  允许的值：json、jsonc、table、tsv。  默认值：json。
#### `--query -q`
JMESPath 查询字符串。 有关详细信息, 请[http://jmespath.org/](http://jmespath.org/])参阅。
#### `--verbose`
提高日志记录详细程度。 使用 --debug 获取完整的调试日志。

## <a name="next-steps"></a>后续步骤

有关如何安装**azdata**工具的详细信息, 请参阅[install [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]azdata to manage ](deploy-install-azdata.md)。
