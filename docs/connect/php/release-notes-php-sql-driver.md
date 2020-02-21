---
title: Microsoft Drivers for PHP for SQL Server 发行说明 | Microsoft Docs
ms.custom: ''
ms.date: 01/31/2020
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
ms.openlocfilehash: 5e279ba446e790a2262e5f0effe160632065dcba
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "76941212"
---
# <a name="release-notes-for-the-microsoft-drivers-for-php-for-sql-server"></a>Microsoft Drivers for PHP for SQL Server 发行说明

[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

本页讨论 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 的每个版本中添加的内容。  

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

## <a name="whats-new-in-version-58"></a>版本 5.8 中的新增功能

| 新建项 | 详细信息 |
| :------- | :------ |
| 添加了对 PHP 7.4 的支持。 | &nbsp; |
| 放弃了对 PHP 7.1 的支持。 | &nbsp; |
| 添加了对所有平台上 Microsoft ODBC 驱动程序 17.5 的支持。 | &nbsp; |
| 添加了对 Debian 10 和 Red Hat 8 的支持。 | 两者都需要 ODBC 驱动程序 17.4 或更高版本。 |
| 添加了对 macOS Catalina、Alpine Linux 3.11<sup>1</sup> 和 Ubuntu 19.10 的支持。 | 这些全都需要 ODBC 驱动程序 17.5 或更高版本。 |
| 放弃了对 SQL Server 2008 R2、macOS Sierra、Ubuntu 18.10 和 Ubuntu 19.04 的支持。 | &nbsp; |
| 连接到 SQL Server 时支持语言选项。 | &nbsp; |
| 支持 PHP 7.2 中引入的 PHP 扩展字符串类型。 | &nbsp; |
| 支持数据分类敏感度元数据检索。 | 需要 SQL Server 2019 和 ODBC 驱动程序 17.4.2 或更高版本。 |
| 支持具有安全 enclave 的 Always Encrypted。 | 需要 ODBC 驱动程序 17.4 或更高版本。 |
| 支持 Linux 和 macOS 中区域设置的可配置选项。 |
| 通过在提取时缓存元数据并省略冗余调用来提高性能。 | &nbsp; |
| &nbsp; | &nbsp; |

<sup>1</sup> 版本 5.8 中的 Alpine Linux 支持是实验性支持。

## <a name="whats-new-in-version-56"></a>版本 5.6 中的新增功能

| 新建项 | 详细信息 |
| :------- | :------ |
| 对 PHP 7.3 的支持。 | &nbsp; |
| 放弃了对 PHP 7.0 的支持。 | &nbsp; |
| 支持所有平台上的 Microsoft ODBC 驱动程序 17.3。 | &nbsp; |
| 支持 macOS Mojave。 | 需要 ODBC 驱动程序 17.3 或更高版本。 |
| 支持 Ubuntu 18.10 和 Suse Linux 15。 | 两者都需要 ODBC 驱动程序 17.3 或更高版本。 |
| 放弃了对 Linux Ubuntu 17.10 和 macOS El Capitan 的支持。 | &nbsp; |
| 支持 Azure AD 访问令牌。 | 在 Linux 和 macOS 中，需要 ODBC 驱动程序 17.2+ 和 unixODBC 2.3.6+。 |
| 支持使用 Azure 资源的托管标识对 Azure AD 进行身份验证。 | 需要 ODBC Driver 17.3+。 |
| 新提取功能 | &bull; &nbsp; pdo_sqlsrv 的 新 PDO::SQLSRV_ATTR_FETCHES_DATETIME_TYPE 标志将日期时间作为对象返回。<br/><br/>&bull; &nbsp; 将 ReturnDatesAsStrings 选项添加到 sqlsrv 的语句级别。<br/><br/>&bull; &nbsp; 两个驱动程序在连接级别和语句级别的新选项，用于在提取的结果中格式化十进制值。 |
| 如果用户选择从源进行构建，则支持对驱动程序进行静态编译。 | &nbsp; |
| 通过在提取时缓存元数据并加快 Unicode 字符串转换来提高性能。 | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="whats-new-in-version-53"></a>版本 5.3 中的新增功能

- 支持所有平台上的 Microsoft ODBC 驱动程序 17.2
- 支持 macOS High Sierra（需要 ODBC 驱动程序 17 及更高版本）
- 支持 Always Encrypted 的 Azure 密钥保管库以实现基本 CRUD 功能，例如，所有受支持的 Windows、Linux 或 macOS 平台都可以使用 Always Encrypted 功能[将 Always Encrypted 与用于 SQL Server 的 PHP 驱动程序结合使用](../../connect/php/using-always-encrypted-php-drivers.md)
- 支持 Ubuntu 18.04 LTS（需要 ODBC 驱动程序 17.2）
- 同时还支持 Linux 或 macOS 中的连接弹性（需要 ODBC 驱动程序 17.2）

## <a name="whats-new-in-version-52"></a>版本 5.2 中的新增功能

- 在 Windows 上支持 PHP 7.2.1 和更高版本，在其他平台上支持 7.2.0 和更高版本
- 支持 Microsoft ODBC 驱动程序 17
  - 现在，版本 17 是所有平台上的默认设置
- 支持 Ubuntu 17.10、Debian 9 和 Suse Enterprise Linux 12
- 放弃了对 Ubuntu 15.10 的支持
- 在 Windows 上支持带有 CRUD 功能的 Always Encrypted。 有关详细信息，请参阅[结合使用 Always Encrypted 和 PHP Driver for SQL Server](../../connect/php/using-always-encrypted-php-drivers.md)
  - 支持 Windows 证书存储
  - 仅 Microsoft ODBC 驱动程序 17 及更高版本支持 Always Encrypted
- 支持 Linux 和 macOS 上的非 UTF8 区域设置
  - 仅 Microsoft ODBC 驱动程序 17 及更高版本支持 Linux 和 macOS 上的非 UTF8 区域设置
- 对 Azure SQL 数据仓库的支持
- 支持 Azure SQL 托管实例

## <a name="whats-new-in-version-43"></a>版本 4.3 中的新增功能

- 对 PHP 7.1 的支持
- 支持 macOS Sierra 和 macOS El Capitan
- 支持 Ubuntu 15.10 和 Debian 8
- 放弃了对 Ubuntu 15.04 的支持
- 通过透明网络 IP 解析支持 AlwaysOn 可用性组。 有关详细信息，请参阅 [Connection Options](../../connect/php/connection-options.md)。
- 添加了对 sql_variant 数据类型的支持，但有限制。
- Windows 中的空闲连接弹性支持。 有关详细信息，请参阅 [Connection Options](../../connect/php/connection-options.md)。
- 适用于 Linux 和 macOS 的连接池支持。 有关详细信息，请参阅[连接池](../../connect/php/connection-pooling-microsoft-drivers-for-php-for-sql-server.md)。
- 通过 ActiveDirectoryPassword 和 SqlPassword 支持 Azure Active Directory 身份验证。 有关详细信息，请参阅 [Connection Options](../../connect/php/connection-options.md)。

## <a name="whats-new-in-version-40"></a>版本 4.0 中的新增功能

- 对 PHP 7.0 的支持  
- 完整的 64 位支持
- 支持 Ubuntu 15.04、Ubuntu 16.04 和 RedHat 7

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
- 对 LocalDB 的支持，该功能已添加在 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 中。 有关详细信息，请参阅[支持 LocalDB](../../connect/php/php-driver-for-sql-server-support-for-localdb.md)。
- 添加了 AttachDBFileName 连接选项。 有关详细信息，请参阅 [Connection Options](../../connect/php/connection-options.md)。  
- 对高可用性、灾难恢复功能的支持。 有关详细信息，请参阅 [对高可用性和灾难恢复的支持](../../connect/php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)。
- 对客户端游标的支持（将结果集缓存到内存）。 有关详细信息，请参阅[游标类型（SQLSRV 驱动程序）](../../connect/php/cursor-types-sqlsrv-driver.md)和[游标类型（PDO_SQLSRV 驱动程序）](../../connect/php/cursor-types-pdo-sqlsrv-driver.md)。
- 添加了 PDO::ATTR_EMULATE_PREPARES 属性。 有关详细信息，请参阅 [PDO::prepare](../../connect/php/pdo-prepare.md)。  

## <a name="whats-new-in-version-20"></a>版本 2.0 中的新增功能

在版本 2.0 中，添加了对 PDO_SQLSRV 驱动程序的支持。 有关详细信息，请参阅 [PDO_SQLSRV 驱动程序参考](../../connect/php/pdo-sqlsrv-driver-reference.md)。  

## <a name="see-also"></a>另请参阅

[Microsoft Drivers for PHP for SQL Server 概述](../../connect/php/overview-of-the-php-sql-driver.md)
