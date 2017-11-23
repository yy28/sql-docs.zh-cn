---
title: "还原 Master 数据库 (Analytics Platform System)"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7870021a-0d89-422e-b8ea-1cc95b45c139
caps.latest.revision: "11"
ms.openlocfilehash: ff00e17d05b13317e009357e8c2089a46cbce4a4
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="restore-the-master-database"></a>还原 Master 数据库
**还原 Master**页的 SQL Server PDW 配置管理器使你可以从备份还原 master 数据库。  
  
## <a name="before-you-begin"></a>开始之前  
  
> [!IMPORTANT]  
> 若要执行还原，SQL Server PDW 必须删除当前的 master 数据库，其中包含用户的安全信息和数据库目录。 我们建议在执行还原之前完成当前的主数据库的备份。  
  
## <a name="to-restore-the-master-database"></a>还原 master 数据库  
  
1.  启动 Configuration Manager。 有关详细信息，请参阅[启动 Configuration Manager &#40;分析平台系统 &#41;](launch-the-configuration-manager.md).  
  
2.  在配置管理器的左窗格中，单击**还原 Master**。  
  
3.  选择要还原的 master 备份。  
  
4.  单击 **“应用”**。  
  
5.  若要执行还原，SQL Server PDW 将关闭所有设备服务并断开所有用户。 还原完成后，SQL Server PDW 将重新启动设备服务。  
  
![DWConfig 设备 PDW 还原 master](./media/restore-the-master-database/SQL_Server_PDW_DWConfig_ApplPDWRestore.png "SQL_Server_PDW_DWConfig_ApplPDWRestore")  
  
