---
title: mssqlctl 存储装载参考
titleSuffix: SQL Server big data clusters
description: Mssqlctl 存储装载命令的参考文章。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 04/23/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 523253e8d1ff2d621d9f7a5ef90dbc957fba82ec
ms.sourcegitcommit: d5cd4a5271df96804e9b1a27e440fb6fbfac1220
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2019
ms.locfileid: "64774687"
---
# <a name="mssqlctl-storage-mount"></a>mssqlctl 存储装载

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

以下文章提供了参考**存储装载**中的命令**mssqlctl**工具。 有关其他详细信息**mssqlctl**命令，请参阅[mssqlctl 引用](reference-mssqlctl.md)。

## <a name="commands"></a>命令
|     |     |
| --- | --- |
[mssqlctl storage mount create](#mssqlctl-storage-mount-create) | 在 HDFS 中创建的远程存储的装载。
[mssqlctl storage mount delete](#mssqlctl-storage-mount-delete) | 删除远程存储在 HDFS 中的装载。
[mssqlctl 存储装载状态](#mssqlctl-storage-mount-status) | Mount(s) 的状态。
## <a name="mssqlctl-storage-mount-create"></a>mssqlctl 存储装载创建
在 HDFS 中创建的远程存储的装载。
```bash
mssqlctl storage mount create --remote-uri 
                              --mount-path  
                              [--credential-file]
```
### <a name="examples"></a>示例
若要使用的共享的密钥的 HDFS 路径 /mounts/adlsv2/data 上装载第 2 代 ADLS 帐户"adlsv2example"中的容器"数据"
```bash
mssqlctl storage mount create --remote-uri abfs://data@adlsv2example.dfs.core.windows.net/
    --mount-path /mounts/adlsv2/data --credentials credential_file
```
若要装载远程 HDFS 群集 (hdfs://namenode1:8080 /) 在本地 HDFS 路径 /mounts/hdfs /
```bash
mssqlctl storage mount create --remote-uri hdfs://namenode1:8080/ --mount-path /mounts/hdfs/
```
### <a name="required-parameters"></a>必需的参数
#### `--remote-uri`
要装载 （装入的源） 的远程存储的 URI。
#### `--mount-path`
HDFS 路径装载不得不创建 （装入的目标）。
### <a name="optional-parameters"></a>可选参数
#### `--credential-file`
包含用于访问远程存储的凭据文件。 凭据必须指定为键 = 值对通过一个键 = 每行的值。 任何等于在键或值需要进行转义。 默认情况下需要没有凭据。 所需的密钥取决于所装入的远程存储的类型和授权使用的类型。
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
## <a name="mssqlctl-storage-mount-delete"></a>mssqlctl 存储装载 delete
删除远程存储在 HDFS 中的装载。
```bash
mssqlctl storage mount delete --mount-path 
                              
```
### <a name="examples"></a>示例
删除装载在 /mounts/adlsv2/data 第 2 代 ADLS 存储帐户的创建。
```bash
mssqlctl storage mount delete --mount-path /mounts/adlsv2/data
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
## <a name="mssqlctl-storage-mount-status"></a>mssqlctl 存储装载状态
Mount(s) 的状态。
```bash
mssqlctl storage mount status [--mount-path] 
                              
```
### <a name="examples"></a>示例
按路径获取装入状态
```bash
mssqlctl storage mount status --mount-path /mounts/hdfs
```
获取所有装载的状态。
```bash
mssqlctl storage mount status
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