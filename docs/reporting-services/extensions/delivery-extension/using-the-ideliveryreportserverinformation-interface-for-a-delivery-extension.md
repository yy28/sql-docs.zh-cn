---
title: "使用用于传递扩展插件的 IDeliveryReportServerInformation 界面 |Microsoft 文档"
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
- IDeliveryReportServerInformation interface
- delivery extensions [Reporting Services], retrieving report server information
ms.assetid: adbce647-18f3-470c-8114-42f8bcc95dc2
caps.latest.revision: 34
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 4a3c2ea843dbfe19b797da7b792d10220018a595
ms.contentlocale: zh-cn
ms.lasthandoff: 06/13/2017

---
# <a name="using-the-ideliveryreportserverinformation-interface-for-a-delivery-extension"></a>将 IDeliveryReportServerInformation 接口用于传递扩展插件
  <xref:Microsoft.ReportingServices.Interfaces.IDeliveryReportServerInformation> 接口公开多个属性，您可以使用这些属性来检索有关报表服务器的信息。 您可以使用此信息来传递通知和报表。 当实现传递扩展插件类时，您按照 <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.ReportServerInformation%2A> 接口的要求实现 <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension> 属性。 <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.ReportServerInformation%2A> 属性返回一个实现 <xref:Microsoft.ReportingServices.Interfaces.IDeliveryReportServerInformation> 接口的对象。 从该对象，您可以获得报表服务器当前支持的呈现扩展插件的列表。  
  
 以下**为**循环无法用于在报表服务器上存储的当前可用的呈现扩展插件列表**ArrayList**对象。  
  
```vb  
Dim renderFormats As New ArrayList()  
Dim e As Microsoft.ReportingServices.Interfaces.Extension  
For Each e In  ReportServerInformation.RenderingExtension  
   If e.Visible Then  
      renderFormats.Add(e.Name)  
   End If  
Next e  
```  
  
```csharp  
ArrayList renderFormats = new ArrayList();  
foreach (Microsoft.ReportingServices.Interfaces.Extension e in ReportServerInformation.RenderingExtension)  
{   
   if (e.Visible)  
   {  
      renderFormats.Add(e.Name);  
   }  
}  
```  
  
 有关详细信息<xref:Microsoft.ReportingServices.Interfaces.IDeliveryReportServerInformation>接口，请参阅[使用用于传递扩展插件的 IDeliveryReportServerInformation 界面](../../../reporting-services/extensions/delivery-extension/using-the-ideliveryreportserverinformation-interface-for-a-delivery-extension.md)。  
  
## <a name="see-also"></a>另请参阅  
 <xref:Microsoft.ReportingServices.Interfaces>   
 [Implementing a Delivery Extension](../../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)   
 [Reporting Services 扩展库](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
