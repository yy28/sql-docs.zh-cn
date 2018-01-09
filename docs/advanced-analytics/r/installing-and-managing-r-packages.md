---
title: "与 SQL Server 安装的 R 包 |Microsoft 文档"
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
dev_langs: R
ms.assetid: 4d426cf6-a658-4d9d-bfca-4cdfc8f1567f
caps.latest.revision: "1"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: 2783d4ce6ca9cd25b41c1e658f5e3bf2a4f05f24
ms.sourcegitcommit: 60d0c9415630094a49d4ca9e4e18c3faa694f034
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/09/2018
---
# <a name="r-packages-installed-with-sql-server"></a>与 SQL Server 安装的 R 包

本文介绍了 R 包，如果你安装和启用机器学习功能与 SQL Server 安装。 本文还介绍如何管理和查看现有包，或将新的包添加到 SQL Server 实例。

**适用于：** SQL Server 自 2017 年 1 机器学习服务 （数据库中）、 SQL Server 2016 R Services （数据库）

## <a name="what-is-the-instance-library-and-where-is-it"></a>实例库和其中是它是什么？

在 SQL 服务器上运行任何 R 解决方案可以使用安装在默认 R 库与实例关联的包。 当在 SQL Server 中安装 R 功能时，R 包库位于实例文件夹下。

+ 默认实例*MSSQLSERVER* 

    SQL Server 自 2017 年 1:`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library` 
    
    SQL Server 2016:`C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library`

+ 命名实例*MyNamedInstance* 

    SQL Server 自 2017 年 1:`C:\Program Files\Microsoft SQL Server\MSSQL14.MyNamedInstance\R_SERVICES\library` 
    
    SQL Server 2016:`C:\Program Files\Microsoft SQL Server\MSSQL13.MyNamedInstance\R_SERVICES\library`

可以运行以下语句来验证 R.的当前实例的默认库。

```sql
EXECUTE sp_execute_external_script  @language = N'R'
, @script = N'OutputDataSet <- data.frame(.libPaths());'
WITH RESULT SETS (([DefaultLibraryName] VARCHAR(MAX) NOT NULL));
GO
```

另外，你可以使用管理新[rxSqlLibPaths](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqllibpaths)函数，如果执行 sp\_执行\_外部\_直接在目标计算机上的脚本。 该函数不能返回为远程连接的库路径。

```sql
EXEC sp_execute_external_script
  @language =N'R',
  @script=N'
  sql_r_path <- rxSqlLibPaths("local")
  print(sql_r_path)
```

> [!NOTE]
> 如果你使用绑定来升级实例中的 R 组件，可以更改实例库的路径。 请务必验证 SQL Server 正在使用的库。

## <a name="r-packages-installed-with-sql-server"></a>与 SQL Server 安装的 R 包

默认情况下，R**基**安装包。 基本包包含核心功能提供通过包如`stats`和`utils`。

SQL Server 2016 或 SQL Server 自 2017 年中的 R 安装始终包含**RevoScaleR**包和相关增强的包和提供程序，它支持远程计算上下文，流式处理，并行执行 rx 函数和许多其他功能。 若要升级 RevoScaleR 包，可以使用绑定来升级学习组件，计算机或修补程序或将您实例升级到较新版本的 SQL Server。

+ 增强的 R 功能的概述，请参阅[有关机器学习服务器](https://docs.microsoft.com/machine-learning-server/what-is-microsoft-r-server)

+ 若要下载到客户端计算机上的 RevoScaleR 库，安装[Microsoft R 客户端](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client)

## <a name="permissions-required-for-installing-r-packages"></a>用于安装 R 包所需权限

在 SQL Server 2016，管理员必须安装在实例范围内的新的 R 包。 

SQL Server 2017 引入包安装和管理的新增功能：

+ 从远程客户端的 R 命令可用于使用私有或共享的作用域安装包。 此功能要求[Microsoft R Server](https://docs.microsoft.com/machine-learning-server/install/r-server-install)或[机器学习服务器](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server)，以及在实例上的 dbo 特权。
+ 新的数据库功能已添加以支持包管理由数据库管理员不使用 T-SQL 的情况下。 在将来，这些功能为 Dba 提供委派到特权用户的管理包的大多数方面的能力。

本部分介绍安装和管理每个版本的包所需的权限。

+ SQL Server 2016 R Services （数据库）

    若要运行的计算机上安装新的 R 包[!INCLUDE [ssCurrent](..\..\includes\sscurrent-md.md)]，你必须具有到计算机的管理权限。 它是数据库管理员或其他服务器上的管理员，以确保上是否安装了所有所需的程序包的任务[!INCLUDE[ssNoVersion_md](..\..\includes\ssnoversion-md.md)]实例。

    如果你没有管理权限的计算机上承载[!INCLUDE[ssNoVersion_md](..\..\includes\ssnoversion-md.md)]可以提供给管理员若要了解如何安装 R 包，并提供到安全包存储库的访问的实例，其中包请求的用户可以获取。

+ SQL Server 2017 机器学习服务

    如果你是 SQL Server 实例上的管理员，你可以安装在将新包。 只需一定要使用的实例相关联的默认库。 当从存储过程调用时，无法运行包安装到其他位置。 使用 SQL Server，因为计算上下文还需要在实例库中的包可供运行任何 R 代码。

    此版本还包括用于支持更简单的包管理的 Dba 在更高版本的版本中一些新功能。 现在，我们建议你继续安装在实例范围内的 R 包。

+ R Server (Standalone)

    你需要对计算机的管理权限来安装新的 R 程序包。

+ 其他客户端环境

    如果在用作 R 工作站的计算机上安装新的 R 包，并且该计算机将执行**不**具有的实例[!INCLUDE[ssNoVersion_md](..\..\includes\ssnoversion-md.md)]安装，仍需要到计算机以管理权限安装包。 该包在安装后可以本地运行。

## <a name="managing-or-viewing-installed-packages"></a>管理或查看已安装的程序包

有多种方法，你可以获取当前安装的包的完整列表。 有关详细信息，请参阅[确定哪些包安装在 SQL Server 上](determine-which-packages-are-installed-on-sql-server.md)。
