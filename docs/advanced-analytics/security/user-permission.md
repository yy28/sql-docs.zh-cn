---
title: 授予执行 R 和 Python 脚本的数据库权限
description: 如何针对 SQL Server 机器学习服务授予对 R 和 Python 脚本执行的数据库用户权限。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/17/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 97e1fb6e2415e30f595d61dffa8a4952cfdc42d0
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715567"
---
# <a name="give-users-permission-to-sql-server-machine-learning-services"></a>向用户授予 SQL Server 的权限机器学习服务
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本文介绍如何向用户授予在 SQL Server 机器学习服务中运行外部脚本的权限, 并向数据库授予读取、写入或数据定义语言 (DDL) 权限。

有关详细信息, 请参阅[扩展性框架安全概述](../../advanced-analytics/concepts/security.md#permissions)中的 "权限" 一节。

<a name="permissions-external-script"></a>

## <a name="permission-to-run-scripts"></a>运行脚本的权限

如果自行安装[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , 并且在自己的实例中运行 R 或 Python 脚本, 则通常以管理员身份执行脚本。 因此, 对数据库中的各种操作和所有数据具有隐式权限。

但是, 大多数用户没有此类提升的权限。 例如, 使用 SQL 登录名访问数据库的组织中的用户通常不具有提升的权限。 因此, 对于使用 R 或 Python 的每个用户, 您必须授予机器学习服务的用户在使用该语言的每个数据库中运行外部脚本的权限。 以下是操作方法：

```sql
USE <database_name>
GO
GRANT EXECUTE ANY EXTERNAL SCRIPT TO [UserName]
```

> [!NOTE]
> 权限不特定于支持的脚本语言。 换句话说, R 脚本与 Python 脚本没有单独的权限级别。 如果需要为这些语言维护单独的权限, 请在单独的实例上安装 R 和 Python。

<a name="permissions-db"></a> 

## <a name="grant-databases-permissions"></a>Grant 数据库权限

当用户运行脚本时, 用户可能需要从其他数据库读取数据。 用户可能还需要创建新表以存储结果, 并将数据写入表中。

对于运行 R 或 Python 脚本的每个 Windows 用户帐户或 SQL 登录名, 请确保它具有特定数据库的相应权限: `db_datareader`读取数据、 `db_datawriter`将对象保存到数据库或`db_ddladmin`创建对象例如包含定型数据和序列化数据的存储过程或表。

例如, 下面[!INCLUDE[tsql](../../includes/tsql-md.md)]的语句为 SQL 登录名*mysqllogin 提供*在*ML_Samples*数据库中运行 t-sql 查询的权限。 若要运行此语句，SQL 登录名必须已经存在于服务器的安全上下文中。

```sql
USE ML_Samples
GO
EXEC sp_addrolemember 'db_datareader', 'MySQLLogin'
```

## <a name="next-steps"></a>后续步骤

有关每个角色中包含的权限的详细信息, 请参阅[数据库级角色](../../relational-databases/security/authentication-access/database-level-roles.md)。