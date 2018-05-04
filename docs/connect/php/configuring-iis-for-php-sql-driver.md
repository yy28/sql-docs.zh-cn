---
title: 将 IIS 配置为 Microsoft Drivers for PHP for SQL Server |Microsoft 文档
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- configuring, Internet Information Services
ms.assetid: d2dc75d3-9bf7-481c-85f2-8b6310b21461
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 48844cbd007b5da65ac9ba3df596212b39682c00
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="configuring-iis-for-the-microsoft-drivers-for-php-for-sql-server"></a>将 IIS 配置为 Microsoft Drivers for PHP for SQL Server
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

本主题提供对资源的链接上[Internet 信息服务 (IIS) 网站](https://www.iis.net/)相关配置 IIS 来托管 PHP 应用程序。 此处列出的资源特定于结合使用 FastCGI 与 IIS。 FastCGI 是一种标准协议，可允许应用程序框架的通用网关接口 (CGI) 可执行文件与 Web 服务器相连接。 FastCGI 与不同，标准 CGI 协议的 FastCGI 重复使用多个请求的 CGI 进程。  
  
## <a name="tutorials"></a>教程  
以下链接指向有关为 PHP 设置 FastCGI 以及在 IIS 6.0 和 IIS 7.0PHP 上托管 PHP 应用程序的教程：  
  
-   [FastCGI 与 PHP](https://docs.microsoft.com/iis/web-hosting/web-server-for-shared-hosting/fastcgi-with-php)  
-   [使用 FastCGI 托管在 IIS 7.0 上的 PHP 应用程序](https://docs.microsoft.com/iis/application-frameworks/install-and-configure-php-applications-on-iis/using-fastcgi-to-host-php-applications-on-iis)  
-   [使用 FastCGI 托管在 IIS 6.0 上的 PHP 应用程序](https://docs.microsoft.com/iis/application-frameworks/install-and-configure-php-applications-on-iis/using-fastcgi-to-host-php-applications-on-iis-60)  
-   [配置 IIS 6.0 的 FastCGI 扩展](https://docs.microsoft.com/iis/application-frameworks/install-and-configure-php-on-iis/configuring-the-fastcgi-extension-for-iis-60)  
  
## <a name="video-presentations"></a>视频演示文稿  
以下链接指向有关为 PHP 设置 FastCGI 和使用 IIS 7.0 功能托管 PHP 应用程序的视频演示文稿：  
  
-   [为 PHP 设置 FastCGI](https://docs.microsoft.com/en-us/iis/application-frameworks/running-php-applications-on-iis/set-up-fastcgi-for-php)  
-   [与在 Microsoft Internet Information Services 7 上的 PHP 合作](https://docs.microsoft.com/en-us/iis/application-frameworks/running-php-applications-on-iis/mix08-partying-with-php-on-microsoft-internet-information-services-7-and-above)  
  
## <a name="support-resources"></a>支持资源  
以下论坛提供对 IIS 上的 FastCGI 的社区支持：  
  
-   [FastCGI 处理程序](https://forums.iis.net/1103.aspx)  
-   [IIS 7-FastCGI 模块](https://forums.iis.net/1104.aspx)  
  
## <a name="see-also"></a>另请参阅  
[开始使用 Microsoft Drivers for PHP for SQL Server](../../connect/php/getting-started-with-the-php-sql-driver.md)

[For PHP for SQL Server 编程 Microsoft 驱动程序的指南](../../connect/php/programming-guide-for-php-sql-driver.md)

[SQLSRV 驱动程序 API 参考](../../connect/php/sqlsrv-driver-api-reference.md)

[常量（Microsoft Drivers for PHP for SQL Server）](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)  
  
