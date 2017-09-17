---
title: "PHP SQL 驱动程序的发行说明 |Microsoft 文档"
ms.custom: 
ms.date: 07/12/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- what's new in version 1.1
ms.assetid: 91cca3d2-ba99-4a6d-b0de-beb9699cb3f8
caps.latest.revision: 37
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2c63079bda91844995540aade94bac397be6b94c
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="release-notes-for-the-php-sql-driver"></a>PHP SQL 驱动程序的发行说明
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

本主题讨论每个版本中的新增[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]。  

## <a name="whats-new-in-version-43"></a>什么是版本 4.3 中的新增功能

- 对 PHP 7.1 的支持
- 对 Mac OS Sierra 和 Mac OS El Capitan 的支持
- 适用于 Ubuntu 15.10 和 Debian 8 的支持
- Ubuntu 15.04 拖放的支持
- 有关通过透明网络 IP 解析的 Always On 可用性组的支持。 有关详细信息，请参阅 [Connection Options](../../connect/php/connection-options.md)。 
- 添加了对具有限制的 sql_variant 数据类型的支持。
- 在 Windows 中的空闲连接复原支持。 有关详细信息，请参阅 [Connection Options](../../connect/php/connection-options.md)。
- 连接池适用于 Linux 和 macOS 的支持。 有关详细信息，请参阅[连接池](../../connect/php/connection-pooling-microsoft-drivers-for-php-for-sql-server.md)。
- 对于使用 ActiveDirectoryPassword 和 SqlPassword 的 Azure Active Directory 身份验证的支持。 有关详细信息，请参阅 [Connection Options](../../connect/php/connection-options.md)。
  
## <a name="whats-new-in-version-40"></a>什么是版本 4.0 中的新增功能 

- 对 PHP 7.0 的支持  
- 完整的 64 位支持
- 支持 Ubuntu 15.04、 Ubuntu 16.04 和 RedHat 7

## <a name="whats-new-in-version-32"></a>版本 3.2 中的新增功能 

- 对 PHP 5.6 的支持   
- 包括以前的 PHP 版本 5.5 和 5.4 的最新更新   
- 需要 Microsoft ODBC Driver 11 for SQL Server  
  
## <a name="whats-new-in-version-31"></a>版本 3.1 中的新增功能
 
- 对 PHP 5.5 的支持  
- 需要 Microsoft ODBC Driver 11 for SQL Server。 以前的版本要求 SQL Native Client。  
  
## <a name="whats-new-in-version-30"></a>版本 3.0 中的新增功能  

- 对 PHP 5.4 的支持。  [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]的版本 3 不支持 PHP 5.2。  
- 添加了 AttachDBFileName 连接选项。 有关详细信息，请参阅 [Connection Options](../../connect/php/connection-options.md)。  
- 对 LocalDB 的支持，该功能已添加在 [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)]中。 有关详细信息，请参阅 [PHP Driver for SQL Server Support for LocalDB](../../connect/php/php-driver-for-sql-server-support-for-localdb.md)。
- 添加了 AttachDBFileName 连接选项。 有关详细信息，请参阅 [Connection Options](../../connect/php/connection-options.md)。  
- 对高可用性、灾难恢复功能的支持。 有关详细信息，请参阅 [PHP Driver for SQL Server 对高可用性和灾难恢复的支持](../../connect/php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)。
- 对客户端游标的支持（将结果集缓存到内存）。 有关详细信息，请参阅[游标类型 &#40;SQLSRV 驱动程序 &#41;](../../connect/php/cursor-types-sqlsrv-driver.md)和[游标类型 &#40;PDO_SQLSRV 驱动程序 &#41;](../../connect/php/cursor-types-pdo-sqlsrv-driver.md).
- 添加了 PDO::ATTR_EMULATE_PREPARES 属性。 有关详细信息，请参阅[pdo:: prepare](../../connect/php/pdo-prepare.md)。  
  
## <a name="whats-new-in-version-20"></a>版本 2.0 中的新增功能  
在版本 2.0 中，添加了对 PDO_SQLSRV 驱动程序的支持。 有关详细信息，请参阅 [PDO_SQLSRV 驱动程序参考](../../connect/php/pdo-sqlsrv-driver-reference.md)。  
  
## <a name="see-also"></a>另请参阅  
[PHP SQL 驱动程序概述](../../connect/php/overview-of-the-php-sql-driver.md)
  

