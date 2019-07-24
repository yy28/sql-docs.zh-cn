---
title: azdata bdc 调试引用
titleSuffix: SQL Server big data clusters
description: Azdata bdc 调试命令的参考文章。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 38c327287273ae6596326d88d9e0d67c8e014d47
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426227"
---
# <a name="azdata-bdc-debug"></a>azdata bdc 调试

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

以下文章提供了**azdata**工具中的**bdc 调试**命令参考。 有关其他**azdata**命令的详细信息, 请参阅[azdata reference](reference-azdata.md)。

## <a name="commands"></a>命令
|     |     |
| --- | --- |
[azdata bdc 调试副本-日志](#azdata-bdc-debug-copy-logs) | 复制日志。
[azdata bdc 调试转储](#azdata-bdc-debug-dump) | 触发器日志记录转储。
## <a name="azdata-bdc-debug-copy-logs"></a>azdata bdc 调试副本-日志
从大数据群集复制调试日志-kube config 在系统上是必需的。
```bash
azdata bdc debug copy-logs --namespace -n 
                           [--container -c]  
                           [--target-folder -d]  
                           [--pod -p]  
                           [--timeout -t]
```
### <a name="required-parameters"></a>必需的参数
#### `--namespace -n`
大数据群集名称, 用于 kubernetes 命名空间。
### <a name="optional-parameters"></a>可选参数
#### `--container -c`
复制具有相似名称的容器的日志 (可选), 默认情况下会复制所有容器的日志。 不能多次指定。 如果多次指定, 则将使用最后一个
#### `--target-folder -d`
要将日志复制到的目标文件夹路径。 可选, 默认情况下在本地文件夹中创建结果。  不能多次指定。 如果多次指定, 则将使用最后一个
#### `--pod -p`
复制具有相似名称的 pod 的日志。 可选, 默认情况下会复制所有 pod 的日志。 不能多次指定。 如果多次指定, 则将使用最后一个
#### `--timeout -t`
等待命令完成的秒数。 默认值为 0, 无限制
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
## <a name="azdata-bdc-debug-dump"></a>azdata bdc 调试转储
触发器日志记录转储, 并将其从容器复制-kube config 在系统上是必需的。
```bash
azdata bdc debug dump --namespace -n 
                      --container -c  
                      [--target-folder -d]
```
### <a name="required-parameters"></a>必需的参数
#### `--namespace -n`
大数据群集名称, 用于 kubernetes 命名空间。
#### `--container -c`
复制具有相似名称的容器的日志 (可选), 默认情况下会复制所有容器的日志。 不能多次指定。 如果多次指定, 则将使用最后一个
### <a name="optional-parameters"></a>可选参数
#### `--target-folder -d`
要将日志复制到的目标文件夹路径。 可选, 默认情况下在本地文件夹中创建结果。  不能多次指定。 如果多次指定, 则将使用最后一个`./output/dump`
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
