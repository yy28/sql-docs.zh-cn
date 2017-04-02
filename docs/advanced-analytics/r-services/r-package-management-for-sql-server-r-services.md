---
title: "SQL Server R Services 的 R 包管理 | Microsoft Docs"
ms.custom: ""
ms.date: "12/16/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "R"
ms.assetid: 98c14b05-750e-44f9-8531-1298bf51e8d2
caps.latest.revision: 7
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 7
---
# SQL Server R Services 的 R 包管理
为了更轻松地管理在 SQL Server 某实例上运行的 R 包，**RevoScaleR** 包现在包括支持 R 包的安装和管理的功能。 

此新功能支持若干方案：

- 无需对 SQL Server 计算机的管理访问权，数据科学家也可在 SQL Server 上安装所需的 R 包。 基于数据库安装包。
- 易于与他人共享包。 只需建立本地包存储库，并让每个数据科学家将包安装到各数据库。
- 数据库管理员不必了解如何运行 R 命令，或了解包的依赖项。 DBA 使用数据库角色控制允许哪些 SQL Server 用户安装、卸载或使用包。
 
**工作方式**

* 数据库管理员负责设置角色并将用户添加到角色，控制有权从 SQL Server 环境添加或删除 R 包的人员。
* 如果有权安装包，从 R 代码中运行一个包管理功能并指定要添加或删除包的计算上下文。 计算上下文可以是本地计算机或 SQL Server 实例上的数据库。 
* 如果在 SQL Server 上运行安装包的调用，凭据将确定是否可以在服务器上完成该操作。 
- 包安装功能检查依赖项并确保任何相关包可安装到 SQL Server，就像本地计算上下文中的 R 包安装一样。
- 卸载包的功能也会计算依赖项，并确保删除 SQL Server 上其他包不再使用的包以释放资源。
- 每位数据科学家都可以安装对他人不可见的专用包，为他们提供独立的沙盒处理自己的 R 包。
-  由于可将包的范围限制为数据库且每个用户会在每个数据库中获得独立包沙盒，因此更易于安装用法不同的相同 R 包版本。 

> [!NOTE]
> 当前，此功能仅发布供与 [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 一起使用。 

## <a name="database-roles-and-database-scoping"></a>数据库角色和数据库作用域

新的包管理功能提供在特定数据库上的 SQL Server 中包安装和使用的两个作用域：

- **共享作用域**

  “共享作用域”意味着取得共享作用域角色权限 (**rpkgs-shared**) 的用户可将包安装和卸载到指定数据库。 在共享作用域库中安装的包可由 SQL Server 上数据库的其他用户使用，前提是这些用户有权使用已安装的 R 包。 

- **专用作用域** 

  “专用作用域”意味着在专用作用域角色 (**rpkgs-private**) 中取得成员资格的用户可将包安装或卸载到根据用户定义的专用库位置。 因此，专用作用域中安装的任何包仅可由安装包的用户使用。 也就是说，SQL Server 上的用户无法使用其他用户安装的专用包。 

可合并这些“共享”和“专用”作用域模型，开发自定义安全系统，从而部署和管理 SQL Server 上的包。 

例如，通过使用共享作用域，可向一组数据科学家的领导或经理授予安装包的权限，随后相同 SQL Server 实例中的所有其他用户或数据科学家可使用这些包。 

其他方案可能会要求在用户之间进行更好地隔离或要求使用不同版本的包。 在此情况下，可使用专用作用域向数据科学家授予单独的权限，这些数据科学家将负责安装和使用其所需的包。 由于是基于用户安装的包，因此由某用户安装的包不会影响使用相同 SQL Server 数据库的其他用户的工作。 

### <a name="database-roles-for-package-management"></a>包管理的数据库角色

以下新的数据库角色支持 SQL R Services 的安全安装和包管理： 

- **rpkgs-users** 允许用户使用任何由 **rpkgs-shared** 角色成员安装的共享包。

- **rpkgs-private** 提供权限访问共享包，共享包的权限与 **rpkgs-users** 角色的权限相同。 此角色的成员还可以安装、删除和使用个人作用域包。

-  **rpkgs-shared** 提供与 **rpkgs-private** 角色相同的权限。 属于此角色成员的用户还可以安装或删除共享包。 
 
- **db_owner** - 与 **rpkgs-shared** 角色具有相同权限。 也可向用户授予安装或删除共享和专用包的权限。



## <a name="new-package-management-functions"></a>新的包管理功能


+ `rxInstalledPackages`：查找在指定的计算上下文中安装的包的相关信息。

+ `rxInstallPackages`：从指定存储库或通过读取本地保存的压缩包，将包安装到计算上下文。

+ `rxRemovePackages`：从计算上下文删除已安装的包。

+ `rxFindPackage`：获取指定计算上下文中一个或多个包的路径。

+ `rxSqlLibPaths`：在 SQL Server 中执行时获取包的库树的搜索路径。

## <a name="examples"></a>示例

### <a name="get-package-location-on-sql-server-compute-context"></a>获取 SQL Server 计算上下文上的包位置

此示例获取计算上下文 sqlServer 上，**RevoScaleR** 包的路径。

  ```R
  sqlPackagePaths <- rxFindPackage(package = "RevoScaleR", computeContext = sqlServerL)
  ```
  
  ### <a name="get-locations-for-multiple-packages"></a>获取多个包的位置

以下示例获取计算上下文 sqlServer 上，**RevoScaleR** 和 **lattice** 包的路径。 查找有关多个包的信息时，传递包含包名称的字符串向量。

  ```R
  packagePaths <- rxFindPackage(package = c("RevoScaleR", "lattice"), computeContext = sqlServer)
  ```



### <a name="list-packages-in-specified-compute-context"></a>列出指定计算上下文中的包

此示例列出并在控制台中显示计算上下文 sqlServer 中安装的所有包。

  ```R
  myPackages <- rxInstalledPackages(computeContext = sqlServer) 
  myPackages
  ```

### <a name="get-package-versions"></a>获取包的版本

此示例获取在计算上下文 sqlServer  中安装的包的内部版本号和版本号。

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

此示例将 **ggplot2** 包及其依赖项从计算上下文 *sqlServer* 删除。

  ```R
  pkgs <- c("ggplot2")
  rxRemovePackages(pkgs = pkgs, verbose = TRUE, scope = "private", computeContext = sqlServer)
  ```

## <a name="see-also"></a>另请参阅

[如何启用或禁用 R 包管理](../../advanced-analytics/r-services/how-to-enable-or-disable-r-package-management.md)