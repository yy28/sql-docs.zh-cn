---
title: "SQL Server 的 R 包管理 |Microsoft 文档"
ms.custom: 
ms.date: 10/09/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: R
ms.assetid: 98c14b05-750e-44f9-8531-1298bf51e8d2
caps.latest.revision: "7"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 5cd3924b79ce5d33adf88bb6c7c267cdc43a3418
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/01/2017
---
# <a name="r-package-management-for-sql-server"></a>SQL Server 的 R 包管理

本文介绍适用于 SQL Server 2017 和 SQL Server 2016 中的 R 包的管理功能。

+ 2016 和自 2017 年之间的 R 包安装方法中的更改
+ 推荐的方法管理 R 包
+ 用于 SQL Server 自 2017 年中的程序包管理的新数据库角色
+ 用于 SQL Server 自 2017 年中的程序包管理的新的 T-SQL 语句

**适用于：** SQL Server 2016 R Services、 SQL Server 自 2017 年 1 机器学习服务

## <a name="differences-in-package-management-between-sql-server-2016-and-sql-server-2017"></a>程序包管理中 SQL Server 2016 和 SQL Server 自 2017 年之间的差异

在**SQL Server 2017**，你可以启用在实例级别的包管理和管理的用户权限来添加或使用在数据库级别的包。

这要求数据库管理员通过运行脚本创建必要的数据库对象启用包管理功能。 有关详细信息，请参阅[如何启用 R 包管理](r-package-how-to-enable-or-disable.md)。

在**SQL Server 2016**，管理员必须在与实例关联的 R 库中安装 R 包。 实例中运行 R 代码的所有用户都使用这些包。 在 SQL server 中运行的 R 代码不能使用安装在用户库中的包。 但是，管理员可以授予单个用户运行特定数据库中的 R 脚本的能力。

**差异和优势的摘要**

+ 如果在 SQL Server 2017 使用机器学习服务，你可以管理并安装 R 包使用传统方法，基于 R 工具，或者通过使用新的数据库角色和 T-SQL 的语句。

+ 我们建议后一种方法，因为它提供更细化的控制，由管理员、 再加上为用户更自由。 例如，用户可以安装其自己的包，或者使用存储的过程或通过 R 代码，并与他人共享包。 

    由于包的范围可以为一个数据库，并且每个用户获取独立的包沙盒，很容易地安装不同版本的相同的 R 包。 你也很容易可以复制或数据库之间移动用户和他们的软件包。 

+ 使用 SQL Server 中的包管理功能使备份和还原操作要容易得多。 在您的工作数据库迁移到新服务器时，你可以使用包同步函数读取所有包的列表，并将其安装在新服务器上的数据库。

+ 你可能会发现更方便地安装 R 包以管理员身份的计算机上，使用传统的 R 工具，如果你是使用机器学习作业的服务器的唯一人员。

+ 如果你使用的 SQL Server 2016 R Services，你应继续安装使用 R 工具的实例使用的 R 包 > 请务必使用与实例关联的 R 库。

以下各节提供有关如何管理包的更多详细信息使用这两个选项执行。

## <a name="r-package-management-using-t-sql"></a>使用 T-SQL 的 R 包管理

SQL Server 2017 包括为 DBA 提供更好地控制在数据库级别的 R 包的新的 T-SQL 语句。 同时，DBA 可以使用户能够安装的包他们所需和与他人共享。

如果你需要包与他人共享，或如果多个用户需要在服务器上运行机器学习作业，我们建议你启用管理包，将用户分配到数据库角色，并上载包，以便用户可以对其进行共享。

SQL Server 自 2017 年中的包管理依赖于这些新的数据库对象和功能：

+ 新的数据库角色，用于管理包访问和使用
+ 包作用域，单独的共享和私有包
+ 创建外部库语句，将新的代码库上载到服务器
+ RevoScaleR，以支持在 SQL Server 中的包的安装中的新 R 函数计算上下文
+ 包同步，以确保轻松备份和还原的包

### <a name="database-roles-for-package-management"></a>包管理的数据库角色

数据库管理员必须创建用于通过运行脚本此处所述的包管理的角色：[启用或禁用包管理](r-package-how-to-enable-or-disable.md)。

运行此脚本后，你应看到以下新的数据库角色：

+ `rpkgs-users`： 此角色的成员可以使用由另一个安装的任何共享的包`rpkgs-shared`角色成员。

+ `rpkgs-private`： 此角色的成员有权访问共享包，使用作为的成员相同的权限`rpkgs-users`角色。 此角色的成员还可以安装、 删除和使用私下指定了作用域的包。

+ `rpkgs-shared`： 此角色的成员具有相同的权限的成员`rpkgs-private`角色。 此外，此角色的成员可以安装或删除共享的包。

+ `db_owner`： 此角色的成员具有相同的权限的成员`rpkgs-shared`角色。 此外，此角色的成员可以**授予**其他用户的权限安装或删除同时共享和私有的包。

数据库管理员将用户添加到上为每个数据库运行，以控制用户的能力安装包的角色。

### <a name="package-scope"></a>包作用域

新的程序包管理功能，通过它们是私有的还是可以由多个用户共享区分包。

+ **共享作用域**

    *共享范围*意味着该用户已分配给共享作用域角色的权限 (`rpkgs-shared`) 可以安装和卸载程序包添加到指定的数据库。 在共享作用域库中安装的包可由 SQL Server 上数据库的其他用户使用，前提是这些用户有权使用已安装的 R 包。

+ **专用作用域**

    *专用作用域*意味着该用户已被授予在专用的作用域角色的成员身份 (`rpkgs-private`) 可以安装或卸载到每个用户定义的专用库位置的包。 因此，专用作用域中安装的任何包仅可由安装包的用户使用。 也就是说，SQL Server 上的用户无法使用其他用户安装的专用包。

可合并这些“共享”和“专用”作用域模型，开发自定义安全系统，从而部署和管理 SQL Server 上的包。

例如，通过使用共享作用域，可向一组数据科学家的领导或经理授予安装包的权限，随后相同 SQL Server 实例中的所有其他用户或数据科学家可使用这些包。

其他方案可能会要求在用户之间进行更好地隔离或要求使用不同版本的包。 在此情况下，可使用专用作用域向数据科学家授予单独的权限，这些数据科学家将负责安装和使用其所需的包。 由于是基于用户安装的包，因此由某用户安装的包不会影响使用相同 SQL Server 数据库的其他用户的工作。

### <a name="create-external-library"></a>创建外部库

[创建外部库](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql)是 SQL Server 2017，以帮助数据库管理员在使用无用户 R 工具的包中引入一个新的 T-SQL 语句。 

你使用**创建外部库**语句将外部库上载到压缩的文件格式中的实例。 然后，授权的用户可以访问库，并安装它们供自己使用。

例如，你可以创建你的 R 项目，每个不同版本的多个副本。 上载为单独的库，可以将某些版本保留为专用和与其他用户共享某些版本。

"库"基本上是你想要向单个名称下的用户提供的外部包的集合。 例如，你可能会发布以下任何到 SQL Server 以用作外部库：

+ 单个 R 包已写入，没有依赖项
+ 你想要安装，包和依赖项所需的安装
+ 与特定任务或项目，但是它们的依赖项有相关的 R 包的集合

库名称是用于管理包或 SQL Server 中的包的集合，并且可以独立于安装的包。 但是，库名称必须是唯一的实例。

若要使用此语句，包管理功能必须启用了实例上。 有关详细信息，请参阅[创建外部库](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql)。

> [!NOTE]
> 当前此语句可用于创建仅基于 Windows 的库，为。 支持计划在将来对于 Python 包，并在其他平台，如 Linux 上执行的包。

已将外部库上载到服务器后，必须将其安装到与实例关联的 R 包库中。 有几种方法执行此操作：

+ 运行标准 R 命令`install.packages`sp_execute_external_script 内。 请确保使用具有的权限安装包的帐户进行连接。

+ 从远程 R 客户端连接到 SQL Server 并运行[rxInstallPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstallpackages)在 SQL Server 计算上下文中。 同样，你必须具有的权限安装包中私有或共享要执行此操作的作用域。

若要查看使用 R 和 T-SQL 安装示例，请参阅[在 SQL Server 上安装其他软件包](install-additional-r-packages-on-sql-server.md)。

### <a name="new-r-functions-for-package-installation"></a>新的包安装的 R 函数

启用了用于程序包管理的数据库角色后，用户还可以使用中的新功能[ **RevoScaleR** ](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)作为 SQL Server 计算上下文指定的实例上安装包。

+ 而不必直接访问 SQL Server 计算机，数据科研人员可以在 SQL Server 上安装所需的 R 程序包。

+ 用户可以安装包，并与他人共享，通过与共享的作用域中安装包。 然后相同的 SQL Server 数据库的其他授权的用户可以访问包。

+ 用户可以安装不会向其他人，显示的专用包创建专用沙盒获取 R 包。

有关安装和删除指定的计算上下文中的程序包中 RevoScaleR，提供了以下包管理功能：

-   [rxInstalledPackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxinstalledpackages)： 查找有关指定的计算上下文中安装的程序包的信息。

-   [rxInstallPackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxinstallpackages)： 安装包复制到以下计算上下文，从指定的存储库，或通过读取本地保存的压缩包。

-   [rxRemovePackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxremovepackages)： 删除计算上下文从安装包。

-   [rxFindPackage](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxfindpackage)： 获取指定的计算上下文中的一个或多个包的路径。

-   [rxSyncPackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsyncpackages)： 在指定的计算上下文中复制的文件系统和数据库之间的包库。

-   [rxSqlLibPaths](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsqllibpaths): SQL Server 的内部执行时的搜索路径获取包的库树。

若要使用这些函数，连接到 SQL Server 具有必需的权限，使用 SQL Server 计算上下文的实例。 连接时，你的凭据将确定是否可以在服务器上完成该操作。

包安装功能检查依赖项并确保任何相关包可安装到 SQL Server，就像本地计算上下文中的 R 包安装一样。 卸载包的功能也会计算依赖项，并确保删除 SQL Server 上其他包不再使用的包以释放资源。

> [!NOTE]
> 
> 默认情况下，SQL Server 2017 中包括的这些新的函数。 你可以更新你的 RevoScaleR 若要通过升级要使用的 Microsoft R Server，例如 Microsoft R Server 9.0.1 更高版本的实例获取这些函数的版本。
> 
> 有关详细信息，请参阅[到升级程序使用 SqlBindR.exe](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)。

### <a name="synchronization-of-r-package-libraries"></a>R 包库的同步

CTP 2.0 版本的 SQL Server 2017 （和 Microsoft R Server 自 2017 年 4 月发行） 包含新的 R 函数*同步包*。

包同步是指数据库引擎跟踪由特定的所有者和组，并可以将这些包写入到文件系统，如果所需的包。 在这些情况下，你可以使用包同步：

+ 你想要移动的 SQL Server 实例之间的 R 包。
+ 你需要重新安装包针对的特定用户或组后还原数据库。

有关如何启用和使用此功能的详细信息，请参阅[for SQL Server 的 R 包同步](package-install-uninstall-and-sync.md)。

## <a name="r-package-management-using-traditional-r-tools"></a>使用传统的 R 工具的 R 包管理

管理 R 包实例上的传统方法是安装和使用 R 工具和命令列出包。 

+ 如果你使用 SQL Server 2016 的早期版本，此选项可能是唯一的选项。  
+ 如果你的 R 包的唯一用户，并且具有到服务器的管理访问权限，此选项还可能会很方便。
+ 若要简化管理 R 程序包版本，可以使用[miniCRAN](create-a-local-package-repository-using-minicran.md)创建本地存储库和共享，在实例之间。

有关详细信息，请参阅以下文章：

+ [在 SQL Server 上安装其他 R 包](install-additional-r-packages-on-sql-server.md)
+ [确定要在 SQL Server 上安装的包](determine-which-packages-are-installed-on-sql-server.md)

对于 SQL Server 自 2017 年，我们建议你使用创建外部库中，从而来管理用户和其 R 包的数据库角色。

## <a name="next-steps"></a>后续步骤

[如何启用或禁用 R 包管理](../r/r-package-how-to-enable-or-disable.md)
