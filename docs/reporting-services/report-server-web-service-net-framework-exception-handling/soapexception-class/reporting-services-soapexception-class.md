---
title: "Reporting Services SoapException 类 |Microsoft 文档"
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
- exceptions [Reporting Services], SoapException class
- SoapException class
ms.assetid: 2cec49ee-20b1-40eb-a75b-0908d9c05b34
caps.latest.revision: 33
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: e24a518bee7b192505fc93ad26d4345f9d710143
ms.contentlocale: zh-cn
ms.lasthandoff: 08/12/2017

---
# <a name="reporting-services-soapexception-class"></a>Reporting Services SoapException 类
  您应该解决已知可能会发生的特定 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 错误。 例如，在您要求用户创建某一文件夹的应用程序中，该用户可能尝试创建已存在的文件夹。 作为开发人员，您无法控制用户在您的应用程序的文件夹名称和路径字段中输入的内容，但可以控制当某人无意中尝试创建已存在的项时的用户体验。  
  
 若要使其更轻松地捕获特定的错误情况，[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]分为两类异常的错误代码并返回使用从属性的错误分类**SoapException**类。 有关详细信息，请参阅 》 中"SoapException 类" [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] SDK 文档。  
  
 下表列出的公共属性**SoapException**类。  
  
|公共属性|Description|  
|---------------------|-----------------|  
|**Actor**|导致了异常的代码。 该值是指向 Web 服务方法的 URL。|  
|**详细信息**|应用程序特定的错误信息。 该值由报表服务器设置并且采用 XML 格式。 有关详细信息，请参阅[Detail 属性](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/detail-property.md)和[使用的处理特定错误的详细信息属性](../../../reporting-services/report-server-web-service-net-framework-exception-handling/best-practices/using-the-detail-property-to-handle-specific-errors.md)。|  
|**HelpLink**|指向与错误相关联的帮助文件的 URL 或 URN。 该值通常由 Web 服务设置并且它设置指向 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 帮助和支持的 URL。 因为[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]支持多个帮助链接是否有错误发生，报表服务器设置帮助链接信息作为的一部分**详细信息**属性。 有关详细信息，请参阅[HelpLink 元素](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/helplink-element.md)。|  
|**消息**|描述错误的描述性的本地化消息。 此文本可能出现在应用程序用户界面中。|  
  
## <a name="see-also"></a>另请参阅  
 [引入了 Reporting Services 中的异常处理](../../../reporting-services/report-server-web-service-net-framework-exception-handling/introducing-exception-handling-in-reporting-services.md)   
 [SoapException 错误表](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/soapexception-errors-table.md)  
  
  

