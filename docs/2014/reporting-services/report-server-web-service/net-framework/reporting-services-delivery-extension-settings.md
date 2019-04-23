---
title: Reporting Services 传递扩展插件设置 | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
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
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d356bc1cb981479de8a4b1baa3bdaaf45b6145ca
ms.sourcegitcommit: b87c384e10d6621cf3a95ffc79d6f6fad34d420f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "60157885"
---
# <a name="reporting-services-delivery-extension-settings"></a>Reporting Services 传递扩展插件设置
  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 包括电子邮件传递扩展插件和文件共享传递扩展插件。 电子邮件传递扩展插件提供了通过电子邮件将报表发送到单个用户或组的方式。 文件共享传递扩展插件可用于将呈现的报表自动发送到网络上的共享区中。 您可以使用具有标准订阅或数据驱动订阅的支持的传递扩展插件之一。 只要您调用 <xref:ReportService2010.ReportingService2010.CreateSubscription%2A>、<xref:ReportService2010.ReportingService2010.CreateDataDrivenSubscription%2A>、<xref:ReportService2010.ReportingService2010.SetSubscriptionProperties%2A> 和 <xref:ReportService2010.ReportingService2010.SetDataDrivenSubscriptionProperties%2A> 方法，就将传递特定于传递扩展插件类型的传递设置。 若要以编程方式检索传递设置的列表，请使用 <xref:ReportService2010.ReportingService2010.GetExtensionSettings%2A> 方法。  
  
> [!NOTE]  
>  传递扩展插件设置区分大小写。  
  
## <a name="e-mail-delivery-settings"></a>电子邮件传递设置  
 下表列出用于使用报表服务器电子邮件的订阅的电子邮件传递设置。  
  
|设置|ReplTest1|  
|-------------|-----------|  
|TO|在电子邮件的 `To` 行中出现的电子邮件地址。 多个电子邮件地址之间用分号分隔。 必需的。|  
|**CC**|在电子邮件的 `Cc` 行中出现的电子邮件地址。 多个电子邮件地址之间用分号分隔。 可选。|  
|BCC|在电子邮件的 `Bcc` 行中出现的电子邮件地址。 多个电子邮件地址之间用分号分隔。 可选。|  
|ReplyTo|在电子邮件的 `Reply-To` 标题中出现的电子邮件地址。 该值必须为单个电子邮件地址。 可选。|  
|`IncludeReport`|指示是否在电子邮件传递中包括报表的值。 如果值为 `true`，则指示在电子邮件的正文中传递报表。|  
|**RenderFormat**|要用于生成呈现的报表的呈现扩展插件的名称。 该名称必须与在报表服务器上安装的可见呈现扩展插件之一相符。 如果该 `IncludeReport` 设置设置为 `true` 值，则该值是必需的。|  
|**Priority**|电子邮件按其发送的优先级。 有效值为 `LOW`、`NORMAL` 和 `HIGH`。 默认值为 `NORMAL`。|  
|**主题**|电子邮件的主题行中的文本。|  
|**注释**|包括在电子邮件的正文中的文本。|  
|IncludeLink|指示是否在电子邮件正文中包括指向报表的链接的值。|  
  
## <a name="file-share-delivery-settings"></a>文件共享传递设置  
 下表列出用于订阅的文件共享传递设置。  
  
|设置|ReplTest1|  
|-------------|-----------|  
|FILENAME|保存到磁盘的文件的名称。|  
|FILEEXTN|指示是否为所呈现报表包括文件扩展名。 该值为 `true` 或 `false`。|  
|PATH|要将报表保存到的文件夹路径或 UNC 文件共享路径。|  
|RENDER_FORMAT|保存到磁盘的报表的格式。|  
|USERNAME|访问网络资源或磁盘所需的用户名。|  
|**PASSWORD**|访问网络资源或磁盘所需的密码。|  
|WRITEMODE|访问磁盘时要使用的写入模式。 有效值为 `None`、`Overwrite` 和 `AutoIncrement`。|  
  
## <a name="see-also"></a>请参阅  
 [技术参考 (SSRS)](../../technical-reference-ssrs.md)   
 [使用 Web 服务和.NET Framework 构建应用程序](building-applications-using-the-web-service-and-the-net-framework.md)  
  
  
