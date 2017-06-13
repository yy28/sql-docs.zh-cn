---
title: "实现 ISubscriptionBaseUIUserControl 接口 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
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
- user controls [Reporting Services]
- ISubscriptionBaseUIUserControl interface
- delivery extensions [Reporting Services], user controls
ms.assetid: a1e9122c-aa0b-45de-b536-4f1202875ab1
caps.latest.revision: 35
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 5b509345723b137941c2f00c054c77f076035dc2
ms.contentlocale: zh-cn
ms.lasthandoff: 06/13/2017

---
# <a name="implementing-the-isubscriptionbaseuiusercontrol-interface"></a>实现 ISubscriptionBaseUIUserControl 接口
  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 传递扩展插件可以包含订阅用户界面 (UI) 的实现，以便在报表管理器中收集扩展插件特定的信息。 当用户创建新的订阅或修改现有订阅时，将调用此 UI。 当创建新订阅时，此 UI 显示适当的默认值并使得用户能够与传递提供程序交互。 当修改订阅时，将使用当前订阅中的信息预填充此 UI。  
  
 传递扩展插件将订阅 UI 作为 ASP.NET 用户控件提供。 在显示订阅 UI 时，报表服务器将合并由传递扩展插件定义的用户控件。 提供实现此功能的抽象方法的基接口是 <xref:Microsoft.ReportingServices.Interfaces.ISubscriptionBaseUIUserControl> 接口。 此接口可确保正确地执行常见操作，如验证输入值。 此外，基本用户控件提供一组默认属性，报表服务器使用这些属性来实现订阅间的一致性。 与报表管理器集成的传递扩展插件需要这些属性。  
  
 您可以在传递提供程序中实现 <xref:Microsoft.ReportingServices.Interfaces.ISubscriptionBaseUIUserControl> 接口，以便为报表管理器生成订阅 UI。 <xref:Microsoft.ReportingServices.Interfaces.ISubscriptionBaseUIUserControl> 接口提供了基础结构，以供用户为订阅设置输入值，处理传递扩展插件所需的设置以及验证这些设置。  
  
> [!NOTE]  
>  不要求您将 <xref:Microsoft.ReportingServices.Interfaces.ISubscriptionBaseUIUserControl> 接口作为传递扩展插件的一部分实现。 而是始终可以通过 SOAP API 方法 <xref:ReportService2010.ReportingService2010.CreateSubscription%2A> 和 <xref:ReportService2010.ReportingService2010.CreateDataDrivenSubscription%2A> 创建使用传递扩展插件的订阅。 有关用于管理订阅和传递的 SOAP API 功能的详细信息，请参阅[Subscription and Delivery Methods](../../../reporting-services/report-server-web-service/methods/subscription-and-delivery-methods.md)。  
  
 <xref:Microsoft.ReportingServices.Interfaces.ISubscriptionBaseUIUserControl> 接口扩展 <xref:Microsoft.ReportingServices.Interfaces.IExtension>。 你的用户控件实现<xref:Microsoft.ReportingServices.Interfaces.ISubscriptionBaseUIUserControl>还必须从继承**System.Web.UI.WebControls.WebControl**。 有关详细信息**WebControl**类，请参阅你[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]开发人员指南。  
  
 有关如何使用的示例<xref:Microsoft.ReportingServices.Interfaces.ISubscriptionBaseUIUserControl>接口，请参阅[SQL Server Reporting Services 产品示例](http://go.microsoft.com/fwlink/?LinkId=177889)。  
  
## <a name="see-also"></a>另请参阅  
 [Implementing a Delivery Extension](../../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)   
 [Reporting Services 扩展库](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
