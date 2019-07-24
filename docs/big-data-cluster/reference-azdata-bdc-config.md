---
title: azdata bdc config 引用
titleSuffix: SQL Server big data clusters
description: Azdata bdc 命令的参考文章。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: ed777391af3695da69e04c0e2693cff912c76771
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426287"
---
# <a name="azdata-bdc-config"></a>azdata bdc 配置

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

以下文章提供了**azdata**工具中的**bdc config**命令参考。 有关其他**azdata**命令的详细信息, 请参阅[azdata reference](reference-azdata.md)。

## <a name="commands"></a>命令
|     |     |
| --- | --- |
[azdata bdc 配置初始化](#azdata-bdc-config-init) | 初始化可用于群集创建的大数据群集配置文件。
[azdata bdc 配置列表](#azdata-bdc-config-list) | 列出可用的配置文件选择。
[azdata bdc config show](#azdata-bdc-config-show) | 显示指定的本地文件的 BDC 当前配置或配置, 即自定义/cluster。
[azdata bdc 配置添加](#azdata-bdc-config-add) | 在配置文件中为 json 路径添加值。
[azdata bdc 配置删除](#azdata-bdc-config-remove) | 在配置文件中删除 json 路径的值。
[azdata bdc config 替换](#azdata-bdc-config-replace) | 在配置文件中替换 json 路径的值。
[azdata bdc 配置修补程序](#azdata-bdc-config-patch) | 修补基于 json 修补程序文件的配置文件。
## <a name="azdata-bdc-config-init"></a>azdata bdc 配置初始化
初始化可用于群集创建的大数据群集配置文件。 可以从3个选项的参数中指定配置文件的特定源。
```bash
azdata bdc config init [--target -t] 
                       [--source -s]  
                       [--force -f]  
                       [--accept-eula -a]
```
### <a name="examples"></a>示例
引导式 BDC config init 体验-您将收到所需值的提示。
```bash
azdata bdc config init
```
BDC config init with arguments, 在/custom. 中创建 aks 的配置配置文件。
```bash
azdata bdc config init --source aks-dev-test --target custom
```
### <a name="optional-parameters"></a>可选参数
#### `--target -t`
要放置配置配置文件的位置的文件路径, 默认值为 "与自定义配置文件的 cwd"。
#### `--source -s`
配置配置文件源: [' aks ', ' kubeadm ', ' minikube-test ']
#### `--force -f`
强制覆盖目标文件。
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
## <a name="azdata-bdc-config-list"></a>azdata bdc 配置列表
列出在中使用的可用配置文件选项`bdc config init`
```bash
azdata bdc config list [--config-profile -c] 
                       [--type -t]  
                       [--accept-eula -a]
```
### <a name="examples"></a>示例
显示所有可用的配置文件名称。
```bash
azdata bdc config list
```
显示特定配置文件的 json。
```bash
azdata bdc config list --config-profile aks-dev-test
```
### <a name="optional-parameters"></a>可选参数
#### `--config-profile -c`
默认配置文件: [' aks ', ' kubeadm ', ' minikube-test ']
#### `--type -t`
要查看的配置类型。
`cluster`
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
## <a name="azdata-bdc-config-show"></a>azdata bdc config show
显示指定的本地文件的 BDC 当前配置或配置, 即自定义/cluster。 如果你只想获取一个部分, 则该命令还可以采用 json 路径。  你还可以指定要输出到的目标文件。  如果未指定目标文件, 则只会将其输出到终端。
```bash
azdata bdc config show [--config-file -c] 
                       [--target -t]  
                       [--json-path -j]  
                       [--force -f]
```
### <a name="examples"></a>示例
在控制台中显示 BDC 配置
```bash
azdata bdc config show
```
在本地配置文件中, 在简单 json 密钥路径的末尾获取值。
```bash
azdata bdc config show --config-file custom-config/cluster.json --json-path 'metadata.name' --target section.json
```
在本地配置文件中, 在 json 密钥路径的末尾获取值, 条件是
```bash
azdata bdc config show --config-file custom-config/cluster.json  --json-path '$.spec.pools[?(@.spec.type=="Storage")].spec' --target section.json
```
### <a name="optional-parameters"></a>可选参数
#### `--config-file -c`
大数据群集配置文件路径 (如果不想 currentlylogged 的配置), 即自定义/cluster。
#### `--target -t`
要在其中存储结果的输出文件。 默认值: 定向到 stdout。
#### `--json-path -j`
Json 密钥路径, 该路径将从配置中获得所需的部分或值 (即 key3)。 使用 jsonpath 查询语言 https://jsonpath.com/ , 例如:-j ' $. pool [？ (@.spec.type = = "Master")]。终结点
#### `--force -f`
强制覆盖目标文件。
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
## <a name="azdata-bdc-config-add"></a>azdata bdc 配置添加
将值添加到配置文件中的 json 路径。  下面的所有示例都在 Bash 中提供。  如果使用其他命令行, 请注意, 可能需要 escapequotations。  或者, 您可以使用修补文件功能。
```bash
azdata bdc config add --config-file -c 
                      --json-values -j
```
### <a name="examples"></a>示例
Ex 1-添加控制平面存储。
```bash
azdata bdc config add --config-file custom/control.json --json-values 'spec.storage={"accessMode":"ReadWriteOnce","className":"managed-premium","size":"10Gi"}'
```
### <a name="required-parameters"></a>必需的参数
#### `--config-file -c`
要设置的配置的大数据群集配置文件路径, 即自定义/cluster。
#### `--json-values -j`
值的 json 路径的键值对列表: subkey1 = value1, subkey2 = value2。 你可以提供内联 json 值, 例如: key = "{" kind ":" cluster "," name ":" test-cluster "}" 或提供文件路径, 如 key =./values.json。 添加不支持条件。  有关路径 http://jsonpatch.com/ 外观的示例, 请参阅。  如果要访问某个数组, 则必须通过指示索引来实现, 如 key. 0 = value
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
## <a name="azdata-bdc-config-remove"></a>azdata bdc 配置删除
删除配置文件的 json 路径中的值。  下面的所有示例都在 Bash 中提供。  如果使用其他命令行, 请注意, 可能需要 escapequotations。  或者, 您可以使用修补文件功能。
```bash
azdata bdc config remove --config-file -c 
                         --json-path -j
```
### <a name="examples"></a>示例
Ex 1-删除控制平面存储。
```bash
azdata bdc config remove --config-file custom/control.json --json-path '.spec.storage'
```
### <a name="required-parameters"></a>必需的参数
#### `--config-file -c`
要设置的配置的大数据群集配置文件路径, 即自定义/cluster。
#### `--json-path -j`
基于 jsonpatch 库的 json 路径列表, 该列表指示要删除的值, 例如: subkey1、subkey2。 删除不支持条件。 有关路径 http://jsonpatch.com/ 外观的示例, 请参阅。  如果要访问某个数组, 则必须通过指示索引来实现, 如 key. 0 = value
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
## <a name="azdata-bdc-config-replace"></a>azdata bdc config 替换
替换配置文件中 json 路径处的值。  Bash 中提供了所有 examplesbelow。  如果使用其他命令行, 请注意, 可能需要 escapequotations。  或者, 您可以使用修补文件功能。
```bash
azdata bdc config replace --config-file -c 
                          --json-values -j
```
### <a name="examples"></a>示例
Ex 1-替换单个终结点 (控制器终结点) 的端口。
```bash
azdata bdc config replace --config-file custom/control.json --json-values '$.spec.endpoints[?(@.name=="Controller")].port=30080'
```
Ex 2-替换控制平面存储。
```bash
azdata bdc config replace --config-file custom/control.json --json-values 'spec.storage={"accessMode":"ReadWriteOnce","className":"managed-premium","size":"10Gi"}'
```
Ex 3-替换池存储, 包括副本 (存储池)。
```bash
azdata bdc config replace --config-file custom/cluster.json --json-values '$.spec.pools[?(@.spec.type == "Storage")].spec={"replicas": 2,"storage": {"className": "managed-premium","size": "10Gi","accessMode": "ReadWriteOnce"},"type": "Storage"}'
```
### <a name="required-parameters"></a>必需的参数
#### `--config-file -c`
要设置的配置的大数据群集配置文件路径, 即自定义/cluster。
#### `--json-values -j`
值的 json 路径的键值对列表: subkey1 = value1, subkey2 = value2。 你可以提供内联 json 值, 例如: key = "{" kind ":" cluster "," name ":" test-cluster "}" 或提供文件路径, 如 key =./values.json。 Replace 支持通过 jsonpath 库进行的条件。  若要使用此方法, 请使用 $ 来启动你的路径。 这将允许你执行诸如-j $. key1. key2 [？ (@.key3= = ' someValue ']. key4 = value。 你可能会看到以下示例。 有关更多帮助, 请参阅: https://jsonpath.com/
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
## <a name="azdata-bdc-config-patch"></a>azdata bdc 配置修补程序
根据给定的修补程序文件对配置文件进行修补。 请参阅 http://jsonpatch.com/ 以更好地了解如何组合路径。 由于 jsonpath 库 https://jsonpath.com/ 的原因, replace 操作可以在其路径中使用条件。 所有修补程序 json 文件必须以包含修补程序及其相应操作 (添加、替换、删除)、路径和值的 "修补程序" 键开头。 "Remove" op 不需要值, 只需要一个路径。 请参阅以下示例。
```bash
azdata bdc config patch --config-file -c 
                        --patch-file -p
```
### <a name="examples"></a>示例
Ex 1-将单个终结点 (控制器终结点) 的端口替换为修补文件。
```bash
azdata bdc config patch --config-file custom/control.json --patch ./patch.json

    Patch File Example (patch.json): 
        {"patch":[{"op":"replace","path":"$.spec.endpoints[?(@.name=='Controller')].port","value":30080}]}
```
Ex 2-将控制平面存储替换为修补文件。
```bash
azdata bdc config patch --config-file custom/control.json --patch ./patch.json

    Patch File Example (patch.json): 
        {"patch":[{"op":"replace","path":".spec.storage","value":{"accessMode":"ReadWriteMany","className":"managed-premium","size":"10Gi"}}]}
```
Ex 3-将池存储替换为包含修补程序文件的副本 (存储池)。
```bash
azdata bdc config patch --config-file custom/cluster.json --patch ./patch.json

    Patch File Example (patch.json): 
        {"patch":[{"op":"replace","path":"$.spec.pools[?(@.spec.type == 'Storage')].spec","value":{"replicas": 2,"storage": {"className": "managed-premium","size": "10Gi","accessMode": "ReadWriteOnce"},"type": "Storage"}}]}
```
### <a name="required-parameters"></a>必需的参数
#### `--config-file -c`
要设置的配置的大数据群集配置文件路径, 即自定义/cluster。
#### `--patch-file -p`
基于 jsonpatch 库的修补 json 文件的路径: http://jsonpatch.com/ 。 必须使用名为 "patch" 的密钥启动修补程序 json 文件, 此密钥的值是要进行的修补程序操作的数组。 对于修补操作的路径, 你可以使用点表示法, 如大多数操作的 key1。 如果要执行 "替换" 操作, 并且要在需要条件的数组中替换值, 请使用 jsonpath 表示法, 并以 $ 开头。 这将允许你执行如 $. key1. key2 [？ (@.key3= = ' someValue ']. key4。 请参阅以下示例。 有关条件的其他帮助, 请参阅: https://jsonpath.com/ 。
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

有关其他**azdata**命令的详细信息, 请参阅[azdata reference](reference-azdata.md)。 有关如何安装**azdata**工具的详细信息, 请参阅[安装 azdata 以管理 SQL Server 2019 大数据群集](deploy-install-azdata.md)。