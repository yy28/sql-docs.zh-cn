---
title: 为 Drivers for PHP 配置 IIS
description: 了解如何配置 IIS 以托管使用 Drivers for PHP for SQL Server 的 PHP 应用程序。 此处列出的资源特定于结合使用 FastCGI 与 IIS。
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- configuring, Internet Information Services
ms.assetid: d2dc75d3-9bf7-481c-85f2-8b6310b21461
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7ab31be628d4c93f0e4331e3d63d47c4924a6fa7
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91726871"
---
# <a name="configuring-iis-for-the-microsoft-drivers-for-php-for-sql-server"></a>为 Microsoft Drivers for PHP for SQL Server 配置 IIS
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

本主题提供 [Internet Information Services (IIS) 网站](https://www.iis.net/)上的资源的链接，它们与配置 IIS 来托管 PHP 应用程序相关。 此处列出的资源特定于结合使用 FastCGI 与 IIS。 FastCGI 是一种标准协议，可允许应用程序框架的通用网关接口 (CGI) 可执行文件与 Web 服务器相连接。 FastCGI 与标准 CGI 协议不同，因为 FastCGI 将 CGI 进程重复用于多个请求。  
  
## <a name="tutorials"></a>教程  
以下链接指向有关为 PHP 设置 FastCGI 以及在 IIS 6.0 和 IIS 7.0PHP 上托管 PHP 应用程序的教程：  
  
-   [FastCGI 与 PHP](/iis/web-hosting/web-server-for-shared-hosting/fastcgi-with-php)  
-   [使用 FastCGI 在 IIS 7.0 上托管 PHP 应用程序](/iis/application-frameworks/install-and-configure-php-applications-on-iis/using-fastcgi-to-host-php-applications-on-iis)  
-   [使用 FastCGI 在 IIS 6.0 上托管 PHP 应用程序](/iis/application-frameworks/install-and-configure-php-applications-on-iis/using-fastcgi-to-host-php-applications-on-iis-60)  
-   [为 IIS 6.0 配置 FastCGI 扩展](/iis/application-frameworks/install-and-configure-php-on-iis/configuring-the-fastcgi-extension-for-iis-60)  
  
## <a name="video-presentations"></a>视频演示文稿  
以下链接指向有关为 PHP 设置 FastCGI 和使用 IIS 7.0 功能托管 PHP 应用程序的视频演示文稿：  
  
-   [为 PHP 设置 FastCGI](/iis/application-frameworks/running-php-applications-on-iis/set-up-fastcgi-for-php)  
-   [在 Microsoft Internet Information Services 7 上与 PHP 合作](/iis/application-frameworks/running-php-applications-on-iis/mix08-partying-with-php-on-microsoft-internet-information-services-7-and-above)  
  
## <a name="support-resources"></a>支持资源  
以下论坛提供对 IIS 上的 FastCGI 的社区支持：  
  
-   [FastCGI 处理程序](https://forums.iis.net/1103.aspx)  
-   [IIS 7 - FastCGI 模块](https://forums.iis.net/1104.aspx)  
  
## <a name="see-also"></a>另请参阅  
[开始使用 Microsoft Drivers for PHP for SQL Server](../../connect/php/getting-started-with-the-php-sql-driver.md)

[Microsoft Drivers for PHP for SQL Server 编程指南](../../connect/php/programming-guide-for-php-sql-driver.md)

[SQLSRV 驱动程序 API 参考](../../connect/php/sqlsrv-driver-api-reference.md)

[常量（Microsoft Drivers for PHP for SQL Server）](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)  
