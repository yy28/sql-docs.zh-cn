---
title: azdata app reference
titleSuffix: SQL Server big data clusters
description: azdata app 命令的参考文章。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: ec7e461705138905713b803e2f0f96934044d971
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2019
ms.locfileid: "70155296"
---
# <a name="azdata-app"></a>azdata app

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)] 

本文是**azdata**的参考文章。 

## <a name="commands"></a>命令
|     |     |
| --- | --- |
[azdata app template](reference-azdata-app-template.md) | 模板。
[azdata app init](#azdata-app-init) | 启动新应用程序主干。
[azdata app create](#azdata-app-create) | 创建应用程序。
[azdata app update](#azdata-app-update) | 更新应用程序。
[azdata app list](#azdata-app-list) | 列出应用程序。
[azdata app delete](#azdata-app-delete) | 删除应用程序。
[azdata app run](#azdata-app-run) | 运行应用程序。
[azdata app describe](#azdata-app-describe) | 描述应用程序。
## <a name="azdata-app-init"></a>azdata app init
帮助基于运行时环境启动新应用程序主干和/或规范文件。
```bash
azdata app init 
```
### <a name="examples"></a>示例
仅搭建新应用程序 `spec.yaml` 的基架。
```bash
azdata app init --spec
```
基于`r`模板基架新的 R 应用程序应用程序框架。
```bash
azdata app init --name reduce --template r
```
基于`python`模板基架新的 Python 应用程序应用程序主干。
```bash
azdata app init --name reduce --template python
```
基于`ssis`模板基架新的 SSIS 应用程序应用程序主干。
```bash
azdata app init --name reduce --template ssis            
```
### <a name="global-arguments"></a>全局参数
#### `--debug`
提高日志记录详细程度以显示所有调试日志。
#### `--help -h`
显示此帮助消息并退出。
#### `--output -o`
输出格式。  允许的值：json、jsonc、table、tsv。  默认值：json。
#### `--query -q`
JMESPath 查询字符串。 请参阅 [http://jmespath.org/](http://jmespath.org/])，获取详细信息和示例。
#### `--verbose`
提高日志记录详细程度。 使用 --debug 获取完整的调试日志。
## <a name="azdata-app-create"></a>azdata app create
创建应用程序。
```bash
azdata app create 
```
### <a name="examples"></a>示例
从包含有效 spec.yaml 部署规范的目录中创建新的应用程序。
```bash
azdata app create --spec /path/to/dir/with/spec/yaml
```
### <a name="global-arguments"></a>全局参数
#### `--debug`
提高日志记录详细程度以显示所有调试日志。
#### `--help -h`
显示此帮助消息并退出。
#### `--output -o`
输出格式。  允许的值：json、jsonc、table、tsv。  默认值：json。
#### `--query -q`
JMESPath 查询字符串。 请参阅 [http://jmespath.org/](http://jmespath.org/])，获取详细信息和示例。
#### `--verbose`
提高日志记录详细程度。 使用 --debug 获取完整的调试日志。
## <a name="azdata-app-update"></a>azdata app update
更新应用程序。
```bash
azdata app update 
```
### <a name="examples"></a>示例
从包含有效 spec.yaml 部署规范的目录更新现有应用程序。
```bash
azdata app update --spec /path/to/dir/with/spec/yaml    
```
### <a name="global-arguments"></a>全局参数
#### `--debug`
提高日志记录详细程度以显示所有调试日志。
#### `--help -h`
显示此帮助消息并退出。
#### `--output -o`
输出格式。  允许的值：json、jsonc、table、tsv。  默认值：json。
#### `--query -q`
JMESPath 查询字符串。 请参阅 [http://jmespath.org/](http://jmespath.org/])，获取详细信息和示例。
#### `--verbose`
提高日志记录详细程度。 使用 --debug 获取完整的调试日志。
## <a name="azdata-app-list"></a>azdata app list
列出应用程序。
```bash
azdata app list 
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
### <a name="global-arguments"></a>全局参数
#### `--debug`
提高日志记录详细程度以显示所有调试日志。
#### `--help -h`
显示此帮助消息并退出。
#### `--output -o`
输出格式。  允许的值：json、jsonc、table、tsv。  默认值：json。
#### `--query -q`
JMESPath 查询字符串。 请参阅 [http://jmespath.org/](http://jmespath.org/])，获取详细信息和示例。
#### `--verbose`
提高日志记录详细程度。 使用 --debug 获取完整的调试日志。
## <a name="azdata-app-delete"></a>azdata app delete
删除应用程序。
```bash
azdata app delete 
```
### <a name="examples"></a>示例
按名称和版本删除应用程序。
```bash
azdata app delete --name reduce --version v1    
```
### <a name="global-arguments"></a>全局参数
#### `--debug`
提高日志记录详细程度以显示所有调试日志。
#### `--help -h`
显示此帮助消息并退出。
#### `--output -o`
输出格式。  允许的值：json、jsonc、table、tsv。  默认值：json。
#### `--query -q`
JMESPath 查询字符串。 请参阅 [http://jmespath.org/](http://jmespath.org/])，获取详细信息和示例。
#### `--verbose`
提高日志记录详细程度。 使用 --debug 获取完整的调试日志。
## <a name="azdata-app-run"></a>azdata app run
运行应用程序。
```bash
azdata app run 
```
### <a name="examples"></a>示例
运行无输入参数的应用程序。
```bash
azdata app run --name reduce --version v1
```
运行具有 1 个输入参数的应用程序。
```bash
azdata app run --name reduce --version v1 --inputs x=10
```
运行具有多个输入参数的应用程序。
```bash
azdata app run --name reduce --version v1 --inputs x=10,y5.6    
```
### <a name="global-arguments"></a>全局参数
#### `--debug`
提高日志记录详细程度以显示所有调试日志。
#### `--help -h`
显示此帮助消息并退出。
#### `--output -o`
输出格式。  允许的值：json、jsonc、table、tsv。  默认值：json。
#### `--query -q`
JMESPath 查询字符串。 请参阅 [http://jmespath.org/](http://jmespath.org/])，获取详细信息和示例。
#### `--verbose`
提高日志记录详细程度。 使用 --debug 获取完整的调试日志。
## <a name="azdata-app-describe"></a>azdata app describe
描述应用程序。
```bash
azdata app describe 
```
### <a name="examples"></a>示例
描述应用程序。
```bash
azdata app describe --name reduce --version v1    
```
### <a name="global-arguments"></a>全局参数
#### `--debug`
提高日志记录详细程度以显示所有调试日志。
#### `--help -h`
显示此帮助消息并退出。
#### `--output -o`
输出格式。  允许的值：json、jsonc、table、tsv。  默认值：json。
#### `--query -q`
JMESPath 查询字符串。 请参阅 [http://jmespath.org/](http://jmespath.org/])，获取详细信息和示例。
#### `--verbose`
提高日志记录详细程度。 使用 --debug 获取完整的调试日志。

## <a name="next-steps"></a>后续步骤

- 有关其他“azdata”命令的详细信息，请参阅 [azdata 参考](reference-azdata.md)。 

- 有关如何安装 **azdata** 工具的详细信息，请参阅[安装 azdata 以管理 SQL Server 2019 大数据群集](deploy-install-azdata.md)。
