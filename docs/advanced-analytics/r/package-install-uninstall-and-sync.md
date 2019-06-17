---
title: 从文件系统-SQL Server 机器学习服务的 R 包同步
description: 使用文件系统上安装较新版本更新 SQL Server 上的 R 库。
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: f6782acd011242cfd9b8ed4fe24a11fba85e932c
ms.sourcegitcommit: a91c3f4fe2587d474cd4d470bda93239ba2693bb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/14/2019
ms.locfileid: "67140520"
---
# <a name="r-package-synchronization-for-sql-server"></a>适用于 SQL Server 的 R 包同步
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

RevoScaleR SQL Server 2017 中包括的版本包括同步文件系统和实例和数据库之间使用的包的位置的 R 包的集合的能力。

提供此功能是为了更加轻松地备份 SQL Server 数据库与关联的 R 包集合。 使用此功能，管理员可以还原不只是数据库中，但已由数据科学家使用该数据库的任何 R 包。

本文介绍了包同步功能，以及如何使用[rxSyncPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsyncpackages)函数来执行以下任务：

+ 同步用于整个 SQL Server 数据库的包列表

+ 同步由单个用户，或一组用户使用的包

+ 如果用户移至不同的 SQL Server，可以执行的用户的工作数据库备份和还原到新的服务器，并为用户的包将安装到文件系统在新服务器上，所需的。

例如，你可以在这些情况下使用包同步：

+ DBA 都还原到新计算机的 SQL Server 实例，并要求用户从其 R 客户端连接和运行`rxSyncPackages`刷新并还原其包。

+ 您认为文件系统上的 R 包已损坏，因此在运行`rxSyncPackages`SQL 服务器上。

## <a name="requirements"></a>要求

您可以使用包同步之前，必须具有适当版本的 Microsoft R 或机器学习服务器。 在 Microsoft R 版本 9.1.0 或更高版本提供此功能。 

您还必须启用[包管理功能](r-package-how-to-enable-or-disable.md)在服务器上。

### <a name="determine-whether-your-server-supports-package-management"></a>确定你的服务器是否支持包管理

此功能非常适用于 SQL Server 2017 CTP 2 或更高版本。

可以通过升级要使用 Microsoft R 的最新版本的实例向 SQL Server 2016 的实例中添加此功能有关详细信息，请参阅[使用 SqlBindR.exe 升级 SQL Server R Services](../install/upgrade-r-and-python.md)。

### <a name="enable-the-package-management-feature"></a>启用包管理功能

若要使用包同步要求的 SQL Server 实例上，并在单独的数据库上启用新的包管理功能。 有关详细信息，请参阅[启用或禁用 SQL Server 的包管理](r-package-how-to-enable-or-disable.md)。

1. 服务器管理员启用 SQL Server 实例的功能。
2. 对于每个数据库，管理员授予单个用户安装或共享的 R 包的功能使用数据库角色。

完成此操作后，你可以使用 RevoScaleR 函数，如[rxInstallPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstallpackages)包安装到数据库。  有关用户以及他们可以使用的包的信息存储在 SQL Server 实例。 

每当添加新的包使用包管理功能，请在更新这两个记录在 SQL Server 和文件系统中。 此信息可用于还原整个数据库的包信息。

### <a name="permissions"></a>权限

+ 执行包同步函数的人员必须是安全主体上的 SQL Server 实例和数据库的包所在的。

+ 函数的调用方必须是其中一种包管理角色的成员： **rpkgs 共享**或**rpkgs 专用**。

+ 若要将包标记为同步**共享**，运行该函数的人员必须拥有成员身份**rpkgs 共享**必须已安装角色，以及要移动的包到共享作用域库。

+ 若要将包标记为同步**专用**，管理员或包的所有者必须运行此函数，并必须是私有的包。

+ 若要同步代表其他用户的包，所有者必须是属于**db_owner**数据库角色。

## <a name="how-package-synchronization-works"></a>包同步工作原理

若要使用包同步，请调用[rxSyncPackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsyncpackages)，这是中的新函数[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)。 

每次调用`rxSyncPackages`，必须指定 SQL Server 实例和数据库。 然后，列出的包进行同步，或指定包作用域。

1. 使用创建 SQL Server 计算上下文`RxInSqlServer`函数。 如果未指定计算上下文，则使用当前的计算上下文。

2. 提供在指定的计算上下文的实例上的数据库的名称。 每个数据库同步的包。

3. 指定要使用的作用域参数同步的包。

    如果您使用**专用**同步作用域，指定所有者所拥有的唯一包。 如果指定**共享**同步作用域，在数据库中的所有非私有包。 
    
    如果函数运行而未指定任一**私有**或**共享**作用域，同步所有包。

4. 如果该命令成功，文件系统中的现有包添加到数据库，使用指定的作用域和所有者。

    如果文件系统已损坏，包将还原基于数据库中维护的列表。

    如果包管理功能不可用目标数据库上，会引发错误："包管理功能或者没有启用 SQL Server 上或版本太旧"

### <a name="example-1-synchronize-all-package-by-database"></a>示例 1： 将所有软件包都同步数据库

此示例从本地文件系统中获取任何新的包，并在数据库 [TestDB] 中安装包。 没有所有者是特定的因为该列表包含已安装的专用和共享作用域的所有包。

```R
connectionString <- "Driver=SQL Server;Server=myServer;Database=TestDB;Trusted_Connection=True;"
computeContext <- RxInSqlServer(connectionString = connectionString )
rxSyncPackages(computeContext=computeContext, verbose=TRUE)
```

### <a name="example-2-restrict-synchronized-packages-by-scope"></a>示例 2。 限制按作用域的同步的包

下面的示例将同步仅在指定范围内的包。

```R
#Shared scope
rxSyncPackages(computeContext=computeContext, scope="shared", verbose=TRUE)

#Private scope
rxSyncPackages(computeContext=computeContext, scope="private", verbose=TRUE)
```

### <a name="example-3-restrict-synchronized-packages-by-owner"></a>示例 3。 限制由所有者同步的包

下面的示例演示了如何同步仅为特定用户安装的包。 SQL 登录名，在此示例中，标识的用户*user1*。

```R
rxSyncPackages(computeContext=computeContext, scope="private", owner = "user1", verbose=TRUE))
```

## <a name="related-resources"></a>相关资源

[SQL Server 的 R 包管理](install-additional-r-packages-on-sql-server.md)
