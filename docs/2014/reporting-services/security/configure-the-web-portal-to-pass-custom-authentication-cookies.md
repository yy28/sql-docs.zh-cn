---
title: 配置报表管理器以便传递自定义身份验证 Cookie |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- authentication [Reporting Services]
- extensions [Reporting Services], custom security
ms.assetid: 91aeb053-149e-4562-ae4c-a688d0e1b2ba
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: bff2f31eb321a24c184580a6b1565f4dbc76bb1d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63242530"
---
# <a name="configure-report-manager-to-pass-custom-authentication-cookies"></a>配置报表管理器以便传递自定义身份验证 Cookie
  如果使用的是自定义身份验证扩展插件，则应配置报表管理器以传输自定义身份验证 Cookie。 否则，报表管理器通过特定的 HTTP 请求将 Cookie 传输到报表服务器。 如果要传输其他 Cookie，则必须修改 RSReportServer.Config 文件。  
  
## <a name="modifying-the-rsreportserverconfig-file"></a>修改 RSReportServer.Config 文件  
 可以启用报表管理器将其他 cookie 传输到报表服务器通过添加 <`PassThroughCookies`> 到 RSReportServer.config 文件中的报表管理器配置设置的元素。 在单一登录身份验证解决方案中，传输其他 Cookie 十分有用，因为此类解决方案不仅需要报表服务器身份验证 Cookie，而且还需要第三方身份验证系统中的 Cookie。  
  
 使用报表服务器时，为了使其他 Cookie 可以通过 HTTP 请求进行传输，请在 RSReportServer.config 文件中设置下列元素：  
  
```  
<UI>  
   <CustomAuthenticationUI>  
      ...  
      <PassThroughCookies>  
         <PassThroughCookie>cookiename1</PassThroughCookie>  
         <PassThroughCookie>cookiename2</PassThroughCookie>  
      </PassThroughCookies>  
   </CustomAuthenticationUI>  
      ...  
</UI>  
```  
  
## <a name="see-also"></a>请参阅  
 [针对报表服务器的身份验证](authentication-with-the-report-server.md)   
 [RSReportServer 配置文件](../report-server/rsreportserver-config-configuration-file.md)   
 [安全扩展插件概述](../extensions/security-extension/security-extensions-overview.md)   
 [配置和管理报表服务器（SSRS 本机模式）](../report-server/configure-and-administer-a-report-server-ssrs-native-mode.md)  
  
  
