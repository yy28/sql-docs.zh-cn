---
title: "SQL Server 的 R 包管理 |Microsoft 文档"
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
dev_langs:
- R
ms.assetid: 98c14b05-750e-44f9-8531-1298bf51e8d2
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: f40bc2a4f17914423eeea944a45c79ae3d259a76
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2018
---
# <a name="r-package-management-for-sql-server"></a>SQL Server 的 R 包管理
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文介绍的 R 包和 SQL Server 2016 中 SQL Server 2017 管理的功能。

+ 推荐的方法管理 R 包 
+ SQL Server 2016 和自 2017 年之间的包管理中的更改

**适用于：** SQL Server 2016 R Services、 SQL Server 自 2017 年 1 机器学习服务

## <a name="recommended-methods-for-package-management"></a>推荐的方法管理包

在 SQL Server 2016 和 SQL Server 自 2017 年中，计算机管理员可以安装启用机器学习了每个实例的包。 

包安装到文件系统中，使用实例库中，无法在实例之间共享。 这是当前用于 SQL Server 2016 和 SQL Server 自 2017 年的建议的方法。

+ [在 SQL Server 上安装其他 R 包](install-additional-r-packages-on-sql-server.md)
+ [确定要在 SQL Server 上安装的包](determine-which-packages-are-installed-on-sql-server.md)

此外，如果你有**dbo**角色成员身份于机器学习中已启用 SQL server 实例中，你可以安装 R 包从远程客户端，使用 RevoScaleR 中的新函数。

+ [新的包安装的 R 函数](#bkmk_remoteInstall)

### <a name="installation-on-servers-with-no-internet-access"></a>在没有 Internet 访问权限的服务器上的安装

若要更加轻松地确定所需的 R 包版本，并提供所有包的依赖关系，可以使用[miniCRAN](https://mran.microsoft.com/package/miniCRAN)。 此 R 包的目标包列表，并创建包含所有其依赖项，以压缩格式的目标包的本地存储库。 然后可以将此内容复制到脱机的服务器，或共享在多个实例之间的存储库。

有关详细信息，请参阅[创建本地包存储库使用 miniCRAN](create-a-local-package-repository-using-minicran.md)。

### <a name="python-packages"></a>Python 包

新的 Python 包安装遵循相同的准则： 

+ 查看 Python 包提前来确定使用最新的 Python 版本的兼容性
+ 评估 Python 包适合于强化的 SQL Server 环境
+ 使用 Python tools 以管理员身份安装包
+ 安装必须仅在实例库中的 SQL Server 上下文中运行的包。 
+ 如果你使用多个环境进行测试，生产等，将确保相同版本的 Python 包安装在实例库。

有关安装步骤，请参阅[在 SQL Server 上安装新的 Python 软件包](../python/install-additional-python-packages-on-sql-server.md)

## <a name="features-for-package-management-in-sql-server-2016-and-sql-server-2017"></a>适用于 SQL Server 2016 和 SQL Server 自 2017 年中的包管理的功能

SQL Server 2017 添加一些新功能来支持 R （和 Python） 包由数据库管理员能够更容易管理。 这些新功能包括：

+ 安装或管理包库使用 T-SQL 的功能
+ 在数据库级别通过数据库角色的用户权限管理。 

在未来版本中，这些功能需要提供用于程序包管理由数据库管理员的主要方法和简化数据科学家安装所需的库。

在大约在同一时间，Microsoft R Server 和机器学习服务器添加新的 R 函数，以使其更轻松地安装并共享 SQL Server 计算上下文中的包。 这些函数基于 T-SQL 的 SQL Server 功能独立运行，并且应将从远程 R 客户端运行。

本部分概述了这些功能。

### <a name="bkmk_remoteInstall"></a>包安装的新 RevoScaleR 函数 

使用最新版本的 R 服务器或计算机学习服务器的用户还可以使用中的新功能[ **RevoScaleR** ](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)指定为 SQL Server 计算上下文的实例上安装包。

+ 而不必直接访问 SQL Server 计算机，数据科研人员可以在 SQL Server 上安装所需的 R 程序包。 但是，用户必须属于数据库所有者 (**dbo**) 角色。

+ 用户可以通过使用共享作用域中安装包与他人共享包。 相同的 SQL Server 数据库的其他授权的用户可以访问包。

+ 用户可以安装不会向其他人，显示的专用包创建专用沙盒获取 R 包。

+ 包同步使轻松备份和还原的包

#### <a name="package-installation-functions"></a>包安装函数

有关安装和删除指定的计算上下文中的程序包中 RevoScaleR，提供了以下包管理功能：

-   [rxInstalledPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstalledpackages)： 查找有关指定的计算上下文中安装的程序包的信息。

-   [rxInstallPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstallpackages)： 安装包复制到以下计算上下文，从指定的存储库，或通过读取本地保存的压缩包。

-   [rxRemovePackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxremovepackages)： 删除计算上下文从安装包。

-   [rxFindPackage](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxfindpackage)： 获取指定的计算上下文中的一个或多个包的路径。

-   [rxSyncPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsyncpackages)： 在指定的计算上下文中复制的文件系统和数据库之间的包库。

-   [rxSqlLibPaths](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqllibpaths): SQL Server 的内部执行时的搜索路径获取包的库树。

若要使用这些函数，连接到 SQL Server 具有必需的权限，使用 SQL Server 计算上下文的实例。 

> [!IMPORTANT]
> 在连接中使用的凭据确定是否可以在服务器上完成该操作。

这些包安装函数依赖关系检查，并确保任何相关的程序包，可以就像在本地计算上下文中的 R 包安装到 SQL Server 进行安装。 卸载包的功能也会计算依赖项，并确保删除 SQL Server 上其他包不再使用的包以释放资源。

这些新的函数都将纳入 RevoScaleR 在 SQL Server 2017 中安装的版本。 此外可以通过获取这些函数[升级的 SQL Server 实例](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)使用了新版本的[Microsoft R Server 或机器学习 Server](https://docs.microsoft.com/machine-learning-server/rebranding-microsoft-r-server)。 需要 9.0.1 版或更高版本。

#### <a name="package-synchronization-functions"></a>包同步函数

包同步是仅限 R 包的新功能。 数据库引擎跟踪由特定的所有者和组，并可以将这些包写入到文件系统，如果所需的包。 通常在这些情况下使用包同步：

+ 你想要移动的 SQL Server 实例之间的 R 包。
+ 你需要重新安装包针对的特定用户或组后还原数据库。

有关如何启用和使用此功能的详细信息，请参阅[for SQL Server 的 R 包同步](package-install-uninstall-and-sync.md)。

### <a name="package-management-using-t-sql"></a>使用 T-SQL 的管理包

SQL Server 2017 添加新的 T-SQL 语句，为 DBA 提供更好地控制在数据库级别的 R 包。 DBA 不一定非要了解使用 R 或 Python tools，但改为应该能够使 R 或 Python 的用户能够安装的包他们所需和与他人共享。

此功能旨在在多用户环境中进行协作和版本管理更容易： 例如：

+ 你想要共享已在你的团队来与其他人开发的包。
+ 多个分析师正处于同一数据库中，且需要使用同一个包的不同版本。
+ 你想要将包和其权限移动时，移动数据库，或执行备份和还原操作时。

SQL Server 自 2017 年中的包管理依赖于这些新的数据库对象和功能：

+ [新的数据库角色](#bkmk_roles)、 用于管理包访问和使用
+ [创建外部库](#bkmk_createExternalLibrary)语句，将包库上载到服务器

使用这些功能需要在实例级别和数据库级别的一些其他准备工作： 

+  数据库管理员必须显式启用包管理功能，通过运行脚本创建必要的数据库对象。 有关详细信息，请参阅[如何启用 R 包管理](r-package-how-to-enable-or-disable.md)。

+ 用户必须分配给角色，每个数据库级别上。 这些角色使用户能够安装共享或私有的包。

+ 可以使用新的 T-SQL 语句，创建外部库安装包库。 但是，必须事先准备好的所有包依赖项并将其作为单个 zip 文件的一部分进行安装。

> [!NOTE]
> 尽管这次，此处描述的功能是完全正常运行，将来的版本将包含其他改进，让你更轻松地准备包库并管理依赖项。 如果你熟悉 R 包安装，我们建议你继续现在使用的 R 工具。

#### <a name="bkmk_createExternalLibrary"></a>创建外部库 

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

若要确保提供所有包依赖关系，因此我们建议使用[miniCRAN](create-a-local-package-repository-using-minicran.md)创建本地存储库。 然后可以使用该压缩的文件以安装目标包和其依赖项。

#### <a name="bkmk_roles"></a>用于程序包管理的数据库角色 

默认情况下，即使是机器学习已安装并启用其中的实例中不包括在 SQL Server 中为管理包提供的新角色。 必须通过运行脚本此处所述添加角色：[启用或禁用包管理](r-package-how-to-enable-or-disable.md)。

运行此脚本后，你应看到以下新的数据库角色：

+ `rpkgs-users`： 此角色的成员可以使用由另一个安装的任何共享的包`rpkgs-shared`角色成员。

+ `rpkgs-private`： 此角色的成员有权访问共享包，使用作为的成员相同的权限`rpkgs-users`角色。 此角色的成员还可以安装、 删除和使用私下指定了作用域的包。

+ `rpkgs-shared`： 此角色的成员具有相同的权限的成员`rpkgs-private`角色。 此外，此角色的成员可以安装或删除共享的包。

+ `db_owner`： 此角色的成员具有相同的权限的成员`rpkgs-shared`角色。 此外，此角色的成员可以**授予**其他用户的权限安装或删除同时共享和私有的包。

数据库管理员可以将用户添加到每个数据库的角色。



## <a name="next-steps"></a>后续步骤

[SQL Server 机器学习的包管理](r-package-management-for-sql-server-r-services.md)
