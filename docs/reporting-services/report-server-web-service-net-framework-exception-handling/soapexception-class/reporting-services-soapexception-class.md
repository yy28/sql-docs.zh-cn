---
title: Reporting Services SoapException 类 | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.component: report-server-web-service-net-framework-exception-handling
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- exceptions [Reporting Services], SoapException class
- SoapException class
ms.assetid: 2cec49ee-20b1-40eb-a75b-0908d9c05b34
caps.latest.revision: 33
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 12d98493c8e83688ee0eb5938e1ee078103bc5fe
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "33024634"
---
# <a name="reporting-services-soapexception-class"></a>Reporting Services SoapException 类
  您应该解决已知可能会发生的特定 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 错误。 例如，在您要求用户创建某一文件夹的应用程序中，该用户可能尝试创建已存在的文件夹。 作为开发人员，您无法控制用户在您的应用程序的文件夹名称和路径字段中输入的内容，但可以控制当某人无意中尝试创建已存在的项时的用户体验。  
  
 为了轻松捕获特定错误情况，[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 使用 SoapException 类的属性分类异常的错误代码，并返回错误的分类。 有关详细信息，请参阅 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] SDK 文档中的“SoapException 类”。  
  
 下表列出 SoapException 类的公共属性。  
  
|公共属性|Description|  
|---------------------|-----------------|  
|Actor|导致了异常的代码。 该值是指向 Web 服务方法的 URL。|  
|Detail|应用程序特定的错误信息。 该值由报表服务器设置并且采用 XML 格式。 有关详细信息，请参阅 [Detail 属性](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/detail-property.md)和[使用 Detail 属性处理特定错误](../../../reporting-services/report-server-web-service-net-framework-exception-handling/best-practices/using-the-detail-property-to-handle-specific-errors.md)。|  
|HelpLink|指向与错误相关联的帮助文件的 URL 或 URN。 该值通常由 Web 服务设置并且它设置指向 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 帮助和支持的 URL。 因为 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 针对发生的错误支持多个帮助链接，所以，报表服务器将帮助链接信息设置为 Detail 属性的一部分。 有关详细信息，请参阅 [HelpLink 元素](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/helplink-element.md)。|  
|**消息**|描述错误的描述性的本地化消息。 此文本可能出现在应用程序用户界面中。|  
  
## <a name="see-also"></a>另请参阅  
 [介绍 Reporting Services 中的异常处理](../../../reporting-services/report-server-web-service-net-framework-exception-handling/introducing-exception-handling-in-reporting-services.md)   
 [SoapException 错误表](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/soapexception-errors-table.md)  
  
  
