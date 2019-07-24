---
title: azdata bdc spark 批处理引用
titleSuffix: SQL Server big data clusters
description: Azdata bdc spark 批处理命令的参考文章。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 6e242b26f439b49dbf0b3cf5ab50ea46c273f45f
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426157"
---
# <a name="azdata-bdc-spark-batch"></a>azdata bdc spark 批处理

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

以下文章提供了**azdata**工具中的**bdc spark 批处理**命令参考。 有关其他**azdata**命令的详细信息, 请参阅[azdata reference](reference-azdata.md)

## <a name="commands"></a>命令
|     |     |
| --- | --- |
[azdata bdc spark batch create](#azdata-bdc-spark-batch-create) | 创建新的 Spark 批处理。
[azdata bdc spark batch 列表](#azdata-bdc-spark-batch-list) | 列出 Spark 中的所有批处理。
[azdata bdc spark 批处理信息](#azdata-bdc-spark-batch-info) | 获取有关活动 Spark 批处理的信息。
[azdata bdc spark 批处理日志](#azdata-bdc-spark-batch-log) | 获取 Spark 批处理的执行日志。
[azdata bdc spark 批处理状态](#azdata-bdc-spark-batch-state) | 获取 Spark 批处理的执行状态。
[azdata bdc spark 批处理删除](#azdata-bdc-spark-batch-delete) | 删除 Spark 批处理。
## <a name="azdata-bdc-spark-batch-create"></a>azdata bdc spark batch create
这将创建一个执行提供的代码的新 batch Spark 作业。
```bash
azdata bdc spark batch create --file -f 
                              [--class-name -c]  
                              [--arguments -a]  
                              [--jar-files -j]  
                              [--py-files -p]  
                              [--files]  
                              [--driver-memory]  
                              [--driver-cores]  
                              [--executor-memory]  
                              [--executor-cores]  
                              [--executor-count]  
                              [--archives]  
                              [--queue -q]  
                              [--name -n]  
                              [--config]
```
### <a name="examples"></a>示例
创建新的 Spark 批处理。
```bash
azdata spark batch create --code "2+2"
```
### <a name="required-parameters"></a>必需的参数
#### `--file -f`
要执行的文件的路径。
### <a name="optional-parameters"></a>可选参数
#### `--class-name -c`
传递一个或多个 jar 文件时要执行的类的名称。
#### `--arguments -a`
参数列表。  若要传入列表, JSON 会对值进行编码。  示例: "[" entry1 "," entry2 "]"。
#### `--jar-files -j`
Jar 文件路径的列表。  若要传入列表, JSON 会对值进行编码。  示例: "[" entry1 "," entry2 "]"。
#### `--py-files -p`
Python 文件路径的列表。  若要传入列表, JSON 会对值进行编码。  示例: "[" entry1 "," entry2 "]"。
#### `--files`
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
#### `--archives`
存档路径的列表。  若要传入列表, JSON 会对值进行编码。  示例: "[" entry1 "," entry2 "]"。
#### `--queue -q`
要在其中执行会话的 Spark 队列的名称。
#### `--name -n`
Spark 会话的名称。
#### `--config`
包含 Spark 配置值的名称值对的列表。  编码为 JSON 字典。  示例: "{" name ":" value "," name2 ":" value2 "}"。
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
## <a name="azdata-bdc-spark-batch-list"></a>azdata bdc spark batch 列表
列出 Spark 中的所有批处理。
```bash
azdata bdc spark batch list 
```
### <a name="examples"></a>示例
列出所有活动的批。
```bash
azdata spark batch list
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
## <a name="azdata-bdc-spark-batch-info"></a>azdata bdc spark 批处理信息
这将获取具有给定 ID 的 Spark 批处理的信息。  批处理 id 从 "spark batch create" 返回。
```bash
azdata bdc spark batch info --batch-id -i 
                            
```
### <a name="examples"></a>示例
获取 ID 为0的批的批处理信息。
```bash
azdata spark batch info --batch-id 0
```
### <a name="required-parameters"></a>必需的参数
#### `--batch-id -i`
Spark 批处理 ID 号。
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
## <a name="azdata-bdc-spark-batch-log"></a>azdata bdc spark 批处理日志
这将获取具有给定 ID 的 Spark 批处理的批处理日志条目。  批处理 id 从 "spark batch create" 返回。
```bash
azdata bdc spark batch log --batch-id -i 
                           
```
### <a name="examples"></a>示例
获取 ID 为0的批的批处理日志。
```bash
azdata spark batch log --batch-id 0
```
### <a name="required-parameters"></a>必需的参数
#### `--batch-id -i`
Spark 批处理 ID 号。
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
## <a name="azdata-bdc-spark-batch-state"></a>azdata bdc spark 批处理状态
这将获取具有给定 ID 的 Spark 批处理的批处理状态。  批处理 id 从 "spark batch create" 返回。
```bash
azdata bdc spark batch state --batch-id -i 
                             
```
### <a name="examples"></a>示例
获取 ID 为0的批的批处理状态。
```bash
azdata spark batch state --batch-id 0
```
### <a name="required-parameters"></a>必需的参数
#### `--batch-id -i`
Spark 批处理 ID 号。
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
## <a name="azdata-bdc-spark-batch-delete"></a>azdata bdc spark 批处理删除
这会删除 Spark 批处理。 批处理 id 从 "spark batch create" 返回。
```bash
azdata bdc spark batch delete --batch-id -i 
                              
```
### <a name="examples"></a>示例
删除批。
```bash
azdata spark batch delete --batch-id 0
```
### <a name="required-parameters"></a>必需的参数
#### `--batch-id -i`
Spark 批处理 ID 号。
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
