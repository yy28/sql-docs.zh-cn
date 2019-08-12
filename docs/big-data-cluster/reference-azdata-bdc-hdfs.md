---
title: azdata bdc hdfs 参考
titleSuffix: SQL Server big data clusters
description: azdata bdc hdfs 命令的参考文章。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 8e892c2d501902ef915a297440ae5a6ffda83bce
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/25/2019
ms.locfileid: "68426177"
---
# <a name="azdata-bdc-hdfs"></a>azdata bdc hdfs

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

以下文章为 **azdata** 工具中的 **bdc hdfs** 命令提供了参考。 有关其他 **azdata** 命令的详细信息，请参阅 [azdata 参考](reference-azdata.md)。

## <a name="commands"></a>命令
|     |     |
| --- | --- |
[azdata bdc hdfs shell](#azdata-bdc-hdfs-shell) | HDFS shell 是用于 HDFS 文件系统的简单交互式命令 shell。
[azdata bdc hdfs ls](#azdata-bdc-hdfs-ls) | 列出给定文件或目录的状态。
[azdata bdc hdfs exists](#azdata-bdc-hdfs-exists) | 确定文件或目录是否存在。  如果存在，则返回 True；否则返回 False。
[azdata bdc hdfs mkdir](#azdata-bdc-hdfs-mkdir) | 在指定的路径创建目录。
[azdata bdc hdfs mv](#azdata-bdc-hdfs-mv) | 将指定的文件或路径移动到指定的位置。
[azdata bdc hdfs create](#azdata-bdc-hdfs-create) | 在指定位置创建文本文件。  可以通过数据参数添加简单的文本内容。
[azdata bdc hdfs cat](#azdata-bdc-hdfs-cat) | 读取文件的内容。  偏移量和长度（以字节为单位）是可选参数。
[azdata bdc hdfs rm](#azdata-bdc-hdfs-rm) | 删除文件或目录。
[azdata bdc hdfs rmr](#azdata-bdc-hdfs-rmr) | 以递归方式删除文件或目录。
[azdata bdc hdfs chmod](#azdata-bdc-hdfs-chmod) | 更改对指定文件或目录的权限。
[azdata bdc hdfs chown](#azdata-bdc-hdfs-chown) | 更改指定文件的所有者或组。
[azdata bdc hdfs mount](reference-azdata-bdc-hdfs-mount.md) | 在 HDFS 中管理远程存储的装载。
## <a name="azdata-bdc-hdfs-shell"></a>azdata bdc hdfs shell
HDFS shell 是用于 HDFS 文件系统的简单交互式命令 shell。
```bash
azdata bdc hdfs shell 
```
### <a name="examples"></a>示例
启动 shell。
```bash
azdata bdc hdfs shell
```
### <a name="global-arguments"></a>全局参数
#### `--debug`
提高日志记录详细程度以显示所有调试日志。
#### `--help -h`
显示此帮助消息并退出。
#### `--output -o`
输出格式。  允许的值：json、jsonc、table、tsv。  默认值：json。
#### `--query -q`
JMESPath 查询字符串。 有关详细信息和示例，请参阅 [http://jmespath.org/](http://jmespath.org/])。
#### `--verbose`
提高日志记录详细程度。 使用 --debug 获取完整的调试日志。
## <a name="azdata-bdc-hdfs-ls"></a>azdata bdc hdfs ls
列出给定文件或目录的状态。
```bash
azdata bdc hdfs ls --path -p 
                   
```
### <a name="examples"></a>示例
列出状态
```bash
azdata bdc hdfs ls --path '/tmp'
```
### <a name="required-parameters"></a>必需的参数
#### `--path -p`
要列出状态的路径。
### <a name="global-arguments"></a>全局参数
#### `--debug`
提高日志记录详细程度以显示所有调试日志。
#### `--help -h`
显示此帮助消息并退出。
#### `--output -o`
输出格式。  允许的值：json、jsonc、table、tsv。  默认值：json。
#### `--query -q`
JMESPath 查询字符串。 有关详细信息和示例，请参阅 [http://jmespath.org/](http://jmespath.org/])。
#### `--verbose`
提高日志记录详细程度。 使用 --debug 获取完整的调试日志。
## <a name="azdata-bdc-hdfs-exists"></a>azdata bdc hdfs exists
确定文件或目录是否存在。  如果存在，则返回 True；否则返回 False。
```bash
azdata bdc hdfs exists --path -p 
                       
```
### <a name="examples"></a>示例
检查文件或目录是否存在。
```bash
azdata bdc hdfs exists --path '/tmp'
```
### <a name="required-parameters"></a>必需的参数
#### `--path -p`
要检查其中是否存在文件或目录的路径。
### <a name="global-arguments"></a>全局参数
#### `--debug`
提高日志记录详细程度以显示所有调试日志。
#### `--help -h`
显示此帮助消息并退出。
#### `--output -o`
输出格式。  允许的值：json、jsonc、table、tsv。  默认值：json。
#### `--query -q`
JMESPath 查询字符串。 有关详细信息和示例，请参阅 [http://jmespath.org/](http://jmespath.org/])。
#### `--verbose`
提高日志记录详细程度。 使用 --debug 获取完整的调试日志。
## <a name="azdata-bdc-hdfs-mkdir"></a>azdata bdc hdfs mkdir
在指定的路径创建目录。
```bash
azdata bdc hdfs mkdir --path -p 
                      
```
### <a name="examples"></a>示例
创建目录。
```bash
azdata bdc hdfs mkdir --path '/tmp'
```
### <a name="required-parameters"></a>必需的参数
#### `--path -p`
要创建的目录的名称。
### <a name="global-arguments"></a>全局参数
#### `--debug`
提高日志记录详细程度以显示所有调试日志。
#### `--help -h`
显示此帮助消息并退出。
#### `--output -o`
输出格式。  允许的值：json、jsonc、table、tsv。  默认值：json。
#### `--query -q`
JMESPath 查询字符串。 有关详细信息和示例，请参阅 [http://jmespath.org/](http://jmespath.org/])。
#### `--verbose`
提高日志记录详细程度。 使用 --debug 获取完整的调试日志。
## <a name="azdata-bdc-hdfs-mv"></a>azdata bdc hdfs mv
将指定的文件或路径移动到指定的位置。
```bash
azdata bdc hdfs mv --source-path -s 
                   --target-path -t
```
### <a name="examples"></a>示例
移动文件或目录。
```bash
azdata bdc hdfs mv --source-path '/tmp' --target-path '/dest'
```
### <a name="required-parameters"></a>必需的参数
#### `--source-path -s`
要移动的目录。
#### `--target-path -t`
要移动到的位置。
### <a name="global-arguments"></a>全局参数
#### `--debug`
提高日志记录详细程度以显示所有调试日志。
#### `--help -h`
显示此帮助消息并退出。
#### `--output -o`
输出格式。  允许的值：json、jsonc、table、tsv。  默认值：json。
#### `--query -q`
JMESPath 查询字符串。 有关详细信息和示例，请参阅 [http://jmespath.org/](http://jmespath.org/])。
#### `--verbose`
提高日志记录详细程度。 使用 --debug 获取完整的调试日志。
## <a name="azdata-bdc-hdfs-create"></a>azdata bdc hdfs create
在指定位置创建文本文件。  可以通过数据参数添加简单的文本内容。
```bash
azdata bdc hdfs create --path -p 
                       --data -d
```
### <a name="examples"></a>示例
创建文件。
```bash
azdata bdc hdfs create --path '/tmp/test.txt' --data "This is a test."
```
### <a name="required-parameters"></a>必需的参数
#### `--path -p`
要创建的文件的名称。
#### `--data -d`
文件的内容。  适用于简单的文本内容。
### <a name="global-arguments"></a>全局参数
#### `--debug`
提高日志记录详细程度以显示所有调试日志。
#### `--help -h`
显示此帮助消息并退出。
#### `--output -o`
输出格式。  允许的值：json、jsonc、table、tsv。  默认值：json。
#### `--query -q`
JMESPath 查询字符串。 有关详细信息和示例，请参阅 [http://jmespath.org/](http://jmespath.org/])。
#### `--verbose`
提高日志记录详细程度。 使用 --debug 获取完整的调试日志。
## <a name="azdata-bdc-hdfs-cat"></a>azdata bdc hdfs cat
读取文件的内容。  偏移量和长度（以字节为单位）是可选参数。
```bash
azdata bdc hdfs cat --path -p 
                    --offset  
                    --length -l
```
### <a name="examples"></a>示例
读取文件。
```bash
azdata bdc hdfs cat --path '/tmp/test.txt'
```
### <a name="required-parameters"></a>必需的参数
#### `--path -p`
要读取的文件的名称。
#### `--offset`
要读取的文件中的字节数偏移量。
#### `--length -l`
要读取的数据的长度。
### <a name="global-arguments"></a>全局参数
#### `--debug`
提高日志记录详细程度以显示所有调试日志。
#### `--help -h`
显示此帮助消息并退出。
#### `--output -o`
输出格式。  允许的值：json、jsonc、table、tsv。  默认值：json。
#### `--query -q`
JMESPath 查询字符串。 有关详细信息和示例，请参阅 [http://jmespath.org/](http://jmespath.org/])。
#### `--verbose`
提高日志记录详细程度。 使用 --debug 获取完整的调试日志。
## <a name="azdata-bdc-hdfs-rm"></a>azdata bdc hdfs rm
删除文件或目录。
```bash
azdata bdc hdfs rm --path -p 
                   
```
### <a name="examples"></a>示例
删除文件或目录。
```bash
azdata bdc hdfs rm --path '/tmp'
```
### <a name="required-parameters"></a>必需的参数
#### `--path -p`
要删除的文件的名称。
### <a name="global-arguments"></a>全局参数
#### `--debug`
提高日志记录详细程度以显示所有调试日志。
#### `--help -h`
显示此帮助消息并退出。
#### `--output -o`
输出格式。  允许的值：json、jsonc、table、tsv。  默认值：json。
#### `--query -q`
JMESPath 查询字符串。 有关详细信息和示例，请参阅 [http://jmespath.org/](http://jmespath.org/])。
#### `--verbose`
提高日志记录详细程度。 使用 --debug 获取完整的调试日志。
## <a name="azdata-bdc-hdfs-rmr"></a>azdata bdc hdfs rmr
以递归方式删除文件或目录。
```bash
azdata bdc hdfs rmr --path -p 
                    
```
### <a name="examples"></a>示例
递归删除目录。
```bash
azdata bdc hdfs rmr --path '/tmp'
```
### <a name="required-parameters"></a>必需的参数
#### `--path -p`
要以递归方式删除的文件的名称。
### <a name="global-arguments"></a>全局参数
#### `--debug`
提高日志记录详细程度以显示所有调试日志。
#### `--help -h`
显示此帮助消息并退出。
#### `--output -o`
输出格式。  允许的值：json、jsonc、table、tsv。  默认值：json。
#### `--query -q`
JMESPath 查询字符串。 有关详细信息和示例，请参阅 [http://jmespath.org/](http://jmespath.org/])。
#### `--verbose`
提高日志记录详细程度。 使用 --debug 获取完整的调试日志。
## <a name="azdata-bdc-hdfs-chmod"></a>azdata bdc hdfs chmod
更改对指定文件或目录的权限。
```bash
azdata bdc hdfs chmod --path -p 
                      --permission
```
### <a name="examples"></a>示例
更改文件或目录权限。
```bash
azdata bdc hdfs chmod --permission 775 --path '/tmp/test.txt'
```
### <a name="required-parameters"></a>必需的参数
#### `--path -p`
要对其设置权限的文件或目录的名称。
#### `--permission`
要设置的权限八进制数。  例如“775”。
### <a name="global-arguments"></a>全局参数
#### `--debug`
提高日志记录详细程度以显示所有调试日志。
#### `--help -h`
显示此帮助消息并退出。
#### `--output -o`
输出格式。  允许的值：json、jsonc、table、tsv。  默认值：json。
#### `--query -q`
JMESPath 查询字符串。 有关详细信息和示例，请参阅 [http://jmespath.org/](http://jmespath.org/])。
#### `--verbose`
提高日志记录详细程度。 使用 --debug 获取完整的调试日志。
## <a name="azdata-bdc-hdfs-chown"></a>azdata bdc hdfs chown
更改指定文件的所有者或组。
```bash
azdata bdc hdfs chown --path -p 
                      --owner  
                      --group -g
```
### <a name="examples"></a>示例
更改所有者和组。
```bash
azdata bdc hdfs chown --owner hdfs --group superusergroup --path '/tmp/test.txt'
```
### <a name="required-parameters"></a>必需的参数
#### `--path -p`
要更改其所有者的文件或目录的名称。
#### `--owner`
要设置为的所有者名称。
#### `--group -g`
要设置为的组名称。
### <a name="global-arguments"></a>全局参数
#### `--debug`
提高日志记录详细程度以显示所有调试日志。
#### `--help -h`
显示此帮助消息并退出。
#### `--output -o`
输出格式。  允许的值：json、jsonc、table、tsv。  默认值：json。
#### `--query -q`
JMESPath 查询字符串。 有关详细信息和示例，请参阅 [http://jmespath.org/](http://jmespath.org/])。
#### `--verbose`
提高日志记录详细程度。 使用 --debug 获取完整的调试日志。

## <a name="next-steps"></a>后续步骤

有关其他 **azdata** 命令的详细信息，请参阅 [azdata 参考](reference-azdata.md)。 有关如何安装 **azdata** 工具的详细信息，请参阅[安装 azdata 以管理 SQL Server 2019 大数据群集](deploy-install-azdata.md)。
