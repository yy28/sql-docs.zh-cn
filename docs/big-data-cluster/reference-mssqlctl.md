---
title: mssqlctl 参考
titleSuffix: SQL Server big data clusters
description: Mssqlctl 命令的参考文章。
author: rothja
ms.author: jroth
manager: jroth
ms.date: 05/22/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: acc25e6b3deca199ad774378318e17991614dcaa
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2019
ms.locfileid: "66779240"
---
# <a name="mssqlctl"></a>mssqlctl

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

以下文章提供了参考**mssqlctl**适用于工具[SQL Server 2019 大数据群集 （预览版）](big-data-cluster-overview.md)。 有关如何安装详细信息**mssqlctl**工具，请参阅[安装 mssqlctl 来管理 SQL Server 2019 大数据群集](deploy-install-mssqlctl.md)。

## <a name="commands"></a>命令
|     |     |
| --- | --- |
|[mssqlctl 应用](reference-mssqlctl-app.md) | 创建、 删除、 运行和管理应用程序。 |
|[mssqlctl cluster](reference-mssqlctl-cluster.md) | 选择、 管理和运行群集。 |
[mssqlctl login](#mssqlctl-login) | 登录到群集的控制器终结点。
[mssqlctl logout](#mssqlctl-logout) | 日志移出群集。
## <a name="mssqlctl-login"></a>mssqlctl 登录名
部署群集时，将在部署期间，应使用列出的控制器终结点到登录名。  如果不知道控制器终结点，您可能会通过群集的 kube 配置对您的系统的默认位置的登录名<user home>/.kube/config 或使用 KUBECONFIG 环境变量，即导出 KUBECONFIG=path/to/.kube/config。
```bash
mssqlctl login [--cluster-name -n] 
               [--controller-username -u]  
               [--controller-endpoint -e]  
               [--accept-eula -a]
```
### <a name="examples"></a>示例
以交互方式登录。 群集名称始终提示输入如果未指定，将作为参数。 如果必须设置你的系统上 CONTROLLER_USERNAME、 CONTROLLER_PASSWORD 和 ACCEPT_EULA 环境变量，则这些将不会提示的。 如果你的系统上具有 kube 配置或使用 KUBECONFIG 环境变量来指定配置的路径，交互式体验将首先尝试使用配置，并在配置时提示您。
```bash
mssqlctl login
```
（非交互式） 登录。 登录群集名称、 控制器用户名称、 控制器终结点和最终用户许可协议接受设置作为参数。 环境变量必须设置 CONTROLLER_PASSWORD。  如果您不想要指定控制器终结点，请在默认位置的计算机上有 kube 配置<user home>/.kube/config 或使用 KUBECONFIG 环境变量，即导出 KUBECONFIG=path/to/.kube/config。
```bash
mssqlctl login --cluster-name ClusterName --controller-user johndoe@contoso.com  --controller-endpoint https://<ip>:30080 --accept-eula yes
```
登录计算机上，然后设置 CONTROLLER_USERNAME、 CONTROLLER_PASSWORD，和 ACCEPT_EULA env var kube 配置。
```bash
mssqlctl login -n ClusterName
```
### <a name="optional-parameters"></a>可选参数
#### `--cluster-name -n`
群集名称。
#### `--controller-username -u`
帐户的用户。 如果您不想要使用此参数，您可能会设置环境变量 CONTROLLER_USERNAME。
#### `--controller-endpoint -e`
群集控制器终结点"https://host:port"。 如果您不想要使用此参数，您可能会在计算机上使用 kube 配置。 请确保在配置的默认位置是位于<user home>/.kube/config 或使用 KUBECONFIG env var。
#### `--accept-eula -a`
您是否接受许可条款？ [是/否]。 如果您不想要使用此参数，您可能会设置环境变量 ACCEPT_EULA 为是
### <a name="global-arguments"></a>全局参数
#### `--debug`
增加日志记录详细程度，以显示所有调试日志。
#### `--help -h`
显示此帮助消息并退出。
#### `--output -o`
输出格式。  允许的值： json、 jsonc、 table、 tsv。  默认值： json。
#### `--query -q`
JMESPath 查询字符串。 请参阅[ http://jmespath.org/ ](http://jmespath.org/])有关详细信息和示例。
#### `--verbose`
提高日志记录详细程度。 使用--debug 可获取完整的调试日志。
## <a name="mssqlctl-logout"></a>mssqlctl 注销
日志移出群集。
```bash
mssqlctl logout 
```
### <a name="examples"></a>示例
注销此用户。
```bash
mssqlctl logout
```
### <a name="global-arguments"></a>全局参数
#### `--debug`
增加日志记录详细程度，以显示所有调试日志。
#### `--help -h`
显示此帮助消息并退出。
#### `--output -o`
输出格式。  允许的值： json、 jsonc、 table、 tsv。  默认值： json。
#### `--query -q`
JMESPath 查询字符串。 请参阅[ http://jmespath.org/ ](http://jmespath.org/])有关详细信息和示例。
#### `--verbose`
提高日志记录详细程度。 使用--debug 可获取完整的调试日志。

## <a name="next-steps"></a>后续步骤

有关如何安装详细信息**mssqlctl**工具，请参阅[安装 mssqlctl 来管理 SQL Server 2019 大数据群集](deploy-install-mssqlctl.md)。