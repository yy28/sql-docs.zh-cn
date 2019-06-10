---
title: mssqlctl 群集配置引用
titleSuffix: SQL Server big data clusters
description: Mssqlctl 群集命令的参考文章。
author: rothja
ms.author: jroth
manager: jroth
ms.date: 05/22/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 74097057702ad32a803c440d92b0ed7c8f855880
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2019
ms.locfileid: "66779417"
---
# <a name="mssqlctl-cluster-config"></a>mssqlctl 群集配置

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

以下文章提供了参考**群集配置**中的命令**mssqlctl**工具。 有关其他详细信息**mssqlctl**命令，请参阅[mssqlctl 引用](reference-mssqlctl.md)。

## <a name="commands"></a>命令
|     |     |
| --- | --- |
[mssqlctl 群集 config show](#mssqlctl-cluster-config-show) | 获取 SQL Server 大数据群集的当前配置。
[mssqlctl 群集配置 init](#mssqlctl-cluster-config-init) | 初始化可用于群集的群集配置配置文件创建。
[mssqlctl 群集配置列表](#mssqlctl-cluster-config-list) | 列出了可用的配置文件选项。
[mssqlctl 群集配置部分](reference-mssqlctl-cluster-config-section.md) | 使用群集配置文件的各个部分的命令。
## <a name="mssqlctl-cluster-config-show"></a>mssqlctl 群集 config show
获取 SQL Server 大数据群集的当前配置文件并将其输出到目标文件或非常将其打印到控制台。
```bash
mssqlctl cluster config show [--target -t] 
                             [--force -f]
```
### <a name="examples"></a>示例
在你的控制台中显示的群集配置
```bash
mssqlctl cluster config show
```
### <a name="optional-parameters"></a>可选参数
#### `--target -t`
若要将结果存储在输出文件。 默认值： 定向到 stdout。
#### `--force -f`
强制覆盖目标文件。
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
初始化可用于群集的群集配置配置文件创建。 可以从 3 个选项中的参数中指定的配置文件的特定源。
```bash
mssqlctl cluster config init [--target -t] 
                             [--src -s]  
                             [--force -f]
```
### <a name="examples"></a>示例
引导式群集配置 init 体验-你将收到会提示你输入所需的值。
```bash
mssqlctl cluster config init
```
群集使用的参数配置 init，创建的 aks 开发-测试中的配置文件。 / custom.json。
```bash
mssqlctl cluster config init --src aks-dev-test.json --target custom.json
```
### <a name="optional-parameters"></a>可选参数
#### `--target -t`
你想在配置配置文件放置，默认为使用自定义 config.json cwd 文件路径。
#### `--src -s`
配置配置文件源: [aks-适用于开发人员-test.json，kubeadm-适用于开发人员-test.json，minikube-适用于开发人员-test.json']
#### `--force -f`
强制覆盖目标文件。
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
mssqlctl cluster config list [--config-file -c] 
                             
```
### <a name="examples"></a>示例
显示所有可用的配置配置文件名称。
```bash
mssqlctl cluster config list
```
显示了特定的配置配置文件的 json。
```bash
mssqlctl cluster config list --config-file aks-dev-test.json
```
### <a name="optional-parameters"></a>可选参数
#### `--config-file -c`
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