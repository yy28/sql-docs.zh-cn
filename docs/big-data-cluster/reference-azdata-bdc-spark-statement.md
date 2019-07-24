---
title: azdata bdc spark 语句参考
titleSuffix: SQL Server big data clusters
description: Azdata bdc spark 语句命令的参考文章。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 778980ac6b93e7db79d59182fbd18ab4cfdb8b75
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426087"
---
# <a name="azdata-bdc-spark-statement"></a>azdata bdc spark 语句

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)] 

以下文章提供了**azdata**工具中的**bdc spark 语句**命令参考。 有关其他**azdata**命令的详细信息, 请参阅[azdata reference](reference-azdata.md)

## <a name="commands"></a>命令
|     |     |
| --- | --- |
[azdata bdc spark 语句列表](#azdata-bdc-spark-statement-list) | 列出给定 Spark 会话中的所有语句。
[azdata bdc spark 语句创建](#azdata-bdc-spark-statement-create) | 在给定的会话中创建新的 Spark 语句。
[azdata bdc spark 语句信息](#azdata-bdc-spark-statement-info) | 获取有关给定 Spark 会话中请求的语句的信息。
[azdata bdc spark 语句取消](#azdata-bdc-spark-statement-cancel) | 取消给定 Spark 会话内的语句。
## <a name="azdata-bdc-spark-statement-list"></a>azdata bdc spark 语句列表
列出给定 Spark 会话中的所有语句。
```bash
azdata bdc spark statement list --session-id -i 
                                
```
### <a name="examples"></a>示例
列出所有会话语句。
```bash
azdata spark statement list --session-id 0
```
### <a name="required-parameters"></a>必需的参数
#### `--session-id -i`
Spark 会话 ID 号。
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
## <a name="azdata-bdc-spark-statement-create"></a>azdata bdc spark 语句创建
这会在给定会话中创建并执行一个新语句。  如果 execute 为 quick, 则结果包含执行的输出。  否则, 在完成语句后, 可以使用 "spark 会话信息" 来检索结果。
```bash
azdata bdc spark statement create --session-id -i 
                                  --code -c
```
### <a name="examples"></a>示例
运行语句。
```bash
azdata spark statement create --session-id 0 --code "2+2"
```
### <a name="required-parameters"></a>必需的参数
#### `--session-id -i`
Spark 会话 ID 号。
#### `--code -c`
字符串, 其中包含作为语句的一部分执行的代码。
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
## <a name="azdata-bdc-spark-statement-info"></a>azdata bdc spark 语句信息
如果语句已完成, 则将获取执行状态和执行结果。 语句 id 从 "spark 语句创建" 返回。
```bash
azdata bdc spark statement info --session-id -i 
                                --statement-id -s
```
### <a name="examples"></a>示例
获取 ID 为0、语句 ID 为0的会话的语句信息。
```bash
azdata spark statement info --session-id 0 --statement-id 0
```
### <a name="required-parameters"></a>必需的参数
#### `--session-id -i`
Spark 会话 ID 号。
#### `--statement-id -s`
给定会话 ID 内的 Spark 语句 ID 号。
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
## <a name="azdata-bdc-spark-statement-cancel"></a>azdata bdc spark 语句取消
这会取消给定 Spark 会话内的语句。 语句 id 从 "spark 语句创建" 返回。
```bash
azdata bdc spark statement cancel --session-id -i 
                                  --statement-id -s
```
### <a name="examples"></a>示例
取消语句。
```bash
azdata spark statement cancel --session-id 0 --statement-id 0
```
### <a name="required-parameters"></a>必需的参数
#### `--session-id -i`
Spark 会话 ID 号。
#### `--statement-id -s`
给定会话 ID 内的 Spark 语句 ID 号。
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
