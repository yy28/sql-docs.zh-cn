---
title: 步骤 1：配置用于 PHP 开发的开发环境 | Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 0bce6022-00bd-45c6-9671-eaa9dfa395a8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 722b1094327ba7ccfce71e5066e683e8a2229aef
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47771595"
---
# <a name="step-1-configure-environment-for-php-development"></a>步骤 1： 配置用于 PHP 开发环境
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]




* 确定要使用哪个版本的 PHP 驱动程序，根据你的环境，按照此处所述： [Microsoft Drivers for PHP for SQL Server 的系统要求](../../connect/php/system-requirements-for-the-php-sql-driver.md)
* 下载并安装适用的 PHP 驱动此处：[下载 Microsoft PHP 驱动程序](https://www.microsoft.com/download/details.aspx?id=20098)  
* 下载并安装适用的 ODBC 驱动此处：[下载 ODBC Driver for SQL Server](../../connect/odbc/download-odbc-driver-for-sql-server.md)  
* 配置 PHP 驱动程序和适用于特定操作系统的 web 服务器：

### <a name="windows"></a>Windows  
  

* 配置加载 PHP 驱动程序，按照此处所述：[加载 Microsoft Drivers for PHP for SQL Server](../../connect/php/loading-the-php-sql-driver.md) 
* 将 IIS 配置托管 PHP 应用程序，按照此处所述：[配置 IIS 以实现 Microsoft Drivers for PHP for SQL Server](../../connect/php/configuring-iis-for-php-sql-driver.md)

### <a name="linux-and-mac"></a>Linux 和 Mac


*   配置 PHP 驱动程序加载和配置 web 服务器托管 PHP 应用程序，按照此处所述： [PHP Linux 和 Mac 驱动程序安装教程](../../connect/php/installation-tutorial-linux-mac.md)
