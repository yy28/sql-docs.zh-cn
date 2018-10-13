---
title: 授予用户对 SQL Server 机器学习服务的权限 |Microsoft Docs
description: 如何向用户提供对 SQL Server 机器学习服务的权限。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/05/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: ad5c3fa3bf94bb88041c9ec81773b2a26013e517
ms.sourcegitcommit: 485e4e05d88813d2a8bb8e7296dbd721d125f940
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/11/2018
ms.locfileid: "49100328"
---
# <a name="give-users-permission-to-sql-server-machine-learning-services"></a>授予用户对 SQL Server 机器学习服务的权限
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文介绍如何在可授予用户权限在 SQL Server 机器学习服务中运行外部脚本并对其授予读取、 写入或数据定义语言 (DDL) 权限的数据库。

SQL Server 登录名或 Windows 用户帐户需要运行外部脚本，使用 SQL Server 数据或使用 SQL Server 作为计算上下文的运行。

登录名或用户帐户标识*安全主体*，那些可能需要多个级别的访问权限，具体取决于外部脚本要求：

+ 若要访问启用了外部脚本的数据库的权限。
+ 若要从受保护的对象，如表中读取数据的权限。
+ 能够将新数据写入到一个表，如某一模型，或评分结果。
+ 能够创建新对象，如表、 存储过程使用外部脚本，或自定义函数，使用 R 或 Python 作业。
+ SQL Server 计算机上安装新包或使用包提供给一组用户权限。

因此，每个人都在运行外部脚本使用 SQL Server 作为执行上下文必须映射到数据库中的用户。 SQL Server 安全性，是最简单的方法创建角色，以管理组的权限，并将用户分配到这些角色，而不是分别设置用户权限。

如果用户需要运行外部脚本中的数据库，或访问数据库对象和数据，即使用户要在外部工具使用 R 或 Python 必须映射到登录名或数据库中的帐户。 外部脚本从远程数据科学客户端发送还是使用 T-SQL 存储过程启动，则需要使用相同的权限。

例如，假设您创建在本地计算机运行的外部脚本，并且你想要在 SQL Server 上运行该代码。 必须确保符合以下条件：

+ 数据库允许远程连接。
+ SQL 登录名或用于数据库访问权限的 Windows 帐户具有已添加到 SQL Server 实例级别。
+ SQL 登录名或 Windows 用户必须有权执行外部脚本。 通常，此权限只能由数据库管理员添加。
+ SQL 登录名或窗口用户必须添加为具有相应的权限，其中的外部脚本执行上述任何操作每个数据库中的用户：
  + 正在检索数据。
  + 写入或更新数据。
  + 创建新对象，如表或存储的过程。

已预配并提供所需的权限的登录名或 Windows 用户帐户后，你可以运行外部脚本在 SQL Server 上通过在 R 中使用数据源对象或**revoscalepy**在 Python 中，或通过调用存储库包含外部脚本的过程。

每次从 SQL Server 启动外部脚本时，数据库引擎安全获取启动作业，并管理用户或登录名对安全对象的映射的用户的安全上下文。

因此，从远程客户端发起的所有外部脚本必须作为连接字符串的一部分指定的登录名或用户的信息。

<a name="permissions-external-script"></a> 

## <a name="permission-to-run-scripts"></a>运行脚本的权限

如果您安装了[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]您和您自己在你自己的实例中运行 R 或 Python 脚本，通常以管理员身份执行脚本。 因此，各种操作和数据库中的所有数据具有隐式权限。

大多数用户，但是，没有此类提升的权限。 例如，使用 SQL 登录名访问数据库通常在组织中的用户不具有提升的权限。 因此，对于每个用户都使用 R 或 Python，则必须授予用户的机器学习服务将使用的语言中的每个数据库运行外部脚本的权限。 以下是操作方法：

```SQL
USE <database_name>
GO
GRANT EXECUTE ANY EXTERNAL SCRIPT  TO [UserName]
```

> [!NOTE]
> 权限不特定于支持的脚本语言。 换而言之，没有与 Python 脚本的 R 脚本的单独的权限级别。 如果您需要保持对这些语言的单独权限，在单独的实例上安装 R 和 Python。

<a name="permissions-db"></a> 

## <a name="grant-databases-permissions"></a>Grant 数据库权限

在用户运行脚本时，用户可能需要从其他数据库读取数据。 用户可能还需要创建新表以存储结果，并将数据写入到表。

对于每个 Windows 用户帐户或 SQL 登录名运行 R 或 Python 脚本，请确保它对特定数据库具有适当的权限：`db_datareader`来读取数据，`db_datawriter`若要将对象保存到数据库，或`db_ddladmin`创建对象例如，存储的过程或表包含训练和序列化数据。

例如，以下[!INCLUDE[tsql](../../includes/tsql-md.md)]语句，为提供的 SQL 登录名*MySQLLogin*中运行 T-SQL 查询的权限*ML_Samples*数据库。 若要运行此语句，SQL 登录名必须已经存在于服务器的安全上下文中。

```SQL
USE ML_Samples
GO
EXEC sp_addrolemember 'db_datareader', 'MySQLLogin'
```

## <a name="next-steps"></a>后续步骤

有关每个角色中包括的权限的详细信息，请参阅[数据库级别角色](../../relational-databases/security/authentication-access/database-level-roles.md)。