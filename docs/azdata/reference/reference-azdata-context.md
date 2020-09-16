---
title: azdata context 参考
titleSuffix: SQL Server big data clusters
description: azdata context 命令的参考文章。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 06/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: d3506d3ab1b2fad9d07496d1041773d26aae6d68
ms.sourcegitcommit: 883435b4c7366f06ac03579752093737b098feab
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89733497"
---
# <a name="azdata-context"></a>azdata context

[!INCLUDE[SQL Server 2019](../../includes/applies-to-version/sqlserver2019.md)]

以下文章提供了 `azdata` 工具中 `sql` 命令的参考。 有关其他 `azdata` 命令的详细信息，请参阅 [azdata 参考](reference-azdata.md)。

## <a name="commands"></a>命令
| 命令 | 描述 |
| --- | --- |
[azdata context list](#azdata-context-list) | 列出用户配置文件中的可用上下文。
[azdata context delete](#azdata-context-delete) | 从用户配置文件中删除具有给定命名空间的上下文。
[azdata context set](#azdata-context-set) | 将具有给定命名空间的上下文设置为用户配置文件中的活动上下文。
## <a name="azdata-context-list"></a>azdata context list
可以通过 `azdata context set` 或 `azdata context delete` 来设置或删除任何上下文。 要登录到新的上下文，请使用 `azdata login`。
```bash
azdata context list [--active -a] 
                    
```
### <a name="examples"></a>示例
列出用户配置文件中的所有可用上下文。
```bash
azdata context list
```
列出用户配置文件中的活动上下文。
```bash
azdata context list --active
```
### <a name="optional-parameters"></a>可选参数
#### `--active -a`
仅列出当前处于活动状态的上下文。
### <a name="global-arguments"></a>全局参数
#### `--debug`
提高日志记录详细程度以显示所有调试日志。
#### `--help -h`
显示此帮助消息并退出。
#### `--output -o`
输出格式。  允许的值：json、jsonc、table、tsv。  默认值：json。
#### `--query -q`
JMESPath 查询字符串。 请参阅 [http://jmespath.org/](http://jmespath.org)，获取详细信息和示例。
#### `--verbose`
提高日志记录详细程度。 使用 --debug 获取完整的调试日志。
## <a name="azdata-context-delete"></a>azdata context delete
如果已删除的上下文处于活动状态，则用户需要设置新的活动上下文。 查看可用于设置或删除 `azdata context list` 的上下文
```bash
azdata context delete --namespace -n 
                      
```
### <a name="examples"></a>示例
从用户配置文件中删除 contextNamespace。
```bash
azdata context delete -n contextNamespace
```
### <a name="required-parameters"></a>必需的参数
#### `--namespace -n`
要删除的上下文的命名空间。
### <a name="global-arguments"></a>全局参数
#### `--debug`
提高日志记录详细程度以显示所有调试日志。
#### `--help -h`
显示此帮助消息并退出。
#### `--output -o`
输出格式。  允许的值：json、jsonc、table、tsv。  默认值：json。
#### `--query -q`
JMESPath 查询字符串。 请参阅 [http://jmespath.org/](http://jmespath.org)，获取详细信息和示例。
#### `--verbose`
提高日志记录详细程度。 使用 --debug 获取完整的调试日志。
## <a name="azdata-context-set"></a>azdata context set
查看可用于设置 `azdata context list` 的上下文。 如果未列出上下文，则需要登录才能在用户配置文件 `azdata login` 中创建上下文。 登录到的内容将成为活动上下文。 如果登录到多个实体，则可以通过此命令在活动上下文间切换。 查看当前活动上下文 `azdata context list --active`
```bash
azdata context set --namespace -n 
                   
```
### <a name="examples"></a>示例
将上下文命名空间设置为用户配置文件中的活动上下文。
```bash
azdata context set -n contextNamespace
```
### <a name="required-parameters"></a>必需的参数
#### `--namespace -n`
要设置的上下文的命名空间。
### <a name="global-arguments"></a>全局参数
#### `--debug`
提高日志记录详细程度以显示所有调试日志。
#### `--help -h`
显示此帮助消息并退出。
#### `--output -o`
输出格式。  允许的值：json、jsonc、table、tsv。  默认值：json。
#### `--query -q`
JMESPath 查询字符串。 请参阅 [http://jmespath.org/](http://jmespath.org)，获取详细信息和示例。
#### `--verbose`
提高日志记录详细程度。 使用 --debug 获取完整的调试日志。

## <a name="next-steps"></a>后续步骤

有关其他 `azdata` 命令的详细信息，请参阅 [azdata 参考](reference-azdata.md)。 有关如何安装 `azdata` 工具的详细信息，请参阅[安装 azdata 以管理 SQL Server 2019 大数据群集](../install/deploy-install-azdata.md)。
