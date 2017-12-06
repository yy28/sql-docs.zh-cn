---
title: "SQL Server 的 R 包同步 |Microsoft 文档"
ms.custom: 
ms.date: 10/02/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: fb56ffa08160934e1a3eac340a81ba7d6427ad49
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/01/2017
---
# <a name="r-package-synchronization-for-sql-server"></a>SQL Server 的 R 包同步

SQL Server 2017 包括可进行同步的文件系统和实例和数据库之间其中使用了包的 R 包的集合。
提供此功能是为了更加轻松地备份 SQL Server 数据库与关联的 R 包集合。 使用此功能，管理员可以还原而不仅仅是数据库中，但已由数据科学家使用该数据库中任何 R 包。

本主题描述包同步功能，以及如何使用[rxSyncPackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsyncpackages)函数来执行以下任务：

+ 同步整个 SQL Server 数据库的包的列表

+ 同步单个用户，或一组用户使用的包

+ 如果用户移到不同的 SQL Server，你可以获取用户的工作数据库的备份，并将其还原到新的服务器，并为用户的包将安装到文件系统在新服务器上，根据需要通过。

例如，你可能在这些情况下使用包同步：

+ DBA 到新计算机已恢复的 SQL Server 实例，并询问用户从其 R 客户端连接和运行`rxSyncPackages`来刷新和还原其包。

+ 你认为文件系统上的 R 包已损坏，因此，你运行`rxSyncPackages`SQL Server 上。

## <a name="requirements"></a>要求

您可以使用包同步之前，你必须具有 Microsoft R 的适当版本，并已启用相关的数据库功能。

### <a name="determine-whether-your-server-supports-package-management"></a>确定你的服务器是否支持包管理

此功能是 SQL Server 自 2017 年 1 CTP 2 中提供或更高版本。

由于此功能在 Microsoft R 版本 9.1.0 中使用 R 函数，您可以添加此功能的 SQL Server 2016 实例通过升级实例，以使用最新版本的 Microsoft。有关详细信息，请参阅[到升级 SQL Server R Services 使用 SqlBindR.exe](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)。

### <a name="enable-the-package-management-feature"></a>启用包管理功能

若要使用包同步需要 SQL Server 实例，以及用于运行 R 任务的单个数据库的情况下启用新的程序包管理功能。

1. 服务器管理员启用 SQL Server 实例的功能。
2. 对于每个数据库，管理员授予用户安装或共享的 R 程序包的功能。

完成此操作后，用户和他们安装的包有关的信息存储在 SQL Server 实例。 此信息然后可应用到文件系统中更新的 R 程序包。

每当添加新的包使用程序包管理功能时，更新 SQL Server 和文件系统中的这两个记录。

> [!NOTE]
> 如果你具有已安装 R 包的传统方法，使用 R 工具直接到文件系统中安装包，则无法使用包同步。
### <a name="permissions"></a>Permissions

+ 执行包同步函数的人员必须是安全主体对 SQL Server 实例和数据库的包。

+ 该函数的调用方必须是这些包管理角色之一的成员： **rpkgs 共享**或**rpkgs 私有**。

+ 若要同步包标记为**共享**，运行该函数的人员必须拥有成员身份**rpkgs 共享**角色和在移动的包必须已安装到共享作用域库。

+ 若要同步包标记为**私有**，管理员或包的所有者必须运行此函数中，和必须是私有的包。

+ 若要同步包代表其他用户，所有者必须是属于**db_owner**数据库角色。

## <a name="how-package-synchronization-works"></a>包同步的工作原理

若要使用包同步，调用[rxSyncPackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsyncpackages)，这是中的新函数[RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)。 您可以从 SQL Server 使用 sp_execute_external_script，调用此函数，或可以从远程 R 客户端上运行并指定 SQL Server 计算上下文。 

因为在数据库级别，每次调用管理程序包`rxSyncPackages`，必须指定 SQL Server 实例和数据库，并列出程序包，或指定包作用域。

1. 通过创建 SQL Server 计算上下文`RxInSqlServer`函数。 如果未指定计算上下文，则使用当前的计算上下文。

2. 提供在指定的计算上下文的实例上的数据库的名称。 每个数据库管理程序包。

3. 列出要同步的包。

4.  （可选） 使用*作用域*参数以指示是否在正在同步包为单个用户，或用户组。 如果运行该函数时未指定**私有**或**共享**作用域，包可用于所有作用域的整个集，用户将被复制。

如果命令能够执行成功，文件系统中的现有包添加到数据库，使用指定的作用域和所有者。 如果文件系统已损坏，包会还原基于数据库中维护的列表。

### <a name="example-1-synchronize-all-package-by-database"></a>示例 1： 通过数据库同步所有包

此示例将获取安装数据库 [TestDB] 中的所有包。 因为任何所有者不是特定的该列表包含已为专用和共享的作用域中安装的所有包。

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

下面的示例演示如何获取特定用户仅已安装的包。 SQL 登录名，在此示例中，标识该用户*user1*。

```R
rxSyncPackages(computeContext=computeContext, scope="private", owner = "user1", verbose=TRUE))
```

### <a name="example-4-restrict-synchronized-packages-by-owner"></a>示例 4。 限制由所有者同步的包

下面的示例将同步的数据库中托管的包列表的文件系统中安装的程序包。 如果缺少任何包，则它将安装在文件系统。

```R
# Instantiate the compute context
connectionString <- "Driver=SQL Server;Server=myServer;Database=TestDB;Trusted_Connection=True;"
computeContext <- RxInSqlServer(connectionString = connectionString )

# Synchronize the packages in the file system for all scopes and users
rxSyncPackages(computeContext=computeContext, verbose=TRUE)
```

## <a name="related-resources"></a>相关资源

[SQL Server 的 R 包管理](r-package-management-for-sql-server-r-services.md)
