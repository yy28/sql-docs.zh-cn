---
title: "启用或禁用对 SQL Server 的 R 包管理 |Microsoft 文档"
ms.custom: 
ms.date: 10/05/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6e384893-04da-43f9-b100-bfe99888f085
caps.latest.revision: 7
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 29122bdf543e82c1f429cf401b5fe1d8383515fc
ms.openlocfilehash: 88337da76b3a44b9dc797fd1d9f187bfda7396c8
ms.contentlocale: zh-cn
ms.lasthandoff: 10/10/2017

---
# <a name="enable-or-disable-r-package-management-for-sql-server"></a>启用或禁用对 SQL Server 的 R 包管理

本文介绍了启用或禁用 SQL Server 自 2017 年中的新包管理功能的过程。 此功能允许数据库管理员控制的实例上的包安装。 功能依赖于新的数据库角色来向用户授予能够安装所需的 R 包或与其他用户共享包。

默认情况下，禁用 SQL Server 的外部包管理功能，即使安装了机器学习功能。

到[启用](#bkmk_enable)此功能有两个步骤，并且需要安装数据库管理员的一些帮助：

1.  在 SQL Server 实例上启用包管理（每个 SQL Server 实例一次）

2.  在 SQL 数据库上启用包管理（每个 SQL Server 数据库一次）

到[禁用](#bkmk_disable)包管理功能，可回退该过程，以删除数据库级包和权限，，然后从服务器删除角色：

1.  在每个数据库上禁用包管理（每个数据库一次）

2.  在 SQL Server 实例上禁用包管理（每个实例一次）

## <a name="bkmk_enable"></a>启用包管理

若要启用或禁用管理包，需要命令行实用工具**RegisterRExt.exe**，包含在**RevoScaleR**包。

1. 打开提升的命令提示符并导航到包含的实用工具，RegisterRExt.exe 的文件夹。 默认位置是`<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRExe.exe`。

2. 运行以下命令，提供你的环境的相应参数：

    `RegisterRExt.exe /installpkgmgmt [/instance:name] [/user:username] [/password:*|password]`

    此命令所需的管理包的 SQL Server 计算机上创建实例级对象。 它还会重新启动实例快速启动板。

    如果未指定实例，则使用默认实例。

    如果未指定用户，则使用当前安全上下文。

2.  若要添加在数据库级别的管理包，请从提升的命令提示符运行以下命令：

    `RegisterRExt.exe /installpkgmgmt /database:databasename [/instance:name] [/user:username] [/password:*|password]`
   
    此命令创建某些数据库项目，包括用于控制用户权限的以下数据库角色： `rpkgs-users`， `rpkgs-private`，和`rpkgs-shared`。

    如果未指定用户，则使用当前安全上下文。

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

4.  启用该功能后，可以使用具有适当权限的任何用户[创建外部库](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql)T-SQL 添加包中的语句。 有关此工作原理的示例，请参阅[在 SQL Server 上安装其他软件包](install-additional-r-packages-on-sql-server.md)。

## <a name="bkmk_disable"></a>禁用包管理

1.  在提升的命令提示符下，运行以下命令以禁用数据库级别上的包管理：

    `RegisterRExt.exe /uninstallpkgmgmt /database:databasename [/instance:name] [/user:username] [/password:*|password]`

    其中使用管理包的情况下运行此命令一次为每个数据库。 此命令将删除与管理包从指定的数据库相关的数据库对象。 它还将删除从 SQL Server 计算机上的受保护的文件系统位置安装的所有包。

2.  （可选）已清除所有数据库的使用上一步包后，请从提升的命令提示符运行以下命令：

    `RegisterRExt.exe /uninstallpkgmgmt [/instance:name] [/user:username] [/password:*|password]`

    此命令从实例中删除包管理功能。

## <a name="see-also"></a>另请参阅

[SQL Server 的 R 包管理](r-package-management-for-sql-server-r-services.md)
