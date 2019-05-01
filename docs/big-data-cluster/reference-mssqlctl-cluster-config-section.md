---
title: mssqlctl 群集配置部分引用
titleSuffix: SQL Server big data clusters
description: Mssqlctl 群集配置部分命令的参考文章。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 04/23/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: d5a793e7d0fcaf782a09a4981491ef0a8d90ab5a
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2019
ms.locfileid: "63759134"
---
# <a name="mssqlctl-cluster-config-section"></a>mssqlctl 群集配置部分

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

以下文章提供了参考**群集配置节**中的命令**mssqlctl**工具。 有关其他详细信息**mssqlctl**命令，请参阅[mssqlctl 引用](reference-mssqlctl.md)。

## <a name="commands"></a>命令
|     |     |
| --- | --- |
[获取 mssqlctl 群集配置部分](#mssqlctl-cluster-config-section-get) | 获取从配置文件的节。
[mssqlctl 群集配置部分，设置](#mssqlctl-cluster-config-section-set) | 设置用于配置文件的节。
## <a name="mssqlctl-cluster-config-section-get"></a>获取 mssqlctl 群集配置部分
从给定的 json 路径根据所选的配置文件中获取指定的节。
```bash
mssqlctl cluster config section get --json-path -j 
                                    --config-file -f  
                                    [--target -t]
```
### <a name="required-parameters"></a>必需的参数
#### `--json-path -j`
从配置文件，即 key1.key2.key3 要指向的部分或值的 json 密钥路径。 使用 jsonpath 查询语言， https://github.com/h2non/jsonpath-ng，例如:-j $。 spec.pools [？ (@.spec.type = ="Master")]...终结点的
#### `--config-file -f`
群集配置文件路径。
### <a name="optional-parameters"></a>可选参数
#### `--target -t`
放置到您喜欢的部分文件的文件路径。
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
根据给定的 json 路径在所选的配置文件中设置指定的节。
```bash
mssqlctl cluster config section set --config-file -f 
                                    [--json-values -j]  
                                    [--patch-file -p]
```
### <a name="required-parameters"></a>必需的参数
#### `--config-file -f`
想要设置的配置的群集配置文件路径
### <a name="optional-parameters"></a>可选参数
#### `--json-values -j`
键值对列表的值的 json 路径： key1.subkey1=value1,key2.subkey2=value2。 你可能会提供内联的 json 值如： 键 = {"kind":"群集"，"name":"测试群集"}，或者提供文件路径，例如 key=./values.json
#### `--patch-file -p`
基于 jsonpatch 库和 jsonpath 的修补程序 json 文件的路径： https://github.com/stefankoegl/python-json-patch ， https://github.com/h2non/jsonpath-ng -一个简单的示例: {"修补": [{"op":"添加"、"路径":"metadata.name"、"value":"test"}，{"op":"添加"、"路径":"metadata.array"、"value": [1，2，3]}]}请包括密钥"修补程序"，并具有的值是你想要的修补程序的数组。  它将这种情况下执行。 A more complex example: {"patch": [{"op": "replace", "path": "$.spec.pools[?(@.spec.type == 'Master')]..endpoints","value": {"name":"新的终结点"}}]}
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