---
title: "如何使用 RevoScaleR 函数来查找或安装 R 包在 SQL Server 上 |Microsoft 文档"
ms.custom: 
ms.date: 09/29/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: R
ms.assetid: 
caps.latest.revision: "1"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.openlocfilehash: 6d85c95a1aa0cba21c52142fa1a7599b208415ca
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/20/2017
---
# <a name="how-to-use-revoscaler-functions-to-find-or-install-r-packages-on-sql-server"></a>如何使用 RevoScaleR 函数来查找或在 SQL Server 上安装 R 包

Microsoft R Server 版本 9.0.1 引入了支持使用 SQL Server 计算上下文中安装包的新 RevoScaleR 函数。 这些新函数轻松数据科学家到服务器，而无需直接访问运行 R 代码 SQL Server。

每个数据科学家可以安装不会对其他可见的专用包。 由于包的范围可以为数据库，并且每个用户每个数据库中获取独立的包沙盒，很容易地安装不同版本的相同的 R 包。

如果您的工作数据库迁移到新服务器时，你可以使用包同步函数读取所有包的列表，并将其安装在新服务器上的数据库。

本文描述了这些函数，并提供的函数的用法示例。

## <a name="requirements"></a>要求

+ 若要执行这些函数，必须有权在实例上运行 R 命令。

+ 如果您不指定用户名和密码创建计算上下文时，使用运行的 R 代码的用户标识。

+ 使用这些函数从远程 R 客户端时，你必须创建计算上下文对象首先，使用 RxInSQLServer 函数。 此后，你使用的每个包管理函数，通过计算上下文作为自变量。

+ 可以运行包管理功能使用`sp_execute_external_script`。 执行此操作时，使用存储的过程调用方的安全上下文执行函数。

## <a name="list-of-package-management-functions"></a>包管理功能的列表

有关安装和删除指定的计算上下文中的程序包中 RevoScaleR，提供了以下包管理功能：

+ [rxInstalledPackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxinstalledpackages)： 查找有关指定的计算上下文中安装的程序包的信息。

+ [rxInstallPackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxinstallpackages)： 安装包复制到以下计算上下文，从指定的存储库，或通过读取本地保存的压缩包。

+ [rxRemovePackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxremovepackages)： 删除计算上下文从安装包。

+ [rxFindPackage](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxfindpackage)： 获取指定的计算上下文中的一个或多个包的路径。

+ [rxSyncPackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsyncpackages)： 在指定的计算上下文中复制的文件系统和数据库之间的包库。

+ [rxSqlLibPaths](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsqllibpaths): SQL Server 的内部执行时的搜索路径获取包的库树。

默认情况下，SQL Server 2017 中包括的这些包。 有关这些函数的信息，请参阅 RevoScaleR 函数参考页: (https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)

> [!NOTE]
> 用于程序包管理的 R 函数是与 Microsoft R Server 9.0.1 开始提供。 如果在 RevoScaleR，找不到函数，你可能需要升级到最新版本。 
## <a name="examples"></a>示例

本部分包含有关如何使用包管理功能与 SQL Server 实例或数据库的示例。 

+ 包安装功能检查依赖项并确保任何相关包可安装到 SQL Server，就像本地计算上下文中的 R 包安装一样。

+ 该函数的_卸载_包还计算依赖关系，并确保不再使用的 SQL Server 上的其他包的包将删除，以释放资源。

+ 用户和作用域的组合可用于查找程序包或将包添加到特定数据库：

    + 包**共享范围**属于的用户可以安装`rpkgs-shared`中指定的数据库角色。 此角色中的所有用户可以都卸载共享的包。
    + 包**专用作用域**可由属于任何用户安装`rpkgs-private`数据库中的角色。 但是，用户可以查看并卸载他们自己的软件包。
    + 数据库所有者可以使用共享或私有的包。

**从 R 代码**

如果您有权安装包，运行包之一从 R 客户端的管理功能，并指定要添加或删除的包将其中的计算上下文。  计算上下文可以是本地计算机或 SQL Server 实例上的数据库。 你的凭据确定是否可以在服务器上完成该操作。

**与 TRANSACT-SQL**

若要从存储过程中运行包管理功能，请将它们包装在调用`sp_execute_external_script`。

### <a name="get-list-of-packages-in-a-sql-server-compute-context"></a>获取 SQL Server 计算上下文中的包的列表

此示例检查该实例已安装的包`myServer`，在数据库中`TestDB`。 管理包适用于特定的数据库和用户。 如果用户未指定，则假定执行计算上下文，请调用的用户。 有关详细信息，请参阅[范围的角色的包](#bkmk_scope)。

```R
sqlServerCompute <- RxInSqlServer(connectionString = "Driver=SQL Server;Server=myServer;Database=TestDB;Uid=myID;Pwd=myPwd;");
sqlPackagePaths <- rxFindPackage(package = "RevoScaleR", computeContext = sqlServerCompute);
```

### <a name="get-package-path-on-a-remote-sql-server-compute-context"></a>获取包路径上的远程 SQL Server 计算上下文

此示例获取计算上下文 sqlServer 上，**RevoScaleR** 包的路径。

  ```R
  sqlPackagePaths <- rxFindPackage(package = "RevoScaleR", computeContext = sqlServerL)
  ```

### <a name="get-locations-for-multiple-packages"></a>获取多个包的位置

以下示例获取计算上下文 sqlServer 上，**RevoScaleR** 和 **lattice** 包的路径。 若要获取有关多个包的信息，请传递一个包含包名称的字符串向量。

  ```R
  packagePaths <- rxFindPackage(package = c("RevoScaleR", "lattice"), computeContext = sqlServer)
  ```


### <a name="get-package-versions-on-a-remote-compute-context"></a>获取远程计算上下文上的包版本

此命令从 R 控制台运行以获得内部版本号和版本号的计算上下文中上, 安装的软件包*sqlServer*。

  ```R
  sqlPackages <- rxInstalledPackages(fields = c("Package", "Version", "Built"), computeContext = sqlServer)
```

### <a name="install-a-package-on-sql-server"></a>在 SQL Server 上安装包

此示例安装**预测**包和到计算上下文中，其依赖项*sqlServer*。

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

### <a name="synchronize-packages-between-database-and-file-system"></a>同步之间的数据库和文件系统的包

下面的示例检查数据库**TestDB**，并确定是否所有程序包都安装在文件系统中。 如果缺少某些包，它们将安装文件系统中。

```R
# Instantiate the compute context
connectionString <- "Driver=SQL Server;Server=myServer;Database=TestDB;Trusted_Connection=True;"
computeContext <- RxInSqlServer(connectionString = connectionString )

# Synchronize the packages in the file system for all scopes and users
rxSyncPackages(computeContext=computeContext, verbose=TRUE)
```

包同步的工作原理每个数据库和每用户为基础。 有关详细信息，请参阅[for SQL Server 的 R 包同步](../r/package-install-uninstall-and-sync.md)。

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

`rxSqlLibPaths`函数可以用于确定 SQL Server 计算机学习 Services 使用的活动库。 此脚本可以返回仅为当前的服务器的库路径。 

```SQL
declare @instance_name nvarchar(100) = @@SERVERNAME, @database_name nvarchar(128) = db_name();
exec sp_execute_external_script 
  @language = N'R',
  @script = N'
    connStr <- paste("Driver=SQL Server;Server=", instance_name, ";Database=", database_name, ";Trusted_Connection=true;", sep="");
    .libPaths(rxSqlLibPaths(connStr));
    print(.libPaths());
  ', 
  @input_data_1 = N'', 
  @params = N'@instance_name nvarchar(100), @database_name nvarchar(128)',
  @instance_name = @instance_name, 
  @database_name = @database_name;
```
