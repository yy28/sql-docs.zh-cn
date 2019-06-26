---
title: mssqlctl bdc 引用
titleSuffix: SQL Server big data clusters
description: Mssqlctl bdc 命令的参考文章。
author: rothja
ms.author: jroth
manager: jroth
ms.date: 06/26/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 2c16a8121f2a0ec90fe8141c78e690bf212b5f27
ms.sourcegitcommit: ce5770d8b91c18ba5ad031e1a96a657bde4cae55
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67394229"
---
# <a name="mssqlctl-bdc"></a>mssqlctl bdc

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

以下文章提供了参考**bdc**中的命令**mssqlctl**工具。 有关其他详细信息**mssqlctl**命令，请参阅[mssqlctl 引用](reference-mssqlctl.md)。

## <a name="commands"></a>命令
|     |     |
| --- | --- |
[mssqlctl bdc create](#mssqlctl-bdc-create) | 创建大数据群集。
[mssqlctl bdc delete](#mssqlctl-bdc-delete) | 删除大数据群集。
[mssqlctl bdc config](reference-mssqlctl-bdc-config.md) | 配置命令。
[mssqlctl bdc endpoint](reference-mssqlctl-bdc-endpoint.md) | 终结点的命令。
[mssqlctl bdc status](reference-mssqlctl-bdc-status.md) | 状态的命令。
[mssqlctl bdc debug](reference-mssqlctl-bdc-debug.md) | 调试命令。
[mssqlctl bdc storage-pool](reference-mssqlctl-bdc-storage-pool.md) | 存储池命令。
[mssqlctl bdc control](reference-mssqlctl-bdc-control.md) | 控制命令。
[mssqlctl bdc pool](reference-mssqlctl-bdc-pool.md) | 池的命令。
## <a name="mssqlctl-bdc-create"></a>mssqlctl bdc 创建
创建 SQL Server 大数据群集-kube 配置要求以及以下环境变量 [CONTROLLER_USERNAME、 CONTROLLER_PASSWORD、 DOCKER_USERNAME、 DOCKER_PASSWORD、 MSSQL_SA_PASSWORD、 KNOX_PASSWORD] 在系统上。
```bash
mssqlctl bdc create [--config-profile -c] 
                    [--accept-eula -a]  
                    [--node-label -l]  
                    [--force -f]
```
### <a name="examples"></a>示例
引导式的 BDC 部署体验-你将收到会提示你输入所需的值。
```bash
mssqlctl bdc create
```
BDC 部署使用的参数。
```bash
mssqlctl bdc create --accept-eula yes --config-profile aks-dev-test
```
使用参数-BDC 部署将作为使用标志--force 提供无提示。
```bash
mssqlctl bdc create --accept-eula yes --config-profile aks-dev-test --force
```
### <a name="optional-parameters"></a>可选参数
#### `--config-profile -c`
BDC 配置配置文件，用于部署群集: [aks-开发-测试、 kubeadm-开发-测试、 minikube-开发-测试]
#### `--accept-eula -a`
您是否接受许可条款？ [是/否]。 如果您不想要使用此参数，您可能会设置环境变量 ACCEPT_EULA 为是
#### `--node-label -l`
BDC 节点标签，用于指定要部署到哪些节点。
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
## <a name="mssqlctl-bdc-delete"></a>mssqlctl bdc 删除
删除 SQL Server 大数据群集-kube 配置要求以及以下环境变量 [CONTROLLER_USERNAME'，'CONTROLLER_PASSWORD] 在系统上。
```bash
mssqlctl bdc delete --name -n 
                    [--force -f]
```
### <a name="examples"></a>示例
BDC 其中控制器用户名和密码已设置系统环境中删除。
```bash
mssqlctl bdc delete --name <cluster_name>
```
### <a name="required-parameters"></a>必需的参数
#### `--name -n`
BDC 的名称，用于 kubernetes 命名空间。
### <a name="optional-parameters"></a>可选参数
#### `--force -f`
强制删除 BDC。
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
