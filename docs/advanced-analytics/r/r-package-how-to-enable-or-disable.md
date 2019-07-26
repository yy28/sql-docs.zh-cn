---
title: 启用或禁用远程 R 包管理
description: 在 SQL Server 2016 R Services 或 SQL Server 2017 机器学习服务上启用远程 R 包管理 (数据库内)
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 9cc08b1227751559ea509838fe8fc3a446296770
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470024"
---
# <a name="enable-or-disable-remote-package-management-for-sql-server"></a>启用或禁用 SQL Server 的远程包管理
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本文介绍如何从客户端工作站或不同 Machine Learning Server 启用 R 包的远程管理。 在 SQL Server 上启用包管理功能后, 可以在客户端上使用 RevoScaleR 命令在 SQL Server 上安装包。

> [!NOTE]
> 目前支持对 R 库进行管理;针对 Python 的支持在路线图上。

默认情况下, 禁用 SQL Server 的外部包管理功能。 若要启用此功能, 必须运行一个单独的脚本, 如下一节所述。

## <a name="overview-of-process-and-tools"></a>过程和工具概述

若要启用或禁用 SQL Server 上的包管理, 请使用**RevoScaleR**包附带的命令行实用程序**registerrext.exe。**

[启用](#bkmk_enable)此功能的过程分为两个步骤: 在 SQL Server 实例上启用包管理 (每个 SQL Server 实例一次), 然后在 SQL 数据库上启用包管理 (每个 SQL Server 数据库一次)).

[禁用](#bkmk_disable)包管理功能还需要 multipel 步骤: 删除数据库级包和权限 (每个数据库一次), 然后从服务器中删除角色 (每个实例一次)。

## <a name="bkmk_enable"></a>启用包管理

1. 在 SQL Server 上, 打开提升的命令提示符, 然后导航到包含实用工具 Registerrext.exe 的文件夹。 默认位置为`<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRExe.exe`。

2. 运行以下命令, 为你的环境提供适当的参数:

    `RegisterRExt.exe /install pkgmgmt [/instance:name] [/user:username] [/password:*|password]`

    此命令在 SQL Server 计算机上创建包管理所需的实例级对象。 它还会重新启动实例的快速启动板。

    如果未指定实例, 将使用默认实例。 如果未指定用户, 则使用当前安全上下文。 例如, 以下命令在 Registerrext.exe 路径中的实例上启用包管理, 使用打开命令提示符的用户的凭据:

    `REgisterRExt.exe /install pkgmgmt`

3. 若要将包管理添加到特定数据库, 请从提升的命令提示符运行以下命令:

    `RegisterRExt.exe /install pkgmgmt /database:databasename [/instance:name] [/user:username] [/password:*|password]`
   
    此命令创建一些数据库项目, 其中包括用于控制用户权限的下列数据库角色: `rpkgs-users`、 `rpkgs-private`和`rpkgs-shared`。

    例如, 以下命令对运行 Registerrext.exe 的实例上的数据库启用包管理。 如果未指定用户, 则使用当前安全上下文。

    `RegisterRExt.exe /install pkgmgmt /database:TestDB`

4. 对必须安装包的每个数据库重复此命令。

5. 若要验证是否已成功创建新角色, 请在 SQL Server Management Studio 中单击数据库, 展开 "**安全性**", 然后展开 "**数据库角色**"。

    你还可以在 database_principals 上运行查询, 如下所示:

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

启用此功能后, 可以使用 RevoScaleR 函数从远程 R 客户端安装或卸载包。

## <a name="bkmk_disable"></a>禁用包管理

1. 从提升权限的命令提示符中, 再次运行 Registerrext.exe 实用程序, 并在数据库级别禁用包管理:

    `RegisterRExt.exe /uninstall pkgmgmt /database:databasename [/instance:name] [/user:username] [/password:*|password]`

    此命令从指定数据库中删除与包管理相关的数据库对象。 它还会从 SQL Server 计算机上的安全文件系统位置中删除已安装的所有包。

2. 对使用包管理的每个数据库重复此命令。

3.  可有可无使用上述步骤清除了所有数据库的包后, 请从提升的命令提示符运行以下命令:

    `RegisterRExt.exe /uninstall pkgmgmt [/instance:name] [/user:username] [/password:*|password]`

    此命令从实例中删除包管理功能。 你可能需要再次手动重新启动快速启动板服务以查看更改。

## <a name="next-steps"></a>后续步骤

+ [使用 RevoScaleR 安装新的 R 包](use-revoscaler-to-manage-r-packages.md)
+ [安装 R 包的提示](packages-installed-in-user-libraries.md)
+ [默认包](../package-management/default-packages.md)
