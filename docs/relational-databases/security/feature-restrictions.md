---
title: 功能限制 | Microsoft Docs
ms.custom: ''
ms.date: 01/09/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
author: vainolo
ms.author: arib
manager: tomerw
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 99a0a768334ab5335591fae69e4f18060fba9866
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66506915"
---
# <a name="feature-restrictions"></a>功能限制

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

通过访问数据库的 Web 应用是 SQL Server 攻击的一个常见来源，其中各种形式的 SQL 注入攻击用于收集有关数据库的信息。  理想情况下，应用程序代码已开发，因此它不允许 SQL 注入。  但是，在包含旧版代码和外部代码的大型代码库中，人们永远也无法确保已解决所有情况，因此 SQL 注入是我们必须要防范的不争事实。  功能限制的目的是为了防止某些形式的 SQL 注入泄漏有关数据库的信息（甚至是在 SQL 注入成功时）。

## <a name="enabling-feature-restrictions"></a>启用功能限制

使用 `sp_add_feature_restriction` 存储过程可以启用功能限制，如下所示：

```sql
EXEC sp_add_feature_restriction <feature>, <object_class>, <object_name>
```

可以限制以下功能：

| 功能          | 描述 |
|------------------|-------------|
| N'ErrorMessages' | 限制后，将屏蔽错误消息中的任何用户数据。 请参阅[错误消息功能限制](#error-messages-feature-restriction) |
| N'Waitfor'       | 限制后，命令将立即返回，不产生延迟。 请参阅 [WAITFOR 功能限制](#waitfor-feature-restriction) |

`object_class` 的值可以为 `N'User'` 或 `N'Role'`，表示 `object_name` 是数据库中的用户名还是角色名。

以下示例将导致屏蔽用户 `MyUser` 的所有错误消息：

```sql
EXEC sp_add_feature_restriction N'ErrorMessages', N'User', N'MyUser'
```

## <a name="disabling-feature-restrictions"></a>禁用功能限制

使用 `sp_drop_feature_restriction` 存储过程可以禁用功能限制，如下所示：

```sql
EXEC sp_drop_feature_restriction <feature>, <object_class>, <object_name>
```

以下示例禁用用户 `MyUser` 的错误消息屏蔽：

```sql
EXEC sp_drop_feature_restriction N'ErrorMessages', N'User', N'MyUser'
```

## <a name="viewing-feature-restrictions"></a>查看功能限制

`sys.sql_feature_restrictions` 视图显示数据库中当前定义的所有功能限制。 有关模式的信息，请参阅 [sys.sql_feature_restrictions](../system-catalog-views/sys-sql-feature-restrictions.md)。

## <a name="feature-restrictions"></a>功能限制

### <a name="error-messages-feature-restriction"></a>错误消息功能限制

一种常见的 SQL 注入攻击方法是注入导致错误的代码。  通过检查错误消息，攻击者可以了解有关系统的信息，从而实现更具针对性的攻击。  当应用程序不显示查询结果而显示错误消息时，此攻击尤其有用。

请考虑使用具有以下形式的请求的 Web 应用：

```html
http://www.contoso.com/employee.php?id=1
```

它将执行以下数据库查询：

```sql
SELECT Name FROM EMPLOYEES WHERE Id=$EmpId
```

如果将作为 `Id` 参数传递给 Web 应用请求的值复制到数据库查询中的替换 $EmpId，则攻击者可以发出以下请求：

```html
http://www.contoso.com/employee.php?id=1 AND CAST(DB_NAME() AS INT)=0
```

将返回以下错误，使攻击者能够了解数据库的名称：

```sql
Conversion failed when converting the nvarchar value 'HR_Data' to data type int.
```

在为数据库中的应用程序用户启用错误消息功能限制后，系统将屏蔽返回的错误消息，以便不泄漏有关数据库的内部信息：

```sql
Conversion failed when converting the ****** value '******' to data type ******.
```

同样，攻击者可以发出以下请求：

```html
http://www.contoso.com/employee.php?id=1 AND CAST(Salary AS TINYINT)=0
```

将返回以下错误，使攻击者能够了解雇员的薪酬：

```sql
Arithmetic overflow error for data type tinyint, value = 140000.
```

使用错误消息功能限制，数据库将返回：

```sql
Arithmetic overflow error for data type ******, value = ******.
```

### <a name="waitfor-feature-restriction"></a>WAITFOR 功能限制

隐蔽 SQL 注入是指应用程序不向攻击者提供注入的 SQL 的结果或错误消息，但攻击者可以通过构造条件查询（其中执行两个条件分支的时间有所相同）来推断数据库中的信息。 通过比较响应时间，攻击者可以了解执行的分支，从而了解有关系统的信息。 此攻击的最简单变体是使用 `WAITFOR` 语句来引入延迟。

请考虑使用具有以下形式的请求的 Web 应用：

```html
http://www.contoso.com/employee.php?id=1
```

它将执行以下数据库查询：

```sql
SELECT Name FROM EMPLOYEES WHERE Id=$EmpId
```

如果将作为 `Id` 参数传递给 Web 应用请求的值复制到数据库查询中的替换 $EmpId，则攻击者可以发出以下请求：

```html
http://www.contoso.com/employee.php?id=1; IF SYSTEM_USER='sa' WAITFOR DELAY '00:00:05'
```

如果正在使用 `sa` 帐户，则查询将需要 5 秒钟的额外时间。 如果在数据库中禁用了 `WAITFOR` 功能限制，则将忽略 `WAITFOR` 语句，并且不会使用此攻击泄露信息。
