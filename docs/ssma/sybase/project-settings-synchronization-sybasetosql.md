---
title: 项目设置 （同步） (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 2cd6bc01-b8e5-4312-83a4-eac66dc1d460
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 0a221d5c24606707ba9876e0980e6c28d2dacc67
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62667972"
---
# <a name="project-settings-synchronization-sybasetosql"></a>项目设置（同步）(SybaseToSQL)
同步页**项目设置**对话框中包含自定义如何 SSMA 将数据库对象，如表和存储的过程加载到设置的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure。  
  
您可以访问包含相同的设置的两个不同的同步页：  
  
-   如果你想要在指定的所有将来的 SSMA 项目设置**工具**菜单中，选择**默认项目设置**，选择为其设置所需查看或更改的迁移项目类型从**迁移目标版本**下拉列表，然后选择**同步**在左窗格的底部。  
  
-   若要在指定的当前项目中，设置**工具**菜单中，选择**项目设置**，然后选择**同步**在左窗格的底部。  
  
## <a name="options"></a>选项  
**尝试次数**  
指定加载到对象时，应使 SSMA 次数[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 对象不会加载到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中当前的尝试将重试直到 SSMA 达到当前的同步过程中最大次数。  
  
## <a name="synchronization-for-sql-server"></a>适用于 SQL Server 的同步  
**刷新本地和远程对象更改上的本地对象**  
指定是否 SSMA 应本地对象元数据将替换为远程对象的元数据是否这两个本地和远程对象更改。  
如果选择**从数据库刷新**，SSMA 将数据库定义到的元数据时加载满足的条件。  
如果选择**写入到数据库**，SSMA 将更新根据 SSMA 元数据内容数据库中的对象时满足的条件。  
如果选择**跳过**，SSMA 将不执行刷新操作。   
默认选项集是**写入数据库。**  
  
**刷新本地对象更改的本地对象**  
指定是否 SSMA 应本地对象元数据将替换为远程对象的元数据是否远程对象发生更改。  
如果选择**从数据库刷新**，SSMA 将数据库定义到的元数据时加载满足的条件。  
如果选择**写入到数据库**，SSMA 将更新根据 SSMA 元数据内容数据库中的对象时满足的条件。  
如果选择**跳过**，SSMA 将不执行刷新操作。   
默认选项集是**写入到数据库**。  
  
**刷新远程对象更改的本地对象**  
指定是否 SSMA 应本地对象元数据将替换为远程对象的元数据是否远程对象发生更改。  
如果选择**从数据库刷新**，SSMA 将数据库定义到的元数据时加载满足的条件。  
如果选择**写入到数据库**，SSMA 将更新根据 SSMA 元数据内容数据库中的对象时满足的条件。  
如果选择**跳过**，SSMA 将不执行刷新操作。   
默认选项集是**从数据库刷新**。  
  
**缺少本地对象元数据时，将刷新**  
指定是否对象存在上目标数据库，而不是本地 SSMA 是否应创建本地元数据。  
如果选择**从数据库刷新**，SSMA 数据库选项中选择刷新时满足的条件。  
如果选择**写入到数据库**，SSMA 将对象从数据库中删除时满足的条件。  
如果选择**跳过**，SSMA 将不执行刷新操作。   
默认选项集是**从数据库刷新**。  
  
