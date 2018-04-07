---
title: 还原 Master 数据库 (Analytics Platform System)
author: barbkess
ms.author: barbkess
manager: craigg
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: ''
ms.component: ''
ms.technology: mpp-data-warehouse
ms.custom: ''
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7870021a-0d89-422e-b8ea-1cc95b45c139
caps.latest.revision: 11
ms.openlocfilehash: 0f1acb692198873897d5dc26e2074beab4517e44
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
# <a name="restore-the-master-database"></a>还原 Master 数据库
**还原 Master**页的 SQL Server PDW 配置管理器使你可以从备份还原 master 数据库。  
  
## <a name="before-you-begin"></a>开始之前  
  
> [!IMPORTANT]  
> 若要执行还原，SQL Server PDW 必须删除当前的 master 数据库，其中包含用户的安全信息和数据库目录。 我们建议在执行还原之前完成当前的主数据库的备份。  
  
## <a name="to-restore-the-master-database"></a>还原 master 数据库  
  
1.  启动 Configuration Manager。 有关详细信息，请参阅[启动配置管理器&#40;Analytics Platform System&#41;](launch-the-configuration-manager.md)。  
  
2.  在配置管理器的左窗格中，单击**还原 Master**。  
  
3.  选择要还原的 master 备份。  
  
4.  单击 **“应用”**。  
  
5.  若要执行还原，SQL Server PDW 将关闭所有设备服务并断开所有用户。 还原完成后，SQL Server PDW 将重新启动设备服务。  
  
![DWConfig 设备 PDW 还原 master](./media/restore-the-master-database/SQL_Server_PDW_DWConfig_ApplPDWRestore.png "SQL_Server_PDW_DWConfig_ApplPDWRestore")  
  
