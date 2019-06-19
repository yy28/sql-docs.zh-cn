---
title: 项目设置 （加载对象） (AccessToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 9ec1c1e8-a3e1-4e81-bf49-631f87daa209
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 90a47a7586d0f3c6b5bd0fee28ed01f3b292a92e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63299459"
---
# <a name="project-settings-loading-objects-accesstosql"></a>项目设置 （加载对象） (AccessToSQL)
正在加载对象项目设置允许你配置的 SQL Server 数据库对象访问数据库对象的同步方式。  
  
刷新访问数据库中的对象以及与 SQL Server 数据库同步对象，则默认操作指定默认设置。 有关详细信息，请参阅[从数据库刷新&#40;AccessToSQL&#41;](../../ssma/access/refresh-from-database-accesstosql.md)  
  
您可以访问包含相同的设置的两个不同的同步页：  
  
-   在指定的所有将来的 SSMA 项目设置**工具**菜单中，单击**DefaultProject 设置**，然后单击**加载对象**在左窗格的底部。  
  
-   若要在指定的当前项目中，设置**工具**菜单中，单击**项目设置**，然后单击**加载对象**在左窗格的底部。  
  
## <a name="options"></a>选项  
  
##### <a name="misc"></a>杂项  
  
##### <a name="attempts"></a>尝试次数  
提供有关若干传递对象加载到 SQL Server 所需的信息。 在多个传递中通常执行加载到 SQL Server 对象。 无法加载在第一次传递，如外键中的对象可能会成功加载下一步中。  
  
默认值为 2。  
  
## <a name="synchronization-for-sql-server"></a>适用于 SQL Server 的同步  
  
##### <a name="default-action-on-local-and-remote-object-change"></a>在本地和远程对象更改的默认操作  
对象定义更改在 SSMA 中和在数据库服务器上时，请在同步对话框中指定的默认设置。  
  
-   如果选择**从数据库刷新**，SSMA 将数据库定义到的元数据时加载满足的条件。  
  
-   如果选择**写入到数据库**，SSMA 将更新根据 SSMA 元数据内容数据库中的对象时满足的条件。  
  
-   如果选择**跳过**，SSMA 将不执行刷新操作。  
  
##### <a name="default-action-on-local-object-change"></a>在本地对象发生更改的默认操作  
在 SSMA 中的对象发生更改时，请在同步对话框中指定的默认设置。  
  
-   如果选择**从数据库刷新**，SSMA 将数据库定义到的元数据时加载满足的条件。  
  
-   如果选择**写入到数据库**，SSMA 将更新根据 SSMA 元数据内容数据库中的对象时满足的条件。  
  
-   如果选择**跳过**，SSMA 将不执行刷新操作。  
  
##### <a name="default-action-on-remote-object-change"></a>在远程对象更改的默认操作  
在同步对话框中指定的默认设置，当数据库服务器上更改对象。  
  
-   如果选择**从数据库刷新**，SSMA 将数据库定义到的元数据时加载满足的条件。  
  
-   如果选择**写入到数据库**，SSMA 将更新根据 SSMA 元数据内容数据库中的对象时满足的条件。  
  
-   如果选择**跳过**，SSMA 将不执行刷新操作。  
  
##### <a name="default-action-when-local-object-metadata-is-missing"></a>缺少本地对象元数据时的默认操作  
缺少本地元数据时，请在同步对话框中指定的默认设置。  
  
-   如果选择**从数据库刷新**，SSMA 数据库选项中选择刷新时满足的条件。  
  
-   如果选择**写入到数据库**，SSMA 将对象从数据库中删除时满足的条件。  
  
-   如果选择**跳过**，SSMA 将不执行刷新操作。  
  
