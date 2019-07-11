---
title: mssqlctl 应用参考
titleSuffix: SQL Server big data clusters
description: Mssqlctl 应用程序命令的参考文章。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
manager: jroth
ms.date: 06/26/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 1ac884a8d77aa241402cedce3eaedeef9f60512a
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/10/2019
ms.locfileid: "67727535"
---
# <a name="mssqlctl-app"></a>mssqlctl 应用

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

以下文章提供了参考**应用程序**中的命令**mssqlctl**工具。 有关其他详细信息**mssqlctl**命令，请参阅[mssqlctl 引用](reference-mssqlctl.md)。

## <a name="commands"></a>命令
|     |     |
| --- | --- |
[mssqlctl 应用模板](reference-mssqlctl-app-template.md) | 模板。
[mssqlctl 应用 init](#mssqlctl-app-init) | 启动新应用程序框架。
[mssqlctl 应用创建](#mssqlctl-app-create) | 创建应用程序。
[mssqlctl 应用更新](#mssqlctl-app-update) | 更新应用程序。
[mssqlctl 应用列表](#mssqlctl-app-list) | 列出应用程序。
[mssqlctl app delete](#mssqlctl-app-delete) | 删除应用程序。
[mssqlctl 应用运行](#mssqlctl-app-run) | 运行应用程序。
[mssqlctl 应用描述](#mssqlctl-app-describe) | 介绍应用程序。
## <a name="mssqlctl-app-init"></a>mssqlctl 应用 init
可帮助你启动新应用程序框架和/或基于运行时环境的规范文件。
```bash
mssqlctl app init [--spec -s] 
                  [--name -n]  
                  [--version -v]  
                  [--template -t]  
                  [--destination -d]  
                  [--url -u]
```
### <a name="examples"></a>示例
创建新的应用程序的基架`spec.yaml`仅。
```bash
mssqlctl app init --spec
```
搭建基架，基于一个新 R 应用程序应用程序框架`r`模板。
```bash
mssqlctl app init --name reduce --template r
```
搭建基架，基于一个新 Python 应用程序应用程序框架`python`模板。
```bash
mssqlctl app init --name reduce --template python
```
搭建基架，基于一个新 SSIS 应用程序应用程序框架`ssis`模板。
```bash
mssqlctl app init --name reduce --template ssis            
```
### <a name="optional-parameters"></a>可选参数
#### `--spec -s`
生成只是应用程序 spec.yaml。
#### `--name -n`
应用程序名称。
#### `--version -v`
应用程序版本。
#### `--template -t`
模板名称。 有关关闭运行受支持的模板名称的完整列表 `mssqlctl app template list`
#### `--destination -d`
要将应用程序框架的位置。 默认值： 当前工作目录。
#### `--url -u`
指定不同的模板存储库位置。 默认值： https://github.com/Microsoft/SQLBDC-AppDeploy.git
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
## <a name="mssqlctl-app-create"></a>mssqlctl 应用创建
创建应用程序。
```bash
mssqlctl app create --spec -s 
                    
```
### <a name="examples"></a>示例
从包含有效 spec.yaml 部署规范的目录中创建新的应用程序。
```bash
mssqlctl app create --spec /path/to/dir/with/spec/yaml
```
### <a name="required-parameters"></a>必需的参数
#### `--spec -s`
包含描述该应用程序的 YAML 规范文件的目录的路径。
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
## <a name="mssqlctl-app-update"></a>mssqlctl 应用更新
更新的应用程序。
```bash
mssqlctl app update [--spec -s] 
                    [--yes -y]
```
### <a name="examples"></a>示例
更新现有应用程序中包含有效 spec.yaml 部署规范的目录。
```bash
mssqlctl app update --spec /path/to/dir/with/spec/yaml    
```
### <a name="optional-parameters"></a>可选参数
#### `--spec -s`
包含描述该应用程序的 YAML 规范文件的目录的路径。
#### `--yes -y`
不提示确认时从 CWD spec.yaml 文件更新应用程序。
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
## <a name="mssqlctl-app-list"></a>mssqlctl 应用列表
列出应用程序。，
```bash
mssqlctl app list [--name -n] 
                  [--version -v]
```
### <a name="examples"></a>示例
列出由名称和版本的应用程序。
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
增加日志记录详细程度，以显示所有调试日志。
#### `--help -h`
显示此帮助消息并退出。
#### `--output -o`
输出格式。  允许的值： json、 jsonc、 table、 tsv。  默认值： json。
#### `--query -q`
JMESPath 查询字符串。 请参阅[ http://jmespath.org/ ](http://jmespath.org/])有关详细信息和示例。
#### `--verbose`
提高日志记录详细程度。 使用--debug 可获取完整的调试日志。
## <a name="mssqlctl-app-delete"></a>mssqlctl 应用删除
删除应用程序。
```bash
mssqlctl app delete --name -n 
                    --version -v
```
### <a name="examples"></a>示例
删除应用程序的名称和版本。
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
增加日志记录详细程度，以显示所有调试日志。
#### `--help -h`
显示此帮助消息并退出。
#### `--output -o`
输出格式。  允许的值： json、 jsonc、 table、 tsv。  默认值： json。
#### `--query -q`
JMESPath 查询字符串。 请参阅[ http://jmespath.org/ ](http://jmespath.org/])有关详细信息和示例。
#### `--verbose`
提高日志记录详细程度。 使用--debug 可获取完整的调试日志。
## <a name="mssqlctl-app-run"></a>mssqlctl 应用运行
运行应用程序。
```bash
mssqlctl app run --name -n 
                 --version -v  
                 [--inputs]
```
### <a name="examples"></a>示例
运行应用程序与任何输入参数。
```bash
mssqlctl app run --name reduce --version v1
```
运行应用程序具有一个输入参数。
```bash
mssqlctl app run --name reduce --version v1 --inputs x=10
```
运行应用程序具有多个输入参数。
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
应用程序的输入参数 CSV`name=value`格式。
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
## <a name="mssqlctl-app-describe"></a>mssqlctl 应用描述
描述应用程序。
```bash
mssqlctl app describe [--spec -s] 
                      [--name -n]  
                      [--version -v]
```
### <a name="examples"></a>示例
介绍应用程序。
```bash
mssqlctl app describe --name reduce --version v1    
```
### <a name="optional-parameters"></a>可选参数
#### `--spec -s`
包含描述该应用程序的 YAML 规范文件的目录的路径。
#### `--name -n`
应用程序名称。
#### `--version -v`
应用程序版本。
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