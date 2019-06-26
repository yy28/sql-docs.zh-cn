---
title: mssqlctl sql 参考
titleSuffix: SQL Server big data clusters
description: Mssqlctl sql 命令的参考文章。
author: rothja
ms.author: jroth
manager: jroth
ms.date: 06/26/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 536d4712a6ccb288ca60c038a37e99c2be8a5eba
ms.sourcegitcommit: ce5770d8b91c18ba5ad031e1a96a657bde4cae55
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67394199"
---
# <a name="mssqlctl-sql"></a>mssqlctl sql

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

以下文章提供了参考**sql**中的命令**mssqlctl**工具。 有关其他详细信息**mssqlctl**命令，请参阅[mssqlctl 引用](reference-mssqlctl.md)。

## <a name="commands"></a>命令
|     |     |
| --- | --- |
[mssqlctl sql shell](#mssqlctl-sql-shell) | SQL DB CLI 允许用户与通过 T-SQL 的 SQL Server 进行交互。
[mssqlctl sql 查询](#mssqlctl-sql-query) | 查询命令允许执行的 T-SQL 查询。
## <a name="mssqlctl-sql-shell"></a>mssqlctl sql shell
SQL DB CLI 允许用户与通过 T-SQL 的 SQL Server 进行交互。
```bash
mssqlctl sql shell 
```
### <a name="examples"></a>示例
若要启动的交互式体验的示例命令行。
```bash
mssqlctl sql shell
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
## <a name="mssqlctl-sql-query"></a>mssqlctl sql 查询
查询命令允许执行的 T-SQL 查询。
```bash
mssqlctl sql query --database -d 
                   -q
```
### <a name="examples"></a>示例
选择表名称的列表。  数据库默认值为 master。
```bash
mssqlctl sql query 'SELECT name FROM SYS.TABLES'
```
### <a name="required-parameters"></a>必需的参数
#### `--database -d`
在运行查询的数据库。  默认值为 master。
#### `-q`
要执行的 T-SQL 查询。
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