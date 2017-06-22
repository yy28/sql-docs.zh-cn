---
title: "Implementing a Delivery Extension |Microsoft 文档"
ms.custom: 
ms.date: 03/16/2017
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
- delivery [Reporting Services]
- custom delivery extensions [Reporting Services]
- extensions [Reporting Services], delivery
- delivery extensions [Reporting Services]
ms.assetid: 600cd229-efcd-480e-8c95-3c3c39ff4e7a
caps.latest.revision: 32
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 9909a4711eb5b1ffde9b865411bd552e6b409bc6
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="implementing-a-delivery-extension"></a>实现传递扩展插件
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)][!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]使用户能够创建和发布报表，一次创建和发布，可以传递给不同的位置。 此外，[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 包括多个传递扩展插件和一个传递 API，它们使得开发人员能够创建其他传递扩展插件，以便在 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 中进一步扩展传递的功能。  
  
 传递扩展插件的示例实现，请参阅[SQL Server Reporting Services 产品示例](http://go.microsoft.com/fwlink/?LinkId=177889)。  
  
## <a name="in-this-section"></a>本节内容  
 [传递扩展概述](../../../reporting-services/extensions/delivery-extension/delivery-extensions-overview.md)  
 介绍如何为 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 编写自定义传递扩展插件。  
  
 [准备实现传递扩展插件](../../../reporting-services/extensions/delivery-extension/preparing-to-implement-a-delivery-extension.md)  
 介绍在实现 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 传递扩展插件时可用的接口和类，以及在实现前要考虑的问题。  
  
 [创建传递扩展库](../../../reporting-services/extensions/delivery-extension/creating-a-delivery-extension-library.md)  
 介绍如何为 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 传递扩展插件分配命名空间以及如何将传递扩展插件编译成库 DLL。  
  
 [实现的传递扩展插件 IDeliveryExtension 接口](../../../reporting-services/extensions/delivery-extension/implementing-the-ideliveryextension-interface-for-a-delivery-extension.md)  
 介绍传递扩展插件的属性以及如何实现您自己的传递扩展插件类。  
  
 [通知类用于传递扩展插件](../../../reporting-services/extensions/delivery-extension/using-a-notification-class-for-a-delivery-extension.md)  
 描述的属性**通知**类以及如何在传递扩展实现中使用。  
  
 [设置类用于传递扩展插件](../../../reporting-services/extensions/delivery-extension/using-the-setting-class-for-a-delivery-extension.md)  
 描述的属性**设置**类以及如何在传递扩展实现中使用。  
  
 [使用用于传递扩展插件的 IDeliveryReportServerInformation 界面](../../../reporting-services/extensions/delivery-extension/using-the-ideliveryreportserverinformation-interface-for-a-delivery-extension.md)  
 描述的属性**IDeliveryReportServerInformation**接口以及如何在传递扩展实现中使用。  
  
 [用于传递扩展插件的报表类](../../../reporting-services/extensions/delivery-extension/using-the-report-class-for-a-delivery-extension.md)  
 描述的属性**报表**类以及如何在传递扩展实现中使用。  
  
 [RenderedOutputFile 类用于传递扩展插件](../../../reporting-services/extensions/delivery-extension/using-the-renderedoutputfile-class-for-a-delivery-extension.md)  
 描述的属性**RenderedOutputFile**类以及如何在传递扩展实现中使用。  
  
 [实现的传递扩展插件 ISubscriptionBaseUIUserControl 接口](../../../reporting-services/extensions/delivery-extension/implementing-the-isubscriptionbaseuiusercontrol-interface.md)  
 介绍传递扩展插件用户控件的属性以及如何实现您自己的用于订阅的用户界面。  
  
 [部署传递扩展插件](../../../reporting-services/extensions/delivery-extension/deploying-a-delivery-extension.md)  
 介绍如何部署传递扩展插件。  
  
 [调试传递扩展插件代码](../../../reporting-services/extensions/delivery-extension/debugging-delivery-extension-code.md)  
 介绍如何调试传递扩展插件中的代码。  
  
 [删除传递扩展插件](../../../reporting-services/extensions/delivery-extension/removing-a-delivery-extension.md)  
 说明如何从报表服务器上删除传递扩展插件。  
  
## <a name="see-also"></a>另请参阅  
 [Reporting Services 扩展插件](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [Reporting Services 扩展库](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
