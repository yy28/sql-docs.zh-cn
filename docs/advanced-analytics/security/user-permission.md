---
title: R 和 Python 脚本执行的 SQL Server 机器学习服务的 Grant 数据库权限
description: 如何授予 SQL Server 机器学习服务上的 R 和 Python 脚本执行的数据库用户权限。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/17/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: e281f1712163aeee1846565458c2b037077c8588
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62641662"
---
# <a name="give-users-permission-to-sql-server-machine-learning-services"></a>授予用户对 SQL Server 机器学习服务的权限
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文介绍如何在可授予用户权限在 SQL Server 机器学习服务中运行外部脚本并对其授予读取、 写入或数据定义语言 (DDL) 权限的数据库。

有关详细信息，请参阅中的权限部分[的可扩展性框架安全概述](../../advanced-analytics/concepts/security.md#permissions)。

<a name="permissions-external-script"></a>

## <a name="permission-to-run-scripts"></a>运行脚本的权限

如果您安装了[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]您和您自己在你自己的实例中运行 R 或 Python 脚本，通常以管理员身份执行脚本。 因此，各种操作和数据库中的所有数据具有隐式权限。

大多数用户，但是，没有此类提升的权限。 例如，使用 SQL 登录名访问数据库通常在组织中的用户不具有提升的权限。 因此，对于每个用户都使用 R 或 Python，则必须授予用户的机器学习服务将使用的语言中的每个数据库运行外部脚本的权限。 以下是操作方法：

```sql
USE <database_name>
GO
GRANT EXECUTE ANY EXTERNAL SCRIPT TO [UserName]
```

> [!NOTE]
> 权限不特定于支持的脚本语言。 换而言之，没有与 Python 脚本的 R 脚本的单独的权限级别。 如果您需要保持对这些语言的单独权限，在单独的实例上安装 R 和 Python。

<a name="permissions-db"></a> 

## <a name="grant-databases-permissions"></a>Grant 数据库权限

在用户运行脚本时，用户可能需要从其他数据库读取数据。 用户可能还需要创建新表以存储结果，并将数据写入到表。

对于每个 Windows 用户帐户或 SQL 登录名运行 R 或 Python 脚本，请确保它对特定数据库具有适当的权限：`db_datareader`来读取数据，`db_datawriter`若要将对象保存到数据库，或`db_ddladmin`创建对象例如，存储的过程或表包含训练和序列化数据。

例如，以下[!INCLUDE[tsql](../../includes/tsql-md.md)]语句，为提供的 SQL 登录名*MySQLLogin*中运行 T-SQL 查询的权限*ML_Samples*数据库。 若要运行此语句，SQL 登录名必须已经存在于服务器的安全上下文中。

```sql
USE ML_Samples
GO
EXEC sp_addrolemember 'db_datareader', 'MySQLLogin'
```

## <a name="next-steps"></a>后续步骤

有关每个角色中包括的权限的详细信息，请参阅[数据库级别角色](../../relational-databases/security/authentication-access/database-level-roles.md)。