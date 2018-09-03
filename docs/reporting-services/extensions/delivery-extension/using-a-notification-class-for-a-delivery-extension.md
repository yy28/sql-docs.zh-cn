---
title: 将 Notification 类用于传递扩展插件 | Microsoft Docs
ms.date: 03/06/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: extensions
ms.suite: pro-bi
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- delivery extensions [Reporting Services], notifications
- notifications [Reporting Services]
- retry queues
- Nofication class
ms.assetid: 549c40c4-d33d-46c2-9d6a-7bbb671ac67a
author: markingmyname
ms.author: maghan
ms.openlocfilehash: dbfc755d6d7e89e3628871f8e43580a68078aaba
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/30/2018
ms.locfileid: "43274095"
---
# <a name="using-a-notification-class-for-a-delivery-extension"></a>将通知类用于传递扩展插件
  <xref:Microsoft.ReportingServices.Interfaces.Notification> 类位于 <xref:Microsoft.ReportingServices.Interfaces> 命名空间中，表示传递扩展插件用于传递报表的订阅信息。 <xref:Microsoft.ReportingServices.Interfaces.Notification> 类提供多种属性，这些属性可用于呈现用于传递的报表、确定通知的状态和设置用户数据。  
  
 ![报表通知流程](../../../reporting-services/extensions/delivery-extension/media/bk-ext-03.gif "Report notification process")  
通知是任何传递的中心对象  
  
 在引发与某一订阅关联的事件时，如果该订阅使用您的自定义传递扩展插件，则将创建包含 <xref:Microsoft.ReportingServices.Interfaces.Report> 对象的通知。 <xref:Microsoft.ReportingServices.Interfaces.Report> 对象封装将给定报表呈现给支持的呈现格式所需的功能，并且包含特定于报表的属性，例如指向服务器上报表的 URL 和报表的名称。 有关 <xref:Microsoft.ReportingServices.Interfaces.Report> 类的详细信息，请参阅[将 Report 类用于传递扩展插件](../../../reporting-services/extensions/delivery-extension/using-the-report-class-for-a-delivery-extension.md)。  
  
 您将 <xref:Microsoft.ReportingServices.Interfaces.Notification> 对象传递到传递扩展插件的 <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.Deliver%2A> 方法。 您的 <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.Deliver%2A> 方法应包含用于处理通知和传递报表的特定代码。  
  
 有关如何使用 <xref:Microsoft.ReportingServices.Interfaces.Notification> 类的示例，请参阅 [SQL Server Reporting Services Product Samples](http://go.microsoft.com/fwlink/?LinkId=177889)（SQL Server Reporting Services 产品示例）。  
  
## <a name="retry-functionality"></a>重试功能  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 允许您为无法立即传递的通知创建重试队列。 在报表服务器调用某一传递扩展插件的 <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.Deliver%2A> 方法后，该传递扩展可以请求报表服务器在以后的某个时间点重试该传递。 如果发生此情况，则报表服务器将把通知置于内部队列中，并且在经过了特定的时间段后重试该传递。 管理员可以使用 MaxNumberOfRetries XML 元素和 PeriodBetweenRetries XML 元素，在 RSReportServer.config 文件的传递扩展插件部分中配置报表服务器执行的重试尝试的最大次数以及两次重试之间的时间段。 如果传递在以后成功，或者达到最大重试尝试数目，则通知将从重试队列中删除。 如果传递在尝试了最大重试数目后仍失败，则通知将被放弃。  
  
## <a name="see-also"></a>另请参阅  
 [实现传递扩展插件](../../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)   
 [Reporting Services 扩展插件库](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
