---
title: "更改时区和报表服务器上的时钟设置 |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- time zones [Reporting Services]
- clocks [Reporting Services]
- schedules [Reporting Services], clock settings
- schedules [Reporting Services], time zones
ms.assetid: 69a19468-baa1-40f6-b158-8afdab0f8968
caps.latest.revision: 22
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 79f8068d11d707c4b0237d32e1645a80a12cdbbb
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="change-time-zones-and-clock-settings-on-a-report-server"></a>更改报表服务器上的时区和时钟设置
  报表服务器始终使用其所在计算机的本地时间。 您不能将它配置为使用其他时区。 如果客户端应用程序指向位于其他时区中的报表服务器，则将按该报表服务器所在时区的时间来执行计划操作。 在报表管理器和 SharePoint 管理页中，每个计划页上都标有时区，这样您可以确切知道执行计划操作的时间。 例如，用于创建自定义计划的页将注明“时间用 (UTC-08:00) 太平洋时间（美国和加拿大）来表示”。  
  
## <a name="changing-the-time-zone-native-mode"></a>更改时区（本机模式）  
 如果更改承载报表服务器的计算机的时区，必须重新启动报表服务器服务才能使时区更改生效。  
  
 现有报表历史记录快照的时间戳值将新的时区设置同步。 如果您在上午 9:00 生成了报表历史记录快照，然后向前调整一个时区，那么所生成快照的时间戳就会从上午 9:00 变为 上午 10:00。  
  
 除非将计划映射到新的时区，否则这些计划将仍然保留现有设置。 例如，如果某个计划将在 太平洋标准时间的凌晨 2:00 运行，而您将时区更改为澳大利亚东部标准时间，则该计划将在澳大利亚东部 标准时间的凌晨 2:00 运行。  
  
 属性时间戳值（如创建文件夹或链接报表项的时间）与新的时区设置不同步。 如果您在 6 月 25 日上午 9:00 创建了一个项，然后重置了时区或时钟，则时间戳将仍然是 6 月 25 日上午 9:00。  
  
## <a name="changing-the-time-zone-sharepoint-mode"></a>更改时区（SharePoint 模式）  
 针对 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 模式的时区配置作为 SharePoint 区域设置的一部分进行管理。 有关详细信息，请参阅 [区域设置 (SharePoint Server 2010) (http://technet.microsoft.com/library/cc824907.aspx)](http://technet.microsoft.com/library/cc824907.aspx)。  
  
## <a name="changing-the-clock-settings"></a>更改时钟设置  
 更改计算机时钟对现有时间戳值没有影响（例如，如果您将时钟拨快一小时，报表历史记录快照的时间戳不会改变）。 计划和传递处理器可能需要 10 秒钟的延迟才会使用新的设置。 如果您修改了配置文件中的轮询间隔设置，实际延迟时间可能会有所不同。  
  
## <a name="see-also"></a>另请参阅  
 [启动和停止报表服务器服务](../../reporting-services/report-server/start-and-stop-the-report-server-service.md)   
 [计划](../../reporting-services/subscriptions/schedules.md)  
  
  
