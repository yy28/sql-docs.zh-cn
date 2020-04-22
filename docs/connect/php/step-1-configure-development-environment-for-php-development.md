---
title: 步骤 1：配置 PHP 环境
description: 本入门指南的第 1 步涉及安装 PHP 和 Microsoft ODBC Driver for SQL Server，以及配置开发环境。
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 0bce6022-00bd-45c6-9671-eaa9dfa395a8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 88eb2c2c67eac3ecd9fba2c79c143de28cf60d22
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81633168"
---
# <a name="step-1-configure-environment-for-php-development"></a>步骤 1：配置用于 PHP 开发的环境
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]




* 根据环境确定你将使用的 PHP 驱动程序的版本，如下所述：[Microsoft Drivers for PHP for SQL Server 系统要求](system-requirements-for-the-php-sql-driver.md)
* 在此处下载并安装适用的 PHP 驱动程序：[下载 Microsoft PHP 驱动程序](https://www.microsoft.com/download/details.aspx?id=20098)  
* 在此处下载并安装适用的 ODBC 驱动程序：[下载 ODBC Driver for SQL Server](../odbc/download-odbc-driver-for-sql-server.md)  
* 为特定操作系统配置 PHP 驱动程序和 Web 服务器：

### <a name="windows"></a>Windows  
  

* 配置加载 PHP 驱动程序，如下所述：[加载 Microsoft Drivers for PHP for SQL Server](../../connect/php/loading-the-php-sql-driver.md) 
* 将 IIS 配置为托管 PHP 应用程序，如下所述：[为 Microsoft Drivers for PHP for SQL Server 配置 IIS](../../connect/php/configuring-iis-for-php-sql-driver.md)

### <a name="linux-and-macos"></a>Linux 和 macOS


*   配置加载 PHP 驱动程序并将 Web 服务器配置为托管 PHP 应用程序，如下所述：[PHP Linux 和 macOS 驱动程序安装教程](../../connect/php/installation-tutorial-linux-mac.md)
