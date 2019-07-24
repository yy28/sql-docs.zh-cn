---
title: azdata 应用引用
titleSuffix: SQL Server big data clusters
description: Azdata 应用命令的参考文章。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 793edde26ebebf9e55c5751adbedf662142280de
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426277"
---
# <a name="azdata-app"></a>azdata 应用

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

以下文章提供了**azdata**工具中**应用程序**命令的参考。 有关其他**azdata**命令的详细信息, 请参阅[azdata reference](reference-azdata.md)。

## <a name="commands"></a>命令
|     |     |
| --- | --- |
[azdata 应用模板](reference-azdata-app-template.md) | 模板.
[azdata 应用初始化](#azdata-app-init) | Kickstart 新的应用程序主干。
[azdata 应用创建](#azdata-app-create) | 创建应用程序。
[azdata 应用更新](#azdata-app-update) | 更新应用程序。
[azdata 应用列表](#azdata-app-list) | 列出应用程序。
[azdata 应用删除](#azdata-app-delete) | 删除应用程序。
[azdata 应用运行](#azdata-app-run) | 运行应用程序。
[azdata 应用描述](#azdata-app-describe) | 描述应用程序。
## <a name="azdata-app-init"></a>azdata 应用初始化
帮助你基于运行时环境 kickstart 新的应用程序主干和/或规范文件。
```bash
azdata app init [--spec -s] 
                [--name -n]  
                [--version -v]  
                [--template -t]  
                [--destination -d]  
                [--url -u]
```
### <a name="examples"></a>示例
仅基架新的`spec.yaml`应用程序。
```bash
azdata app init --spec
```
基于`r`模板基架新的 R 应用程序主干。
```bash
azdata app init --name reduce --template r
```
基于`python`模板基架新的 Python 应用程序主干。
```bash
azdata app init --name reduce --template python
```
基于`ssis`模板基架新的 SSIS 应用程序主干。
```bash
azdata app init --name reduce --template ssis            
```
### <a name="optional-parameters"></a>可选参数
#### `--spec -s`
仅生成应用程序 yaml。
#### `--name -n`
应用程序名称。
#### `--version -v`
应用程序版本。
#### `--template -t`
模板名称。 有关支持的模板名称的完整列表, 请运行`azdata app template list`
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
## <a name="azdata-app-create"></a>azdata 应用创建
创建应用程序。
```bash
azdata app create --spec -s 
                  
```
### <a name="examples"></a>示例
从包含有效 yaml 部署规范的目录中创建新的应用程序。
```bash
azdata app create --spec /path/to/dir/with/spec/yaml
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
## <a name="azdata-app-update"></a>azdata 应用更新
更新应用程序。
```bash
azdata app update [--spec -s] 
                  [--yes -y]
```
### <a name="examples"></a>示例
从包含有效 yaml 部署规范的目录更新现有应用程序。
```bash
azdata app update --spec /path/to/dir/with/spec/yaml    
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
## <a name="azdata-app-list"></a>azdata 应用列表
列出一个或多个应用程序。
```bash
azdata app list [--name -n] 
                [--version -v]
```
### <a name="examples"></a>示例
按名称和版本列出应用程序。
```bash
azdata app list --name reduce  --version v1
```
按名称列出所有应用程序版本。
```bash
azdata app list --name reduce
```
按名称列出所有应用程序版本。
```bash
azdata app list
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
## <a name="azdata-app-delete"></a>azdata 应用删除
删除应用程序。
```bash
azdata app delete --name -n 
                  --version -v
```
### <a name="examples"></a>示例
按名称和版本删除应用程序。
```bash
azdata app delete --name reduce --version v1    
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
## <a name="azdata-app-run"></a>azdata 应用运行
运行应用程序。
```bash
azdata app run --name -n 
               --version -v  
               [--inputs]
```
### <a name="examples"></a>示例
运行不带输入参数的应用程序。
```bash
azdata app run --name reduce --version v1
```
运行具有1个输入参数的应用程序。
```bash
azdata app run --name reduce --version v1 --inputs x=10
```
运行具有多个输入参数的应用程序。
```bash
azdata app run --name reduce --version v1 --inputs x=10,y5.6    
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
## <a name="azdata-app-describe"></a>azdata 应用描述
描述应用程序。
```bash
azdata app describe [--spec -s] 
                    [--name -n]  
                    [--version -v]
```
### <a name="examples"></a>示例
描述应用程序。
```bash
azdata app describe --name reduce --version v1    
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

有关其他**azdata**命令的详细信息, 请参阅[azdata reference](reference-azdata.md)。 有关如何安装**azdata**工具的详细信息, 请参阅[安装 azdata 以管理 SQL Server 2019 大数据群集](deploy-install-azdata.md)。
