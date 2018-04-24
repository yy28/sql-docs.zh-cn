---
title: 具有 SCOM-分析平台系统监视器，|Microsoft 文档
description: 使用 System Center Operations Manager (SCOM) 来监视分析平台系统 (AP) 设备。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: c2b26462ab37cf7d63960ff7db6e20c57e8290bb
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/19/2018
---
# <a name="monitor-with-system-center-operations-manager---analytics-platform-system"></a>与 System Center Operations Manager-分析平台系统监视器
使用 System Center Operations Manager (SCOM) 来监视分析平台系统 (AP) 设备。
  
## <a name="before-you-begin"></a>开始之前  
  
### <a name="prerequisites"></a>必要條件  
  
1.  System Center Operations Manager 2007 R2、 2012年或 2012 SP1 必须已安装并且正在运行。  
  
2.  必须安装 SQL Server 2008 R2 Native Client 或 SQL Server 2012 Native Client。  
  
3.  必须安装、 导入，并配置管理包以监视 SQL Server PDW 和 HDInsight。 使用以下文章获得说明来执行这些任务。  
  
    -   [安装 SCOM 管理包&#40;分析平台系统&#41;](install-the-scom-management-packs.md)  
  
    -   [导入 PDW SCOM 管理包&#40;分析平台系统&#41;](import-the-scom-management-pack-for-pdw.md) 
    
    -   [配置 SCOM 以便监视 Analytics Platform System&#40;分析平台系统&#41;](configure-scom-to-monitor-analytics-platform-system.md)
  
<!-- MISSING LINKS    -   [Import the SCOM Management Pack for HDInsight &#40;Analytics Platform System&#41;](import-the-scom-management-pack-for-hdinsight.md)  -->  
   
  
## <a name="to-monitor-sql-server-pdw-with-scom"></a>若要监视 SQL Server PDW 与 SCOM  
配置 SCOM 管理包之后, 单击监视 SCOM 窗格中，然后深化至**SQL Server 设备**然后**Microsoft SQL Server 并行数据仓库**。 在 Microsoft SQL Server 并行数据仓库，下方，有四个选项： 警报、 设备、 设备图和节点。  
  
### <a name="alerts"></a>警报  
警报是可在其中找到要管理的当前警报。  
  
![警报](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM.png "SCOM_SCOM")  
  
### <a name="appliances"></a>设备  
设备是，你会发现你的环境中的当前发现和监视 SQL Server PDW 设备。 如果设备未显示在此处，并且你已创建它的 ODBC 连接，然后可能有出现错误 PDWWatcher 帐户。 如果它们显示为"未监视"，可能有出现错误 PDWMonitor 帐户。 请耐心等待，因为 SCOM 不的实时，进行更改，但会定期检查用于新设备的监视和定期将查询发送到监视的设备。  
  
![设备](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM2.png "SCOM_SCOM2")  
  
### <a name="appliances-diagram"></a>设备关系图  
设备关系图页是设备的你可以查看你与树视图的运行状况：  
  
![设备图](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM3.png "SCOM_SCOM3")  
  
### <a name="nodes"></a>节点  
最后，通过节点视图可查看你的设备通过每个节点的运行状况：  
  
![Nodes](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM4.png "SCOM_SCOM4")  
  
## <a name="see-also"></a>另请参阅  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
[了解管理控制台警报&#40;分析平台系统&#41;](understanding-admin-console-alerts.md)  
  
