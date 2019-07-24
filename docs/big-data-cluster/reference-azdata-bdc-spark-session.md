---
title: azdata bdc spark 会话参考
titleSuffix: SQL Server big data clusters
description: Azdata bdc spark 会话命令的参考文章。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 20b7ac3dcf72482e80278ce0f0df922026232a6d
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426097"
---
# <a name="azdata-bdc-spark-session"></a>azdata bdc spark 会话

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)] 

以下文章提供了**azdata**工具中的**bdc spark 会话**命令参考。 有关其他**azdata**命令的详细信息, 请参阅[azdata reference](reference-azdata.md)

## <a name="commands"></a>命令
|     |     |
| --- | --- |
[azdata bdc spark 会话创建](#azdata-bdc-spark-session-create) | 创建新的 Spark 会话。
[azdata bdc spark 会话列表](#azdata-bdc-spark-session-list) | 列出 Spark 中的所有活动会话。
[azdata bdc spark 会话信息](#azdata-bdc-spark-session-info) | 获取有关活动 Spark 会话的信息。
[azdata bdc spark 会话日志](#azdata-bdc-spark-session-log) | 获取活动 Spark 会话的执行日志。
[azdata bdc spark 会话状态](#azdata-bdc-spark-session-state) | 获取活动 Spark 会话的执行状态。
[azdata bdc spark 会话删除](#azdata-bdc-spark-session-delete) | 删除 Spark 会话。
## <a name="azdata-bdc-spark-session-create"></a>azdata bdc spark 会话创建
这将创建一个新的交互式 Spark 会话。 调用方必须指定 Spark 会话的类型。 此会话超出了 azdata 执行的生存期, 必须使用 "spark 会话删除" 删除
```bash
azdata bdc spark session create [--session-kind -k] 
                                [--jar-files -j]  
                                [--py-files -p]  
                                [--files -f]  
                                [--driver-memory]  
                                [--driver-cores]  
                                [--executor-memory]  
                                [--executor-cores]  
                                [--executor-count]  
                                [--archives -a]  
                                [--queue -q]  
                                [--name -n]  
                                [--config -c]  
                                [--timeout-seconds -t]
```
### <a name="examples"></a>示例
创建会话。
```bash
azdata spark session create --session-kind pyspark
```
### <a name="optional-parameters"></a>可选参数
#### `--session-kind -k`
要创建的会话类型的名称。  Spark、pyspark、sparkr 或 sql 中的一个。
#### `--jar-files -j`
Jar 文件路径的列表。  若要传入列表, JSON 会对值进行编码。  示例: "[" entry1 "," entry2 "]"。
#### `--py-files -p`
Python 文件路径的列表。  若要传入列表, JSON 会对值进行编码。  示例: "[" entry1 "," entry2 "]"。
#### `--files -f`
文件路径的列表。  若要传入列表, JSON 会对值进行编码。  示例: "[" entry1 "," entry2 "]"。
#### `--driver-memory`
要分配给驱动程序的内存量。  将单位指定为值的一部分。  示例512M 或2G。
#### `--driver-cores`
要分配给驱动程序的 CPU 内核数。
#### `--executor-memory`
要分配给执行器的内存量。  将单位指定为值的一部分。  示例512M 或2G。
#### `--executor-cores`
要分配给执行器的 CPU 内核数。
#### `--executor-count`
要运行的执行程序的实例数。
#### `--archives -a`
存档路径的列表。  若要传入列表, JSON 会对值进行编码。  示例: "[" entry1 "," entry2 "]"。
#### `--queue -q`
要在其中执行会话的 Spark 队列的名称。
#### `--name -n`
Spark 会话的名称。
#### `--config -c`
包含 Spark 配置值的名称值对的列表。  编码为 JSON 字典。  示例: "{" name ":" value "," name2 ":" value2 "}"。
#### `--timeout-seconds -t`
会话空闲超时 (以秒为单位)。
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
## <a name="azdata-bdc-spark-session-list"></a>azdata bdc spark 会话列表
列出 Spark 中的所有活动会话。
```bash
azdata bdc spark session list 
```
### <a name="examples"></a>示例
列出所有活动会话。
```bash
azdata spark session list
```
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
## <a name="azdata-bdc-spark-session-info"></a>azdata bdc spark 会话信息
这将获取具有给定 ID 的活动 Spark 会话的会话信息。  从 "spark 会话创建" 返回会话 id。
```bash
azdata bdc spark session info --session-id -i 
                              
```
### <a name="examples"></a>示例
获取 ID 为0的会话的会话信息。
```bash
azdata spark session info --session-id 0
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
## <a name="azdata-bdc-spark-session-log"></a>azdata bdc spark 会话日志
这将获取具有给定 ID 的活动 Spark 会话的会话日志条目。  从 "spark 会话创建" 返回会话 id。
```bash
azdata bdc spark session log --session-id -i 
                             
```
### <a name="examples"></a>示例
获取 ID 为0的会话的会话日志。
```bash
azdata spark session log --session-id 0
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
## <a name="azdata-bdc-spark-session-state"></a>azdata bdc spark 会话状态
这将获取具有给定 ID 的活动 Spark 会话的会话状态。  从 "spark 会话创建" 返回会话 id。
```bash
azdata bdc spark session state --session-id -i 
                               
```
### <a name="examples"></a>示例
获取 ID 为0的会话的会话状态。
```bash
azdata spark session state --session-id 0
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
## <a name="azdata-bdc-spark-session-delete"></a>azdata bdc spark 会话删除
这会删除交互式 Spark 会话。 从 "spark 会话创建" 返回会话 id。
```bash
azdata bdc spark session delete --session-id -i 
                                
```
### <a name="examples"></a>示例
删除会话。
```bash
azdata spark session delete --session-id 0
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

## <a name="next-steps"></a>后续步骤

有关其他**azdata**命令的详细信息, 请参阅[azdata reference](reference-azdata.md)。 有关如何安装**azdata**工具的详细信息, 请参阅[安装 azdata 以管理 SQL Server 2019 大数据群集](deploy-install-azdata.md)。
