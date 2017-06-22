---
title: "使用的详细信息属性来处理特定错误 |Microsoft 文档"
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
- exceptions [Reporting Services], Detail property
- Detail property
- InnerText property
ms.assetid: 4392633d-b46b-41e6-bc12-efb64e166704
caps.latest.revision: 30
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 096e12d3b87eeb12092915dcec3a43f7ac585656
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="using-the-detail-property-to-handle-specific-errors"></a>使用 Detail 属性处理特定错误
  若要进一步分类异常，[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]返回中的其他错误信息**InnerText** SOAP 异常中的子元素的属性**详细信息**属性。 因为**详细信息**属性是**XmlNode**对象，你可以访问的内部文本**消息**使用下面的代码的子元素。  
  
 有关的所有可用的子元素中包含的列表**详细信息**属性，请参阅[Detail 属性](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/detail-property.md)。 有关详细信息，请参阅"详细信息属性" [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] SDK 文档。  
  
```vb  
Try  
' Code for accessing the report server  
Catch ex As SoapException  
   ' The exception is a SOAP exception, so use  
   ' the Detail property's Message element.  
   Console.WriteLine(ex.Detail("Message").InnerXml)  
End Try  
```  
  
```csharp  
try  
{  
   // Code for accessing the report server  
}  
catch (SoapException ex)  
{  
   // The exception is a SOAP exception, so use  
   // the Detail property's Message element.  
   Console.WriteLine(ex.Detail["Message"].InnerXml);  
}  
```  
  
```vb  
Try  
' Code for accessing the report server  
Catch ex As SoapException  
   If ex.Detail("ErrorCode").InnerXml = "rsInvalidItemName" Then  
   End If ' Perform an action based on the specific error code  
End Try  
```  
  
```csharp  
try  
{  
   // Code for accessing the report server  
}  
catch (SoapException ex)  
{  
   if (ex.Detail["ErrorCode"].InnerXml == "rsInvalidItemName")  
   {  
      // Perform an action based on the specific error code  
   }  
}  
```  
  
 下面的代码行将在 SOAP 异常中返回的特定错误代码写入控制台。 您还可以对错误代码进行评估并执行特定操作。  
  
```vb  
Console.WriteLine(ex.Detail("ErrorCode").InnerXml)  
```  
  
```csharp  
Console.WriteLine(ex.Detail["ErrorCode"].InnerXml);  
```  
  
## <a name="see-also"></a>另请参阅  
 [引入了 Reporting Services 中的异常处理](../../../reporting-services/report-server-web-service-net-framework-exception-handling/introducing-exception-handling-in-reporting-services.md)   
 [Reporting Services SoapException 类](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/reporting-services-soapexception-class.md)   
 [SoapException 错误表](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/soapexception-errors-table.md)  
  
  
