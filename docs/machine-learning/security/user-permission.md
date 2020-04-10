---
title: 为脚本授予权限
description: 如何为 SQL Server 机器学习服务上的 R 和 Python 脚本执行授予数据库用户权限。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/17/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 55a76b070a5f54562957f138d55896b49dbb15f1
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/04/2020
ms.locfileid: "81117090"
---
# <a name="give-users-permission-to-sql-server-machine-learning-services"></a>向用户授予 SQL Server 机器学习服务的权限
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本文介绍如何向用户授予在 SQL Server 机器学习服务中运行外部脚本的权限，以及向数据库授予读取、写入或数据定义语言 (DDL) 权限。

有关详细信息，请参阅[扩展框架安全性概述](../../machine-learning/concepts/security.md#permissions)中的“权限”部分。

<a name="permissions-external-script"></a>

## <a name="permission-to-run-scripts"></a>运行脚本的权限

如果自行安装了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，并且在自己的实例中运行 R 或 Python 脚本，则通常以管理员身份执行脚本。 因此，对数据库中的各种操作和所有数据都具有隐式权限。

但是，大多数用户没有此类的提升权限。 例如，组织中使用 SQL 登录访问数据库的用户通常没有提升权限。 因此，对于使用 R 或 Python 的每个用户，必须授予机器学习服务的用户在使用该语言的每个数据库中运行外部脚本的权限。 以下是操作方法：

```sql
USE <database_name>
GO
GRANT EXECUTE ANY EXTERNAL SCRIPT TO [UserName]
```

> [!NOTE]
> 权限不特定于受支持的脚本语言。 换句话说，R 脚本和 Python 脚本没有单独的权限级别。 如果需要为这些语言维护单独的权限，请在单独的实例上安装 R 和 Python。

<a name="permissions-db"></a> 

## <a name="grant-databases-permissions"></a>Grant 数据库权限

当某个用户运行脚本时，该用户可能需要从其他数据库读取数据。 此外，该用户可能还需要创建新表来存储结果，并将数据写入表中。

对于运行 R 或 Python 脚本的每个 Windows 用户帐户或 SQL 登录，请确保它对特定数据库具有以下适当权限：`db_datareader`（用于读取数据）、`db_datawriter`（用于将对象保存到数据库）或`db_ddladmin`（用于创建对象，例如包含已定型和序列化的数据的存储过程或表）。

例如，以下 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句为 SQL 登录名 MySQLLogin 提供在 ML_Samples 数据库中运行 T-SQL 查询的权限   。 若要运行此语句，SQL 登录名必须已经存在于服务器的安全上下文中。

```sql
USE ML_Samples
GO
EXEC sp_addrolemember 'db_datareader', 'MySQLLogin'
```

## <a name="next-steps"></a>后续步骤

若要详细了解每个角色包括的权限，请参阅 [数据库级别的角色](../../relational-databases/security/authentication-access/database-level-roles.md)。