---
title: mssqlctl bdc 存储池装入参考
titleSuffix: SQL Server big data clusters
description: Mssqlctl bdc 存储池装入命令的参考文章。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 06/26/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: b6a412c6d7cab9fb869a9aa8ee1b62ae0ed3f717
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67958005"
---
# <a name="mssqlctl-bdc-storage-pool-mount"></a>mssqlctl bdc 存储池装入

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

以下文章提供了参考**bdc 存储池装入**中的命令**mssqlctl**工具。 有关其他详细信息**mssqlctl**命令，请参阅[mssqlctl 引用](reference-mssqlctl.md)。

## <a name="commands"></a>命令
|     |     |
| --- | --- |
[mssqlctl bdc 存储池装入创建](#mssqlctl-bdc-storage-pool-mount-create) | 在 HDFS 中创建的远程存储的装载。
[mssqlctl bdc 存储池装入删除](#mssqlctl-bdc-storage-pool-mount-delete) | 删除远程存储在 HDFS 中的装载。
[mssqlctl bdc 存储池装入状态](#mssqlctl-bdc-storage-pool-mount-status) | Mount(s) 的状态。
## <a name="mssqlctl-bdc-storage-pool-mount-create"></a>mssqlctl bdc 存储池装入创建
在 HDFS 中创建的远程存储的装载。 应为逗号分隔的键列表中使用环境变量 MOUNT_CREDENTIALS 指定的凭据用于访问远程存储，如果有，= 值对。 中键或值的任何逗号必须进行转义。
```bash
mssqlctl bdc storage-pool mount create --remote-uri 
                                       --mount-path
```
### <a name="examples"></a>示例
若要使用的共享的密钥的 HDFS 路径 /mounts/adlsv2/data 上装载第 2 代 ADLS 帐户"adlsv2example"中的容器"数据"
```bash
Set the MOUNT_CREDENTIALS environment variable as "fs.azure.abfs.account.name=<your-storage-account-name>.dfs.core.windows.net,fs.azure.account.key.<your-storage-account-name>.dfs.core.windows.net=<storage-account-access-key>".
mssqlctl bdc storage-pool mount create --remote-uri abfs://data@adlsv2example.dfs.core.windows.net/
    --mount-path /mounts/adlsv2/data
```
若要装载远程 HDFS BDC (hdfs://namenode1:8080 /) 在本地 HDFS 路径 /mounts/hdfs /
```bash
mssqlctl bdc storage-pool mount create --remote-uri hdfs://namenode1:8080/ --mount-path /mounts/hdfs/
```
### <a name="required-parameters"></a>必需的参数
#### `--remote-uri`
要装载 （装入的源） 的远程存储的 URI。
#### `--mount-path`
HDFS 路径装载不得不创建 （装入的目标）。
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
## <a name="mssqlctl-bdc-storage-pool-mount-delete"></a>mssqlctl bdc 存储池装入删除
删除远程存储在 HDFS 中的装载。
```bash
mssqlctl bdc storage-pool mount delete --mount-path 
                                       
```
### <a name="examples"></a>示例
删除装载在 /mounts/adlsv2/data 第 2 代 ADLS 存储帐户的创建。
```bash
mssqlctl bdc storage-pool mount delete --mount-path /mounts/adlsv2/data
```
### <a name="required-parameters"></a>必需的参数
#### `--mount-path`
对应于具有要删除此安装的 HDFS 路径。
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
## <a name="mssqlctl-bdc-storage-pool-mount-status"></a>mssqlctl bdc 存储池装入状态
Mount(s) 的状态。
```bash
mssqlctl bdc storage-pool mount status [--mount-path] 
                                       
```
### <a name="examples"></a>示例
按路径获取装入状态
```bash
mssqlctl bdc storage-pool mount status --mount-path /mounts/hdfs
```
获取所有装载的状态。
```bash
mssqlctl bdc storage-pool mount status
```
### <a name="optional-parameters"></a>可选参数
#### `--mount-path`
装载路径。
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