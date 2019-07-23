---
title: mssqlctl 应用引用
titleSuffix: SQL Server big data clusters
description: Mssqlctl 应用命令的参考文章。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 06/26/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: d0df3e9ca007fb6546310236f4c23d1775687cc5
ms.sourcegitcommit: d667fa9d6f1c8035f15fdb861882bd514be020d9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/23/2019
ms.locfileid: "68388386"
---
# <a name="mssqlctl-app"></a>mssqlctl 应用

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

以下文章提供了**mssqlctl**工具中**应用程序**命令的参考。 有关其他**mssqlctl**命令的详细信息, 请参阅[mssqlctl reference](reference-mssqlctl.md)。

## <a name="commands"></a>命令
|     |     |
| --- | --- |
[mssqlctl 应用模板](reference-mssqlctl-app-template.md) | 模板.
[mssqlctl 应用初始化](#mssqlctl-app-init) | Kickstart 新的应用程序主干。
[mssqlctl 应用创建](#mssqlctl-app-create) | 创建应用程序。
[mssqlctl 应用更新](#mssqlctl-app-update) | 更新应用程序。
[mssqlctl 应用列表](#mssqlctl-app-list) | 列出应用程序。
[mssqlctl 应用删除](#mssqlctl-app-delete) | 删除应用程序。
[mssqlctl 应用运行](#mssqlctl-app-run) | 运行应用程序。
[mssqlctl 应用描述](#mssqlctl-app-describe) | 描述应用程序。
## <a name="mssqlctl-app-init"></a>mssqlctl 应用初始化
帮助你基于运行时环境 kickstart 新的应用程序主干和/或规范文件。
```bash
mssqlctl app init [--spec -s] 
                  [--name -n]  
                  [--version -v]  
                  [--template -t]  
                  [--destination -d]  
                  [--url -u]
```
### <a name="examples"></a>示例
仅基架新的`spec.yaml`应用程序。
```bash
mssqlctl app init --spec
```
基于`r`模板基架新的 R 应用程序主干。
```bash
mssqlctl app init --name reduce --template r
```
基于`python`模板基架新的 Python 应用程序主干。
```bash
mssqlctl app init --name reduce --template python
```
基于`ssis`模板基架新的 SSIS 应用程序主干。
```bash
mssqlctl app init --name reduce --template ssis            
```
### <a name="optional-parameters"></a>可选参数
#### `--spec -s`
仅生成应用程序 yaml。
#### `--name -n`
应用程序名称。
#### `--version -v`
应用程序版本。
#### `--template -t`
模板名称。 有关支持的模板名称的完整列表, 请运行`mssqlctl app template list`
#### `--destination -d`
应用程序主干的放置位置。 默认值: 当前工作目录。
#### `--url -u`
指定不同的模板存储库位置。 缺省值 https://github.com/Microsoft/SQLBDC-AppDeploy.git
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
## <a name="mssqlctl-app-create"></a>mssqlctl 应用创建
创建应用程序。
```bash
mssqlctl app create --spec -s 
                    
```
### <a name="examples"></a>示例
从包含有效 yaml 部署规范的目录中创建新的应用程序。
```bash
mssqlctl app create --spec /path/to/dir/with/spec/yaml
```
### <a name="required-parameters"></a>必需的参数
#### `--spec -s`
目录的路径, 其中包含 YAML 规范文件, 用于描述应用程序。
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
## <a name="mssqlctl-app-update"></a>mssqlctl 应用更新
更新应用程序。
```bash
mssqlctl app update [--spec -s] 
                    [--yes -y]
```
### <a name="examples"></a>示例
从包含有效 yaml 部署规范的目录更新现有应用程序。
```bash
mssqlctl app update --spec /path/to/dir/with/spec/yaml    
```
### <a name="optional-parameters"></a>可选参数
#### `--spec -s`
目录的路径, 其中包含 YAML 规范文件, 用于描述应用程序。
#### `--yes -y`
从 CWD 的 yaml 文件更新应用程序时, 不提示进行确认。
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
## <a name="mssqlctl-app-list"></a>mssqlctl 应用列表
列出一个或多个应用程序。
```bash
mssqlctl app list [--name -n] 
                  [--version -v]
```
### <a name="examples"></a>示例
按名称和版本列出应用程序。
```bash
mssqlctl app list --name reduce  --version v1
```
按名称列出所有应用程序版本。
```bash
mssqlctl app list --name reduce
```
按名称列出所有应用程序版本。
```bash
mssqlctl app list
```
### <a name="optional-parameters"></a>可选参数
#### `--name -n`
应用程序名称。
#### `--version -v`
应用程序版本。
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
## <a name="mssqlctl-app-delete"></a>mssqlctl 应用删除
删除应用程序。
```bash
mssqlctl app delete --name -n 
                    --version -v
```
### <a name="examples"></a>示例
按名称和版本删除应用程序。
```bash
mssqlctl app delete --name reduce --version v1    
```
### <a name="required-parameters"></a>必需的参数
#### `--name -n`
应用程序名称。
#### `--version -v`
应用程序版本。
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
## <a name="mssqlctl-app-run"></a>mssqlctl 应用运行
运行应用程序。
```bash
mssqlctl app run --name -n 
                 --version -v  
                 [--inputs]
```
### <a name="examples"></a>示例
运行不带输入参数的应用程序。
```bash
mssqlctl app run --name reduce --version v1
```
运行具有1个输入参数的应用程序。
```bash
mssqlctl app run --name reduce --version v1 --inputs x=10
```
运行具有多个输入参数的应用程序。
```bash
mssqlctl app run --name reduce --version v1 --inputs x=10,y5.6    
```
### <a name="required-parameters"></a>必需的参数
#### `--name -n`
应用程序名称。
#### `--version -v`
应用程序版本。
### <a name="optional-parameters"></a>可选参数
#### `--inputs`
CSV `name=value`格式的应用程序输入参数。
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
## <a name="mssqlctl-app-describe"></a>mssqlctl 应用描述
描述应用程序。
```bash
mssqlctl app describe [--spec -s] 
                      [--name -n]  
                      [--version -v]
```
### <a name="examples"></a>示例
描述应用程序。
```bash
mssqlctl app describe --name reduce --version v1    
```
### <a name="optional-parameters"></a>可选参数
#### `--spec -s`
目录的路径, 其中包含 YAML 规范文件, 用于描述应用程序。
#### `--name -n`
应用程序名称。
#### `--version -v`
应用程序版本。
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

有关其他**mssqlctl**命令的详细信息, 请参阅[mssqlctl reference](reference-mssqlctl.md)。 有关如何安装**mssqlctl**工具的详细信息, 请参阅[安装 mssqlctl 以管理 SQL Server 2019 大数据群集](deploy-install-mssqlctl.md)。