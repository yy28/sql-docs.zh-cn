---
title: 还原 master 数据库的分析平台系统 |Microsoft 文档
description: 还原分析平台系统中的主数据库。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 184184f332225e76e152c2d909cfff788b4fea91
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/19/2018
---
# <a name="restore-the-master-database-in-analytics-platform-system"></a>还原 master 数据库中分析平台系统
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
  
