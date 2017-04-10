---
title: "如何启用或禁用 R 包管理 | Microsoft Docs"
ms.custom: ""
ms.date: "12/22/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 6e384893-04da-43f9-b100-bfe99888f085
caps.latest.revision: 7
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
---
# 如何启用或禁用 R 包管理

即使安装了 R Services，默认情况下，SQL Server 实例上也会禁用包管理。 若要启用此功能，需要两个步骤，整个过程必须由数据库管理员执行： 

1. 在 SQL Server 实例上启用包管理（每个 SQL Server 实例一次） 
2. 在 SQL 数据库上启用包管理（每个 SQL Server 数据库一次） 


如果禁用包管理功能，则反向执行此过程，删除数据库级的包和权限，然后从服务器删除角色：
 
1. 在每个数据库上禁用包管理（每个数据库一次） 
2. 在 SQL Server 实例上禁用包管理（每个实例一次） 

> [!IMPORTANT]
> 此功能处于开发阶段。 请注意，更高版本中的语法或功能可能会发生改变。 

### <a name="to-enable-package-management"></a>启用包管理

若要启用或禁用包管理，需要命令行实用程序 **RegisterRExt.exe**，它包括在与 SQL Server R Services 一起安装的 **RevoScaleR** 包中。 默认位置是：

`<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRExe.exe` 
    
1. 打开提升的命令提示符，并使用以下命令：

    `RegisterRExt.exe /installpkgmgmt [/instance:name] [/user:username] [/password:*|password]`

    此命令在包管理所需的 SQL Server 计算机上创建实例级的项目。 

2. 若要在数据库级别上添加包管理，针对每个必须安装包的数据库，请在提升的命令提示符下运行以下命令： 

    `RegisterRExt.exe /installpkgmgmt /database:databasename [/instance:name] [/user:username] [/password:*|password]` 

    此命令将创建一些数据库项目，包括控制用户权限所需的以下数据库角色：**rpkgs-users**、**rpkgs-private** 和 **rpkgs-shared** 

### <a name="to-disable-package-management"></a>禁用包管理 

1. 在提升的命令提示符下，运行以下命令以禁用数据库级别上的包管理：

   `RegisterRExt.exe /uninstallpkgmgmt /database:databasename [/instance:name] [/user:username] [/password:*|password]` 

    此命令将从指定数据库中删除与包管理相关的数据库项目。  此命令还将从 SQL Server 计算机的受保护文件系统位置中，删除每个数据库安装的所有包。
    
    必须在使用包管理的每个数据库上运行一次该命令。
 
2. （可选）若要从实例中完全删除包管理功能，使用前面的步骤清除所有数据库中的包之后，请在提升的命令提示符下运行以下命令：

    `RegisterRExt.exe /uninstallpkgmgmt [/instance:name] [/user:username] [/password:*|password]`

    此命令将从 SQL Server 实例中删除用于包管理的实例级项目。 


## <a name="see-also"></a>另请参阅
[SQL Server R Services 的 R 包管理](../../advanced-analytics/r-services/r-package-management-for-sql-server-r-services.md)