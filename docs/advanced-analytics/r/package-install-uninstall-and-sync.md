---
title: "包安装、 卸载和同步 |Microsoft 文档"
ms.custom: 
ms.date: 04/12/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 959282395d178a090a3d447769ced4dca8882f89
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---

# <a name="r-package-synchronization-for-sql-server"></a>SQL Server 的 R 包同步

SQL Server 自 2017 年 1 CTP 2.0 包括新的函数的 R 包，可用于支持备份和还原的 SQL Server 数据库与关联的 R 包集合进行同步。 此功能有助于确保复杂套所创建的用户的 R 包不会丢失，并可以轻松地还原。  

本主题介绍程序包同步功能的用途，以及如何使用`rxSyncPackages()`函数来执行以下任务：

+  同步整个 SQL Server 数据库的包的列表
+  单个用户，或一组用户使用的同步包

> [!NOTE]
> 此函数作为预发行版软件的一部分提供，并可能需要在最终版本之前的更改。

## <a name="what-is-package-synchronization"></a>包同步是什么 

包同步是一项新功能专门用于 SQL Server 计算上下文。 它旨在以获取对特定的数据库，为特定用户或组，安装的 R 包的列表，并确保包在排在文件系统匹配那些在数据库中。 

这是你需要移动用户数据库和移动的数据库的包的情况下很有用。 备份和还原使用 R 作业的 SQL Server 数据库时，你还可以使用包同步。

包同步使用的新函数， `rxSyncPackages()`。 若要同步的包列表，打开了 R 命令提示符下，传递定义实例和你想要使用的数据库的计算上下文，然后提供的包作用域或用户或所有者名称。 

### <a name="how-packages-are-managed-in-r-and-sql-server"></a>如何在 R 和 SQL Server 管理包的

通常情况下，在运行 R 脚本使用标准 R 工具时，文件系统上安装 R 包。 如果多个人员在同一台计算机上使用 R，则表明可能存在的相同的包，在不同的文件夹或其他用户库中的多个副本。

但是，若要使用从 SQL Server 的 R 包，包必须安装在实例相关联的默认 R 库中。 服务器计算机可能承载多个实例的 SQL Server 的 R 启用，并且在这种情况下，每个实例可以一组单独的 R 包。 

数据库管理员负责在实例上安装包。 但是，与包管理库中，管理员可以此责任委派给用户。 

+ 对于每个数据库，管理员可以使用户能够自由地安装所需的 R 包。 此机制可确保，多个用户可以安装不同版本的 R 包，而不会导致 SQL Server 计算机的其他用户的冲突。 单个用户可以安装其自己使用的包使用标记为的文件系统位置**私有**，如果它们属于的数据库角色**rpkgs 私有**。

+ 管理员可以设置的上一个数据库，程序包用户组，并安装共享的所有用户组中的包。 包可以在数据库角色的成员间共享**rpkgs 共享**。 此类用户还可以安装到专用作用域的位置的包。 

### <a name="goal-of-package-synchronization"></a>包同步的目标

如果服务器上的数据库都将丢失，或必须移动，通过使用包同步，你可以将特定的包集中还原到数据库、 用户或组。 

有关用户和他们安装的包的信息存储在 SQL Server 实例中，并使用文件系统中更新的程序包。 每当添加新的包使用程序包管理功能时，更新 SQL Server 和文件系统中的这两个记录。 因此，如果用户移到不同的 SQL Server，你可以获取的用户的工作数据库备份并将其还原到新的服务器，并且用户的包将安装到文件系统在新服务器上，根据需要通过。


### <a name="supported-versions"></a>支持的版本

SQL Server 自 2017 年 1 CTP 2.0 中包含此函数。

因为此函数是 Microsoft R 版本 9.1.0 的一部分，你可以添加此功能的 SQL Server 2016 的实例通过升级要使用的 Microsoft 键。 最新版本的实例有关详细信息，请参阅[到升级 SQL Server R Services 使用 SqlBindR.exe](../r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)。

## <a name="to-synchronize-packages"></a>若要同步包

你调用`rxSyncPackages`后将 SQL Server 的实例还原到新计算机，或如果文件系统上的 R 包被认为可能已损坏。

如果命令能够执行成功，文件系统中的现有包添加到数据库、 范围和指定的所有者。 如果文件系统被损坏，包是 restred 基于数据库中维护的列表。

### <a name="syntax"></a>语法
`rxSyncPackages(computeContext = rxGetOption("computeContext"),  scope = c("shared", "private"), owner = c(), verbose = getOption("verbose"))`

+ 计算上下文

    定义 SQL Server 计算上下文，组成实例和数据库，并要同步的包。通过创建 SQ 服务器上下文`RxInSqlServer`函数。 如果未指定计算上下文，则使用当前的计算上下文。 

+ 范围

  指示您安装为单个用户，或用户组的包： 

    + **私有**操作将包括只指定所有者安装用于这些包。
    + **共享**oepration 将包括为一组用户安装的所有包。 

  如果运行该函数时未指定私有或共享的作用域，将应用两个作用域。 因此，将复制整个包可用于所有作用域和用户集。

+ 所有者 

    指定要同步的包的所有者。 所有者名称必须是有效的 SQL 数据库用户。 如果你保留为空，则使用的连接中指定的 SQL 登录用户名称。


### <a name="requirements"></a>要求

+ 执行函数的人员必须是对 SQL Server 实例和数据库的包，并且必须可包管理角色的成员的安全主体： **rpkgs 共享**或**rpkgs 私有** 
  + 若要同步包标记为**共享**，运行该函数的人员必须拥有成员身份**rpkgs 共享**角色和在移动的包必须已安装到共享作用域库。
  + 小心地同步包标记为**私有**，管理员或包的所有者必须运行此函数中，和必须是私有的包。
+ **rpkgs 用户**-此角色的成员可以运行的代码，使用 SQL Server 实例上安装的包，但无法安装或同步包。
+ 若要同步包代表其他用户，所有者必须是属于**db_owner**数据库角色。

## <a name="examples"></a>示例

下面的示例创建与 SQL Server 的特定实例的连接，指定一个数据库，，然后指定一组要同步的包。 

当调用`rxSyncPackages`进行，列表将文件系统和数据库之间同步的包。 

### <a name="synchronize-all-by-database"></a>所有通过数据库同步

此示例将获取安装数据库 [TestDB] 中的所有包。 因为任何所有者不是特定的该列表包含已为专用和共享的作用域中安装的所有包。

```R
connectionString <- "Driver=SQL Server;Server=myServer;Database=TestDB;Trusted_Connection=True;"
computeContext <- RxInSqlServer(connectionString = connectionString )

rxSyncPackages(computeContext=computeContext, verbose=TRUE)
```

### <a name="restrict-synchronized-packages-by-scope"></a>限制作用域的同步的的包 

下面的示例同步共享的作用域或专用作用域中的包。

**共享作用域**

```R
rxSyncPackages(computeContext=computeContext, scope="shared", verbose=TRUE)
```

**专用作用域**

```R
rxSyncPackages(computeContext=computeContext, scope="private", verbose=TRUE)
```

### <a name="restrict-synchronized-packages-by-owner"></a>限制由所有者同步的包 

下面的示例演示如何获取特定用户仅已安装的包。 SQL 登录名，在此示例中，标识该用户*user1*。

```R
rxSyncPackages(computeContext=computeContext, scope="private", owner = "user1", verbose=TRUE))
```

## <a name="see-also"></a>另请参阅

[SQL Server 的 R 包管理](../r/r-package-management-for-sql-server-r-services.md)
