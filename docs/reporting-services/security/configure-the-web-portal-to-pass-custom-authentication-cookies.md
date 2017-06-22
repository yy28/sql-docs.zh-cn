---
title: "配置 Web 门户来传递自定义身份验证 Cookie |Microsoft 文档"
ms.custom: 
ms.date: 04/18/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- authentication [Reporting Services]
- extensions [Reporting Services], custom security
ms.assetid: 91aeb053-149e-4562-ae4c-a688d0e1b2ba
caps.latest.revision: 18
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 0f1131c191fa64c6dc6f2a074a9cd5db7a8b0e1b
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="configure-the-web-portal-to-pass-custom-authentication-cookies"></a>配置 Web 门户以传递自定义身份验证 Cookie

如果你使用的自定义身份验证扩展，则应配置 web 门户来传输自定义身份验证 cookie。 否则，web 门户将 cookie 传输通过特定于报表服务器的 HTTP 请求。 如果要传输其他 Cookie，则必须修改 RSReportServer.Config 文件。

## <a name="modifying-the-rsreportserverconfig-file"></a>修改 RSReportServer.Config 文件

你可以启用[!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)]传输其他 cookie 通过到报表服务器通过添加\< **PassThroughCookies**> RSReportServer.config 文件中的 web 门户的配置设置的元素。 在单一登录身份验证解决方案中，传输其他 Cookie 十分有用，因为此类解决方案不仅需要报表服务器身份验证 Cookie，而且还需要第三方身份验证系统中的 Cookie。

若要使其他 cookie 可以通过 HTTP 请求传输，使用 web 门户时，请在 RSReportServer.config 文件中设置下列元素：
  
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
  
## <a name="see-also"></a>另请参阅

[针对报表服务器的身份验证](../../reporting-services/security/authentication-with-the-report-server.md)   
[RsReportServer.config 配置文件](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
[安全扩展插件概述](../../reporting-services/extensions/security-extension/security-extensions-overview.md)   
[配置和管理报表服务器 &#40;SSRS 本机模式 &#41;](../../reporting-services/report-server/configure-and-administer-a-report-server-ssrs-native-mode.md)  
更多问题？ [尝试的 Reporting Services 论坛](http://go.microsoft.com/fwlink/?LinkId=620231)
