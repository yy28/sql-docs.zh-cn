---
title: "启用或禁用对 SQL Server 的 R 包管理 |Microsoft 文档"
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
ms.assetid: 6e384893-04da-43f9-b100-bfe99888f085
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 35bcae1e29e9b640d2e04b9adc788e382b18b6e8
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2018
---
# <a name="enable-or-disable-r-package-management-for-sql-server"></a>启用或禁用对 SQL Server 的 R 包管理
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本指南介绍了 SQL Server 2017，旨在允许数据库管理员联系，以控制使用 T-SQL 的而不是。 实例上的包安装中的新包管理功能

启用包管理 frature ater，你还可以使用 R 命令上 databae 移除，远程客户端安装包。

> [!NOTE]
> 默认情况下，禁用 SQL Server 的外部包管理功能，即使安装了机器学习功能。 

## <a name="enable-package-management"></a>启用包管理

到[启用](#bkmk_enable)此功能是一个两步过程，要求数据库管理员：

1.  在 SQL Server 实例上启用包管理（每个 SQL Server 实例一次）

2.  在 SQL 数据库上启用包管理（每个 SQL Server 数据库一次）

到[禁用](#bkmk_disable)包管理功能，可回退该过程，以删除数据库级包和权限，，然后从服务器删除角色：

1.  在每个数据库上禁用包管理（每个数据库一次）

2.  在 SQL Server 实例上禁用包管理（每个实例一次）

## <a name="bkmk_enable"></a>启用包管理

若要启用或禁用管理包，请使用命令行实用工具**RegisterRExt.exe**，包含在**RevoScaleR**包。

1. 打开提升的命令提示符并导航到包含的实用工具，RegisterRExt.exe 的文件夹。 默认位置是`<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRExe.exe`。

2. 运行以下命令，并提供有关你的环境的相应参数：

    `RegisterRExt.exe /installpkgmgmt [/instance:name] [/user:username] [/password:*|password]`

    此命令所需的管理包的 SQL Server 计算机上创建实例级对象。 它还会重新启动实例快速启动板。

    如果未指定实例，则使用默认实例。 如果未指定用户，则使用当前安全上下文。 例如，以下命令将启用 RegisterRExt.exe，使用的凭据打开命令提示符下的用户在路径中的实例上的包管理：

    `REgisterRExt.exe /installpkgmgmt`

2.  若要将管理包添加到特定数据库，请从提升的命令提示符运行以下命令：

    `RegisterRExt.exe /installpkgmgmt /database:databasename [/instance:name] [/user:username] [/password:*|password]`
   
    此命令创建某些数据库项目，包括用于控制用户权限的以下数据库角色： `rpkgs-users`， `rpkgs-private`，和`rpkgs-shared`。

    例如，以下命令启用的数据库，运行 RegisterRExt 的实例上的管理包。 如果未指定用户，则使用当前安全上下文。 

    `RegisterRExt.exe /installpkgmgmt /database:TestDB`

3. 必须为安装包的每个数据库重复执行该命令。

4.  要验证是否已成功创建新的角色，请在 SQL Server Management Studio，请单击数据库，展开**安全**，然后展开**数据库角色**。

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

4.  启用该功能后，您可以连接到服务器和安装或同步包远程，使用 R 命令。 有关此工作原理的示例，请参阅[在 SQL Server 上安装其他软件包](install-additional-r-packages-on-sql-server.md)。

## <a name="bkmk_disable"></a>禁用包管理

1.  从提升的命令提示符，RegisterRExt 实用程序再次运行，然后禁用在数据库级别的包管理：

    `RegisterRExt.exe /uninstallpkgmgmt /database:databasename [/instance:name] [/user:username] [/password:*|password]`

    此命令删除与管理包从指定的数据库相关的数据库对象。 它还会删除已从 SQL Server 计算机上的受保护的文件系统位置中安装的所有包。

2. 其中使用管理包的情况下运行此命令一次为每个数据库。 

3.  （可选）已清除所有数据库的使用上一步包后，请从提升的命令提示符运行以下命令：

    `RegisterRExt.exe /uninstallpkgmgmt [/instance:name] [/user:username] [/password:*|password]`

    此命令从实例中删除包管理功能。 你可能需要手动重新启动快速启动板服务以查看更改。

## <a name="see-also"></a>另请参阅

[SQL Server 的 R 包管理](r-package-management-for-sql-server-r-services.md)
