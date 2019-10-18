---
title: 通过 sqlmlutils 安装新的 R 包
description: 了解如何使用 sqlmlutils 将新的 R 包安装到 SQL Server 机器学习服务或 SQL Server R Services 的实例。
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/15/2019
ms.topic: conceptual
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: f8ce5c7bcf12a2431c2de779912d2e309c628cb1
ms.sourcegitcommit: 8cb26b7dd40280a7403d46ee59a4e57be55ab462
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/17/2019
ms.locfileid: "72542143"
---
# <a name="install-new-r-packages-with-sqlmlutils"></a>通过 sqlmlutils 安装新的 R 包

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本文介绍如何使用[**sqlmlutils**](https://github.com/Microsoft/sqlmlutils)包中的函数将新的 R 包安装到 SQL Server 机器学习服务或 SQL Server R Services 的实例。 安装的包可用于在使用[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) t-sql 语句的数据库中运行的 R 脚本。

> [!NOTE]
> 不建议在 SQL Server 上添加 R 包的标准 R `install.packages` 命令。 请改用本文中所述的**sqlmlutils** 。

## <a name="prerequisites"></a>必备条件

- 在用于连接 SQL Server 的客户端计算机上安装[R](https://www.r-project.org)和[RStudio Desktop](https://www.rstudio.com/products/rstudio/download/) 。 你可以使用任何 R IDE 来运行脚本，但本文假设 RStudio。

- 在用于连接到 SQL Server 的客户端计算机上安装[Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/what-is)或[SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms) （SSMS）。 您可以使用其他数据库管理或查询工具，但本文假定 Azure Data Studio 或 SSMS。

### <a name="other-considerations"></a>其他注意事项

- 在 SQL Server 中运行的 R 脚本只能使用在默认实例库中安装的包。 SQL Server 无法从外部库加载包，即使该库位于同一台计算机上也是如此。 这包括与其他 Microsoft 产品一起安装的 R 库。

- 在强化的 SQL Server 环境中，你可能需要避免以下情况：
  - 需要网络访问的包
  - 需要提升文件系统访问权限的包
  - 用于 web 开发或其他任务的包，这些包不能通过在 SQL Server 内部运行

## <a name="install-sqlmlutils-on-the-client-computer"></a>在客户端计算机上安装 sqlmlutils

若要使用**sqlmlutils**，首先需要将其安装在用于连接 SQL Server 的客户端计算机上。

**Sqlmlutils**包依赖于**RODBCext**包，而**RODBCext**依赖于许多其他包。 以下过程按正确的顺序安装所有这些包。

### <a name="install-sqlmlutils-online"></a>联机安装 sqlmlutils

如果客户端计算机具有 Internet 访问权限，你可以在线下载并安装**sqlmlutils**及其依赖的程序包。

1. 从 https://github.com/Microsoft/sqlmlutils/tree/master/R/dist 下载最新的**sqlmlutils** zip 文件到客户端计算机。 请勿解压缩文件。

1. 打开**命令提示符**并运行以下命令以安装包**sqlmlutils**和**RODBCext**。 替换下载的**sqlmlutils** zip 文件的完整路径（此示例假定文件位于 "文档" 文件夹中）。 **RODBCext**包可联机查找并安装。

   ```console
   R -e "install.packages('RODBCext', repos='https://cran.microsoft.com')"
   R CMD INSTALL %UserProfile%\Documents\sqlmlutils_0.7.1.zip
   ```

### <a name="install-sqlmlutils-offline"></a>脱机安装 sqlmlutils

如果客户端计算机没有 Internet 连接，则需要使用能够访问 Internet 的计算机预先下载包**sqlmlutils**和**RODBCext** 。 然后，你可以将这些文件复制到客户端计算机上的一个文件夹中，并将包脱机安装。

**RODBCext**包包含许多依赖包，并且标识包的所有依赖项都非常复杂。 建议使用[**miniCRAN**](https://andrie.github.io/miniCRAN/)为包含所有相关包的包创建一个本地存储库文件夹。
有关详细信息，请参阅[使用 MiniCRAN 创建本地 R 包存储库](create-a-local-package-repository-using-minicran.md)。

**Sqlmlutils**包包含一个 zip 文件，你可以将该文件复制到客户端计算机并安装。

在具有 Internet 访问权限的计算机上：

1. 安装**miniCRAN**。 有关详细信息，请参阅[安装 miniCRAN](create-a-local-package-repository-using-minicran.md#install-minicran) 。

1. 在 RStudio 中，运行以下 R 脚本来创建包**RODBCext**的本地存储库。 此示例在 `c:\downloads\rodbcext` 的文件夹中创建存储库。

   ::: moniker range=">=sql-server-2016||=sqlallproducts-allversions"

   ```R
   CRAN_mirror <- c(CRAN = "https://cran.microsoft.com")
   local_repo <- "c:/downloads/rodbcext"
   pkgs_needed <- "RODBCext"
   pkgs_expanded <- pkgDep(pkgs_needed, repos = CRAN_mirror);

   makeRepo(pkgs_expanded, path = local_repo, repos = CRAN_mirror, type = "win.binary", Rversion = "3.5");
   ```

   ::: moniker-end

   ::: moniker range=">=sql-server-linux-ver15||=sqlallproducts-allversions"

   ```R
   CRAN_mirror <- c(CRAN = "https://cran.microsoft.com")
   local_repo <- "c:/downloads/rodbcext"
   pkgs_needed <- "RODBCext"
   pkgs_expanded <- pkgDep(pkgs_needed, repos = CRAN_mirror);

   makeRepo(pkgs_expanded, path = local_repo, repos = CRAN_mirror, type = "source", Rversion = "3.5");
   ```

   ::: moniker-end

   对于 `Rversion` 值，请使用安装在 SQL Server 上的 R 版本。 若要验证已安装的版本，请使用以下 T-sql 命令。

   ```sql
   EXECUTE sp_execute_external_script @language = N'R'
    , @script = N'print(R.version)'
   ```

1. 从 https://github.com/Microsoft/sqlmlutils/tree/master/R/dist 下载最新的**sqlmlutils** zip 文件（不要解压缩文件）。 例如，将文件下载到 `c:\downloads\sqlmlutils_0.7.1.zip`。

1. 将整个**RODBCext**存储库文件夹（`c:\downloads\rodbcext`）和**sqlmlutils** zip 文件（`c:\downloads\sqlmlutils_0.7.1.zip`）复制到客户端计算机。 例如，将它们复制到客户端计算机上 `c:\temp\packages` 的文件夹中。

在用于连接到 SQL Server 的客户端计算机上，打开命令提示符并运行以下命令，安装**RODBCext** ，然后**sqlmlutils**。

```console
R -e "install.packages('RODBCext', repos='c:\temp\packages\rodbcext')"
R CMD INSTALL c:\temp\packages\sqlmlutils_0.7.1.zip
```

## <a name="add-an-r-package-on-sql-server"></a>SQL Server 上添加 R 包

在下面的示例中，您将把[**胶水**](https://cran.r-project.org/web/packages/glue/)包添加到 SQL Server。

### <a name="add-the-package-online"></a>联机添加包

如果用于连接到 SQL Server 的客户端计算机具有 Internet 访问权限，则可以使用**sqlmlutils**通过 internet 查找**胶水**包和任何依赖项，然后远程安装包到 SQL Server 实例。

1. 在客户端计算机上，打开 "RStudio" 并创建一个新的**R 脚本**文件。

1. 使用以下 R 脚本通过**sqlmlutils**安装**粘合**包。 替换你自己的 SQL Server 数据库连接信息（如果不使用 Windows 身份验证，请添加 `uid` 和 `pwd` 参数）。

   ```R
   library(sqlmlutils)
   connection <- connectionInfo(
     server= "yourserver",
     database = "yourdatabase")

   sql_install.packages(connectionString = connection, pkgs = "glue", verbose = TRUE, scope = "PUBLIC")
   ```

   > [!TIP]
   > **作用域**可以是 "**公用**" 或 "**专用**"。 公共范围可用于数据库管理员安装所有用户均可使用的包。 专用作用域使得包仅对安装它的用户可用。 如果未指定作用域，则默认作用域为 "**专用**"。

### <a name="add-the-package-offline"></a>脱机添加包

如果客户端计算机没有 Internet 连接，则可以使用**miniCRAN**通过可访问 internet 的计算机下载**胶水**包。 然后，将包复制到客户端计算机，您可以在其中脱机安装包。
有关安装**miniCRAN**的信息，请参阅[安装 miniCRAN](create-a-local-package-repository-using-minicran.md#install-minicran) 。

在具有 Internet 访问权限的计算机上：

1. 运行以下 R 脚本，为**胶水**创建本地存储库。 此示例在 `c:\downloads\glue` 中创建存储库文件夹。

   ::: moniker range=">=sql-server-2016||=sqlallproducts-allversions"

   ```R
   CRAN_mirror <- c(CRAN = "https://cran.microsoft.com")
   local_repo <- "c:/downloads/glue"
   pkgs_needed <- "glue"
   pkgs_expanded <- pkgDep(pkgs_needed, repos = CRAN_mirror);

   makeRepo(pkgs_expanded, path = local_repo, repos = CRAN_mirror, type = "win.binary", Rversion = "3.5");
   ```

   ::: moniker-end

   ::: moniker range=">=sql-server-linux-ver15||=sqlallproducts-allversions"

   ```R
   CRAN_mirror <- c(CRAN = "https://cran.microsoft.com")
   local_repo <- "c:/downloads/glue"
   pkgs_needed <- "glue"
   pkgs_expanded <- pkgDep(pkgs_needed, repos = CRAN_mirror);

   makeRepo(pkgs_expanded, path = local_repo, repos = CRAN_mirror, type = "source", Rversion = "3.5");
   ```

   ::: moniker-end


   对于 `Rversion` 值，请使用安装在 SQL Server 上的 R 版本。 若要验证已安装的版本，请使用以下 T-sql 命令。

   ```sql
   EXECUTE sp_execute_external_script @language = N'R'
    , @script = N'print(R.version)'
   ```

1. 将整个 "**胶水**存储库" 文件夹（`c:\downloads\glue`）复制到客户端计算机。 例如，将它复制到 `c:\temp\packages\glue` 文件夹。

在客户端计算机上：

1. 打开 RStudio 并创建一个新的**R 脚本**文件。

1. 使用以下 R 脚本通过**sqlmlutils**安装**粘合**包。 替换你自己的 SQL Server 数据库连接信息（如果不使用 Windows 身份验证，请添加 `uid` 和 `pwd` 参数）。

   ```R
   library(sqlmlutils)
   connection <- connectionInfo(
     server= "yourserver",
     database = "yourdatabase")
   localRepo = "c:/temp/packages/glue"

   sql_install.packages(connectionString = connection, pkgs = "glue", verbose = TRUE, scope = "PUBLIC", repos=paste0("file:///",localRepo))
   ```

   > [!TIP]
   > **作用域**可以是 "**公用**" 或 "**专用**"。 公共范围可用于数据库管理员安装所有用户均可使用的包。 专用作用域使得包仅对安装它的用户可用。 如果未指定作用域，则默认作用域为 "**专用**"。

## <a name="use-the-package"></a>使用包

安装**粘合**包后，可以在使用 t-sql **sp_execute_external_script**命令 SQL Server 的 R 脚本中使用它。

1. 打开 Azure Data Studio 或 SSMS 并连接到 SQL Server 数据库。

1. 运行以下命令：

   ```sql
   EXECUTE sp_execute_external_script @language = N'R'
       , @script = N'
   library(glue)

   name <- "Fred"
   birthday <- as.Date("2020-06-14")
   text <- glue(''My name is {name} '',
   ''and my birthday is {format(birthday, "%A, %B %d, %Y")}.'')

   print(text)
         ';
   ```

    结果

    ```text
    My name is Fred and my birthday is Sunday, June 14, 2020.
    ```

## <a name="remove-the-package"></a>删除包

如果要删除**粘附**包，请运行以下 R 脚本。 使用之前定义的同一个**连接**变量。

```R
sql_remove.packages(connectionString = connection, pkgs = "glue", scope = "PUBLIC")
```

## <a name="next-steps"></a>后续步骤

- 有关已安装的 R 包的信息，请参阅[获取 r 包信息](r-package-information.md)
- 有关使用 R 包的帮助，请参阅[使用 r 包的提示](tips-for-using-r-packages.md)
- 有关安装 Python 包的信息，请参阅[安装具有 pip 的 python 包](install-additional-python-packages-on-sql-server.md)
- 有关 SQL Server 机器学习服务的详细信息，请参阅[什么是 SQL Server 机器学习服务（Python 和 R）？](../what-is-sql-server-machine-learning.md)
