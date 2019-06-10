---
title: mssqlctl 群集引用
titleSuffix: SQL Server big data clusters
description: Mssqlctl 群集命令的参考文章。
author: rothja
ms.author: jroth
manager: jroth
ms.date: 05/22/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 654888bc27fec43abb8a8f511b0de7a4972e4377
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2019
ms.locfileid: "66779258"
---
# <a name="mssqlctl-cluster"></a>mssqlctl 群集

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

以下文章提供了参考**群集**中的命令**mssqlctl**工具。 有关其他详细信息**mssqlctl**命令，请参阅[mssqlctl 引用](reference-mssqlctl.md)。

## <a name="commands"></a>命令
|     |     |
| --- | --- |
[mssqlctl 群集创建](#mssqlctl-cluster-create) | 创建群集。
[mssqlctl 群集删除](#mssqlctl-cluster-delete) | 删除群集。
[mssqlctl 群集配置](reference-mssqlctl-cluster-config.md) | 群集配置命令。
[mssqlctl 群集终结点](reference-mssqlctl-cluster-endpoint.md) | 终结点的命令。
[mssqlctl 群集状态](reference-mssqlctl-cluster-status.md) | 状态的命令。
[mssqlctl 群集调试](reference-mssqlctl-cluster-debug.md) | 调试命令。
[mssqlctl cluster storage-pool](reference-mssqlctl-cluster-storage-pool.md) | 管理群集存储池。
## <a name="mssqlctl-cluster-create"></a>mssqlctl 群集创建
创建 SQL Server 大数据群集-kube 配置要求以及以下环境变量 [CONTROLLER_USERNAME、 CONTROLLER_PASSWORD、 DOCKER_USERNAME、 DOCKER_PASSWORD、 MSSQL_SA_PASSWORD、 KNOX_PASSWORD] 在系统上。
```bash
mssqlctl cluster create [--config-file -c] 
                        [--accept-eula -a]  
                        [--node-label -l]  
                        [--force -f]
```
### <a name="examples"></a>示例
引导式群集的部署体验-你将收到会提示你输入所需的值。
```bash
mssqlctl cluster create
```
群集部署使用的参数。
```bash
mssqlctl cluster create --accept-eula yes --config-file aks-dev-test.json
```
使用参数-无提示的群集部署将作为使用标志--force 提供。
```bash
mssqlctl cluster create --accept-eula yes --config-file aks-dev-test.json --force
```
### <a name="optional-parameters"></a>可选参数
#### `--config-file -c`
群集用于部署群集的配置配置文件: [aks-适用于开发人员-test.json，kubeadm-适用于开发人员-test.json，minikube-适用于开发人员-test.json']
#### `--accept-eula -a`
您是否接受许可条款？ [是/否]。 如果您不想要使用此参数，您可能会设置环境变量 ACCEPT_EULA 为是
#### `--node-label -l`
群集节点标签，用于指定要部署到哪些节点。
#### `--force -f`
强制创建，将不提示用户输入任何值并将 stderr 的一部分打印所有问题。
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
## <a name="mssqlctl-cluster-delete"></a>mssqlctl 群集删除
删除 SQL Server 大数据群集-kube 配置要求以及以下环境变量 [CONTROLLER_USERNAME'，'CONTROLLER_PASSWORD] 在系统上。
```bash
mssqlctl cluster delete --name -n 
                        [--force -f]
```
### <a name="examples"></a>示例
群集删除其中的控制器的用户名和密码已设置系统环境中。
```bash
mssqlctl cluster delete --name <cluster_name>
```
### <a name="required-parameters"></a>必需的参数
#### `--name -n`
群集名称，用于 kubernetes 命名空间。
### <a name="optional-parameters"></a>可选参数
#### `--force -f`
强制删除群集。
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

有关其他详细信息**mssqlctl**命令，请参阅[mssqlctl 引用](reference-mssqlctl.md)。 有关如何安装详细信息**mssqlctl**工具，请参阅[安装 mssqlctl 来管理 SQL Server 2019 大数据群集](deploy-install-mssqlctl.md)。
