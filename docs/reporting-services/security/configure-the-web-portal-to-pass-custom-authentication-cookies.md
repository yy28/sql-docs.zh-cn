---
title: 配置 Web 门户以传递自定义身份验证 Cookie | Microsoft Docs
ms.date: 04/18/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- authentication [Reporting Services]
- extensions [Reporting Services], custom security
ms.assetid: 91aeb053-149e-4562-ae4c-a688d0e1b2ba
author: markingmyname
ms.author: maghan
ms.openlocfilehash: b538523839be0260eda33934a18e682579aaa3f9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47810215"
---
# <a name="configure-the-web-portal-to-pass-custom-authentication-cookies"></a>配置 Web 门户以传递自定义身份验证 Cookie

如果使用自定义身份验证扩展插件，则应将 Web 门户配置为传输自定义身份验证 Cookie。 否则，Web 门户通过 HTTP 请求仅传输特定于报表服务器的 Cookie。 如果要传输其他 Cookie，则必须修改 RSReportServer.Config 文件。

## <a name="modifying-the-rsreportserverconfig-file"></a>修改 RSReportServer.Config 文件

通过将 \<PassThroughCookies> 元素添加到 RSReportServer.config 文件的 Web 门户配置设置中，可允许 [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] 将其他 Cookie 传输到报表服务器。 在单一登录身份验证解决方案中，传输其他 Cookie 十分有用，因为此类解决方案不仅需要报表服务器身份验证 Cookie，而且还需要第三方身份验证系统中的 Cookie。

使用 Web 门户时，为了使其他 Cookie 可以通过 HTTP 请求进行传输，请在 RSReportServer.config 文件中设置下列元素：
  
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
[配置和管理报表服务器（SSRS 本机模式）](../../reporting-services/report-server/configure-and-administer-a-report-server-ssrs-native-mode.md)  
更多疑问？ [请访问 Reporting Services 论坛](http://go.microsoft.com/fwlink/?LinkId=620231)
