---
title: 还原 master 数据库
description: 在分析平台系统（AP）中还原 master 数据库。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 6d122881f5283da86f66494ee2f049756d151551
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/22/2019
ms.locfileid: "74400455"
---
# <a name="restore-the-master-database-in-analytics-platform-system-aps"></a>在分析平台系统（AP）中还原 master 数据库
使用 SQL Server PDW Configuration Manager 的**还原母版页**，可以从备份中还原 Master 数据库。  
  
## <a name="before-you-begin"></a>开始之前  
  
> [!IMPORTANT]  
> 若要执行还原，SQL Server PDW 必须删除当前的 master 数据库，其中包含用户安全信息和数据库目录。 建议在执行还原之前备份当前的 master 数据库。  
  
## <a name="to-restore-the-master-database"></a>还原 master 数据库  
  
1.  启动 Configuration Manager。 有关详细信息，请参阅[启动 Configuration Manager &#40;Analytics 平台系统&#41;](launch-the-configuration-manager.md)。  
  
2.  在 Configuration Manager 的左窗格中，单击 "**还原 Master**"。  
  
3.  选择要还原的主备份。  
  
4.  单击 **“应用”**。  
  
5.  若要执行还原，SQL Server PDW 会关闭所有设备服务并断开所有用户的连接。 还原完成后，SQL Server PDW 将重新启动设备服务。  
  
![DWConfig 工具 PDW 还原 Master](./media/restore-the-master-database/SQL_Server_PDW_DWConfig_ApplPDWRestore.png "SQL_Server_PDW_DWConfig_ApplPDWRestore")  
  
