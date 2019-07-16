---
title: 还原 master 数据库的分析平台系统 |Microsoft Docs
description: 还原 master 数据库分析平台系统中。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 7c9931ab6fb0946de83c3113a36de723a7a05cd0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67960130"
---
# <a name="restore-the-master-database-in-analytics-platform-system"></a>还原 master 数据库中分析平台系统
**还原 Master**页的 SQL Server PDW 配置管理器使你可以从备份还原 master 数据库。  
  
## <a name="before-you-begin"></a>开始之前  
  
> [!IMPORTANT]  
> 若要执行还原，SQL Server PDW 必须删除当前的 master 数据库，其中包含用户的安全信息和数据库目录。 我们建议在执行还原之前制作当前主数据库的备份。  
  
## <a name="to-restore-the-master-database"></a>还原 master 数据库  
  
1.  启动配置管理器。 有关详细信息，请参阅[启动配置管理器&#40;Analytics Platform System&#41;](launch-the-configuration-manager.md)。  
  
2.  在配置管理器的左窗格中，单击**还原 Master**。  
  
3.  选择要还原的 master 备份。  
  
4.  单击 **“应用”** 。  
  
5.  若要执行还原，SQL Server PDW 将关闭所有的设备服务并断开所有用户的都连接。 在还原完成后，SQL Server PDW 将重新启动设备服务。  
  
![DWConfig 工具 PDW 还原 master](./media/restore-the-master-database/SQL_Server_PDW_DWConfig_ApplPDWRestore.png "SQL_Server_PDW_DWConfig_ApplPDWRestore")  
  
