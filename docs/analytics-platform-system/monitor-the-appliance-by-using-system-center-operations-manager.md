---
title: 使用 SCOM 的分析平台系统监视 |Microsoft Docs
description: 使用 System Center Operations Manager (SCOM) 以监视 Analytics Platform System (APS) 设备。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 0da122b7ff4f17621a896e3a9f5076f8564d32c8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67960541"
---
# <a name="monitor-with-system-center-operations-manager---analytics-platform-system"></a>使用 System Center Operations Manager 的分析平台系统监视器
使用 System Center Operations Manager (SCOM) 以监视 Analytics Platform System (APS) 设备。
  
## <a name="before-you-begin"></a>开始之前  
  
### <a name="prerequisites"></a>先决条件  
  
1.  System Center Operations Manager 2007 R2、 2012年或 2012 SP1 必须安装并正在运行。  
  
2.  必须安装 SQL Server 2008 R2 Native Client 或 SQL Server 2012 Native Client。  
  
3.  必须安装、 导入，并配置要监视 SQL Server PDW 的管理包。 使用以下文章获得说明来执行这些任务。  
  
    -   [安装 SCOM 管理包&#40;分析平台系统&#41;](install-the-scom-management-packs.md)  
  
    -   [SCOM 管理包为 PDW 导入&#40;分析平台系统&#41;](import-the-scom-management-pack-for-pdw.md) 
    
    -   [配置 SCOM 以监视 Analytics Platform System&#40;分析平台系统&#41;](configure-scom-to-monitor-analytics-platform-system.md)
  
<!-- MISSING LINKS    -   [Import the SCOM Management Pack for HDInsight &#40;Analytics Platform System&#41;](import-the-scom-management-pack-for-hdinsight.md)  -->  
   
  
## <a name="to-monitor-sql-server-pdw-with-scom"></a>监视 SQL Server PDW scom  
配置 SCOM 管理包之后, 监视 SCOM 窗格中单击，然后向下钻取**SQL Server 装置**，然后**Microsoft SQL Server 并行数据仓库**。 Microsoft SQL Server 并行数据仓库，下方有四个选项：警报、 设备、 设备图和节点。  
  
### <a name="alerts"></a>警报  
警报是在哪里可以找到要管理的当前警报。  
  
![警报](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM.png "SCOM_SCOM")  
  
### <a name="appliances"></a>设备  
您将在你的环境中发现当前发现和监视 SQL Server PDW 设备了设备。 如果设备未在此处显示，并且已创建的 ODBC 连接，然后可能有 PDWWatcher 帐户出现了一些问题。 如果它们显示为"未监视"，可能有 PDWMonitor 帐户出现了一些问题。 请耐心等待，因为 SCOM 不在真实时间中进行更改，但会定期检查新设备来监视并定期将查询发送到监视的设备。  
  
![装置](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM2.png "SCOM_SCOM2")  
  
### <a name="appliances-diagram"></a>工具关系图  
设备关系图页是设备的您可以查看你的树视图的运行状况：  
  
![工具关系图](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM3.png "SCOM_SCOM3")  
  
### <a name="nodes"></a>节点  
最后，通过节点视图可查看你的设备通过每个节点的运行状况：  
  
![Nodes](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM4.png "SCOM_SCOM4")  
  
## <a name="see-also"></a>请参阅  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
[了解管理控制台警报&#40;分析平台系统&#41;](understanding-admin-console-alerts.md)  
  
