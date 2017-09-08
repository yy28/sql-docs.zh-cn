---
title: "SQL Server 的 R 包管理 |Microsoft 文档"
ms.custom: 
ms.date: 08/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- R
ms.assetid: 98c14b05-750e-44f9-8531-1298bf51e8d2
caps.latest.revision: 7
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f19982251b629d12215595685c0633b4c6b61c98
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="r-package-management-for-sql-server"></a>SQL Server 的 R 包管理

本主题介绍可用于管理 SQL server 的实例运行的 R 包的包管理功能。

**适用于：** SQL Server 2016 R Services、 SQL Server 自 2017 年 1 机器学习服务

## <a name="package-management-using-t-sql"></a>使用 T-SQL 的管理包

你可以继续以管理员身份的计算机上，安装 R 包，如果您具有这些权限，以及如果是使用机器学习作业的服务器的唯一人员。

但是，如果你需要包与他人共享，或如果多个用户需要在服务器上运行机器学习作业，会设置共享的包库更高效。 SQL Server 支持此功能通过数据库角色。

数据库管理员负责设置角色并将用户添加到角色。 通过角色，数据库管理员可以控制谁有权添加或删除从 SQL Server 环境中，R 包，并可以审核包安装。

### <a name="database-roles-for-package-management"></a>包管理的数据库角色

以下新的数据库角色在 SQL Server 中支持安全的安装和 R 包管理：

- `rpkgs-users`： 允许用户使用安装的成员的任何共享的包`rpkgs-shared`角色。

- `rpkgs-private`： 提供对共享的包的访问相同的权限`rpkgs-users`角色。 此角色的成员还可以安装、删除和使用个人作用域包。

-  `rpkgs-shared`： 提供相同的权限`rpkgs-private`角色。 属于此角色成员的用户还可以安装或删除共享包。

- `db_owner`： 具有相同的权限`rpkgs-shared`角色。 也可向用户授予安装或删除共享和专用包的权限。

### <a name="creating-an-external-package-library-using-t-sql"></a>创建使用 T-SQL 的外部包库

此外，SQL Server 2017 支持 T-SQL 语句，**创建外部库**，以支持由数据库管理员管理的外部库。 当前此语句可用于为。 其他支持计划在将来的 Python 包和为执行编写在其他平台，如 Linux 上的包中创建基于 Windows 的库。

有关详细信息，请参阅[创建外部库](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql)。

## <a name="package-management-using-r"></a>使用 R 包管理

**RevoScaleR**包现在包括函数来支持更轻松安装和管理的 R 包。 这些新函数中，与用于程序包管理的数据库角色相结合支持这些方案：

- 无 SQL Server 计算机的管理访问权限，数据科研人员可以在 SQL Server 上安装所需的 R 程序包。
- 包已安装基于每个数据库，并且当移动数据库时，包将随之移动。
- 很容易地与他人共享包。 如果你设置本地包存储库时，每个数据科研人员可以使用存储库以将包安装到他或她自己的数据库。
- 数据库管理员不需要了解如何运行 R 命令，并且不需要跟踪复杂的包的依赖项。
- DBA 可以使用熟悉的数据库角色控制允许哪些 SQL Server 的用户安装、 卸载或使用包。

### <a name="r-package-management-functions"></a>R 包管理功能

有关安装和删除指定的计算上下文中的程序包中 RevoScaleR，提供了以下包管理功能：

+ [rxInstalledPackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxinstalledpackages)： 查找有关指定的计算上下文中安装的程序包的信息。

+ [rxInstallPackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxinstallpackages)： 安装包复制到以下计算上下文，从指定的存储库，或通过读取本地保存的压缩包。

+ [rxRemovePackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxremovepackages)： 删除计算上下文从安装包。

+ [rxFindPackage](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxfindpackage)： 获取指定的计算上下文中的一个或多个包的路径。

+ [rxSyncPackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsyncpackages)： 在指定的计算上下文中复制的文件系统和数据库之间的包库。

+ [rxSqlLibPaths](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsqllibpaths): SQL Server 的内部执行时的搜索路径获取包的库树。

默认情况下，在 SQL Server 2017 也包括这些包。 可以将包添加到 SQL Server 2016 的实例中，如果升级实例，以使用至少 Microsoft R 9.0.1。 有关详细信息，请参阅[使用 SqlBindR.exe 升级 R](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)。

有关这些函数的信息，请参阅 RevoScaleR 函数参考页: (https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)

## <a name="how-package-management-works"></a>包管理的工作原理

如果有权安装包，从 R 代码中运行一个包管理功能并指定要添加或删除包的计算上下文。 计算上下文可以是本地计算机或 SQL Server 实例上的数据库。 如果在 SQL Server 上运行安装包的调用，凭据将确定是否可以在服务器上完成该操作。 包安装功能检查依赖项并确保任何相关包可安装到 SQL Server，就像本地计算上下文中的 R 包安装一样。 卸载包的功能也会计算依赖项，并确保删除 SQL Server 上其他包不再使用的包以释放资源。

每个数据科学家可以安装不会向其他人，显示的专用包创建专用沙盒获取 R 包。 由于包的范围可以为数据库，并且每个用户每个数据库中获取独立的包沙盒，很容易地安装不同版本的相同的 R 包。

如果您的工作数据库迁移到新服务器时，你可以使用包同步函数读取所有包的列表，并将其安装在新服务器上的数据库。

> [!NOTE]
> 
> 从 Microsoft R Server 9.0.1 开始提供了用于程序包管理的 R 函数。 如果在 RevoScaleR，找不到函数，你可能需要升级到最新版本。

### <a name="bkmk_scope"></a>通过角色的包作用域

新的包管理功能提供在特定数据库上的 SQL Server 中包安装和使用的两个作用域：

- **共享作用域**

  *共享范围*意味着该用户已分配给共享作用域角色的权限 (`rpkgs-shared`) 可以安装和卸载程序包添加到指定的数据库。 在共享作用域库中安装的包可由 SQL Server 上数据库的其他用户使用，前提是这些用户有权使用已安装的 R 包。

- **专用作用域**

  *专用作用域*意味着该用户已被授予在专用的作用域角色的成员身份 (`rpkgs-private`) 可以安装或卸载到每个用户定义的专用库位置的包。 因此，专用作用域中安装的任何包仅可由安装包的用户使用。 也就是说，SQL Server 上的用户无法使用其他用户安装的专用包。

可合并这些“共享”和“专用”作用域模型，开发自定义安全系统，从而部署和管理 SQL Server 上的包。

例如，通过使用共享作用域，可向一组数据科学家的领导或经理授予安装包的权限，随后相同 SQL Server 实例中的所有其他用户或数据科学家可使用这些包。

其他方案可能会要求在用户之间进行更好地隔离或要求使用不同版本的包。 在此情况下，可使用专用作用域向数据科学家授予单独的权限，这些数据科学家将负责安装和使用其所需的包。 由于是基于用户安装的包，因此由某用户安装的包不会影响使用相同 SQL Server 数据库的其他用户的工作。

### <a name="synchronizing-r-package-libraries"></a>同步的 R 包库

CTP 2.0 版本的 SQL Server 2017 （和 Microsoft R Server 自 2017 年 4 月发行） 包含新的 R 函数*同步包*。

包同步是指数据库引擎跟踪由特定的所有者和组，并可以将这些包写入到文件系统，如果所需的包。 在这些情况下，你可以使用包同步：

+ 你想要移动的 SQL Server 实例之间的 R 包
+ 你需要重新安装包针对的特定用户或组后还原数据库

有关详细信息，请参阅[rxSyncPackages](../r/package-install-uninstall-and-sync.md)。

## <a name="examples"></a>示例

这些示例演示包管理功能的基本使用情况。 若要执行这些命令需要有权在实例上运行 R 命令。

+ 当从终端远程 R 运行时，创建一个指定的 SQL Server 实例的计算上下文对象，然后运行函数、 函数作为自变量传递的计算上下文。

+ 若要从存储过程中运行包管理功能，你必须将它们包装在调用`sp_execute_external_script`。

### <a name="package-scoping"></a>包作用域

此示例检查该实例已安装的包`myServer`，在数据库中`TestDB`。 管理包适用于特定的数据库和用户。 如果用户未指定，则假定执行计算上下文，请调用的用户。 有关详细信息，请参阅[范围的角色的包](#bkmk_scope)。

```R
sqlServerCompute <- RxInSqlServer(connectionString = "Driver=SQL Server;Server=myServer;Database=TestDB;Uid=myID;Pwd=myPwd;");
sqlPackagePaths <- rxFindPackage(package = "RevoScaleR", computeContext = sqlServerCompute);
```

### <a name="get-package-location-on-a-remote-sql-server-compute-context"></a>获取在远程 SQL Server 计算上下文上的包位置

此示例获取计算上下文 sqlServer 上，**RevoScaleR** 包的路径。

  ```R
  sqlPackagePaths <- rxFindPackage(package = "RevoScaleR", computeContext = sqlServerL)
  ```

### <a name="get-locations-for-multiple-packages"></a>获取多个包的位置

以下示例获取计算上下文 sqlServer 上，**RevoScaleR** 和 **lattice** 包的路径。 若要获取有关多个包的信息，请传递一个包含包名称的字符串向量。

  ```R
  packagePaths <- rxFindPackage(package = c("RevoScaleR", "lattice"), computeContext = sqlServer)
  ```

### <a name="use-a-stored-procedure-to-list-packages-in-sql-server"></a>使用 SQL Server 中的存储的过程以列出程序包

从 Management Studio 或支持 T-SQL，以获取当前实例上已安装的包列表的其他工具运行此命令使用`rxInstalledPackages`在存储过程。

```SQL
EXEC sp_execute_external_script 
  @language=N'R', 
  @script=N'
    myPackages <- rxInstalledPackages();
    OutputDataSet <- as.data.frame(myPackages);
    '
```

### <a name="get-package-versions-on-a-remote-compute-context"></a>获取远程计算上下文上的包版本

此命令从 R 控制台运行以获得内部版本号和版本号的计算上下文中上, 安装的软件包*sqlServer*。

  ```R
  sqlPackages <- rxInstalledPackages(fields = c("Package", "Version", "Built"), computeContext = sqlServer)
```

### <a name="install-a-package-on-sql-server"></a>在 SQL Server 上安装包

此示例将 **ggplot2** 包及其依赖项安装到计算上下文 *sqlServer*。

  ```R
  pkgs <- c("ggplot2")
  rxInstallPackages(pkgs = pkgs, verbose = TRUE, scope = "private", computeContext = sqlServer)
  ```

### <a name="remove-a-package-from-sql-server"></a>从 SQL Server 删除包

此示例将 **ggplot2** 包及其依赖项从计算上下文 *sqlServer*删除。

  ```R
  pkgs <- c("ggplot2")
  rxRemovePackages(pkgs = pkgs, verbose = TRUE, scope = "private", computeContext = sqlServer)
  ```

### <a name="package-synchronization"></a>包同步

下面的示例将同步的数据库中托管的包列表的文件系统中安装的程序包。 如果缺少某些包，它们将安装文件系统中。

```R
# Instantiate the compute context
connectionString <- "Driver=SQL Server;Server=myServer;Database=TestDB;Trusted_Connection=True;"
computeContext <- RxInSqlServer(connectionString = connectionString )

# Synchronize the packages in the file system for all scopes and users
rxSyncPackages(computeContext=computeContext, verbose=TRUE)
```

## <a name="next-steps"></a>后续步骤

[如何启用或禁用 R 包管理](../r/r-package-how-to-enable-or-disable.md)

