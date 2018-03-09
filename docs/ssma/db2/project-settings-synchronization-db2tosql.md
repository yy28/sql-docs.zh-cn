---
title: "项目 Settings(Synchronization) (DB2ToSQL) |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-db2
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: a5629a72-8c17-46a4-bb4d-19d51a0b98a2
caps.latest.revision: "4"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9a701544d5f7d111d234b4a87def52beb3e1edbd
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="project-settingssynchronization-db2tosql"></a>项目 Settings(Synchronization) (DB2ToSQL)
同步页**项目设置**对话框中包含自定义如何 SSMA 加载和刷新到数据库对象，如表和存储的过程，设置[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
默认操作选项指定默认设置，用于刷新从 DB2 数据库的对象和与 SQL Server 数据库同步对象。 有关详细信息，请参阅[刷新从数据库 &#40; DB2ToSQL &#41;](../../ssma/db2/refresh-from-database-db2tosql.md)。  
  
您可以访问包含相同的设置的两个不同的同步页：  
  
-   若要对指定针对所有将来的 SSMA 项目中，设置**工具**菜单上，单击**默认项目设置**，然后单击**同步**在左窗格的底部。  
  
-   若要对指定为当前项目中，设置**工具**菜单上，单击**项目设置**，然后单击**同步**在左窗格的底部。  
  
## <a name="miscellaneous-options"></a>其他选项  
**尝试**  
指定的 SSMA 应加载到对象时的尝试次数[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 不会加载到的对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]中当前的尝试将重试直到 SSMA 达到当前的同步过程中最大次数。 设置默认值是**2**  
  
## <a name="synchronization-for-db2-options"></a>DB2 选项的同步  
**在本地和远程对象更改的操作**  
对象定义更改在 SSMA 和数据库服务器上时，请在同步对话框中指定的默认设置。 设置默认值是**从数据库刷新**。  
  
-   如果你选择**从数据库刷新**，SSMA 时，会加载数据库定义到元数据满足的条件。  
  
-   如果你选择**跳过**，SSMA 将不执行任何刷新操作。  
  
**本地对象发生更改的操作**  
SSMA 中更改对象时，请在同步对话框中指定的默认设置。 设置默认值是**跳过**。  
  
-   如果你选择**从数据库刷新**，SSMA 时，会加载数据库定义到元数据满足的条件。  
  
-   如果你选择**跳过**，SSMA 将不执行任何刷新操作。  
  
**远程对象更改的操作**  
当对象在数据库服务器上更改，请在同步对话框中指定的默认设置。 设置默认值是**从数据库刷新**。  
  
-   如果你选择**从数据库刷新**，SSMA 时，会加载数据库定义到元数据满足的条件。  
  
-   如果你选择**跳过**，SSMA 将不执行任何刷新操作。  
  
**缺少本地对象元数据时的操作**  
缺少本地元数据时，请在同步对话框中指定的默认设置。 设置默认值是**从数据库刷新**。  
  
-   如果你选择**从数据库刷新**，SSMA SSMA 时，会加载数据库定义到元数据满足的条件。  
  
-   如果你选择**跳过**，SSMA 将不执行任何刷新操作。  
  
## <a name="synchronization-for-sql-server-options"></a>SQL Server 选项的同步  
**在本地和远程对象更改的操作**  
对象定义更改在 SSMA 和数据库服务器上时，请在同步对话框中指定的默认设置。 设置默认值是**写入数据库**。  
  
-   如果你选择**从数据库刷新**，SSMA 时，会加载数据库定义到元数据满足的条件。  
  
-   如果你选择**写入数据库**，SSMA 满足的条件时将更新根据 SSMA 元数据内容数据库中的对象。  
  
-   如果你选择**跳过**，SSMA 将不执行任何刷新操作。  
  
**本地对象发生更改的操作**  
SSMA 中更改对象时，请在同步对话框中指定的默认设置。 设置默认值是**写入数据库**。  
  
-   如果你选择**从数据库刷新**，SSMA 时，会加载数据库定义到元数据满足的条件。  
  
-   如果你选择**写入数据库**，SSMA 满足的条件时将更新根据 SSMA 元数据内容数据库中的对象。  
  
-   如果你选择**跳过**，SSMA 将不执行任何刷新操作。  
  
**远程对象更改的操作**  
当对象在数据库服务器上更改，请在同步对话框中指定的默认设置。  设置默认值是**从数据库刷新**。  
  
-   如果你选择**从数据库刷新**，SSMA 时，会加载数据库定义到元数据满足的条件。  
  
-   如果你选择**写入数据库**，SSMA 满足的条件时将更新根据 SSMA 元数据内容数据库中的对象。  
  
-   如果你选择**跳过**，SSMA 将不执行任何刷新操作。  
  
**缺少本地对象元数据时的操作**  
缺少本地元数据时，请在同步对话框中指定的默认设置。 设置默认值是**从数据库刷新**。  
  
-   如果你选择**从数据库刷新**，SSMA 选择**从数据库刷新**选项时满足的条件。  
  
-   如果你选择**写入数据库**，SSMA 将对象从数据库中删除满足的条件时。  
  
-   如果你选择**跳过**，SSMA 将不执行任何刷新操作。  
  
