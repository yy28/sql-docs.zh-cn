---
title: 项目设置 （同步） (MySQLToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 42061ff7-e6e7-497b-a0d9-440b9cf5986c
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: e82fa9d02fdbfe876f4097c54c6877c3a3a81fee
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62473903"
---
# <a name="project-settings-synchronization-mysqltosql"></a>项目设置（同步）(MySQLToSQL)
同步**项目设置**使您可以配置 MySQL 数据库对象的 SQL Server 数据库对象的同步方式。  
  
刷新对象从 MySQL 数据库和 SQL Server 数据库与同步对象，则默认操作指定默认设置。 有关详细信息，请参阅[从数据库刷新&#40;MySQLToSQL&#41;](../../ssma/mysql/refresh-from-database-mysqltosql.md)  
  
您可以访问包含相同的设置的两个不同的同步页：  
  
-   若要在指定的所有将来的 SSMA 项目设置**工具**菜单中，单击**DefaultProject 设置**，然后单击**同步**在左窗格的底部。  
  
-   若要在指定的当前项目中，设置**工具**菜单中，单击**项目设置**，然后单击**同步**在左窗格的底部。  
  
## <a name="options"></a>选项  
  
##### <a name="misc"></a>杂项  
  
##### <a name="attempts"></a>尝试次数  
提供有关若干传递对象加载到 SQL Server 所需的信息。 在多个传递中通常执行加载到 SQL Server 对象。 无法加载在第一次传递，如外键中的对象可能会成功加载下一步中。  
  
默认值为 2。  
  
## <a name="synchronization-for-mysql"></a>用于 MySQL 的同步  
  
##### <a name="action-on-local-and-remote-object-change"></a>在本地和远程对象更改的操作  
对象定义更改在 SSMA 中和在数据库服务器上时，请在同步对话框中指定的默认设置。  
  
-   如果从数据库中选择刷新，SSMA 将数据库定义到的元数据时加载满足的条件。  
  
-   如果选择跳过，SSMA 将不执行刷新操作。  
  
##### <a name="action-on-local-object-change"></a>在本地对象发生更改的操作  
在 SSMA 中的对象发生更改时，请在同步对话框中指定的默认设置。  
  
-   如果选择**从数据库刷新**，SSMA 将数据库定义到的元数据时加载满足的条件。  
  
-   如果选择**跳过**，SSMA 将不执行刷新操作。  
  
##### <a name="action-on-remote-object-change"></a>在远程对象更改的操作  
在同步对话框中指定的默认设置，当数据库服务器上更改对象。  
  
-   如果选择**从数据库刷新**，SSMA 将数据库定义到的元数据时加载满足的条件。  
  
-   如果选择**跳过**，SSMA 将不执行刷新操作。  
  
##### <a name="action-when-local-object-metadata-is-missing"></a>缺少本地对象元数据时执行的操作  
缺少本地元数据时，请在同步对话框中指定的默认设置。  
  
-   如果选择**从数据库刷新**，SSMA 将数据库定义到的元数据时加载满足的条件。  
  
-   如果选择**跳过**，SSMA 将不执行刷新操作  
  
## <a name="synchronization-for-sql-server"></a>适用于 SQL Server 的同步  
  
##### <a name="action-on-local-and-remote-object-change"></a>在本地和远程对象更改的操作  
对象定义更改在 SSMA 中和在数据库服务器上时，请在同步对话框中指定的默认设置。  
  
-   如果选择**从数据库刷新**，SSMA 将数据库定义到的元数据时加载满足的条件。  
  
-   如果选择**写入到数据库**，SSMA 将更新根据 SSMA 元数据内容数据库中的对象时满足的条件。  
  
-   如果选择**跳过**，SSMA 将不执行刷新操作。  
  
##### <a name="action-on-local-object-change"></a>在本地对象发生更改的操作  
在 SSMA 中的对象发生更改时，请在同步对话框中指定的默认设置。  
  
-   如果选择**从数据库刷新**，SSMA 将数据库定义到的元数据时加载满足的条件。  
  
-   如果选择**写入到数据库**，SSMA 将更新根据 SSMA 元数据内容数据库中的对象时满足的条件。  
  
-   如果选择**跳过**，SSMA 将不执行刷新操作。  
  
##### <a name="action-on-remote-object-change"></a>在远程对象更改的操作  
在同步对话框中指定的默认设置，当数据库服务器上更改对象。  
  
-   如果选择**从数据库刷新**，SSMA 将数据库定义到的元数据时加载满足的条件。  
  
-   如果选择**写入到数据库**，SSMA 将更新根据 SSMA 元数据内容数据库中的对象时满足的条件。  
  
-   如果选择**跳过**，SSMA 将不执行刷新操作。  
  
##### <a name="action-when-local-object-metadata-is-missing"></a>缺少本地对象元数据时执行的操作  
缺少本地元数据时，请在同步对话框中指定的默认设置。  
  
-   如果选择**从数据库刷新**，SSMA 数据库选项中选择刷新时满足的条件。  
  
-   如果选择**写入到数据库**，SSMA 将对象从数据库中删除时满足的条件。  
  
-   如果选择**跳过**，SSMA 将不执行刷新操作。  
  
