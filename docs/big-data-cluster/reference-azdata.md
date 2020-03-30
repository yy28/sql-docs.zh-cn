---
title: azdata 参考
titleSuffix: SQL Server big data clusters
description: azdata 命令的参考文章。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 94adabb2ace2f5619abd700b2652aa7d88f3e1aa
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "74822344"
---
# <a name="azdata"></a>azdata

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]  

本参考文章介绍 `azdata` 命令。

## <a name="commands"></a>命令
|     |     |
| --- | --- |
|[azdata bdc](reference-azdata-bdc.md) | 选择、管理和操作 SQL Server 大数据群集。 |
|[azdata app](reference-azdata-app.md) | 创建、删除、运行和管理应用程序。 |
[azdata login](#azdata-login) | 登录到群集的控制器终结点，并将其命名空间设置为活动上下文。 若要在登录时使用密码，必须设置 AZDATA_PASSWORD 环境变量。
[azdata logout](#azdata-logout) | 注销群集。
|[azdata context](reference-azdata-context.md) | 上下文管理命令。 |
|[azdata control](reference-azdata-control.md) | 创建、删除和管理控制平面。 |
|[azdata sql](reference-azdata-sql.md) | SQL DB CLI 允许用户通过 T-SQL 与 SQL Server 交互。 |
|[azdata notebook](reference-azdata-notebook.md) | 用于从终端查看、运行和管理笔记本的命令。 |
## <a name="azdata-login"></a>azdata login
部署群集时，它将在部署期间列出控制器终结点，你应该使用该终结点登录。  如果不知道控制器终结点，则可通过在系统上将群集的 kube 配置置于默认位置 <user home>/.kube/config 进行登录，或使用 KUBECONFIG 环境变量（即 export KUBECONFIG=path/to/.kube/config）进行登录。登录时，此群集的命名空间将设置为活动上下文。
```bash
azdata login [--auth] 
             [--endpoint -e]  
             [--accept-eula -a]  
             [--namespace -n]  
             [--username -u]  
             [--principal -p]
```
### <a name="examples"></a>示例
使用基本身份验证登录。
```bash
azdata login --auth basic --username johndoe --endpoint https://<ip or domain name>:30080            
```
使用 Active Directory 登录。
```bash
azdata login --auth ad --endpoint https://<ip or domain name>:30080                
```
使用带有显式主体的 Active Directory 登录。
```bash
azdata login --auth ad --principal johndoe@COSTOSO.COM --endpoint https://<ip or domain name>:30080
```
以交互方式登录。 如果未指定为参数，则系统会始终提示输入群集名称。 如果在系统上设置了 AZDATA_USERNAME、AZDATA_PASSWORD 和 ACCEPT_EULA 环境变量，则不会提示输入这些变量。 如果系统上设置了 kube 配置或正在使用 KUBECONFIG 环境变量来指定配置路径，则交互式体验将首先尝试使用该配置，然后在配置失败时进行提示。
```bash
azdata login
```
登录（非交互式）。 通过将群集名称、控制器用户名、控制器终结点和接受 EULA 设置为参数进行登录。 必须设置 AZDATA_PASSWORD 环境变量。  如果不想指定控制器终结点，请在计算机上将 kube 配置置于默认位置 <user home>/.kube/config，或使用 KUBECONFIG 环境变量（即 export KUBECONFIG=path/to/.kube/config）。
```bash
azdata login --namespace ClusterName --username johndoe@contoso.com  --endpoint https://<ip or domain name>:30080 --accept-eula yes
```
在计算机上使用 kube 配置登录，并设置 AZDATA_USERNAME、AZDATA_PASSWORD 和 ACCEPT_EULA 环境变量。
```bash
azdata login -n ClusterName
```
### <a name="optional-parameters"></a>可选参数
#### `--auth`
身份验证策略。 基本身份验证或 Active Directory 身份验证。 默认为“基本”身份验证。
#### `--endpoint -e`
群集控制器终结点“https://host:port”。 如果不想使用此参数，则可在计算机上使用 kube 配置。 请确保配置位于默认位置 <user home>/.kube/config 或使用 KUBECONFIG 环境变量。
#### `--accept-eula -a`
是否接受许可条款？ [是/否]。 如果不想使用此参数，可以将环境变量 ACCEPT_EULA 设置为“yes”。 可以在 https://aka.ms/eula-azdata-en 查看此产品的许可条款。
#### `--namespace -n`
群集控制平面的命名空间。
#### `--username -u`
帐户用户。 如果不想使用此参数，则可设置环境变量 AZDATA_USERNAME。
#### `--principal -p`
你的 Kerberos 领域。 在大多数情况下，Kerberos 领域是你的域名，采用大写字母。
### <a name="global-arguments"></a>全局参数
#### `--debug`
提高日志记录详细程度以显示所有调试日志。
#### `--help -h`
显示此帮助消息并退出。
#### `--output -o`
输出格式。  允许的值：json、jsonc、table、tsv。  默认值：json。
#### `--query -q`
JMESPath 查询字符串。 请参阅 [http://jmespath.org/](http://jmespath.org/)，获取详细信息和示例。
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
JMESPath 查询字符串。 请参阅 [http://jmespath.org/](http://jmespath.org/)，获取详细信息和示例。
#### `--verbose`
提高日志记录详细程度。 使用 --debug 获取完整的调试日志。

## <a name="next-steps"></a>后续步骤

有关其他 `azdata` 命令的详细信息，请参阅 [azdata 参考](reference-azdata.md)。 有关如何安装 `azdata` 工具的详细信息，请参阅[安装 azdata 以管理 SQL Server 2019 大数据群集](deploy-install-azdata.md)。
