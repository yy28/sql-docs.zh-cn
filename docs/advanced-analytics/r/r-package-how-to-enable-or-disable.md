---
title: 启用或禁用对 SQL Server 机器学习的远程 R 包管理 |Microsoft 文档
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: fc51428a4e6bd214fee8c4889eb218f3664ba118
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="enable-or-disable-remote-package-management-for-sql-server"></a>启用或禁用 SQL Server 的远程包管理
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文介绍如何启用管理的计算机学习 Server 的远程实例中的 R 包。 已启用包管理功能后，你可以使用 RevoScaleR 命令上将数据库从远程客户端安装包。

> [!NOTE]
> 当前支持的 R 库管理;支持 Python 是在规划之中。

默认情况下，禁用 SQL Server 的外部包管理功能，即使安装了机器学习功能。 你必须运行一个单独的脚本，以启用该功能，如在下一部分中所述。

## <a name="overview-of-process-and-tools"></a>进程和工具的概述

若要启用或禁用管理包，请使用命令行实用工具**RegisterRExt.exe**，包含在**RevoScaleR**包。

[启用](#bkmk_enable)此功能是一个两步过程，要求数据库管理员： 你启用 （一次每个 SQL Server 实例），SQL Server 实例上的管理包，然后启用 （一次每个 SQL Server 的 SQL 数据库上的包管理数据库）。

[禁用](#bkmk_disable)包管理功能还需要 multipel 步骤： 删除数据库级包和权限 （一次每个数据库），并随后从 （一次每个实例） 的服务器中删除角色。

## <a name="bkmk_enable"></a> 启用包管理

1. 打开提升的命令提示符并导航到包含的实用工具，RegisterRExt.exe 的文件夹。 默认位置是`<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRExe.exe`。

2. 运行以下命令，并提供有关你的环境的相应参数：

    `RegisterRExt.exe /installpkgmgmt [/instance:name] [/user:username] [/password:*|password]`

    此命令所需的管理包的 SQL Server 计算机上创建实例级对象。 它还会重新启动实例快速启动板。

    如果未指定实例，则使用默认实例。 如果未指定用户，则使用当前安全上下文。 例如，以下命令将启用 RegisterRExt.exe，使用的凭据打开命令提示符下的用户在路径中的实例上的包管理：

    `REgisterRExt.exe /installpkgmgmt`

3. 若要将管理包添加到特定数据库，请从提升的命令提示符运行以下命令：

    `RegisterRExt.exe /installpkgmgmt /database:databasename [/instance:name] [/user:username] [/password:*|password]`
   
    此命令创建某些数据库项目，包括用于控制用户权限的以下数据库角色： `rpkgs-users`， `rpkgs-private`，和`rpkgs-shared`。

    例如，以下命令启用的数据库，运行 RegisterRExt 的实例上的管理包。 如果未指定用户，则使用当前安全上下文。

    `RegisterRExt.exe /installpkgmgmt /database:TestDB`

4. 必须为安装包的每个数据库重复执行该命令。

5. 要验证是否已成功创建新的角色，请在 SQL Server Management Studio，请单击数据库，展开**安全**，然后展开**数据库角色**。

    此外可以在如下所示的 sys.database_principals 上运行查询：

    ```SQL
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

启用此功能后，你可以使用 RevoScaleR 函数来安装或卸载程序包从远程 R 客户端。

## <a name="bkmk_disable"></a> 禁用包管理

1. 从提升的命令提示符，RegisterRExt 实用程序再次运行，然后禁用在数据库级别的包管理：

    `RegisterRExt.exe /uninstallpkgmgmt /database:databasename [/instance:name] [/user:username] [/password:*|password]`

    此命令删除与管理包从指定的数据库相关的数据库对象。 它还会删除已从 SQL Server 计算机上的受保护的文件系统位置中安装的所有包。

2. 重复此命令在管理包已使用其中每个数据库上。

3.  （可选）已清除所有数据库的使用上一步包后，请从提升的命令提示符运行以下命令：

    `RegisterRExt.exe /uninstallpkgmgmt [/instance:name] [/user:username] [/password:*|password]`

    此命令从实例中删除包管理功能。 你可能需要手动重新启动快速启动板服务以查看更改。

