---
title: "SQL Server 的 R 包同步 |Microsoft 文档"
ms.custom: 
ms.date: 01/04/2018
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: efb0477481e47af1ace78b938a64e72bace6d81f
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2018
---
# <a name="r-package-synchronization-for-sql-server"></a>SQL Server 的 R 包同步
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

包含在 SQL Server 2017 RevoScaleR 的版本包括可进行同步的文件系统和实例和数据库之间其中使用了包的 R 包的集合。

提供此功能是为了更加轻松地备份 SQL Server 数据库与关联的 R 包集合。 使用此功能，管理员可以还原而不仅仅是数据库中，但已由数据科学家使用该数据库中任何 R 包。

本指南介绍了包同步功能，以及如何使用[rxSyncPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsyncpackages)函数来执行以下任务：

+ 同步整个 SQL Server 数据库的包的列表

+ 同步单个用户，或一组用户使用的包

+ 如果用户移到不同的 SQL Server，你可以获取用户的工作数据库的备份，并将其还原到新的服务器，并为用户的包将安装到文件系统在新服务器上，根据需要通过。

例如，你可能在这些情况下使用包同步：

+ DBA 到新计算机已恢复的 SQL Server 实例，并询问用户从其 R 客户端连接和运行`rxSyncPackages`来刷新和还原其包。

+ 你认为文件系统上的 R 包已损坏，因此，你运行`rxSyncPackages`SQL Server 上。

## <a name="requirements"></a>需求

您可以使用包同步之前，你必须具有适当版本的 Microsoft R 或机器学习服务器。 此功能被提供 Microsoft R 版本 9.1.0 或更高版本。 

你还必须启用[包管理功能](r-package-how-to-enable-or-disable.md)服务器上。

### <a name="determine-whether-your-server-supports-package-management"></a>确定你的服务器是否支持包管理

此功能是 SQL Server 自 2017 年 1 CTP 2 中提供或更高版本。

可以通过升级要使用的 Microsoft 键。 最新版本的实例向 SQL Server 2016 的实例中添加此功能有关详细信息，请参阅[使用 SqlBindR.exe 升级 SQL Server R Services](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)。

### <a name="enable-the-package-management-feature"></a>启用包管理功能

若要使用包同步需要在 SQL Server 实例中，并在单独的数据库上启用了新的包管理功能。 有关详细信息，请参阅[启用或禁用 SQL Server 的包管理](r-package-how-to-enable-or-disable.md)。

1. 服务器管理员启用 SQL Server 实例的功能。
2. 对于每个数据库，管理员授予单个用户的功能安装或共享 R 包，使用数据库角色。

完成此操作后，你可以使用 RevoScaleR 函数，如[rxInstallPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstallpackages)来将包安装到数据库。  有关用户和他们可以使用的包，信息存储在 SQL Server 实例。 

每当添加新的包使用程序包管理功能时，更新 SQL Server 和文件系统中的这两个记录。 此信息可以用于还原整个数据库的包信息。

### <a name="permissions"></a>权限

+ 执行包同步函数的人员必须是安全主体对 SQL Server 实例和数据库的包。

+ 该函数的调用方必须是这些包管理角色之一的成员： **rpkgs 共享**或**rpkgs 私有**。

+ 若要同步包标记为**共享**，运行该函数的人员必须拥有成员身份**rpkgs 共享**角色和在移动的包必须已安装到共享作用域库。

+ 若要同步包标记为**私有**，管理员或包的所有者必须运行此函数中，和必须是私有的包。

+ 若要同步包代表其他用户，所有者必须 bhe 的成员**db_owner**数据库角色。

## <a name="how-package-synchronization-works"></a>包同步的工作原理

若要使用包同步，调用[rxSyncPackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsyncpackages)，这是中的新函数[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)。 

每次调用`rxSyncPackages`，必须指定 SQL Server 实例和数据库。 然后，列出的包，若要同步，或指定包作用域。

1. 通过创建 SQL Server 计算上下文`RxInSqlServer`函数。 如果未指定计算上下文，则使用当前的计算上下文。

2. 提供在指定的计算上下文的实例上的数据库的名称。 包将每个数据库同步。

3. 指定使用作用域参数进行同步的包。

    如果你使用**私有**同步作用域，仅拥有由指定的所有者的包。 如果指定**共享**同步作用域，在数据库中的所有非私有包。 
    
    如果运行该函数时未指定**私有**或**共享**作用域，同步所有包。

4. 如果该命令成功，文件系统中的现有包添加到数据库，使用指定的作用域和所有者。

    如果文件系统已损坏，包会还原基于数据库中维护的列表。

    未提供目标数据库上的包管理功能时，将引发错误:"包管理功能未被启用 SQL Server 上或版本不太旧"

### <a name="example-1-synchronize-all-package-by-database"></a>示例 1： 通过数据库同步所有包

此示例从本地文件系统中获取的任何新包，并安装数据库 [TestDB] 中的程序包。 因为任何所有者不是特定的该列表包含已为专用和共享的作用域中安装的所有包。

```R
connectionString <- "Driver=SQL Server;Server=myServer;Database=TestDB;Trusted_Connection=True;"
computeContext <- RxInSqlServer(connectionString = connectionString )
rxSyncPackages(computeContext=computeContext, verbose=TRUE)
```

### <a name="example-2-restrict-synchronized-packages-by-scope"></a>示例 2。 限制作用域的同步的的包

下面的示例将同步仅指定作用域中的包。

```R
#Shared scope
rxSyncPackages(computeContext=computeContext, scope="shared", verbose=TRUE)

#Private scope
rxSyncPackages(computeContext=computeContext, scope="private", verbose=TRUE)
```

### <a name="example-3-restrict-synchronized-packages-by-owner"></a>示例 3。 限制由所有者同步的包

下面的示例演示如何同步仅特定用户已安装的包。 SQL 登录名，在此示例中，标识该用户*user1*。

```R
rxSyncPackages(computeContext=computeContext, scope="private", owner = "user1", verbose=TRUE))
```

## <a name="related-resources"></a>相关资源

[SQL Server 的 R 包管理](r-package-management-for-sql-server-r-services.md)
