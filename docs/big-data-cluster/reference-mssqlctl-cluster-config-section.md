---
title: mssqlctl 群集配置部分引用
titleSuffix: SQL Server big data clusters
description: Mssqlctl 群集配置部分命令的参考文章。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 05/22/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 8239367b45ac327abde919910ccc1336ebb8f5b1
ms.sourcegitcommit: be09f0f3708f2e8eb9f6f44e632162709b4daff6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/21/2019
ms.locfileid: "65993344"
---
# <a name="mssqlctl-cluster-config-section"></a>mssqlctl 群集配置部分

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

以下文章提供了参考**群集配置节**中的命令**mssqlctl**工具。 有关其他详细信息**mssqlctl**命令，请参阅[mssqlctl 引用](reference-mssqlctl.md)。

## <a name="commands"></a>命令
|     |     |
| --- | --- |
[mssqlctl 群集配置部分中显示](#mssqlctl-cluster-config-section-show) | 获取从配置文件的节。
[mssqlctl 群集配置部分，设置](#mssqlctl-cluster-config-section-set) | 设置用于配置文件的节。
## <a name="mssqlctl-cluster-config-section-show"></a>mssqlctl 群集配置部分中显示
从给定的 json 路径根据所选的配置文件中获取指定的节。
```bash
mssqlctl cluster config section show --json-path -j 
                                     --config-file -c  
                                     [--target -t]  
                                     [--force -f]
```
### <a name="examples"></a>示例
获取一个值的简单 json 密钥路径的末尾。
```bash
mssqlctl cluster config section show --config-file custom-config.json --json-path 'metadata.name' --target section.json
```
获取与条件以 json 密钥路径的结束值
```bash
mssqlctl cluster config section show --config-file custom-config.json  --json-path '$.spec.pools[?(@.spec.type=="Storage")].spec' --target section.json
```
### <a name="required-parameters"></a>必需的参数
#### `--json-path -j`
从配置文件，即 key1.key2.key3 要指向的部分或值的 json 密钥路径。 使用 jsonpath 查询语言， https://github.com/h2non/jsonpath-ng，例如:-j $。 spec.pools [？ (@.spec.type = ="Master")]...终结点的
#### `--config-file -c`
群集配置文件路径。
### <a name="optional-parameters"></a>可选参数
#### `--target -t`
放置到您喜欢的部分文件的文件路径。 默认值： 定向到 stdout。
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
## <a name="mssqlctl-cluster-config-section-set"></a>mssqlctl 群集配置部分，设置
根据给定的 json 路径在所选的配置文件中设置指定的节。  在 Bash 中提供所有 examplesbelow。  如果使用另一个命令行，请注意，您可能需要相应地为 escapequotations。  或者，可以使用修补程序文件功能。
```bash
mssqlctl cluster config section set --config-file -c 
                                    [--json-values -j]  
                                    [--patch-file -p]
```
### <a name="examples"></a>示例
示例 1 （内联）-设置单个终结点 （控制器终结点） 的端口。
```bash
mssqlctl cluster config section set --config-file custom-config.json --json-values '$.spec.controlPlane.spec.endpoints[?(@.name=="Controller")].port=30080'
```
1 （修补程序）-例如使用修补程序文件设置的单个终结点 （控制器终结点） 的端口。
```bash
mssqlctl cluster config section set --config-file custom-config.json --patch ./patch.json

    Patch File Example (patch.json): 
        {"patch":[{"op":"replace","path":"$.spec.controlPlane.spec.endpoints[?(@.name=='Controller')].port","value":30080}]}
```
示例 2 （内联） 的组控制平面存储。
```bash
mssqlctl cluster config section set --config-file custom-config.json --json-values 'spec.controlPlane.spec.storage=spec.controlPlane.spec.storage={"accessMode":"ReadWriteOnce","className":"managed-premium","size":"10Gi"}'
```
示例 2 （修补程序） 的组控制平面存储与修补程序文件。
```bash
mssqlctl cluster config section set --config-file custom-config.json --patch ./patch.json

    Patch File Example (patch.json): 
        {"patch":[{"op":"replace","path":"spec.controlPlane.spec.storage","value":{"accessMode":"ReadWriteMany","className":"managed-premium","size":"10Gi"}}]}
```
例如 3(inline)-设置池存储，包括副本 （存储池）。
```bash
mssqlctl cluster config section set --config-file custom-config.json --json-values '$.spec.pools[?(@.spec.type == "Storage")].spec={"replicas": 2,"storage": {"className": "managed-premium","size": "10Gi","accessMode": "ReadWriteOnce"},"type": "Storage"}'
```
示例 3 (patch)-设置池存储，包括使用修补程序文件的副本 （存储池）。
```bash
mssqlctl cluster config section set --config-file custom-config.json --patch ./patch.json

    Patch File Example (patch.json): 
        {"patch":[{"op":"replace","path":"$.spec.pools[?(@.spec.type == 'Storage')].spec","value":{"replicas": 2,"storage": {"className": "managed-premium","size": "10Gi","accessMode": "ReadWriteOnce"},"type": "Storage"}}]}
```
### <a name="required-parameters"></a>必需的参数
#### `--config-file -c`
想要设置的配置的群集配置文件路径
### <a name="optional-parameters"></a>可选参数
#### `--json-values -j`
键值对列表的值的 json 路径： key1.subkey1=value1,key2.subkey2=value2。 你可能会提供内联的 json 值如： 键 = {"kind":"群集"，"name":"测试群集"}，或者提供文件路径，例如 key=./values.json。 如果你想要设置一个值，需要条件，请使用 jsonpath 表示法由起始你以 $ 的路径。 This will allow you to do a conditional such as -j $.key1.key2[?(@.key3=='someValue'].key4=value. 可能会看到下面的示例。 有关更多帮助，请参阅： https://jsonpath.com/
#### `--patch-file -p`
基于 jsonpatch 库修补程序 json 文件的路径： http://jsonpatch.com/。 你必须使用名为"patch"，其值是你想要的修补程序操作的数组的项启动修补程序 json 文件。 对于修补操作的路径，可能会使用点表示法，例如 key1.key2 来执行大部分操作。 如果你想要执行替换操作，并且你正在替换一个数组，其中需要在条件中的值，请使用 jsonpath 表示法由起始你以 $ 的路径。 This will allow you to do a conditional such as $.key1.key2[?(@.key3=='someValue'].key4. 请参阅下面的示例。 有关更多帮助，请参阅： https://jsonpath.com/。
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