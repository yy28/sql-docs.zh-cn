---
title: "详细介绍属性 |Microsoft 文档"
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
- Detail property
- SoapException class
ms.assetid: c1ddaeb6-c540-49fa-b06e-b6359d377ee8
caps.latest.revision: 33
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: 51b99212acac0029bf246ce1668cd3a8b474fb84
ms.contentlocale: zh-cn
ms.lasthandoff: 08/12/2017

---
# <a name="detail-property"></a>Detail 属性
  **详细信息**属性[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] **SoapException**类具有以下 XML 结构：  
  
## <a name="elements"></a>元素  
 **详细信息**  
 包含所有其他错误详细信息元素的顶级元素。  
  
 **ErrorCode**  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 特定的错误代码。  
  
 **HttpStatus**  
 HTTP 状态代码。  
  
 **消息**  
 报表服务器分配的错误消息和错误代码。  
  
 **HelpLink**  
 指向某网站的帮助链接 URL，在该网站中可以找到有关错误的更多信息。 有关详细信息，请参阅[HelpLink 元素](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/helplink-element.md)。  
  
 **LinkID**  
 分配给链接的 ID。  
  
 **ProductName**  
 产品的名称。 默认值是**Microsoft SQL Server Reporting Services**。  
  
 **ProductVersion**  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]的版本。 最大长度为 15 个字符。 版本号的格式应如下所示：8.00.0xxx.00。  
  
 **ProductLocaleId**  
 应用程序的 INTL DLL 的区域设置 ID 或语言 ID（例如，0x41A）。  
  
 **操作系统**  
 在其中安装 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 的操作系统。 有效的值包括**0**操作系统独立， **1**为[!INCLUDE[win2kfamily](../../../includes/win2kfamily-md.md)]，和**16**对于 Windows XP。  
  
 **CountryLocaleId**  
 操作系统的区域设置 ID 或语言 ID。 例如，对应于 Windows 法语版的值为 0x040c。  
  
 **详细信息**  
 一个 XML 字符串，其中包含在运行方法时出现的嵌套异常。  
  
 **源**  
 子元素**的详细信息**。 错误根源。  
  
 **消息**  
 子元素**的详细信息**。 嵌套异常的错误消息。 此元素包含 XML 属性**ErrorCode**和**HelpLink**。  
  
 **警告**  
 一个 XML 字符串，其中包含从报表处理返回的警告。  
  
## <a name="see-also"></a>另请参阅  
 [引入了 Reporting Services 中的异常处理](../../../reporting-services/report-server-web-service-net-framework-exception-handling/introducing-exception-handling-in-reporting-services.md)   
 [Reporting Services SoapException 类](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/reporting-services-soapexception-class.md)   
 [使用的详细信息属性来处理特定的错误](../../../reporting-services/report-server-web-service-net-framework-exception-handling/best-practices/using-the-detail-property-to-handle-specific-errors.md)  
  
  

