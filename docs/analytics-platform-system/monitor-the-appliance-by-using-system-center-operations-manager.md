---
title: 使用 System Center Operations Manager 监视 AP
description: 使用 System Center Operations Manager （SCOM）监视分析平台系统（AP）设备。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 539c18efe43afcf5436c6913c20cab081974b7f5
ms.sourcegitcommit: 591bbf4c7e4e2092f8abda6a2ffed263cb61c585
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/22/2020
ms.locfileid: "86941119"
---
# <a name="monitor-with-system-center-operations-manager---analytics-platform-system"></a>监视 System Center Operations Manager 分析平台系统
使用 System Center Operations Manager （SCOM）监视分析平台系统（AP）设备。
  
## <a name="before-you-begin"></a>开始之前  
  
### <a name="prerequisites"></a>先决条件  
  
1.  System Center Operations Manager 2007 R2、2012或 2012 SP1 必须安装并运行。  
  
2.  必须安装 SQL Server 2008 R2 Native Client 或 SQL Server 2012 Native Client。  
  
3.  必须安装、导入和配置要监视的管理包 SQL Server PDW。 使用以下文章来了解有关如何执行这些任务的说明。  
  
    -   [&#40;分析平台系统安装 SCOM 管理包&#41;](install-the-scom-management-packs.md)  
  
    -   [为 PDW &#40;Analytics 平台系统导入 SCOM 管理包&#41;](import-the-scom-management-pack-for-pdw.md) 
    
    -   [配置 SCOM 以监视分析平台系统 &#40;分析平台系统&#41;](configure-scom-to-monitor-analytics-platform-system.md)
  
<!-- MISSING LINKS    -   [Import the SCOM Management Pack for HDInsight &#40;Analytics Platform System&#41;](import-the-scom-management-pack-for-hdinsight.md)  -->  
   
  
## <a name="to-monitor-sql-server-pdw-with-scom"></a>用 SCOM 监视 SQL Server PDW  
配置 SCOM 管理包后，单击 SCOM 的 "监视" 窗格并向下钻取到**SQL Server "设备**"，然后**Microsoft SQL Server 并行数据仓库**"。 Microsoft SQL Server 并行数据仓库的下面有四种选择：警报、设备、设备关系图和节点。  
  
### <a name="alerts"></a>警报  
可以在 "警报" 中找到要管理的当前警报。  
  
![警报](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM.png "SCOM_SCOM")  
  
### <a name="appliances"></a>电器  
设备是在你的环境中查找当前发现和监视 SQL Server PDW 设备的位置。 如果设备未显示在此处，并且你已为其创建了 ODBC 连接，则你的 PDWWatcher 帐户可能有问题。 如果它们显示为 "未监视"，则你的 PDWMonitor 帐户可能有问题。 请耐心等待，因为 SCOM 不会实时进行更改，而是定期检查是否有新的设备监视并定期将查询发送到设备进行监视。  
  
![3400](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM2.png "SCOM_SCOM2")  
  
### <a name="appliances-diagram"></a>设备关系图  
通过 "设备关系图" 页，您可以在其中查看具有树视图的设备的运行状况：  
  
![工具关系图](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM3.png "SCOM_SCOM3")  
  
### <a name="nodes"></a>Nodes  
最后，"节点" 视图允许您通过每个节点查看设备的运行状况：  
  
![Nodes](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM4.png "SCOM_SCOM4")  
  
## <a name="see-also"></a>另请参阅  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
[了解 &#40;Analytics Platform System&#41;的管理控制台警报](understanding-admin-console-alerts.md)  
  
