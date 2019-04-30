---
title: 实现 ISubscriptionBaseUIUserControl 接口传递扩展插件 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- user controls [Reporting Services]
- ISubscriptionBaseUIUserControl interface
- delivery extensions [Reporting Services], user controls
ms.assetid: a1e9122c-aa0b-45de-b536-4f1202875ab1
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 2664d71243d98e9b8152c5c5c7ce241a4f3669f8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63164352"
---
# <a name="implementing-the-isubscriptionbaseuiusercontrol-interface-for-a-delivery-extension"></a>为传递扩展插件实现 ISubscriptionBaseUIUserControl 接口
  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 传递扩展插件可以包含订阅用户界面 (UI) 的实现，以便在报表管理器中收集扩展插件特定的信息。 当用户创建新的订阅或修改现有订阅时，将调用此 UI。 当创建新订阅时，此 UI 显示适当的默认值并使得用户能够与传递提供程序交互。 当修改订阅时，将使用当前订阅中的信息预填充此 UI。  
  
 传递扩展插件将订阅 UI 作为 ASP.NET 用户控件提供。 在显示订阅 UI 时，报表服务器将合并由传递扩展插件定义的用户控件。 提供实现此功能的抽象方法的基接口是 <xref:Microsoft.ReportingServices.Interfaces.ISubscriptionBaseUIUserControl> 接口。 此接口可确保正确地执行常见操作，如验证输入值。 此外，基本用户控件提供一组默认属性，报表服务器使用这些属性来实现订阅间的一致性。 与报表管理器集成的传递扩展插件需要这些属性。  
  
 您可以在传递提供程序中实现 <xref:Microsoft.ReportingServices.Interfaces.ISubscriptionBaseUIUserControl> 接口，以便为报表管理器生成订阅 UI。 <xref:Microsoft.ReportingServices.Interfaces.ISubscriptionBaseUIUserControl> 接口提供了基础结构，以供用户为订阅设置输入值，处理传递扩展插件所需的设置以及验证这些设置。  
  
> [!NOTE]  
>  不要求您将 <xref:Microsoft.ReportingServices.Interfaces.ISubscriptionBaseUIUserControl> 接口作为传递扩展插件的一部分实现。 而是始终可以通过 SOAP API 方法 <xref:ReportService2010.ReportingService2010.CreateSubscription%2A> 和 <xref:ReportService2010.ReportingService2010.CreateDataDrivenSubscription%2A> 创建使用传递扩展插件的订阅。 有关用于管理订阅和传递的 SOAP API 功能的详细信息，请参阅[订阅和传递方法](../../report-server-web-service/methods/subscription-and-delivery-methods.md)。  
  
 <xref:Microsoft.ReportingServices.Interfaces.ISubscriptionBaseUIUserControl> 接口扩展 <xref:Microsoft.ReportingServices.Interfaces.IExtension>。 实现 <xref:Microsoft.ReportingServices.Interfaces.ISubscriptionBaseUIUserControl> 的用户控件也必须从 System.Web.UI.WebControls.WebControl 继承。 有关 WebControl 类的详细信息，请参阅 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 开发人员指南。  
  
 有关如何使用 <xref:Microsoft.ReportingServices.Interfaces.ISubscriptionBaseUIUserControl> 接口的示例，请参阅 [SQL Server Reporting Services Product Samples](https://go.microsoft.com/fwlink/?LinkId=177889)（SQL Server Reporting Services 产品示例）。  
  
## <a name="see-also"></a>请参阅  
 [实现传递扩展插件](implementing-a-delivery-extension.md)   
 [Reporting Services 扩展插件库](../reporting-services-extension-library.md)  
  
  
