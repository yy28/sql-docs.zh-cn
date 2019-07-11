---
title: mssqlctl hdfs 引用
titleSuffix: SQL Server big data clusters
description: Mssqlctl hdfs 命令的参考文章。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
manager: jroth
ms.date: 06/26/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 8f211faf827bdf925a8fde938fff8f96998bc359
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/10/2019
ms.locfileid: "67728528"
---
# <a name="mssqlctl-hdfs"></a>mssqlctl hdfs

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

以下文章提供了参考**hdfs**中的命令**mssqlctl**工具。 有关其他详细信息**mssqlctl**命令，请参阅[mssqlctl 引用](reference-mssqlctl.md)。

## <a name="commands"></a>命令
|     |     |
| --- | --- |
[mssqlctl hdfs shell](#mssqlctl-hdfs-shell) | HDFS shell 是 HDFS 文件系统的交互的简单命令 shell。
[mssqlctl hdfs ls](#mssqlctl-hdfs-ls) | 列出给定的文件或目录的状态。
[mssqlctl hdfs exists](#mssqlctl-hdfs-exists) | 确定文件或目录是否存在。  返回存在则为 True 和 False 否则为。
[mssqlctl hdfs mkdir](#mssqlctl-hdfs-mkdir) | 在指定的路径创建一个目录。
[mssqlctl hdfs mv](#mssqlctl-hdfs-mv) | 将指定的文件或路径移动到指定位置。
[mssqlctl hdfs create](#mssqlctl-hdfs-create) | 在指定位置创建的文本文件。  可以通过数据参数添加简单的文本内容。
[mssqlctl hdfs read](#mssqlctl-hdfs-read) | 读取文件的内容。  偏移量和长度 （字节） 是可选参数。
[mssqlctl hdfs rm](#mssqlctl-hdfs-rm) | 删除文件或目录。
[mssqlctl hdfs rmr](#mssqlctl-hdfs-rmr) | 以递归方式删除文件或目录。
[mssqlctl hdfs chmod](#mssqlctl-hdfs-chmod) | 更改指定的文件或目录的权限。
[mssqlctl hdfs chown](#mssqlctl-hdfs-chown) | 更改所有者或组指定的文件。
## <a name="mssqlctl-hdfs-shell"></a>mssqlctl hdfs shell
HDFS shell 是 HDFS 文件系统的交互的简单命令 shell。
```bash
mssqlctl hdfs shell 
```
### <a name="examples"></a>示例
启动 shell。
```bash
mssqlctl hdfs shell
```
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
## <a name="mssqlctl-hdfs-ls"></a>mssqlctl hdfs ls
列出给定的文件或目录的状态。
```bash
mssqlctl hdfs ls --path -p 
                 
```
### <a name="examples"></a>示例
列出状态
```bash
mssqlctl hdfs ls --path '/tmp'
```
### <a name="required-parameters"></a>必需的参数
#### `--path -p`
列出状态的路径。
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
## <a name="mssqlctl-hdfs-exists"></a>mssqlctl hdfs 存在
确定文件或目录是否存在。  返回存在则为 True 和 False 否则为。
```bash
mssqlctl hdfs exists --path -p 
                     
```
### <a name="examples"></a>示例
检查有文件或目录存在。
```bash
mssqlctl hdfs exists --path '/tmp'
```
### <a name="required-parameters"></a>必需的参数
#### `--path -p`
若要检查存在的路径。
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
## <a name="mssqlctl-hdfs-mkdir"></a>mssqlctl hdfs mkdir
在指定的路径创建一个目录。
```bash
mssqlctl hdfs mkdir --path -p 
                    
```
### <a name="examples"></a>示例
创建目录。
```bash
mssqlctl hdfs mkdir --path '/tmp'
```
### <a name="required-parameters"></a>必需的参数
#### `--path -p`
要创建的目录的名称。
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
## <a name="mssqlctl-hdfs-mv"></a>mssqlctl hdfs mv
将指定的文件或路径移动到指定位置。
```bash
mssqlctl hdfs mv --source-path -s 
                 --target-path -t
```
### <a name="examples"></a>示例
移动文件或目录。
```bash
mssqlctl hdfs mv --source-path '/tmp' --target-path '/dest'
```
### <a name="required-parameters"></a>必需的参数
#### `--source-path -s`
要移动的目录。
#### `--target-path -t`
要将移动到的位置。
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
## <a name="mssqlctl-hdfs-create"></a>mssqlctl hdfs 创建
在指定位置创建的文本文件。  可以通过数据参数添加简单的文本内容。
```bash
mssqlctl hdfs create --path -p 
                     --data -d
```
### <a name="examples"></a>示例
创建文件。
```bash
mssqlctl hdfs create --path '/tmp/test.txt' --data "This is a test."
```
### <a name="required-parameters"></a>必需的参数
#### `--path -p`
要创建的文件的名称。
#### `--data -d`
文件的内容。  适用于简单的文本内容。
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
## <a name="mssqlctl-hdfs-read"></a>读取 mssqlctl hdfs
读取文件的内容。  偏移量和长度 （字节） 是可选参数。
```bash
mssqlctl hdfs read --path -p 
                   --offset  
                   --length -l
```
### <a name="examples"></a>示例
读取文件。
```bash
mssqlctl hdfs read --path '/tmp/test.txt'
```
### <a name="required-parameters"></a>必需的参数
#### `--path -p`
要读取的文件的名称。
#### `--offset`
要读取的文件内的偏移量的字节数。
#### `--length -l`
要读取的数据的长度。
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
## <a name="mssqlctl-hdfs-rm"></a>mssqlctl hdfs rm
删除文件或目录。
```bash
mssqlctl hdfs rm --path -p 
                 
```
### <a name="examples"></a>示例
删除文件或目录。
```bash
mssqlctl hdfs rm --path '/tmp'
```
### <a name="required-parameters"></a>必需的参数
#### `--path -p`
要删除的文件的名称。
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
## <a name="mssqlctl-hdfs-rmr"></a>mssqlctl hdfs rmr
以递归方式删除文件或目录。
```bash
mssqlctl hdfs rmr --path -p 
                  
```
### <a name="examples"></a>示例
递归删除目录。
```bash
mssqlctl hdfs rmr --path '/tmp'
```
### <a name="required-parameters"></a>必需的参数
#### `--path -p`
要以递归方式删除的文件的名称。
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
## <a name="mssqlctl-hdfs-chmod"></a>mssqlctl hdfs chmod
更改指定的文件或目录的权限。
```bash
mssqlctl hdfs chmod --path -p 
                    --permission
```
### <a name="examples"></a>示例
更改文件或目录的权限。
```bash
mssqlctl hdfs chmod --permission 775 --path '/tmp/test.txt'
```
### <a name="required-parameters"></a>必需的参数
#### `--path -p`
文件或目录设置权限的名称。
#### `--permission`
若要设置的权限八进制数。  示例"775"。
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
## <a name="mssqlctl-hdfs-chown"></a>mssqlctl hdfs chown
更改所有者或组指定的文件。
```bash
mssqlctl hdfs chown --path -p 
                    --owner  
                    --group -g
```
### <a name="examples"></a>示例
更改所有者和组。
```bash
mssqlctl hdfs chown --owner hdfs --group superusergroup --path '/tmp/test.txt'
```
### <a name="required-parameters"></a>必需的参数
#### `--path -p`
若要更改的所有者的目录的文件的名称。
#### `--owner`
若要设置为所有者名称。
#### `--group -g`
若要设置的组名称。
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

有关如何安装详细信息**mssqlctl**工具，请参阅[安装 mssqlctl 来管理 SQL Server 2019 大数据群集](deploy-install-mssqlctl.md)。