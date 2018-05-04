---
title: 项目设置 （同步） (SybaseToSQL) |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-sybase
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 2cd6bc01-b8e5-4312-83a4-eac66dc1d460
caps.latest.revision: 3
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 0bbbe5982ced12fddabe3fd0a6ce629e0cc10c03
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="project-settings-synchronization-sybasetosql"></a>项目设置 （同步） (SybaseToSQL)
同步页**项目设置**对话框中包含自定义 SSMA 如何将数据库对象，如表和存储的过程加载到设置的[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。  
  
您可以访问包含相同的设置的两个不同的同步页：  
  
-   如果你想要对指定针对所有将来的 SSMA 项目中，设置**工具**菜单上，选择**默认项目设置**，选择为其设置所需查看或更改，不再是迁移项目类型**迁移目标版本**下拉列表中，然后选择**同步**在左窗格的底部。  
  
-   若要对指定为当前项目中，设置**工具**菜单上，选择**项目设置**，然后选择**同步**在左窗格的底部。  
  
## <a name="options"></a>选项  
**尝试**  
指定的 SSMA 应加载到对象时的尝试次数[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 不会加载到的对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]中当前的尝试将重试直到 SSMA 达到当前的同步过程中最大次数。  
  
## <a name="synchronization-for-sql-server"></a>SQL Server 的同步  
**刷新本地和远程对象更改上的本地对象**  
指定是否 SSMA 应将本地对象的元数据和远程对象元数据一起是否本地和远程对象更改。  
如果你选择**从数据库刷新**，SSMA 时，会加载数据库定义到元数据满足的条件。  
如果你选择**写入数据库**，SSMA 满足的条件时将更新根据 SSMA 元数据内容数据库中的对象。  
如果你选择**跳过**，SSMA 将不执行任何刷新操作。   
默认选项集是**写入数据库。**  
  
**刷新本地对象更改上的本地对象**  
指定是否 SSMA 应将本地对象的元数据和远程对象元数据一起是否远程对象更改。  
如果你选择**从数据库刷新**，SSMA 时，会加载数据库定义到元数据满足的条件。  
如果你选择**写入数据库**，SSMA 满足的条件时将更新根据 SSMA 元数据内容数据库中的对象。  
如果你选择**跳过**，SSMA 将不执行任何刷新操作。   
默认选项集是**写入数据库**。  
  
**刷新远程对象更改上的本地对象**  
指定是否 SSMA 应将本地对象的元数据和远程对象元数据一起是否远程对象更改。  
如果你选择**从数据库刷新**，SSMA 时，会加载数据库定义到元数据满足的条件。  
如果你选择**写入数据库**，SSMA 满足的条件时将更新根据 SSMA 元数据内容数据库中的对象。  
如果你选择**跳过**，SSMA 将不执行任何刷新操作。   
默认选项集是**从数据库刷新**。  
  
**缺少本地对象元数据时的刷新**  
指定是否在目标数据库中，而不是本地存在的对象，SSMA 是否应创建本地元数据。  
如果你选择**从数据库刷新**，SSMA 将满足的条件时从数据库选项选择刷新。  
如果你选择**写入数据库**，SSMA 将对象从数据库中删除满足的条件时。  
如果你选择**跳过**，SSMA 将不执行任何刷新操作。   
默认选项集是**从数据库刷新**。  
  
