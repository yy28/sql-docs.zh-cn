---
title: Microsoft Drivers for PHP for SQL Server 支持矩阵 |Microsoft Docs
ms.custom: ''
ms.date: 07/20/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
caps.latest.revision: 1
author: David-Engel
ms.author: v-daveng
manager: ''
ms.openlocfilehash: 3ee34b40af4f72b32286067e5853c673f62ad240
ms.sourcegitcommit: ae25f8be8b18c4b89e560f80862ff245b0c6e065
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/26/2018
ms.locfileid: "39268765"
---
# <a name="microsoft-php-drivers-for-sql-server-support-matrix"></a>Microsoft PHP Drivers for SQL Server 支持矩阵
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

  本页包含 SQL Server 的 Microsoft PHP 驱动程序的支持矩阵和支持生命周期策略。

## <a name="microsoft-php-drivers-support-lifecycle-matrix-and-policy"></a>Microsoft PHP 驱动程序支持生命周期矩阵和策略
 Microsoft 支持生命周期 (MSL) 策略提供了与 Microsoft 产品的支持生命周期有关的可预测透明信息。 PHP 驱动程序版本 3.x、 4.x 和 5.x 有五年的主流支持从驱动程序发布日期。 主流支持在 [Microsoft 支持生命周期网站](https://support.microsoft.com/lifecycle)上定义。

 Microsoft PHP 驱动程序不提供扩展和自定义支持选项。

 支持以下 Microsoft PHP 驱动程序，直到指定的支持结束日期。

|驱动程序名称|驱动程序包版本|主流支持结束|
|-|-|-|
|SQL Server 的 Microsoft PHP 驱动程序 5.3|5.3|2023 年 7 月 20 日|
|SQL Server 的 Microsoft PHP 驱动程序 5.2|5.2|2023 年 2 月 9 日|
|SQL Server 的 Microsoft PHP 驱动程序 4.3|4.3|2022 年 7 月 6 日|
|SQL Server 的 Microsoft PHP 驱动程序 4.0|4.0|2021 年 7 月 11 日|
|Microsoft PHP Drivers 3.2 for SQL Server|3.2|于 2020 年 3 月 9日日|
|Microsoft PHP Drivers 3.1 for SQL Server|3.1|2019 年 12 月 12 日|

 不再支持以下 Microsoft PHP 驱动程序。

|驱动程序名称|驱动程序包版本|主流支持结束|
|-|-|-|
|SQL Server 的 Microsoft PHP 驱动程序 3.0|3.0|2017 年 3 月 6 日|
|SQL Server 的 Microsoft PHP 驱动程序 2.0|2.0|2015 年 8 月 10日日|
|SQL Server 的 Microsoft PHP 驱动程序 1.0|1.0|2014 年 4 月 28 日|

## <a name="sql-server-version-certified-compatibility"></a>SQL Server 版本认证兼容性
 以下矩阵列出了经过测试和认证为与相应的驱动程序版本兼容的 SQL Server 版本。 我们将努力保持向后的兼容早期驱动程序版本，但测试和认证与新的 SQL Server 版本的 SQL Server 发布仅最新支持的驱动程序。

|SQL Server 驱动程序版本的 PHP&#8594;<br />&#8595; SQL Server 版本|5.3 和 5.2<br />&nbsp;|4.3<br />&nbsp;|4.0<br />&nbsp;|3.2<br />&nbsp;|3.1<br />&nbsp;|3.0<br />&nbsp;|2.0<br />&nbsp;|
|---|---|---|---|---|---|---|---|
|Azure SQL 托管实例<br/> （扩展个人预览版）|是|是| | | | | |
|Azure SQL 数据仓库|是|是| | | | | |
|SQL Server 2017   |是|是| | | | | |
|SQL Server 2016   |是|是|是| | | | |
|SQL Server 2014   |是|是|是|是|是| | |
|SQL Server 2012   |是|是|是|是|是|是| |
|SQL Server 2008 R2|是|是|是|是|是|是|是|
|SQL Server 2008   | | |是|是|是|是|是|

## <a name="php-version-support"></a>PHP 版本支持
 与列出的版本的 Microsoft PHP 驱动程序支持以下版本的 PHP:

|SQL Server 驱动程序版本的 PHP&#8594;<br />&#8595; PHP 版本|5.3 和 5.2<br />&nbsp;|4.3<br />&nbsp;|4.0<br />&nbsp;|3.2<br />&nbsp;|3.1<br />&nbsp;|3.0<br />&nbsp;|2.0<br />&nbsp;|
|---|---|---|---|---|---|---|---|
|7.2|7.2.1+（在 Windows 上）<br/>在其他平台上 7.2.0+| | | | | | |
|7.1|7.1.0+ |7.1.0+ |       |        |        |        |        |
|7.0|7.0.0+ |7.0.0+ |7.0.0+ |        |        |        |        |
|5.6|       |       |       |5.6.4 +  |        |        |        |
|5.5|       |       |       |5.5.16 + |5.5.16 + |        |        |
|5.4|       |       |       |5.4.32  |5.4.32  |5.4.32  |        |
|5.3|       |       |       |        |        |5.3.0   |5.3.0   |
|5.2|       |       |       |        |        |        |5.2.4<br />5.2.13|

## <a name="supported-operating-systems"></a>支持的操作系统
 与列出的版本的 Microsoft PHP 驱动程序支持以下 Windows 操作系统版本：

|SQL Server 驱动程序版本的 PHP&#8594;<br />&#8595; 操作系统|5.3 和 5.2<br />&nbsp;|4.3<br />&nbsp;|4.0<br />&nbsp;|3.2<br />&nbsp;|3.1<br />&nbsp;|3.0<br />&nbsp;|2.0<br />&nbsp;|
|---|---|---|---|---|---|---|---|
|Windows Server 2016                 |是  |是  |   |   |   |   |   |
|Windows Server 2012 R2              |是  |是  |是  |是  |是  |   |   |
|Windows Server 2012                 |是  |是  |是  |是  |是  |   |   |
|Windows Server 2008 R2 SP1          |   |   |是  |是  |是  |是  |   |
|Windows Server 2008 R2              |   |   |   |   |   |   |是  |
|Windows Server 2008 SP2             |   |   |是  |是  |是  |是  |   |
|Windows Server 2008（可能为英文页面）                 |   |   |   |   |   |   |是  |
|Windows Server 2003 SP1             |   |   |   |   |   |   |是  |
|Windows 10                          |是  |是  |是  |   |   |   |   |
|Windows 8.1                         |是  |是  |是  |是  |是  |   |   |
|Windows 8                           |   |是  |是  |是  |是  |   |   |
|Windows 7 SP1                       |   |   |是  |是  |是  |是  |   |
|Windows Vista SP2                   |   |   |是  |是  |是  |是  |是  |
|Windows XP SP3                      |   |   |   |   |   |   |是  |

 与列出的版本的 Microsoft PHP 驱动程序支持以下 Linux 和 Mac 操作系统版本 （仅限 64 位）：

|SQL Server 驱动程序版本的 PHP&#8594;<br />&#8595; 操作系统|5.3<br />&nbsp;|5.2<br />&nbsp;|4.3<br />&nbsp;|4.0<br />&nbsp;|3.2<br />&nbsp;|3.1<br />&nbsp;|3.0<br />&nbsp;|2.0<br />&nbsp;|
|--|---|---|---|---|---|---|---|---|
|Ubuntu 18.04 （64 位）               |是  |   |   |   |   |   |   |   |
|Ubuntu 17.10 （64 位）               |是  |是  |   |   |   |   |   |   |
|Ubuntu 16.04 （64 位）               |是  |是  |是  |是  |   |   |   |   |
|Ubuntu 15.10 （64 位）               |   |   |是  |   |   |   |   |   |
|Ubuntu 15.04 （64 位）               |   |   |   |是  |   |   |   |   |
|Debian 9 （64 位）                   |是  |是  |   |   |   |   |   |   |
|Debian 8 （64 位）                   |是  |是  |是  |   |   |   |   |   |
|Red Hat Enterprise Linux 7（64 位） |是  |是  |是  |是  |   |   |   |   |
|Suse Enterprise Linux 12 （64 位）   |是  |是  |   |   |   |   |   |   |
|macOS High Sierra （64 位）          |是  |   |   |   |   |   |   |   |
|macOS Sierra （64 位）               |是  |是  |是  |   |   |   |   |   |
|macOS El Capitan （64 位）           |是  |是  |是  |   |   |   |   |   |

## <a name="see-also"></a>另请参阅  
[发行说明](../../connect/php/release-notes-for-the-php-sql-driver.md)

[支持资源](../../connect/php/support-resources-for-the-php-sql-driver.md)

[系统要求](../../connect/php/system-requirements-for-the-php-sql-driver.md)
