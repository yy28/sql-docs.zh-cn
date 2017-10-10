---
title: "与 SQL Server 安装的 R 包 |Microsoft 文档"
ms.custom: 
ms.date: 09/29/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- R
ms.assetid: 4d426cf6-a658-4d9d-bfca-4cdfc8f1567f
caps.latest.revision: 1
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 29122bdf543e82c1f429cf401b5fe1d8383515fc
ms.openlocfilehash: 0e96334850554ab642e3372c3631f3ab672109d6
ms.contentlocale: zh-cn
ms.lasthandoff: 10/10/2017

---
# <a name="r-packages-installed-with-sql-server"></a>与 SQL Server 安装的 R 包

本文介绍与 SQL Server 安装的 R 包，并提供有关如何管理和查看现有包的信息。

本文还提供了有关如何添加用于 SQL Server 的新包的信息的链接。

**适用于：** SQL Server 自 2017 年 1 机器学习服务 （数据库中）、 SQL Server 2016 R Services （数据库）

## <a name="what-is-the-instance-library-and-where-is-it"></a>实例库和其中是它是什么？

在 SQL 服务器上运行任何 R 解决方案可以使用安装在默认 R 库与实例关联的包。

当在 SQL Server 中安装 R 功能时，R 包库位于实例文件夹下。

+ 默认实例*MSSQLSERVER* 

    SQL Server 自 2017 年 1:`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library` 
    
    SQL Server 2016:`C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library`

+ 命名实例*MyNamedInstance* 

    SQL Server 自 2017 年 1:`C:\Program Files\Microsoft SQL Server\MSSQL14.MyNamedInstance\R_SERVICES\library` 
    
    SQL Server 2016:`C:\Program Files\Microsoft SQL Server\MSSQL13.MyNamedInstance\R_SERVICES\library`

可以运行以下语句来验证 R.的当前实例的默认库。

```SQL
EXECUTE sp_execute_external_script  @language = N'R'
, @script = N'OutputDataSet <- data.frame(.libPaths());'
WITH RESULT SETS (([DefaultLibraryName] VARCHAR(MAX) NOT NULL));
GO
```
## <a name="r-packages-installed-with-sql-server"></a>与 SQL Server 安装的 R 包

在 R 语言中安装 SQL Server，默认情况下，R**基**安装包。 基本包包含核心功能提供通过包如`stats`和`utils`。

安装 SQL Server 2016 和 SQL Server 自 2017 年中的 R 还包括**RevoScaleR**包和相关增强的包和提供程序，它支持远程计算上下文，流式处理，并行执行 rx 函数和许多其他功能。

+ 增强的 R 功能的概述，请参阅[有关机器学习服务器](https://docs.microsoft.com/r-server/what-is-microsoft-r-server)

+ 若要下载到客户端计算机上的 RevoScaleR 库，安装[Microsoft R 客户端](https://docs.microsoft.com/r-server/r-client/what-is-microsoft-r-client)

## <a name="permissions-required-for-installing-r-packages"></a>用于安装 R 包所需权限

在 SQL Server 2016，管理员必须安装在实例范围内的新的 R 包。 在 SQL Server 自 2017 年，新的数据库功能已添加，使数据库管理员能够包将管理委派给所选用户。

本部分介绍安装和管理每个版本的包所需的权限。

+ SQL Server 2016 R Services （数据库）

    若要运行的计算机上安装新的 R 包[!INCLUDE [ssCurrent](..\..\includes\sscurrent-md.md)]，你必须具有到计算机的管理权限。 它是数据库管理员或其他服务器上的管理员，以确保上是否安装了所有所需的程序包的任务[!INCLUDE[ssNoVersion_md](..\..\includes\ssnoversion-md.md)]实例。

    如果你没有管理权限的计算机上承载[!INCLUDE[ssNoVersion_md](..\..\includes\ssnoversion-md.md)]可以提供给管理员若要了解如何安装 R 包，并提供到安全包存储库的访问的实例，其中包请求的用户可以获取。

+ SQL Server 2017 机器学习服务

    此版本包括可使数据库管理员委托给选定用户的包的安装权限的包管理功能。 如果已启用此功能，则请求，数据库管理员将你添加到新的包角色之一。 有关详细信息，请参阅[for SQL Server 的 R 包管理](r-package-management-for-sql-server-r-services.md)。

    如果你是 SQL Server 实例上的管理员，你可以安装在将新包。 只需一定要使用的实例相关联的默认库。 当从存储过程调用时，无法运行包安装到其他位置。 使用 SQL Server，因为计算上下文还需要在实例库中的包可供运行任何 R 代码。

+ R Server (Standalone)

    你需要对计算机的管理权限来安装新的 R 程序包。

+ 其他客户端环境

    如果在用作 R 工作站的计算机上安装新的 R 包，并且该计算机将执行**不**具有的实例[!INCLUDE[ssNoVersion_md](..\..\includes\ssnoversion-md.md)]安装，仍需要到计算机以管理权限安装包。 该包在安装后可以本地运行。

## <a name="managing-or-viewing-installed-packages"></a>管理或查看已安装的程序包

有多种方法，你可以获取当前安装的包的完整列表。 有关详细信息，请参阅[确定哪些包安装在 SQL Server 上](determine-which-packages-are-installed-on-sql-server.md)。

