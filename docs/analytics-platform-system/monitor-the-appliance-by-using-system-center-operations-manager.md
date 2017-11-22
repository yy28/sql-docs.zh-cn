---
title: "与 System Center Operations Manager (AP) 的监视设备"
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
ms.assetid: de6cbf6e-f2e9-4877-94df-9c13b1182d56
caps.latest.revision: "14"
ms.openlocfilehash: 115d32ab8f633752dacfaf245017803bcdbfb8d3
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="monitor-the-appliance-by-using-system-center-operations-manager"></a>使用 System Center Operations Manager 来监视设备
介绍如何使用 System Center Operations Manager 来监视 SQL Server PDW 和 HDInsight。  
  
## <a name="before-you-begin"></a>开始之前  
  
### <a name="prerequisites"></a>先决条件  
  
1.  System Center Operations Manager 2007 R2、 2012年或 2012 SP1 必须已安装并且正在运行。  
  
2.  必须安装 SQL Server 2008 R2 Native Client 或 SQL Server 2012 Native Client。  
  
3.  必须安装、 导入，并配置管理包以监视 SQL Server PDW 和 HDInsight。 使用以下项作为说明来执行这些任务。  
  
    -   [安装 SCOM 管理包 &#40;分析平台系统 &#41;](install-the-scom-management-packs.md)  
  
    -   [导入 PDW &#40; 的 SCOM 管理包分析平台系统 &#41;](import-the-scom-management-pack-for-pdw.md) 
    
    -   [配置 SCOM 以便监视 Analytics Platform System &#40;分析平台系统 &#41;](configure-scom-to-monitor-analytics-platform-system.md)
  
<!-- MISSING LINKS    -   [Import the SCOM Management Pack for HDInsight &#40;Analytics Platform System&#41;](import-the-scom-management-pack-for-hdinsight.md)  -->  
   
  
## <a name="to-monitor-sql-server-pdw-with-scom"></a>若要监视 SQL Server PDW 与 SCOM  
配置 SCOM 管理包之后, 单击监视 SCOM 窗格中，然后深化至**SQL Server 设备**然后**Microsoft SQL Server 并行数据仓库**。 在 Microsoft SQL Server 并行数据仓库，下方，有四个选项： 警报、 设备、 设备图和节点。  
  
### <a name="alerts"></a>警报  
警报是可在其中找到要管理的当前警报。  
  
![警报](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM.png "SCOM_SCOM")  
  
### <a name="appliances"></a>设备  
设备是，你会发现你的环境中的当前发现和监视 SQL Server PDW 设备。 如果设备未显示在此处，并且你已创建它的 ODBC 连接，然后可能有出现错误 PDWWatcher 帐户。 如果它们显示为"未监视"可能出现错误 PDWMonitor 帐户。 请保持耐心 SCOM 不的实时，进行更改，但是定期检查新的设备，以监视和定期将查询发送到监视的设备。  
  
![设备](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM2.png "SCOM_SCOM2")  
  
### <a name="appliances-diagram"></a>设备关系图  
设备关系图页是设备的你可以查看你与树视图的运行状况：  
  
![设备图](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM3.png "SCOM_SCOM3")  
  
### <a name="nodes"></a>节点  
最后，通过节点视图可查看你的设备通过每个节点的运行状况：  
  
![节点](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM4.png "SCOM_SCOM4")  
  
## <a name="see-also"></a>另请参阅  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
[了解管理控制台警报 &#40;分析平台系统 &#41;](understanding-admin-console-alerts.md)  
  
