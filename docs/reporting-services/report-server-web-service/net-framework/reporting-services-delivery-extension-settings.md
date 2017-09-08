---
title: "Reporting Services 传递扩展插件设置 |Microsoft 文档"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- XML Web service [Reporting Services], delivery extension settings
- Report Server Web service, delivery extension settings
- delivery [Reporting Services]
- network share delivery [Reporting Services]
- file share delivery [Reporting Services]
- e-mail [Reporting Services]
- mailing reports [Reporting Services]
- sharing reports
- extensions [Reporting Services], delivery
- mail [Reporting Services]
- Web service [Reporting Services], delivery extension settings
ms.assetid: 68c31a85-261c-4ec4-b8df-1f9842b46f8a
caps.latest.revision: 36
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: bc52f95cdc038c0074feb10b05fffe916b3d3da1
ms.contentlocale: zh-cn
ms.lasthandoff: 08/12/2017

---
# <a name="reporting-services-delivery-extension-settings"></a>Reporting Services 传递扩展插件设置
  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]包括电子邮件传递扩展插件和文件共享传递扩展插件。 电子邮件传递扩展插件提供了通过电子邮件将报表发送到单个用户或组的方式。 文件共享传递扩展插件可用于将呈现的报表自动发送到网络上的共享区中。 您可以使用具有标准订阅或数据驱动订阅的支持的传递扩展插件之一。 只要您调用 <xref:ReportService2010.ReportingService2010.CreateSubscription%2A>、<xref:ReportService2010.ReportingService2010.CreateDataDrivenSubscription%2A>、<xref:ReportService2010.ReportingService2010.SetSubscriptionProperties%2A> 和 <xref:ReportService2010.ReportingService2010.SetDataDrivenSubscriptionProperties%2A> 方法，就将传递特定于传递扩展插件类型的传递设置。 若要以编程方式检索传递设置的列表，请使用 <xref:ReportService2010.ReportingService2010.GetExtensionSettings%2A> 方法。  
  
> [!NOTE]  
>  传递扩展插件设置区分大小写。  
  
## <a name="e-mail-delivery-settings"></a>电子邮件传递设置  
 下表列出用于使用报表服务器电子邮件的订阅的电子邮件传递设置。  
  
|设置|“值”|  
|-------------|-----------|  
|**自**|将出现在电子邮件地址**到**封电子邮件行。 多个电子邮件地址之间用分号分隔。 必需的。|  
|**抄送**|将出现在电子邮件地址**Cc**封电子邮件行。 多个电子邮件地址之间用分号分隔。 選擇性。|  
|**密件抄送**|将出现在电子邮件地址**密件抄送**封电子邮件行。 多个电子邮件地址之间用分号分隔。 選擇性。|  
|**ReplyTo**|将出现在电子邮件地址**答复到**电子邮件消息标头。 该值必须为单个电子邮件地址。 選擇性。|  
|**IncludeReport**|指示是否在电子邮件传递中包括报表的值。 值为**true**指示电子邮件的正文中传递报表。|  
|**RenderFormat**|要用于生成呈现的报表的呈现扩展插件的名称。 该名称必须与在报表服务器上安装的可见呈现扩展插件之一相符。 此值是必需的如果**IncludeReport**设置的值为**true**。|  
|**Priority**|电子邮件按其发送的优先级。 有效值为**低**，**正常**，和**高**。 默认值是**正常**。|  
|**主题**|电子邮件的主题行中的文本。|  
|**注释**|包括在电子邮件的正文中的文本。|  
|**IncludeLink**|指示是否在电子邮件正文中包括指向报表的链接的值。|  
  
## <a name="file-share-delivery-settings"></a>文件共享传递设置  
 下表列出用于订阅的文件共享传递设置。  
  
|设置|“值”|  
|-------------|-----------|  
|**文件名**|保存到磁盘的文件的名称。|  
|**FILEEXTN**|指示是否为所呈现报表包括文件扩展名。 值可以是**true**或**false**。|  
|**路径**|要将报表保存到的文件夹路径或 UNC 文件共享路径。|  
|**RENDER_FORMAT**|保存到磁盘的报表的格式。|  
|**用户名**|访问网络资源或磁盘所需的用户名。|  
|**密码**|访问网络资源或磁盘所需的密码。|  
|**WRITEMODE**|访问磁盘时要使用的写入模式。 有效值为**无**，**覆盖**，和**AutoIncrement**。|  
  
## <a name="see-also"></a>另請參閱  
 [技术参考 &#40;SSRS &#41;](../../../reporting-services/technical-reference-ssrs.md)   
 [使用 Web 服务和.NET Framework 构建应用程序](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)  
  
  
