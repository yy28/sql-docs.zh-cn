---
title: "项目设置 （同步） (MySQLToSQL) |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-mysql
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
ms.assetid: 42061ff7-e6e7-497b-a0d9-440b9cf5986c
caps.latest.revision: "3"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: cc7bd0c7dce1c8ad2b70cdaa6b66ed7872c5062d
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="project-settings-synchronization-mysqltosql"></a>项目设置 （同步） (MySQLToSQL)
同步**项目设置**让你配置 MySQL 数据库对象都在与 SQL Server 数据库对象进行同步。  
  
默认操作指定默认设置，为刷新中的 MySQL 数据库的对象和与 SQL Server 数据库同步对象。 有关详细信息，请参阅[刷新从数据库 &#40;MySQLToSQL &#41;](../../ssma/mysql/refresh-from-database-mysqltosql.md)  
  
您可以访问包含相同的设置的两个不同的同步页：  
  
-   若要对指定针对所有将来的 SSMA 项目中，设置**工具**菜单上，单击**DefaultProject 设置**，然后单击**同步**在左窗格的底部。  
  
-   若要对指定为当前项目中，设置**工具**菜单上，单击**项目设置**，然后单击**同步**在左窗格的底部。  
  
## <a name="options"></a>“常规”  
  
##### <a name="misc"></a>杂项  
  
##### <a name="attempts"></a>尝试  
提供有关传递数对象需要加载到 SQL Server 的信息。 通常，在多个传递中执行加载到 SQL Server 对象。 无法加载到第一次传递，如外键中的对象可能已成功加载在下一步传递。  
  
默认值为 2。  
  
## <a name="synchronization-for-mysql"></a>有关 MySQL 的同步  
  
##### <a name="action-on-local-and-remote-object-change"></a>在本地和远程对象更改的操作  
对象定义更改在 SSMA 和数据库服务器上时，请在同步对话框中指定的默认设置。  
  
-   如果从数据库中选择刷新，SSMA 将数据库定义到元数据时加载满足的条件。  
  
-   如果你选择跳过，SSMA 将不执行任何刷新操作。  
  
##### <a name="action-on-local-object-change"></a>本地对象发生更改的操作  
SSMA 中更改对象时，请在同步对话框中指定的默认设置。  
  
-   如果你选择**从数据库刷新**，SSMA 时，会加载数据库定义到元数据满足的条件。  
  
-   如果你选择**跳过**，SSMA 将不执行任何刷新操作。  
  
##### <a name="action-on-remote-object-change"></a>远程对象更改的操作  
当对象在数据库服务器上更改，请在同步对话框中指定的默认设置。  
  
-   如果你选择**从数据库刷新**，SSMA 时，会加载数据库定义到元数据满足的条件。  
  
-   如果你选择**跳过**，SSMA 将不执行任何刷新操作。  
  
##### <a name="action-when-local-object-metadata-is-missing"></a>缺少本地对象元数据时的操作  
缺少本地元数据时，请在同步对话框中指定的默认设置。  
  
-   如果你选择**从数据库刷新**，SSMA SSMA 时，会加载数据库定义到元数据满足的条件。  
  
-   如果你选择**跳过**，SSMA 将不执行任何刷新操作  
  
## <a name="synchronization-for-sql-server"></a>SQL Server 的同步  
  
##### <a name="action-on-local-and-remote-object-change"></a>在本地和远程对象更改的操作  
对象定义更改在 SSMA 和数据库服务器上时，请在同步对话框中指定的默认设置。  
  
-   如果你选择**从数据库刷新**，SSMA 时，会加载数据库定义到元数据满足的条件。  
  
-   如果你选择**写入数据库**，SSMA 满足的条件时将更新根据 SSMA 元数据内容数据库中的对象。  
  
-   如果你选择**跳过**，SSMA 将不执行任何刷新操作。  
  
##### <a name="action-on-local-object-change"></a>本地对象发生更改的操作  
SSMA 中更改对象时，请在同步对话框中指定的默认设置。  
  
-   如果你选择**从数据库刷新**，SSMA 时，会加载数据库定义到元数据满足的条件。  
  
-   如果你选择**写入数据库**，SSMA 满足的条件时将更新根据 SSMA 元数据内容数据库中的对象。  
  
-   如果你选择**跳过**，SSMA 将不执行任何刷新操作。  
  
##### <a name="action-on-remote-object-change"></a>远程对象更改的操作  
当对象在数据库服务器上更改，请在同步对话框中指定的默认设置。  
  
-   如果你选择**从数据库刷新**，SSMA 时，会加载数据库定义到元数据满足的条件。  
  
-   如果你选择**写入数据库**，SSMA 满足的条件时将更新根据 SSMA 元数据内容数据库中的对象。  
  
-   如果你选择**跳过**，SSMA 将不执行任何刷新操作。  
  
##### <a name="action-when-local-object-metadata-is-missing"></a>缺少本地对象元数据时的操作  
缺少本地元数据时，请在同步对话框中指定的默认设置。  
  
-   如果你选择**从数据库刷新**，SSMA 将满足的条件时从数据库选项选择刷新。  
  
-   如果你选择**写入数据库**，SSMA 将对象从数据库中删除满足的条件时。  
  
-   如果你选择**跳过**，SSMA 将不执行任何刷新操作。  
  
