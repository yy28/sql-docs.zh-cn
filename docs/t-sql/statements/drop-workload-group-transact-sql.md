---
title: DROP WORKLOAD GROUP (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/10/2020
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP_WORKLOAD_GROUP_TSQL
- DROP WORKLOAD GROUP
dev_langs:
- TSQL
helpviewer_keywords:
- DROP WORKLOAD GROUP statement
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azure-sqldw-latest||=azuresqldb-mi-current'
ms.openlocfilehash: 6e75e84884bca1fef4d42a64056e2ef38111e6db
ms.sourcegitcommit: 0a9058c7da0da9587089a37debcec4fbd5e2e53a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/14/2020
ms.locfileid: "75952342"
---
# <a name="drop-workload-group-transact-sql"></a>DROP WORKLOAD GROUP (Transact-SQL)

## <a name="click-a-product"></a>单击一个产品！

在下一行中，单击你感兴趣的产品名称。 单击时此网页上的此位置会显示适合你单击的任何产品的不同内容。

::: moniker range=">=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current||=sqlallproducts-allversions"

> |||||
> |---|---|---|---|
> |**_\* SQL Server \*_** &nbsp;|[SQL 数据库<br />托管实例](drop-workload-group-transact-sql.md?view=azuresqldb-mi-current)|[Azure Synapse<br />Analytics](drop-workload-group-transact-sql.md?view=azure-sqldw-latest)|

&nbsp;

## <a name="sql-server-and-sql-database-managed-instance"></a>SQL Server 和 SQL 数据库托管实例

删除现有的用户定义资源调控器工作负荷组。

![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)。

## <a name="syntax"></a>语法

```
DROP WORKLOAD GROUP group_name
[;]
```

## <a name="arguments"></a>参数

*group_name* 现有的用户定义工作负荷组的名称。

## <a name="remarks"></a>备注

不允许对资源调控器内部组或默认组使用 DROP WORKLOAD GROUP 语句。

建议您在熟悉资源调控器状态之后再执行 DDL 语句。 有关详细信息，请参阅 [Resource Governor](../../relational-databases/resource-governor/resource-governor.md)。

如果工作负荷组包含活动会话，则调用 ALTER RESOURCE GOVERNOR RECONFIGURE 语句以应用更改时，删除工作负荷组或将其移至其他资源池的操作将失败。 若要避免此问题，可以执行以下操作之一：

- 等待受影响组的所有会话均断开连接，然后重新运行 ALTER RESOURCE GOVERNOR RECONFIGURE 语句。

- 使用 KILL 命令显式停止受影响的组中的会话，然后重新运行 ALTER RESOURCE GOVERNOR RECONFIGURE 语句。

- 重新启动服务器。 完成重新启动过程后，将不会创建已删除的组，并且已移动的组将使用新分配的资源池。

- 在已发出 DROP WORKLOAD GROUP 语句但决定不打算显式停止会话以应用更改的情况下，您可以使用在发出 DROP 语句之前组的名称来重新创建组，然后将该组移动到原始资源池。 若要应用更改，请运行 ALTER RESOURCE GOVERNOR RECONFIGURE 语句。

## <a name="permissions"></a>权限

需要 CONTROL SERVER 权限。

## <a name="examples"></a>示例

下面的示例删除名为 `adhoc` 的工作负荷组。

```
DROP WORKLOAD GROUP adhoc;
GO
ALTER RESOURCE GOVERNOR RECONFIGURE;
GO
```

## <a name="see-also"></a>另请参阅

- [资源调控器](../../relational-databases/resource-governor/resource-governor.md)
- [CREATE WORKLOAD GROUP (Transact-SQL)](../../t-sql/statements/create-workload-group-transact-sql.md)  
- [ALTER 工作负荷组 (Transact-SQL)](../../t-sql/statements/alter-workload-group-transact-sql.md)
- [创建资源池 (Transact-SQL)](../../t-sql/statements/create-resource-pool-transact-sql.md)
- [ALTER RESOURCE POOL (Transact-SQL)](../../t-sql/statements/alter-resource-pool-transact-sql.md)
- [DROP RESOURCE POOL (Transact-SQL)](../../t-sql/statements/drop-resource-pool-transact-sql.md)
- [ALTER RESOURCE GOVERNOR (Transact-SQL)](../../t-sql/statements/alter-resource-governor-transact-sql.md)  
  
::: moniker-end
::: moniker range="=azure-sqldw-latest||=sqlallproducts-allversions"

> ||||
> |---|---|---|
> |[SQL Server](drop-workload-group-transact-sql.md?view=sql-server-2017)||[SQL 数据库<br />托管实例](drop-workload-group-transact-sql.md?view=azuresqldb-mi-current)||**_\* Azure Synapse<br />Analytics \*_** &nbsp;||||

&nbsp;

## <a name="azure-synapse-analytics-preview"></a>Azure Synapse Analytics（预览）

删除工作负荷组。  语句完成后，设置生效。

![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)。

## <a name="syntax"></a>语法

```
DROP WORKLOAD GROUP group_name  
```

## <a name="arguments"></a>参数

group_name   
现有的用户定义工作负荷组的名称。

## <a name="remarks"></a>备注

如果存在用于工作负荷组的分类器，则不能删除工作负荷组。  在删除工作负荷组之前，先删除分类器。  如果有活动请求正在使用要删除的工作负荷组中的资源，则删除工作负载语句将在这些请求之后被阻止。

## <a name="examples"></a>示例

使用以下代码示例来确定在删除工作负荷组之前需要删除的分类器。

```sql
SELECT c.name as classifier_name
      ,'DROP WORKLOAD CLASSIFIER '+c.name as drop_command
  FROM sys.workload_management_workload_classifiers c
  JOIN sys.workload_management_workload_groups g
    ON c.group_name = g.name
  WHERE g.name = 'wgXYZ' --change the filter to the workload being dropped
```

## <a name="permissions"></a>权限

需要 CONTROL DATABASE 权限

## <a name="see-also"></a>另请参阅

[CREATE WORKLOAD GROUP (Transact-SQL)](../../t-sql/statements/create-workload-group-transact-sql.md)

::: moniker-end
