---
title: Microsoft Drivers for PHP for SQL Server 发行说明
ms.custom: ''
ms.date: 07/20/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- what's new in version 1.1
ms.assetid: 91cca3d2-ba99-4a6d-b0de-beb9699cb3f8
caps.latest.revision: 37
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d06042b61e96da8e003cf893f86dac905832743b
ms.sourcegitcommit: b70b99c2e412b4d697021f3bf1a92046aafcbe37
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2018
ms.locfileid: "42785719"
---
# <a name="release-notes-for-the-microsoft-drivers-for-php-for-sql-server"></a>Microsoft Drivers for PHP for SQL Server 发行说明
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

此页介绍了中的每个版本的新增[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]。  

## <a name="whats-new-in-version-53"></a>版本 5.3 中的新增功能

- 在所有平台上支持 Microsoft ODBC 驱动程序 17.2
- 支持将 macOS High Sierra (需要 ODBC Driver 17 和更高版本)
- 支持 Azure 密钥保管库始终加密的基本 CRUD 功能这类的 Always Encrypted 功能是否适用于所有受支持的 Windows、 Linux 或 macOS 平台[使用始终加密与 SQL Server PHP 驱动程序](../../connect/php/using-always-encrypted-php-drivers.md)
- 支持 Ubuntu 18.04 LTS （需要 ODBC 驱动程序 17.2）
- 支持在 Linux 或 macOS （需要 ODBC 驱动程序 17.2） 以及连接复原

## <a name="whats-new-in-version-52"></a>版本 5.2 中的新增功能

- 对 PHP 7.2.1 支持 Windows 和 7.2.0 上最多支持其他平台上最多支持
- 支持的 Microsoft ODBC Driver 17
  - 现在在所有平台上的默认版本 17，是
- 支持 Ubuntu 17.10、 Debian 9 和 Suse Enterprise Linux 12
- 已删除的支持 Ubuntu 15.10
- 在 Windows 上的 CRUD 功能使用 Always encrypted 支持。 有关详细信息，请参阅[使用始终加密与 SQL Server PHP 驱动程序](../../connect/php/using-always-encrypted-php-drivers.md)
  - 对 Windows 证书存储区的支持
  - 支持始终加密仅使用 Microsoft ODBC Driver 17 及更高版本
- 对 Linux 和 macOS 上的非 UTF8 区域设置的支持
  - 使用 Microsoft ODBC Driver 17 及更高版本仅支持 Linux 和 macOS 上的非 UTF8 区域设置
- 对 Azure SQL 数据仓库的支持
- 对 Azure SQL 托管实例 （扩展个人预览版） 的支持


## <a name="whats-new-in-version-43"></a>版本 4.3 中的新增功能

- 对 PHP 7.1 的支持
- 支持将 macOS Sierra 和 macOS El Capitan
- 支持适用于 Ubuntu 15.10 和 Debian 8
- 已删除的支持 Ubuntu 15.04
- 通过透明网络 IP 解析的 Always On 可用性组的支持。 有关详细信息，请参阅 [Connection Options](../../connect/php/connection-options.md)。
- 添加了的对 sql_variant 数据类型限制。
- 在 Windows 中的空闲连接复原支持。 有关详细信息，请参阅 [Connection Options](../../connect/php/connection-options.md)。
- 连接池适用于 Linux 和 macOS 的支持。 有关详细信息，请参阅[连接池](../../connect/php/connection-pooling-microsoft-drivers-for-php-for-sql-server.md)。
- 使用 ActiveDirectoryPassword 和 SqlPassword 的 Azure Active Directory 身份验证的支持。 有关详细信息，请参阅 [Connection Options](../../connect/php/connection-options.md)。

## <a name="whats-new-in-version-40"></a>版本 4.0 中的新增功能

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
- 对 LocalDB 的支持，该功能已添加在 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]中。 有关详细信息，请参阅[对 LocalDB 的支持](../../connect/php/php-driver-for-sql-server-support-for-localdb.md)。
- 添加了 AttachDBFileName 连接选项。 有关详细信息，请参阅 [Connection Options](../../connect/php/connection-options.md)。  
- 对高可用性、灾难恢复功能的支持。 有关详细信息，请参阅[对高可用性和灾难恢复的支持](../../connect/php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)。
- 对客户端游标的支持（将结果集缓存到内存）。 有关详细信息，请参阅[游标类型（SQLSRV 驱动程序）](../../connect/php/cursor-types-sqlsrv-driver.md)和[游标类型（PDO_SQLSRV 驱动程序）](../../connect/php/cursor-types-pdo-sqlsrv-driver.md)。
- 添加了 PDO::ATTR_EMULATE_PREPARES 属性。 有关详细信息，请参阅 [PDO::prepare](../../connect/php/pdo-prepare.md)。  

## <a name="whats-new-in-version-20"></a>版本 2.0 中的新增功能  
在版本 2.0 中，添加了对 PDO_SQLSRV 驱动程序的支持。 有关详细信息，请参阅 [PDO_SQLSRV 驱动程序参考](../../connect/php/pdo-sqlsrv-driver-reference.md)。  

## <a name="see-also"></a>另请参阅  
[Microsoft Drivers for PHP for SQL Server 概述](../../connect/php/overview-of-the-php-sql-driver.md)
