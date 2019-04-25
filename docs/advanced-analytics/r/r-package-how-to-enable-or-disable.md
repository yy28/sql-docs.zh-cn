---
title: 启用或禁用远程 R 包管理的 SQL Server 机器学习服务
description: 启用 SQL Server 2016 R Services 或 SQL Server 2017 机器学习服务 （数据库内） 上的远程 R 包管理
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/10/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: ee52fd9b7a116156f794303b828a83e9b06de6ab
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62641808"
---
# <a name="enable-or-disable-remote-package-management-for-sql-server"></a>启用或禁用 SQL Server 的远程包管理
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文介绍如何启用远程管理的客户端工作站或不同的机器学习服务器中的 R 包。 SQL Server 上启用包管理功能后，可以使用客户端上 RevoScaleR 命令在 SQL Server 上安装包。

> [!NOTE]
> 当前支持的 R 库的管理;对 Python 已列入计划的支持。

默认情况下，SQL Server 的外部包管理功能已禁用。 必须运行一个单独的脚本以启用该功能在下一节中所述。

## <a name="overview-of-process-and-tools"></a>过程和工具的概述

若要启用或禁用包管理 SQL Server 上的，使用命令行实用工具**RegisterRExt.exe**，这是附带**RevoScaleR**包。

[启用](#bkmk_enable)此功能是一个两步过程，要求数据库管理员： 你的 SQL Server 实例 （一次每个 SQL Server 实例） 上启用包管理，然后启用 （一次每个 SQL Server 的 SQL 数据库上的包管理数据库）。

[禁用](#bkmk_disable)包管理功能也需要 multipel 步骤： 删除数据库级的包和权限 （一次每个数据库），然后 （一次每个实例） 服务器中删除角色。

## <a name="bkmk_enable"></a> 启用包管理

1. SQL Server 上打开提升的命令提示符并导航到包含该实用工具，RegisterRExt.exe 的文件夹。 默认位置是`<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRExe.exe`。

2. 运行以下命令，提供你的环境的相应参数：

    `RegisterRExt.exe /install pkgmgmt [/instance:name] [/user:username] [/password:*|password]`

    此命令所需的包管理的 SQL Server 计算机上创建实例级对象。 它也会重启实例快速启动板。

    如果不指定实例，使用默认实例。 如果未指定用户，使用当前安全上下文。 例如，以下命令启用 RegisterRExt.exe，使用的凭据打开命令提示符下的用户路径中的实例上的包管理：

    `REgisterRExt.exe /install pkgmgmt`

3. 若要添加到特定数据库的包管理，请从提升的命令提示符运行以下命令：

    `RegisterRExt.exe /install pkgmgmt /database:databasename [/instance:name] [/user:username] [/password:*|password]`
   
    此命令将创建一些数据库项目，包括用于控制用户权限的以下数据库角色： `rpkgs-users`， `rpkgs-private`，和`rpkgs-shared`。

    例如，以下命令启用的数据库，运行 RegisterRExt 的实例上的包管理。 如果未指定用户，使用当前安全上下文。

    `RegisterRExt.exe /install pkgmgmt /database:TestDB`

4. 对于必须在其中安装包的每个数据库重复该命令。

5. 若要验证是否已成功创建新角色，请在 SQL Server Management Studio 中，单击数据库，展开**安全**，然后展开**数据库角色**。

    此外可以在如下所示的 sys.database_principals 上运行的查询：

    ```sql
    SELECT pr.principal_id, pr.name, pr.type_desc,   
        pr.authentication_type_desc, pe.state_desc,   
        pe.permission_name, s.name + '.' + o.name AS ObjectName  
    FROM sys.database_principals AS pr  
    JOIN sys.database_permissions AS pe  
        ON pe.grantee_principal_id = pr.principal_id  
    JOIN sys.objects AS o  
        ON pe.major_id = o.object_id  
    JOIN sys.schemas AS s  
        ON o.schema_id = s.schema_id;
    ```

启用此功能后，可以使用 RevoScaleR 函数来安装或从远程 R 客户端卸载包。

## <a name="bkmk_disable"></a> 禁用包管理

1. 从提升的命令提示符，RegisterRExt 实用程序再次运行，并禁用数据库级别的包管理：

    `RegisterRExt.exe /uninstall pkgmgmt /database:databasename [/instance:name] [/user:username] [/password:*|password]`

    此命令将删除数据库对象中指定的数据库相关的包管理。 它还会删除已从 SQL Server 计算机上的受保护的文件系统位置安装的所有包。

2. 重复此命令使用包管理的每个数据库上。

3.  （可选）所有数据库均已都清除的包使用前面的步骤后，请从提升的命令提示符运行以下命令：

    `RegisterRExt.exe /uninstall pkgmgmt [/instance:name] [/user:username] [/password:*|password]`

    此命令从实例中删除包管理功能。 您可能需要手动重新启动 Launchpad 服务一次，以查看更改。

## <a name="next-steps"></a>后续步骤

+ [使用 RevoScaleR 安装新的 R 包](use-revoscaler-to-manage-r-packages.md)
+ [安装 R 包的提示](packages-installed-in-user-libraries.md)
+ [默认包](installing-and-managing-r-packages.md)
