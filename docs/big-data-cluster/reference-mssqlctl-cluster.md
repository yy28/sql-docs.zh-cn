---
title: mssqlctl 群集引用
titleSuffix: SQL Server big data clusters
description: Mssqlctl 群集命令的参考文章。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 04/23/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: c69aeced2378e018376172e1fb6370d56706ecb7
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2019
ms.locfileid: "63473332"
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
[mssqlctl 群集调试](reference-mssqlctl-cluster-debug.md) | 调试命令。
## <a name="mssqlctl-cluster-create"></a>mssqlctl 群集创建
创建 SQL Server 大数据群集。
```bash
mssqlctl cluster create [--config-file -f] 
                        [--accept-eula -e]  
```
### <a name="optional-parameters"></a>可选参数
#### `--config-file -f`
群集用于部署群集的配置配置文件: [aks-适用于开发人员-test.json，kubeadm-适用于开发人员-test.json，minikube-适用于开发人员-test.json']
#### `--accept-eula -e`
您是否接受许可条款？ [是/否]。
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
删除 SQL Server 大数据群集。
```bash
mssqlctl cluster delete --name -n 
                        [--force -f]
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
