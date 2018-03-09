---
title: "HelpLink 元素 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: report-server-web-service-net-framework-exception-handling
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- HelpLink element
- SoapException class
ms.assetid: a4489103-a874-44c2-8f75-95cb238928ed
caps.latest.revision: "30"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 9dd69bd5a2dcdf71a3dccd211d5e464e75994cb9
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/09/2018
---
# <a name="helplink-element"></a>HelpLink 元素
  Detail 属性的 HelpLink 元素是报表服务器生成的 URL 字符串。 此 URL 指向由 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 帮助和支持管理的一个网页，并针对在 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 中出现的特定错误提供附加帮助和知识库文章。 此 URL 具有以下语法：  
  
 **http://**www.microsoft.com**/**products**/**ee**/**transform.aspx**?EvtSrc**=v*alue***&EvtID**=*value***&ProdName**=*value***&ProdVer**=*value*  
  
 下表列出 HelpLink URL 的参数。  
  
|参数|ReplTest1|  
|--------------|-----------|  
|EvtSrc|“Microsoft.ReportingServices.Diagnostics.ErrorStrings.resources.Strings”|  
|EvtID|报表服务器错误代码，例如，rsReservedItem。|  
|ProdName|“Microsoft SQL%20Server%20Reporting%20Services”。 产品名称的值已进行 URL 编码。|  
|ProdVer|[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 的版本号。 值为“8.00”指示 [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]。|  
  
 下面的示例说明针对错误代码 rsReservedItem 返回的 HelpLinkURL。 当用户尝试修改或删除 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 中的保留项时，将出现此错误。  
  
```  
http://www.microsoft.com/products/ee/transform.aspx?  
EvtSrc=Microsoft.ReportingServices.Diagnostics.ErrorStrings.resources.Strings  
&EvtID=rsReservedItem&ProdName=Microsoft%20SQL%20Server%20Reporting%20Services&ProdVer=8.00  
```  
  
 可以使用 SoapException 类在代码中访问 HelpLink 元素。  
  
```vb  
Try  
   rs.DeleteItem("/Report1")  
  
Catch e As SoapException  
   Console.WriteLine(e.Detail("HelpLink").InnerXml)  
End Try  
```  
  
```csharp  
try  
{  
   rs.DeleteItem("/Report1");  
}  
  
catch (SoapException e)  
{  
   Console.WriteLine(e.Detail["HelpLink"].InnerXml);  
}  
```  
  
## <a name="see-also"></a>另请参阅  
 [介绍 Reporting Services 中的异常处理](../../../reporting-services/report-server-web-service-net-framework-exception-handling/introducing-exception-handling-in-reporting-services.md)   
 [Reporting Services SoapException 类](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/reporting-services-soapexception-class.md)   
 [使用 Detail 属性处理特定错误](../../../reporting-services/report-server-web-service-net-framework-exception-handling/best-practices/using-the-detail-property-to-handle-specific-errors.md)  
  
  
