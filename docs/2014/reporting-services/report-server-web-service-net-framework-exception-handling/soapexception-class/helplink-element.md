---
title: HelpLink 元素 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.topic: reference
helpviewer_keywords:
- HelpLink element
- SoapException class
ms.assetid: a4489103-a874-44c2-8f75-95cb238928ed
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 358c0b03e56130fed642fe1ff0bbbc80f9717170
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2019
ms.locfileid: "56041098"
---
# <a name="helplink-element"></a>HelpLink 元素
  Detail 属性的 HelpLink 元素是报表服务器生成的 URL 字符串。 此 URL 指向由 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 帮助和支持管理的一个网页，并针对在 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 中出现的特定错误提供附加帮助和知识库文章。 此 URL 具有以下语法：  
  
 **http://** www.microsoft.com**/** 产品**/** ee**/** transform.aspx **？EvtSrc**=_值_**& EvtID**=_值_**& ProdName** =_值_**& ProdVer**=_值_  
  
 下表列出 HelpLink URL 的参数。  
  
|参数|ReplTest1|  
|--------------|-----------|  
|EvtSrc|“Microsoft.ReportingServices.Diagnostics.ErrorStrings.resources.Strings”|  
|EvtID|报表服务器错误代码，例如，rsReservedItem。|  
|ProdName|“Microsoft SQL%20Server%20Reporting%20Services”。 产品名称的值已进行 URL 编码。|  
|ProdVer|[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 的版本号。 值为“8.00”指示 [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]。|  
  
 下面的示例阐释**HelpLink**返回的错误代码的 URL `rsReservedItem`。 当用户尝试修改或删除 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 中的保留项时，将出现此错误。  
  
```  
https://www.microsoft.com/products/ee/transform.aspx?  
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
  
## <a name="see-also"></a>请参阅  
 [介绍 Reporting Services 中的异常处理](../introducing-exception-handling-in-reporting-services.md)   
 [Reporting Services SoapException 类](reporting-services-soapexception-class.md)   
 [使用 Detail 属性处理特定错误](../best-practices/using-the-detail-property-to-handle-specific-errors.md)  
  
  
