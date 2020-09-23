---
title: azdata sql 参考
titleSuffix: SQL Server big data clusters
description: azdata sql 命令的参考文章。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 06/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 9965c6805cb8e12e6a5a2990a43bb7bf7c937fe1
ms.sourcegitcommit: 883435b4c7366f06ac03579752093737b098feab
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89733496"
---
# <a name="azdata-sql"></a>azdata sql

[!INCLUDE[SQL Server 2019](../../includes/applies-to-version/sqlserver2019.md)]

以下文章提供了 `azdata` 工具中 `sql` 命令的参考。 有关其他 `azdata` 命令的详细信息，请参阅 [azdata 参考](reference-azdata.md)。

## <a name="commands"></a>命令
| 命令 | 描述 |
| --- | --- |
[azdata sql shell](#azdata-sql-shell) | SQL 数据库 CLI 允许用户通过 T-SQL 与 SQL Server 交互。
[azdata sql query](#azdata-sql-query) | query 命令允许执行 T-SQL 查询。
## <a name="azdata-sql-shell"></a>azdata sql shell
SQL 数据库 CLI 允许用户通过 T-SQL 与 SQL Server 交互。
```bash
azdata sql shell 
```
### <a name="examples"></a>示例
用于启动交互式体验的示例命令行。
```bash
azdata sql shell
```
### <a name="global-arguments"></a>全局参数
#### `--debug`
提高日志记录详细程度以显示所有调试日志。
#### `--help -h`
显示此帮助消息并退出。
#### `--output -o`
输出格式。  允许的值：json、jsonc、table、tsv。  默认值：json。
#### `--query -q`
JMESPath 查询字符串。 请参阅 [http://jmespath.org/](http://jmespath.org)，获取详细信息和示例。
#### `--verbose`
提高日志记录详细程度。 使用 --debug 获取完整的调试日志。
## <a name="azdata-sql-query"></a>azdata sql query
query 命令允许执行 T-SQL 查询。
```bash
azdata sql query --database -d 
                 -q
```
### <a name="examples"></a>示例
选择表名列表。  数据库默认为 master。
```bash
azdata sql query "SELECT name FROM SYS.TABLES"
```
### <a name="required-parameters"></a>必需的参数
#### `--database -d`
要在其中运行查询的数据库。  默认为 master。
#### `-q`
要执行的 T-SQL 查询。
### <a name="global-arguments"></a>全局参数
#### `--debug`
提高日志记录详细程度以显示所有调试日志。
#### `--help -h`
显示此帮助消息并退出。
#### `--output -o`
输出格式。  允许的值：json、jsonc、table、tsv。  默认值：json。
#### `--query -q`
JMESPath 查询字符串。 请参阅 [http://jmespath.org/](http://jmespath.org)，获取详细信息和示例。
#### `--verbose`
提高日志记录详细程度。 使用 --debug 获取完整的调试日志。

## <a name="next-steps"></a>后续步骤

有关其他 `azdata` 命令的详细信息，请参阅 [azdata 参考](reference-azdata.md)。 有关如何安装 `azdata` 工具的详细信息，请参阅[安装 azdata 以管理 SQL Server 2019 大数据群集](../install/deploy-install-azdata.md)。
