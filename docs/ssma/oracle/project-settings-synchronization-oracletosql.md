---
title: "项目 Settings(Synchronization) (OracleToSQL) |Microsoft 文档"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e223fb7d-05ec-4fa5-8973-d845c33a23dd
caps.latest.revision: 5
author: sabotta
ms.author: carlasab
manager: v-thobro
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 40e18de9f96f69472fc3fb7b8720a0abdb27d2fb
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="project-settingssynchronization-oracletosql"></a>项目 Settings(Synchronization) (OracleToSQL)
同步页**项目设置**对话框中包含自定义如何 SSMA 加载和刷新到数据库对象，如表和存储的过程，设置[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
默认操作选项指定默认设置，用于刷新 Oracle 数据库中的对象以及用于与 SQL Server 数据库进行同步对象。 有关详细信息，请参阅[刷新从数据库的 Oracle](../../ssma/oracle/refresh-from-database-oracletosql.md)。  
  
您可以访问包含相同的设置的两个不同的同步页：  
  
-   若要对指定针对所有将来的 SSMA 项目中，设置**工具**菜单上，单击**默认项目设置**，然后单击**同步**在左窗格的底部。  
  
-   若要对指定为当前项目中，设置**工具**菜单上，单击**项目设置**，然后单击**同步**在左窗格的底部。  
  
## <a name="miscellaneous-options"></a>其他选项  
**尝试**  
指定的 SSMA 应加载到对象时的尝试次数[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 不会加载到的对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]中当前的尝试将重试直到 SSMA 达到当前的同步过程中最大次数。 设置默认值是**2**  
  
## <a name="synchronization-for-oracle-options"></a>有关 Oracle 选项的同步  
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
  

