---
title: 如何使用 RevoScaleR 函数来查找或安装 R 包在 SQL Server 上 |Microsoft 文档
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: c872a945388696a75a07116c0a84a64d64d668d4
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="how-to-use-revoscaler-functions-to-find-or-install-r-packages-on-sql-server"></a>如何使用 RevoScaleR 函数来查找或在 SQL Server 上安装 R 包
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Microsoft R Server 版本 9.0.1 引入了支持使用 SQL Server 计算上下文中安装包的新 RevoScaleR 函数。 这些新函数轻松数据科学家运行 R 代码，并在 SQL Server 上安装包，而直接访问服务器。

## <a name="how-does-it-work"></a>它是如何工作的

如果你有 R Server 9.0.1 或更高版本，你可以使用[rxInstallPackages](https://docs.microsoft.com/en-us/machine-learning-server/r-reference/revoscaler/rxinstallpackages)从远程 R 客户端安装包在 SQL Server 计算上下文中的函数。 若要使用此选项，你必须具有启用服务器和数据库上的包管理。 此功能还需要在服务器上安装的 R Services 或机器学习服务为相应的版本。

RevoScaleR 的新版本还包括这些函数： 

+ [RxFindPackage](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxfindpackage)函数获取指定的计算上下文中的一个或多个包的路径。

    用户和作用域的组合可用于查找程序包或将包添加到特定数据库：

+ [RxInstalledPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstalledpackages)函数获取指定的计算上下文中安装的程序包的列表。

+ [RxInstallPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstallpackages)函数将包安装到计算上下文，从指定的存储库，或通过读取本地保存的压缩包。

    此函数为依赖关系检查，并确保任何相关的程序包，可以就像在本地计算上下文中的 R 包安装到 SQL Server 进行安装。

+ [RxRemovePackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxremovepackages)函数从指定的计算上下文中删除包。

    它还计算依赖关系，并确保不再使用的 SQL Server 上的其他包的包将删除，以释放资源。

+ 使用[rxSyncPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsyncpackages)函数要复制的文件系统和数据库，为指定的计算上下文之间的包库有关的信息。

+ 使用[rxSqlLibPaths](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqllibpaths)函数来确定 SQL 服务器上的实例库路径计算上下文。

**适用于：** [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]。 中也受支持[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)][!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)]与升级到 R Server 9.0 或更高版本。 其他限制条件。

## <a name="requirements"></a>需求

+ 若要执行这些函数，必须具有权限，以连接到服务器和数据库，以及运行 R 命令。

+ 使用这些函数从远程 R 客户端时，你必须创建计算上下文对象首先，使用[RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver)函数。 此后，你使用的每个包管理函数，通过计算上下文作为自变量。

+ 如果您不指定用户名和密码创建计算上下文时，使用运行的 R 代码的用户标识。

+ 还有可能运行包内的管理功能`sp_execute_external_script`。 执行此操作时，使用存储的过程调用方的安全上下文执行函数。

+ 包**共享范围**属于的用户可以安装`rpkgs-shared`中指定的数据库角色。 此角色中的所有用户可以都卸载共享的包。

+ 包**专用作用域**可由属于任何用户安装`rpkgs-private`数据库中的角色。 但是，用户可以查看并卸载他们自己的软件包。

+ 数据库所有者可以使用共享或私有的包。

## <a name="package-installation-from-machine-learning-server-or-remote-r-client"></a>从机器学习服务器或远程 R 客户端的包安装

在开始之前，确保满足这些条件：

+ 客户端具有 RevoScale 9.0.1 或更高版本。
+ SQL Server 实例上已安装的 RevoScaleR 为相应的版本。
+ [包管理功能](..\r\r-package-how-to-enable-or-disable.md)实例上已启用。
+ 现在允许你指定的实例和数据库上安装包的数据库角色的成员。 在将来，角色将支持为安装包的共享或专用位置。 现在，你可以安装包，如果你是数据库的所有者。

1. 从 R 的命令行，实例和数据库中定义的连接字符串。
2. 使用[RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver)构造函数定义 SQL Server 计算上下文，使用连接字符串。

    ```R
    sqlcc <- RxInSqlServer(connectionString = myConnString, shareDir = sqlShareDir, wait = sqlWait, consoleOutput = sqlConsoleOutput)
    ```
3. 创建你想要安装并将该列表保存在一个字符串变量中的包的列表。

    ```R
    packageList <- c("e1071", "mice")
    ```

4. 调用[rxInstallPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstallpackages)并传递计算上下文和包含包名称的字符串变量。

    ```R
    rxInstallPackages(pkgs = packageList, verbose = TRUE, computeContext = sqlcc)
    ```

    如果从属包是必需的它们会同时安装，假设 internet 连接在客户端上可用。
    
    未安装程序包，使用该用户的默认作用域中建立的连接，用户的凭据。

## <a name="examples"></a>示例

本部分提供有关如何连接到 SQL Server 实例或数据库作为计算上下文时使用这些函数从远程客户端的示例。

对于所有示例中，你必须提供连接字符串或计算上下文，这需要连接字符串。 本示例提供了一种方法要创建 SQL Server 计算上下文：

```R
instance_name <- "Machine name/Instance name";
database_name <- "TestDB";
sqlWait= TRUE;
sqlConsoleOutput <- TRUE;
connString <- paste("Driver=SQL Server;Server=", instance_name, ";Database=", database_name, ";Trusted_Connection=true;", sep="");
sqlcc <- RxInSqlServer(connectionString = connString, wait = sqlWait, consoleOutput = sqlConsoleOutput, numTasks = 4);
```

根据服务器所在的位置，和的安全模型，你可能需要提供的连接字符串中的域和子网规范或使用 SQL 登录名。 例如：

```R
connStr <- "Driver=SQL Server;Server=myserver.financeweb.contoso.com;Database=Finance;Uid=RUser1;Pwd=RUserPassword"


### Get package path on a remote SQL Server compute context

This example gets the path for the **RevoScaleR** package on the compute context, `sqlcc`.

```R
sqlPackagePaths <- rxFindPackage(package = "RevoScaleR", computeContext = sqlcc)
print(sqlPackagePaths)
```

**结果**

"C: / Program 文件/Microsoft SQL Server/MSSQL14。MSSQLSERVER/R_SERVICES/库/RevoScaleR"

> [!TIP]
> 如果已启用的选项，以查看 SQL 控制台输出，你可能从之前的函数收到状态消息`print`语句。 完成测试你的代码后，设置`consoleOutput`为 FALSE 计算上下文构造函数来消除消息中。

### <a name="get-locations-for-multiple-packages"></a>获取多个包的位置

下面的示例获取的路径**RevoScaleR**和**格状**上计算上下文中，包`sqlcc`。 若要获取有关多个包的信息，请传递一个包含包名称的字符串向量。

```R
packagePaths <- rxFindPackage(package = c("RevoScaleR", "lattice"), computeContext = sqlcc)
print(packagePaths)
```

### <a name="get-package-versions-on-a-remote-compute-context"></a>获取远程计算上下文上的包版本

此命令从 R 控制台运行以获得内部版本号和版本号的计算上下文中上, 安装的软件包*sqlServer*。

```R
sqlPackages <- rxInstalledPackages(fields = c("Package", "Version", "Built"), computeContext = sqlServer)
```

**结果**

```text
[1] "C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER/R_SERVICES/library/RevoScaleR"

[2] "C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER/R_SERVICES/library/lattice"
```

### <a name="install-a-package-on-sql-server"></a>在 SQL Server 上安装包

此示例安装**预测**包和其依赖项到计算上下文。

  ```R
  pkgs <- c("forecast")
  rxInstallPackages(pkgs = pkgs, verbose = TRUE, scope = "private", computeContext = sqlcc)
  ```

### <a name="remove-a-package-from-sql-server"></a>从 SQL Server 删除包

此示例将删除**预测**包和计算上下文从其依赖项。

  ```R
  pkgs <- c("forecast")
  rxRemovePackages(pkgs = pkgs, verbose = TRUE, scope = "private", computeContext = sqlcc)
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

