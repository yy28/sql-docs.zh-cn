---
title: mssqlctl 群集配置引用
titleSuffix: SQL Server big data clusters
description: Mssqlctl 群集命令的参考文章。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 04/23/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 3a4693c5ffb68ad555d97d02f983fadf4e6bbd9a
ms.sourcegitcommit: d5cd4a5271df96804e9b1a27e440fb6fbfac1220
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2019
ms.locfileid: "64774670"
---
# <a name="mssqlctl-cluster-config"></a>mssqlctl 群集配置

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

以下文章提供了参考**群集配置**中的命令**mssqlctl**工具。 有关其他详细信息**mssqlctl**命令，请参阅[mssqlctl 引用](reference-mssqlctl.md)。

## <a name="commands"></a>命令
|     |     |
| --- | --- |
[mssqlctl cluster config get](#mssqlctl-cluster-config-get) | 获取群集配置-kube 配置需要你的系统上。
[mssqlctl 群集配置 init](#mssqlctl-cluster-config-init) | 初始化群集配置。
[mssqlctl 群集配置列表](#mssqlctl-cluster-config-list) | 列出了可用的配置文件选项。
[mssqlctl 群集配置部分](reference-mssqlctl-cluster-config-section.md) | 使用配置文件的各个部分的命令。
## <a name="mssqlctl-cluster-config-get"></a>获取 mssqlctl 群集配置
获取 SQL Server 大数据群集的当前配置文件。
```bash
mssqlctl cluster config get --name -n 
                            [--output-file -f]
```
### <a name="required-parameters"></a>必需的参数
#### `--name -n`
群集名称，用于 kubernetes 命名空间。
### <a name="optional-parameters"></a>可选参数
#### `--output-file -f`
若要将结果存储在输出文件。 默认值： 定向到 stdout。
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
## <a name="mssqlctl-cluster-config-init"></a>mssqlctl 群集配置 init
初始化群集配置文件，根据为用户指定的默认类型。
```bash
mssqlctl cluster config init [--target -t] 
                             [--src -s]
```
### <a name="optional-parameters"></a>可选参数
#### `--target -t`
你希望放置，在配置文件默认为使用自定义 config.json cwd 文件路径。
#### `--src -s`
配置源: [aks-适用于开发人员-test.json，kubeadm-适用于开发人员-test.json，minikube-适用于开发人员-test.json']
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
## <a name="mssqlctl-cluster-config-list"></a>mssqlctl 群集配置列表
列出了在群集配置 init 中使用的可用配置文件选项
```bash
mssqlctl cluster config list [--config-file -f] 
                             
```
### <a name="optional-parameters"></a>可选参数
#### `--config-file -f`
默认的配置文件: [aks-适用于开发人员-test.json，kubeadm-适用于开发人员-test.json，minikube-适用于开发人员-test.json]
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