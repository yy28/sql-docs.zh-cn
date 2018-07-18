---
title: Microsoft Drivers for PHP for SQL Server 支持矩阵 |Microsoft 文档
ms.custom: ''
ms.date: 03/26/2018
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
ms.openlocfilehash: 9aae3c88e1460304cf4b2bea7dbc529f31393bde
ms.sourcegitcommit: f16003fd1ca28b5e06d5700e730f681720006816
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/11/2018
ms.locfileid: "35307916"
---
# <a name="microsoft-php-drivers-for-sql-server-support-matrix"></a>SQL Server 支持矩阵的 Microsoft PHP 驱动程序
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

  SQL Server 的情况下，此页包含适用于 Microsoft PHP 驱动程序的支持矩阵和支持生命周期策略。

## <a name="microsoft-php-drivers-support-lifecycle-matrix-and-policy"></a>Microsoft PHP 驱动程序支持生命周期矩阵和策略
 Microsoft 支持生命周期 (MSL) 策略提供了与 Microsoft 产品的支持生命周期有关的可预测透明信息。 3.x、 4.x 和 5.x 具有五年的驱动程序的发布日期的主流支持的 PHP 驱动程序版本。 上定义主流支持[Microsoft 支持生命周期网站](https://support.microsoft.com/lifecycle)。

 扩展和自定义支持选项不可用于 Microsoft PHP 驱动程序。

 支持以下 Microsoft PHP 驱动程序，直到指定的支持结束日期为止。

|驱动程序名称|驱动程序包版本|终止主流支持|
|-|-|-|
|SQL Server 的 Microsoft PHP 驱动程序 5.2|5.2|2023 年 2 月 9 日|
|SQL Server 的 Microsoft PHP 驱动程序 4.3|4.3|2022 年 7 月 6 日|
|SQL Server 的 Microsoft PHP 驱动程序 4.0|4.0|2021 年 7 月 11 日|
|SQL Server 的 Microsoft PHP 驱动程序 3.2|3.2|于 2020 2020年 3 月 9日日|
|SQL Server 的 Microsoft PHP 驱动程序 3.1|3.1|2019 年 12 月 12 日|

 不再支持以下 Microsoft PHP 驱动程序。

|驱动程序名称|驱动程序包版本|终止主流支持|
|-|-|-|
|SQL Server 的 Microsoft PHP 驱动程序 3.0|3.0|2017 年 3 月 6 日|
|SQL Server 的 Microsoft PHP 驱动程序 2.0|2.0|2015 年 8 月 10日日|
|SQL Server 的 Microsoft PHP 驱动程序 1.0|1.0|2014 年 4 月 28 日，|

## <a name="sql-server-version-certified-compatibility"></a>SQL Server 版本认证兼容性
 下表列出了测试和认证为与相应的驱动程序版本兼容的 SQL Server 版本。 我们还尽量保持与以前的驱动程序版本的向后兼容，但只有最新支持驱动程序进行测试并发布 SQL Server 时用新的 SQL Server 版本认证。

|SQL Server 驱动程序版本的 PHP&#8594;<br />&#8595;SQL Server 版本|5.2<br />&nbsp;|4.3<br />&nbsp;|4.0<br />&nbsp;|3.2<br />&nbsp;|3.1<br />&nbsp;|3.0<br />&nbsp;|2.0<br />&nbsp;|
|---|---|---|---|---|---|---|---|
|Azure SQL 托管的实例<br/> （扩展特邀预览阶段）|是|是| | | | | |
|Azure SQL 数据仓库|是|是| | | | | |
|SQL Server 2017   |是|是| | | | | |
|SQL Server 2016   |是|是|是| | | | |
|SQL Server 2014   |是|是|是|是|是| | |
|SQL Server 2012   |是|是|是|是|是|是| |
|SQL Server 2008 R2|是|是|是|是|是|是|是|
|SQL Server 2008   | | |是|是|是|是|是|

## <a name="php-version-support"></a>PHP 版本支持
 与列出的版本的 Microsoft PHP 驱动程序支持以下版本的 PHP:

|SQL Server 驱动程序版本的 PHP&#8594;<br />&#8595;PHP 版本|5.2<br />&nbsp;|4.3<br />&nbsp;|4.0<br />&nbsp;|3.2<br />&nbsp;|3.1<br />&nbsp;|3.0<br />&nbsp;|2.0<br />&nbsp;|
|---|---|---|---|---|---|---|---|
|7.2|在 Windows 上的 7.2.1+<br/>在其他平台上的 7.2.0+| | | | | | |
|7.1|7.1.0+ |7.1.0+ |       |        |        |        |        |
|7.0|7.0.0+ |7.0.0+ |7.0.0+ |        |        |        |        |
|5.6|       |       |       |5.6.4+  |        |        |        |
|5.5|       |       |       |5.5.16+ |5.5.16+ |        |        |
|5.4|       |       |       |5.4.32  |5.4.32  |5.4.32  |        |
|5.3|       |       |       |        |        |5.3.0   |5.3.0   |
|5.2|       |       |       |        |        |        |5.2.4<br />5.2.13|

## <a name="supported-operating-systems"></a>支持的操作系统
 与列出的版本的 Microsoft PHP 驱动程序支持以下 Windows 操作系统版本：

|SQL Server 驱动程序版本的 PHP&#8594;<br />&#8595;操作系统|5.2<br />&nbsp;|4.3<br />&nbsp;|4.0<br />&nbsp;|3.2<br />&nbsp;|3.1<br />&nbsp;|3.0<br />&nbsp;|2.0<br />&nbsp;|
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

|SQL Server 驱动程序版本的 PHP&#8594;<br />&#8595;操作系统|5.2<br />&nbsp;|4.3<br />&nbsp;|4.0<br />&nbsp;|3.2<br />&nbsp;|3.1<br />&nbsp;|3.0<br />&nbsp;|2.0<br />&nbsp;|
|---|---|---|---|---|---|---|---|
|Ubuntu 17.10 （64 位）               |是  |   |   |   |   |   |   |
|Ubuntu 16.04 （64 位）               |是  |是  |是  |   |   |   |   |
|Ubuntu 15.10 （64 位）               |   |是  |   |   |   |   |   |
|Ubuntu 15.04 （64 位）               |   |   |是  |   |   |   |   |
|Debian 9 （64 位）                   |是  |   |   |   |   |   |   |
|Debian 8 （64 位）                   |是  |是  |   |   |   |   |   |
|Red Hat Enterprise Linux 7 （64 位） |是  |是  |是  |   |   |   |   |
|Suse Enterprise Linux 12 （64 位）   |是  |   |   |   |   |   |   |
|macOS Sierra （64 位）               |是  |是  |   |   |   |   |   |
|macOS El Capitan （64 位）           |是  |是  |   |   |   |   |   |

## <a name="see-also"></a>请参阅  
[发行说明](../../connect/php/release-notes-for-the-php-sql-driver.md)

[支持资源](../../connect/php/support-resources-for-the-php-sql-driver.md)

[系统要求](../../connect/php/system-requirements-for-the-php-sql-driver.md)
