---
title: mssqlctl 应用参考
titleSuffix: SQL Server 2019 big data clusters
description: Mssqlctl 应用程序命令的参考文章。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/28/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: fa2b43c352fbab39cd00112b9646a87a2b752f5b
ms.sourcegitcommit: 2533383a7baa03b62430018a006a339c0bd69af2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57018483"
---
# <a name="mssqlctl-app"></a>mssqlctl 应用

以下文章提供了参考**应用程序**中的命令**mssqlctl**工具。 有关其他详细信息**mssqlctl**命令，请参阅[mssqlctl 引用](reference-mssqlctl.md)。

## <a id="commands"></a> 命令

|||
|---|---|
| [create](#create) | 创建应用程序。 |
| [delete](#delete) | 删除应用程序。 |
| [describe](#describe) | 介绍应用程序。 |
| [init](#init) | 启动新应用程序框架。 |
| [list](#list) | 列出应用程序。 |
| [run](#run) | 运行应用程序。 |
| [update](#update) | 更新应用程序。 |
| [template](reference-mssqlctl-app-template.md) | 模板命令。 |

## <a id="create"></a> mssqlctl 应用创建

创建应用程序。

```
mssqlctl app create
   --assets
   --code
   --description
   --entrypoint
   --inputs
   --name
   --outputs
   --runtime
   --spec
   --version
   --yes
```

### <a name="parameters"></a>Parameters

| Parameters | Description |
|---|---|
| **--assets -a** | 要包含的其他应用程序文件资产的列表。 |
| **--code -c** | R 或 Python 代码文件的路径。 |
| **--description -d** | 应用程序的说明。 |
| **--entrypoint** |  |
| **--inputs** | 输入的参数架构。 |
| **--name -n** | 应用程序名称。 |
| **--outputs** | 输出参数架构。 |
| **--runtime -r** | 应用程序运行时。  允许的值：Mleap, Python, R, SSIS. |
| **--spec -s** | 包含描述该应用程序的 YAML 规范文件的目录的路径。 |
| **--version -v** | 应用程序版本。 |
| **-是-y** | 不提示确认时从 CWD spec.yaml 文件创建应用程序。 |

### <a name="examples"></a>示例

创建新的应用程序通过 spec.yaml （推荐）。

```
mssqlctl app create --spec /path/to/dir/with/spec/yaml
```

创建新的 Python 应用内联，它使用的参数。

```
mssqlctl app create --name add --version v1 --inputs x=float, y=float --outputs result=float --runtime Python --code add.py  --init init.py
```

创建新 R 应用程序内联的使用的参数。

```
mssqlctl app create --name add --version v1 --inputs x=numeric, y=numeric --outputs result=numeric --runtime R --code add.R  --init init.R
```

使用其他文件的资产，以包括创建新的 R 应用程序内联。

```
mssqlctl app create --name add --version v1 --runtime R --code  add.R --assets file.RData,/path/to/more/files
```

## <a id="delete"></a> mssqlctl app delete

删除应用程序。

```
mssqlctl app delete
   --name
   --version
```

### <a name="parameters"></a>Parameters

| Parameters | Description |
|---|---|
| **--name -n** | 应用程序名称。 |
| **--version -v** | 应用程序版本。 |

### <a name="examples"></a>示例

删除应用程序的名称和版本。

```
mssqlctl app delete --name reduce --version v1
```

## <a id="describe"></a> mssqlctl app describe

介绍应用程序。

```
mssqlctl app describe
   --name
   --spec
   --version
```

### <a name="parameters"></a>Parameters

| Parameters | Description |
|---|---|
| **--name -n** | 应用程序名称。 |
| **--spec -s** | 包含描述该应用程序的 YAML 规范文件的目录的路径。 |
| **--version -v** | 应用程序版本。 |

### <a name="examples"></a>示例

介绍应用程序。

```
mssqlctl app describe --name reduce --version v1
```

## <a id="init"></a> mssqlctl 应用 init

启动新应用程序框架。

```
mssqlctl app init
   --destination
   --name
   --spec
   --template
   --url
   --version
```

### <a name="parameters"></a>Parameters

| Parameters | Description |
|---|---|
| **--destination -d** | 要将应用程序框架的位置。 默认值： 当前工作目录。 |
| **--name -n** | 应用程序名称。 |
| **--spec -s** | 生成只是应用程序 spec.yaml。 |
| **--template -t** | 模板名称。 有关关闭受支持的模板名称的完整列表运行`mssqlctl app template list`。 |
| **--url -u** | 指定不同的模板存储库位置。 默认值： https://github.com/Microsoft/sql-server-samples.git。 |
| **--version -v** | 应用程序版本。 |

### <a name="examples"></a>示例

创建新的应用程序的基架`spec.yaml`仅。

```
mssqlctl app init --spec
```

搭建基架，基于一个新 R 应用程序应用程序框架`r`模板。

```
mssqlctl app init --name reduce --template r
```

搭建基架，基于一个新 Python 应用程序应用程序框架`python`模板。

```
mssqlctl app init --name reduce --template python
```

搭建基架，基于一个新 SSIS 应用程序应用程序框架`ssis`模板。

```
mssqlctl app init --name reduce --template ssis
```

## <a id="list"></a> mssqlctl app list

列出应用程序。

```
mssqlctl app list
   --name
   --version
```

### <a name="parameters"></a>Parameters

| Parameters | Description |
|---|---|
| **--name -n** | 应用程序名称。 |
| **--version -v** | 应用程序版本。 |

### <a name="examples"></a>示例

列出由名称和版本的应用程序。

```
mssqlctl app list --name reduce  --version v1
```

按名称列出所有应用程序版本。

```
mssqlctl app list --name reduce
```

列出所有应用程序。

```
mssqlctl app list
```

## <a id="run"></a> mssqlctl app run

运行应用程序。

```
mssqlctl app run
   --name
   --version
   --inputs
```

### <a name="parameters"></a>Parameters

| Parameters | Description |
|---|---|
| **--name -n** | 应用程序名称。 |
| **--version -v** | 应用程序版本。 |
| **--inputs** | 应用程序的输入参数 CSV`name=value`格式。 |

### <a name="examples"></a>示例

运行应用程序与任何输入参数。

```
mssqlctl app run --name reduce --version v1
```

运行应用程序具有一个输入参数。

```
mssqlctl app run --name reduce --version v1 --inputs x=10
```

运行应用程序具有多个输入参数。

```
mssqlctl app run --name reduce --version v1 --inputs x=10,y5.6
```

## <a id="update"></a> mssqlctl app update

更新应用程序。

```
mssqlctl app update
   --spec
   --yes
```

### <a name="parameters"></a>Parameters

| Parameters | Description |
|---|---|
| **--spec -s** | 包含描述该应用程序的 YAML 规范文件的目录的路径。 |
| **-是-y** | 不提示确认时从 CWD spec.yaml 文件更新应用程序。 |

## <a name="next-steps"></a>后续步骤

有关其他详细信息**mssqlctl**命令，请参阅[mssqlctl 引用](reference-mssqlctl.md)。 有关如何安装详细信息**mssqlctl**工具，请参阅[安装 mssqlctl 来管理 SQL Server 2019 大数据群集](deploy-install-mssqlctl.md)。