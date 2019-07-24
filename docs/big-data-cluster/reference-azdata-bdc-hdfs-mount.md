---
title: azdata bdc hdfs 装载参考
titleSuffix: SQL Server big data clusters
description: Azdata bdc hdfs 装载命令的参考文章。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 7f0b259a3ac4ac0850fa05de3867e928b035307b
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426267"
---
# <a name="azdata-bdc-hdfs-mount"></a>azdata bdc hdfs 装载

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

以下文章提供了**azdata**工具中的**bdc hdfs mount**命令参考。 有关其他**azdata**命令的详细信息, 请参阅[azdata reference](reference-azdata.md)。

## <a name="commands"></a>命令
|     |     |
| --- | --- |
[azdata bdc hdfs 装载创建](#azdata-bdc-hdfs-mount-create) | 在 HDFS 中创建远程存储的装载。
[azdata bdc hdfs 装载删除](#azdata-bdc-hdfs-mount-delete) | 删除 HDFS 中远程存储的装载。
[azdata bdc hdfs 装入状态](#azdata-bdc-hdfs-mount-status) | 装载状态。
[azdata bdc hdfs 装载刷新](#azdata-bdc-hdfs-mount-refresh) | 在 HDFS 中刷新装载的内容。
## <a name="azdata-bdc-hdfs-mount-create"></a>azdata bdc hdfs 装载创建
在 HDFS 中创建远程存储的装载。 用于访问远程存储的凭据 (如果有) 应使用环境变量 MOUNT_CREDENTIALS 指定为键 = 值对的逗号分隔列表。 键或值中的所有逗号都必须进行转义。
```bash
azdata bdc hdfs mount create --remote-uri -r 
                             --mount-path -m
```
### <a name="examples"></a>示例
使用共享密钥在 HDFS 路径/mounts/adlsv2/data 上的 ADLS 第2代帐户 "adlsv2example" 中装载容器 "data"
```bash
Set the MOUNT_CREDENTIALS environment variable as "fs.azure.abfs.account.name=<your-storage-account-name>.dfs.core.windows.net,fs.azure.account.key.<your-storage-account-name>.dfs.core.windows.net=<storage-account-access-key>".
azdata bdc hdfs mount create --remote-uri abfs://data@adlsv2example.dfs.core.windows.net/
    --mount-path /mounts/adlsv2/data
```
在本地 HDFS 路径/mounts/hdfs/上装载远程 HDFS BDC (hdfs://namenode1:8080/)
```bash
azdata bdc hdfs mount create --remote-uri hdfs://namenode1:8080/ --mount-path /mounts/hdfs/
```
### <a name="required-parameters"></a>必需的参数
#### `--remote-uri -r`
要装载的远程存储 (装入源) 的 URI。
#### `--mount-path -m`
要在其中创建装载的 HDFS 路径 (装载目标)。
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
## <a name="azdata-bdc-hdfs-mount-delete"></a>azdata bdc hdfs 装载删除
删除 HDFS 中远程存储的装载。
```bash
azdata bdc hdfs mount delete --mount-path -m 
                             
```
### <a name="examples"></a>示例
删除在/mounts/adlsv2/data 上为 ADLS 第2代存储帐户创建的装载。
```bash
azdata bdc hdfs mount delete --mount-path /mounts/adlsv2/data
```
### <a name="required-parameters"></a>必需的参数
#### `--mount-path -m`
与必须删除的装载相对应的 HDFS 路径。
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
## <a name="azdata-bdc-hdfs-mount-status"></a>azdata bdc hdfs 装入状态
装载状态。
```bash
azdata bdc hdfs mount status [--mount-path -m] 
                             
```
### <a name="examples"></a>示例
按路径获取装入状态
```bash
azdata bdc hdfs mount status --mount-path /mounts/hdfs
```
获取所有装载的状态。
```bash
azdata bdc hdfs mount status
```
### <a name="optional-parameters"></a>可选参数
#### `--mount-path -m`
装载路径。
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
## <a name="azdata-bdc-hdfs-mount-refresh"></a>azdata bdc hdfs 装载刷新
在 HDFS 中刷新装载的内容。
```bash
azdata bdc hdfs mount refresh --mount-path -m 
                              
```
### <a name="examples"></a>示例
刷新在/mounts/adlsv2/data. 创建的装载
```bash
azdata bdc hdfs mount refresh --mount-path /mounts/adlsv2/data
```
### <a name="required-parameters"></a>必需的参数
#### `--mount-path -m`
对应于必须刷新的装载的 HDFS 路径。
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
