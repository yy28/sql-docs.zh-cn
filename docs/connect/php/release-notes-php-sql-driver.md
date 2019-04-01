---
title: Microsoft Drivers for PHP for SQL Server 发行说明 | Microsoft Docs
ms.custom: ''
ms.date: 02/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: v-dapugl, kenvh
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- what's new in version 1.1
ms.assetid: 91cca3d2-ba99-4a6d-b0de-beb9699cb3f8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 48c4497dfa8974fe5fd59747d4b7023002d3f762
ms.sourcegitcommit: c60784d1099875a865fd37af2fb9b0414a8c9550
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2019
ms.locfileid: "58646412"
---
# <a name="release-notes-for-the-microsoft-drivers-for-php-for-sql-server"></a>Microsoft Drivers for PHP for SQL Server 发行说明

[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

此页介绍了中的每个版本的新增[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]。  

<!--
Hello, We are standardizing the format of content inside our Release Notes (or What's New) articles.
Instead of bullets (or paragraphs), we have shifted to the 2-column format you see for H2 **What's New in Version 5.6**.
It is not necessary to reformat all the older H2 sections in this Release Notes file, but.....

Going forward, please be sure to use the 2-column format.

Also, all Release Notes .md file names now must begin with 'release-notes-*.md'.  And no filler words.
The 5.6 edition of this file is being renamed.....
FROM:  'release-notes-for-the-php-sql-driver.md'
TO  :  'release-notes-php-sql-driver.md'

For any questions, ask GeneMi or CraigG.
Thanks a lot.  2019-03-28  (DevO= 1467988)
-->

## <a name="whats-new-in-version-56"></a>版本 5.6 中的新增功能

| 新建项 | 详细信息 |
| :------- | :------ |
| 对 PHP 7.3 的支持。 | &nbsp; |
| 对于 PHP 7.0 的拖放的支持。 | &nbsp; |
| 在所有平台上 Microsoft ODBC 驱动程序 17.3 支持。 | &nbsp; |
| 支持将 macOS Mojave。 | 需要 ODBC 驱动程序 17.3 或更高版本。 |
| 支持 Ubuntu 18.10 和 Suse Linux 15。 | 两者都需要 ODBC 驱动程序 17.3 或更高版本。 |
| 删除适用于 Linux Ubuntu 17.10 和 macOS El Capitan 的支持。 | &nbsp; |
| 对 Azure AD 访问令牌的支持。 | 在 Linux 和 macOS，需要 ODBC 驱动程序 17.2 + 和 unixODBC 2.3.6+。 |
| 对 Azure 资源的使用托管标识的 Azure AD 身份验证的支持。 | 需要 ODBC 驱动程序 17.3 +。 |
| 新的提取功能 | &bull; &nbsp; Pdo_sqlsrv 以对象形式返回日期时间的新 PDO::SQLSRV_ATTR_FETCHES_DATETIME_TYPE 标志。<br/><br/>&bull; &nbsp; 将 ReturnDatesAsStrings 选项添加到 sqlsrv 的语句级别。<br/><br/>&bull; &nbsp; 在这两种用于提取结果中的十进制值的格式的驱动程序的连接和语句级别的新选项。 |
| 如果用户选择从源生成的驱动程序的静态编译的支持。 | &nbsp; |
| 通过缓存提取的元数据并加快 Unicode 字符串转换的改进了的性能。 | &nbsp; |
| &nbsp; | &nbsp; |

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
- 对 LocalDB 的支持，该功能已添加在 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 中。 有关详细信息，请参阅[对 LocalDB 的支持](../../connect/php/php-driver-for-sql-server-support-for-localdb.md)。
- 添加了 AttachDBFileName 连接选项。 有关详细信息，请参阅 [Connection Options](../../connect/php/connection-options.md)。  
- 对高可用性、灾难恢复功能的支持。 有关详细信息，请参阅[对高可用性和灾难恢复的支持](../../connect/php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)。
- 对客户端游标的支持（将结果集缓存到内存）。 有关详细信息，请参阅[游标类型（SQLSRV 驱动程序）](../../connect/php/cursor-types-sqlsrv-driver.md)和[游标类型（PDO_SQLSRV 驱动程序）](../../connect/php/cursor-types-pdo-sqlsrv-driver.md)。
- 添加了 PDO::ATTR_EMULATE_PREPARES 属性。 有关详细信息，请参阅 [PDO::prepare](../../connect/php/pdo-prepare.md)。  

## <a name="whats-new-in-version-20"></a>版本 2.0 中的新增功能

在版本 2.0 中，添加了对 PDO_SQLSRV 驱动程序的支持。 有关详细信息，请参阅 [PDO_SQLSRV 驱动程序参考](../../connect/php/pdo-sqlsrv-driver-reference.md)。  

## <a name="see-also"></a>另请参阅

[Microsoft Drivers for PHP for SQL Server 概述](../../connect/php/overview-of-the-php-sql-driver.md)
