---
title: "使用适用于的传递扩展插件设置类 |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
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
- delivery extensions [Reporting Services], settings
- Setting class
ms.assetid: 50746639-da7c-46a5-ac7b-e87dd6b91880
caps.latest.revision: 32
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: c3f077388f6dc568e238b2e6346663ba1bb9807c
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="using-the-setting-class-for-a-delivery-extension"></a>将 Setting 类用于传递扩展插件
  <xref:Microsoft.ReportingServices.Interfaces.Setting> 类位于 <xref:Microsoft.ReportingServices.Interfaces> 命名空间中，表示与传递扩展插件的扩展插件设置有关的信息。 <xref:Microsoft.ReportingServices.Interfaces.Setting> 类提供了基础结构，用于存储与为使传递扩展插件正常工作所需的设置有关的信息。 例如，在报表服务器电子邮件传递中，要求某一用户提供特定于电子邮件传递的设置，例如收件人的地址、发件人的地址、电子邮件的标题行等。 毋庸置疑，您的自定义传递提供程序将要求用户提供特定设置，以便传递扩展插件可以提供通知和报表。  
  
 在实现 <xref:Microsoft.ReportingServices.Interfaces.Setting> 接口的 <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.ExtensionSettings%2A> 属性时，使用 <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension> 类。 <xref:Microsoft.ReportingServices.Interfaces.Setting> 类还用于处理用户在创建订阅或通知时提供的扩展插件设置数据。  
  
 有关如何使用的示例<xref:Microsoft.ReportingServices.Interfaces.Setting>类，请参阅[SQL Server Reporting Services 产品示例](http://go.microsoft.com/fwlink/?LinkId=177889)。  
  
## <a name="see-also"></a>另请参阅  
 [Implementing a Delivery Extension](../../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)   
 [Reporting Services 扩展库](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
