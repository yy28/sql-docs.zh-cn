---
title: 如何使用 RevoScaleR 函数来查找或安装 R 包上 SQL Server |Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/31/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: e9009e26a891c031194697de78cac97db6844d58
ms.sourcegitcommit: b8e2e3e6e04368aac54100c403cc15fd4e4ec13a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2018
ms.locfileid: "45563973"
---
# <a name="how-to-use-revoscaler-functions-to-find-or-install-r-packages-on-sql-server"></a>如何使用 RevoScaleR 函数来查找或 SQL Server 上安装 R 包
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

RevoScaleR 9.0.1 和更高版本包括 SQL Server 计算上下文的 R 包管理函数。 远程，非管理员可以使用这些函数在 SQL Server 上安装包，而无需直接访问服务器。

SQL Server 2017 机器学习服务已包括 RevoScaleR 的较新版本。 SQL Server 2016 R Services 的客户必须执行[组件升级](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)获取 RevoScaleR 包管理功能。 有关说明如何检索包版本和内容，请参阅[获取包信息](determine-which-packages-are-installed-on-sql-server.md)。

## <a name="revoscaler-functions-for-package-management"></a>包管理的 RevoScaleR 函数

下表介绍用于 R 包安装和管理的函数。

| 函数 | Description |
|----------|-------------|
| [rxSqlLibPaths](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqllibpaths) | 确定远程 SQL 服务器上的实例库的路径。 |
| [rxFindPackage](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxfindpackage) | 获取远程的 SQL Server 上的一个或多个包的路径。 |
| [rxInstallPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstallpackages) | 从远程 R 客户端安装包的 SQL Server 计算上下文中调用此函数，从指定的存储库，或通过读取本地保存的压缩的包。 此函数依赖关系检查，并确保任何相关的包可安装到 SQL Server，就像在本地计算上下文中的 R 包安装一样。 若要使用此选项，您必须已启用的服务器和数据库上的包管理。 客户端和服务器环境必须具有相同版本的 RevoScaleR。 |
| [rxInstalledPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstalledpackages) | 获取指定的计算上下文中安装的包的列表。 |
| [rxSyncPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsyncpackages) | 复制包库之间的文件系统和数据库，为指定的计算上下文有关的信息。 |
| [rxRemovePackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxremovepackages) | 从指定的计算上下文中删除包。 它还计算依赖项，并确保不再由 SQL Server 上的其他包的包将删除，以释放资源。 |

## <a name="prerequisites"></a>必要條件

+ [启用 SQL Server 上的远程 R 包管理](r-package-how-to-enable-or-disable.md)

+ RevoScaleR 版本必须是客户端和服务器环境上相同。 有关详细信息，请参阅[获取包信息](determine-which-packages-are-installed-on-sql-server.md)。

+ 若要连接到服务器和数据库，以及运行 R 命令的权限。 必须是允许你指定的实例和数据库上安装包的数据库角色的成员。

+ 中的包**共享作用域**属于的用户可以安装`rpkgs-shared`中指定的数据库角色。 此角色中的所有用户可以都卸载共享的包。

+ 中的包**专用作用域**属于任何用户可以安装`rpkgs-private`在数据库中的角色。 但是，用户可以查看并卸载其自己的包。

+ 数据库所有者可以使用共享或专用包。

## <a name="client-connections"></a>客户端连接

可以是客户端工作站[Microsoft R Client](https://docs.microsoft.com/machine-learning-server/r-client/install-on-windows)或[Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install) （数据科学家经常使用的是免费的 developer edition） 在同一网络上。

当从远程 R 客户端调用的包管理功能，首先必须创建计算上下文对象，使用[RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver)函数。 此后，每个包管理功能的使用，作为参数传递的计算上下文。

设置计算上下文时，通常指定用户标识。 如果您不指定用户名和密码创建计算上下文时，则使用运行 R 代码的用户的标识。

1. 从 R 命令行，将实例和数据库中定义的连接字符串。
2. 使用[RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver)构造函数来定义 SQL Server 计算上下文，使用连接字符串。

    ```R
    sqlcc <- RxInSqlServer(connectionString = myConnString, shareDir = sqlShareDir, wait = sqlWait, consoleOutput = sqlConsoleOutput)
    ```
3. 创建你想要安装并将列表保存在一个字符串变量中的包的列表。

    ```R
    packageList <- c("e1071", "mice")
    ```

4. 调用[rxInstallPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstallpackages)并将计算上下文和包含包名称的字符串变量传递。

    ```R
    rxInstallPackages(pkgs = packageList, verbose = TRUE, computeContext = sqlcc)
    ```

    如果需要的依赖项包，它们还会安装，假定客户端上可用的 internet 连接。
    
    使用的凭据进行连接，该用户的默认作用域中的用户安装包。

## <a name="call-package-management-functions-in-stored-procedures"></a>在存储过程中调用的包管理功能

Cam 运行中的包管理功能`sp_execute_external_script`。 执行此操作时，会执行函数时使用的存储的过程调用方的安全上下文。

## <a name="examples"></a>示例

本部分提供有关如何连接到 SQL Server 实例或数据库作为计算上下文时使用这些函数从远程客户端的示例。

对于所有示例，必须提供连接字符串或计算上下文，需要一个连接字符串。 此示例提供了适用于 SQL Server 创建的计算上下文的一种方法：

```R
instance_name <- "computer-name/instance-name";
database_name <- "TestDB";
sqlWait= TRUE;
sqlConsoleOutput <- TRUE;
connString <- paste("Driver=SQL Server;Server=", instance_name, ";Database=", database_name, ";Trusted_Connection=true;", sep="");
sqlcc <- RxInSqlServer(connectionString = connString, wait = sqlWait, consoleOutput = sqlConsoleOutput, numTasks = 4);
```

具体取决于服务器所在的位置，和安全模型，您可能需要提供连接字符串中的域和子网规范或使用 SQL 登录名。 例如：

```R
connStr <- "Driver=SQL Server;Server=myserver.financeweb.contoso.com;Database=Finance;Uid=RUser1;Pwd=RUserPassword"
```

### <a name="get-package-path-on-a-remote-sql-server-compute-context"></a>获取包路径在远程 SQL Server 计算上下文

此示例将获取的路径**RevoScaleR**上计算上下文中，包`sqlcc`。

```R
sqlPackagePaths <- rxFindPackage(package = "RevoScaleR", computeContext = sqlcc)
print(sqlPackagePaths)
```

**结果**

"C: / Program 文件/Microsoft SQL Server/MSSQL14。MSSQLSERVER/R_SERVICES/库/RevoScaleR"

> [!TIP]
> 如果已经启用了查看 SQL 控制台输出选项，可能会从前面的函数收到状态消息`print`语句。 完成测试代码后，设置`consoleOutput`为 FALSE 计算上下文构造函数来消除的消息中。

### <a name="get-locations-for-multiple-packages"></a>获取多个包的位置

下面的示例获取的路径**RevoScaleR**并**点阵**包，在计算上下文， `sqlcc`。 若要获取多个包的信息，请将传递一个包含包名称的字符串向量。

```R
packagePaths <- rxFindPackage(package = c("RevoScaleR", "lattice"), computeContext = sqlcc)
print(packagePaths)
```

### <a name="get-package-versions-on-a-remote-compute-context"></a>在远程计算上下文中获取包的版本

运行此命令从 R 控制台中，若要获取计算上下文中，安装的包的内部版本号和版本号*sqlServer*。

```R
sqlPackages <- rxInstalledPackages(fields = c("Package", "Version", "Built"), computeContext = sqlServer)
```

**结果**

```text
[1] "C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER/R_SERVICES/library/RevoScaleR"

[2] "C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER/R_SERVICES/library/lattice"
```

### <a name="install-a-package-on-sql-server"></a>在 SQL Server 上安装包

此示例安装**预测**包及其依赖项到计算上下文。

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

### <a name="synchronize-packages-between-database-and-file-system"></a>同步数据库和文件系统之间的包

以下示例将检查数据库**TestDB**，并确定是否在文件系统中安装所有包。 如果丢失了某些包，它们安装在文件系统中。

```R
# Instantiate the compute context
connectionString <- "Driver=SQL Server;Server=myServer;Database=TestDB;Trusted_Connection=True;"
computeContext <- RxInSqlServer(connectionString = connectionString )

# Synchronize the packages in the file system for all scopes and users
rxSyncPackages(computeContext=computeContext, verbose=TRUE)
```

包同步的工作原理每个数据库和每个用户。 有关详细信息，请参阅[适用于 SQL Server 的 R 包同步](../r/package-install-uninstall-and-sync.md)。

### <a name="use-a-stored-procedure-to-list-packages-in-sql-server"></a>使用 SQL Server 中的存储的过程以列出的包

从 Management Studio 或另一个工具，它支持 T-SQL，若要获取的已安装的包列表的当前实例上运行此命令使用`rxInstalledPackages`存储过程中。

```SQL
EXEC sp_execute_external_script 
  @language=N'R', 
  @script=N'
    myPackages <- rxInstalledPackages();
    OutputDataSet <- as.data.frame(myPackages);
    '
```

`rxSqlLibPaths`函数可用于确定使用 SQL Server 机器学习服务的活动库。 此脚本可以返回仅为当前的服务器的库路径。 

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

## <a name="see-also"></a>另请参阅

+ [启用远程 R 包管理](r-package-how-to-enable-or-disable.md)
+ [同步 R 包](package-install-uninstall-and-sync.md)
+ [安装 R 包的提示](packages-installed-in-user-libraries.md)
+ [默认包](installing-and-managing-r-packages.md)