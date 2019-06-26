---
title: mssqlctl bdc 配置参考
titleSuffix: SQL Server big data clusters
description: Mssqlctl bdc 命令的参考文章。
author: rothja
ms.author: jroth
manager: jroth
ms.date: 06/26/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: f57ba87ea7cbd770380497bd340b5eaa4d80f29c
ms.sourcegitcommit: ce5770d8b91c18ba5ad031e1a96a657bde4cae55
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67394159"
---
# <a name="mssqlctl-bdc-config"></a>mssqlctl bdc config

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

以下文章提供了参考**bdc config**中的命令**mssqlctl**工具。 有关其他详细信息**mssqlctl**命令，请参阅[mssqlctl 引用](reference-mssqlctl.md)。

## <a name="commands"></a>命令
|     |     |
| --- | --- |
[mssqlctl bdc config show](#mssqlctl-bdc-config-show) | 获取大数据群集的当前配置。
[mssqlctl bdc config init](#mssqlctl-bdc-config-init) | 初始化大数据群集可用于群集的配置文件创建。
[mssqlctl bdc config list](#mssqlctl-bdc-config-list) | 列出了可用的配置配置文件选项。
[mssqlctl bdc config section](reference-mssqlctl-bdc-config-section.md) | 使用大数据群集配置配置文件的各个部分的命令。
## <a name="mssqlctl-bdc-config-show"></a>mssqlctl bdc config show
获取大数据群集的当前配置的配置文件并将其输出到目标目录或相当将其打印到控制台。
```bash
mssqlctl bdc config show [--target -t] 
                         [--force -f]
```
### <a name="examples"></a>示例
在你的控制台中显示 BDC 配置
```bash
mssqlctl bdc config show
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
## <a name="mssqlctl-bdc-config-init"></a>mssqlctl bdc config init
初始化大数据群集可用于群集的配置文件创建。 可以从 3 个选项中的参数中指定的配置文件的特定源。
```bash
mssqlctl bdc config init [--target -t] 
                         [--source -s]  
                         [--force -f]
```
### <a name="examples"></a>示例
引导式的 BDC 配置 init 体验-你将收到会提示你输入所需的值。
```bash
mssqlctl bdc config init
```
BDC 配置 init，用的参数创建的 aks 开发-测试中的配置文件。 / 自定义。
```bash
mssqlctl bdc config init --source aks-dev-test --target custom
```
### <a name="optional-parameters"></a>可选参数
#### `--target -t`
你想在配置配置文件放置，默认为使用自定义 config.json cwd 文件路径。
#### `--source -s`
配置配置文件源: [aks-开发-测试、 kubeadm-开发-测试、 minikube-开发-测试]
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
## <a name="mssqlctl-bdc-config-list"></a>mssqlctl bdc config list
列出了可用的配置中使用的配置文件选项 `bdc config init`
```bash
mssqlctl bdc config list [--config-profile -c] 
                         
```
### <a name="examples"></a>示例
显示所有可用的配置配置文件名称。
```bash
mssqlctl bdc config list
```
显示了特定的配置配置文件的 json。
```bash
mssqlctl bdc config list --config-profile aks-dev-test
```
### <a name="optional-parameters"></a>可选参数
#### `--config-profile -c`
默认配置配置文件: [aks-开发-测试、 kubeadm-开发-测试、 minikube-开发-测试]
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