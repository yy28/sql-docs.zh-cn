---
title: mssqlctl 群集调试参考
titleSuffix: SQL Server big data clusters
description: Mssqlctl 群集调试命令的参考文章。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 04/23/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 5099a9ac611602e0c4c8d7f0103421e34b7fa8a2
ms.sourcegitcommit: d5cd4a5271df96804e9b1a27e440fb6fbfac1220
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2019
ms.locfileid: "64774856"
---
# <a name="mssqlctl-cluster-debug"></a>mssqlctl 群集调试

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

以下文章提供了参考**群集调试**中的命令**mssqlctl**工具。 有关其他详细信息**mssqlctl**命令，请参阅[mssqlctl 引用](reference-mssqlctl.md)。

## <a name="commands"></a>命令
|     |     |
| --- | --- |
[mssqlctl cluster debug copy-logs](#mssqlctl-cluster-debug-copy-logs) | 复制日志。
[mssqlctl 群集调试转储](#mssqlctl-cluster-debug-dump) | 触发器日志记录转储。
## <a name="mssqlctl-cluster-debug-copy-logs"></a>mssqlctl cluster debug copy-logs
从群集复制调试日志。
```bash
mssqlctl cluster debug copy-logs --namespace -n 
                                 [--container -c]  
                                 [--target-folder -d]  
                                 [--pod -p]  
                                 [--timeout -t]
```
### <a name="required-parameters"></a>必需的参数
#### `--namespace -n`
群集名称，用于 kubernetes 命名空间。
### <a name="optional-parameters"></a>可选参数
#### `--container -c`
复制日志的容器的名称类似，可选，默认情况下将复制的所有容器的日志。 无法指定多次。 如果指定了多次，最后一个将使用
#### `--target-folder -d`
要复制到日志的目标文件夹路径。 可选，默认情况下结果中创建的本地文件夹。  无法指定多次。 如果指定了多次，最后一个将使用
#### `--pod -p`
将复制的 pod 名称相似的日志。 可选的所有 pod 的默认副本日志。 无法指定多次。 如果指定了多次，最后一个将使用
#### `--timeout -t`
等待命令完成的秒数。 默认值为 0，这是不受限制
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
## <a name="mssqlctl-cluster-debug-dump"></a>mssqlctl 群集调试转储
触发日志记录转储并将其复制容器中。
```bash
mssqlctl cluster debug dump --namespace -n 
                            --container -c  
                            [--target-folder -d]
```
### <a name="required-parameters"></a>必需的参数
#### `--namespace -n`
群集名称，用于 kubernetes 命名空间。
#### `--container -c`
复制日志的容器的名称类似，可选，默认情况下将复制的所有容器的日志。 无法指定多次。 如果指定了多次，最后一个将使用
### <a name="optional-parameters"></a>可选参数
#### `--target-folder -d`
要复制到日志的目标文件夹路径。 可选，默认情况下结果中创建的本地文件夹。  无法指定多次。 如果指定了多次，最后一个将使用 `./output/dump`
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