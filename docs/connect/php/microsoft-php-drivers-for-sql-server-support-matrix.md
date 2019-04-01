---
title: Microsoft Drivers for PHP for SQL Server 支持矩阵 |Microsoft Docs
ms.custom: ''
ms.date: 02/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: genemi
manager: ''
ms.openlocfilehash: 0790d2cc0497ef2912f96cd4679e4541fc9b2262
ms.sourcegitcommit: c60784d1099875a865fd37af2fb9b0414a8c9550
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2019
ms.locfileid: "58645499"
---
# <a name="microsoft-php-drivers-for-sql-server-support-matrix"></a>Microsoft PHP Drivers for SQL Server 支持矩阵

[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

本页包含 SQL Server 的 Microsoft PHP 驱动程序的支持矩阵和支持生命周期策略。

## <a name="microsoft-php-drivers-support-lifecycle-matrix-and-policy"></a>Microsoft PHP 驱动程序支持生命周期矩阵和策略

Microsoft 支持生命周期 (MSL) 策略提供了与 Microsoft 产品的支持生命周期有关的可预测透明信息。 PHP Driver 3.x 版、4.x 版和 5.x 版提供五年主要支持（自驱动程序发布之日起开始计算）。 主流支持在 [Microsoft 支持生命周期网站](https://support.microsoft.com/lifecycle)上定义。

Microsoft PHP 驱动程序不提供扩展和自定义支持选项。

支持以下 Microsoft PHP 驱动程序，直到指定的支持结束日期。

|驱动程序名称|驱动程序包版本|主流支持结束|
|-|:-:|-|
|SQL Server 的 Microsoft PHP 驱动程序 5.6|5.6|2024 年 2 月 21 日|
|SQL Server 的 Microsoft PHP 驱动程序 5.3|5.3|2023 年 7 月 20 日|
|SQL Server 的 Microsoft PHP 驱动程序 5.2|5.2|2023 年 2 月 9 日|
|SQL Server 的 Microsoft PHP 驱动程序 4.3|4.3|2022 年 7 月 6 日|
|SQL Server 的 Microsoft PHP 驱动程序 4.0|4.0|2021 年 7 月 11 日|
|Microsoft PHP Drivers 3.2 for SQL Server|3.2|于 2020 年 3 月 9日日|
|Microsoft PHP Drivers 3.1 for SQL Server|3.1|2019 年 12 月 12 日|
| &nbsp; | &nbsp; | &nbsp; |

不再支持以下 Microsoft PHP 驱动程序。

|驱动程序名称|驱动程序包版本|主流支持结束|
|-|:-:|-|
|SQL Server 的 Microsoft PHP 驱动程序 3.0|3.0|2017 年 3 月 6 日|
|SQL Server 的 Microsoft PHP 驱动程序 2.0|2.0|2015 年 8 月 10日日|
|SQL Server 的 Microsoft PHP 驱动程序 1.0|1.0|2014 年 4 月 28 日|
| &nbsp; | &nbsp; | &nbsp; |

## <a name="sql-server-version-certified-compatibility"></a>SQL Server 版本认证兼容性
 以下矩阵列出了经过测试和认证为与相应的驱动程序版本兼容的 SQL Server 版本。 我们将努力保持向后的兼容早期驱动程序版本，但测试和认证与新的 SQL Server 版本的 SQL Server 发布仅最新支持的驱动程序。

|SQL Server 驱动程序版本的 PHP&#8594;<br />&#8595; SQL Server 版本|5.6|5.3|5.2|4.3|4.0|3.2|3.1|3.0|2.0|
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|Azure SQL 托管实例<br/> （扩展个人预览版）|是|是|是|是| | | | | |
|Azure SQL 数据仓库|是|是|是|是| | | | | |
|SQL Server 2017         |是|是|是|是| | | | | |
|SQL Server 2016         |是|是|是|是|是| | | | |
|SQL Server 2014         |是|是|是|是|是|是|是| | |
|SQL Server 2012         |是|是|是|是|是|是|是|是| |
|SQL Server 2008 R2      |是|是|是|是|是|是|是|是|是|
|SQL Server 2008         | | | | |是|是|是|是|是|
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |

## <a name="php-version-support"></a>PHP 版本支持

与列出的版本的 Microsoft PHP 驱动程序支持以下版本的 PHP:

|SQL Server 驱动程序版本的 PHP&#8594;<br />&#8595; PHP 版本|5.6|5.3|5.2|4.3|4.0|3.2|3.1|3.0|2.0|
|:---:|---|---|---|---|---|---|---|---|---|
|7.3|7.3.0+          |                |                |       |       | | | | |
|7.2|7.2+<sup>1</sup>|7.2+<sup>1</sup>|7.2+<sup>1</sup>|       |       | | | | |
|7.1|7.1.0+          |7.1.0+          |7.1.0+          |7.1.0+ |       |        |        |        |        |
|7.0|                |7.0.0+          |7.0.0+          |7.0.0+ |7.0.0+ |        |        |        |        |
|5.6|                |                |                |       |       |5.6.4+  |        |        |        |
|5.5|                |                |                |       |       |5.5.16+ |5.5.16+ |        |        |
|5.4|                |                |                |       |       |5.4.32  |5.4.32  |5.4.32  |        |
|5.3|                |                |                |       |       |        |        |5.3.0   |5.3.0   |
|5.2|                |                |                |       |       |        |        |        |5.2.4<br />5.2.13|
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |

1. 版本 7.2.1 和更高版本上支持 Windows，同时版本 7.2.0 和更高版本支持 Linux 和 macOS 上。

## <a name="supported-operating-systems"></a>支持的操作系统

与列出的版本的 Microsoft PHP 驱动程序支持以下 Windows 操作系统版本：

|SQL Server 驱动程序版本的 PHP&#8594;<br />&#8595; 操作系统|5.6|5.3|5.2|4.3|4.0|3.2|3.1|3.0|2.0|
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|Windows Server 2016                 |是  |是  |是  |是  |   |   |   |   |   |
|Windows Server 2012 R2              |是  |是  |是  |是  |是  |是  |是  |   |   |
|Windows Server 2012                 |是  |是  |是  |是  |是  |是  |是  |   |   |
|Windows Server 2008 R2 SP1          |   |   |   |   |是  |是  |是  |是  |   |
|Windows Server 2008 R2              |   |   |   |   |   |   |   |   |是  |
|Windows Server 2008 SP2             |   |   |   |   |是  |是  |是  |是  |   |
|Windows Server 2008（可能为英文页面）                 |   |   |   |   |   |   |   |   |是  |
|Windows Server 2003 SP1             |   |   |   |   |   |   |   |   |是  |
|Windows 10                          |是  |是  |是  |是  |是  |   |   |   |   |
|Windows 8.1                         |是  |是  |是  |是  |是  |是  |是  |   |   |
|Windows 8                           |   |   |   |是  |是  |是  |是  |   |   |
|Windows 7 SP1                       |   |   |   |   |是  |是  |是  |是  |   |
|Windows Vista SP2                   |   |   |   |   |是  |是  |是  |是  |是  |
|Windows XP SP3                      |   |   |   |   |   |   |   |   |是  |
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |

与列出的版本的 Microsoft PHP 驱动程序支持以下 Linux 和 Mac 操作系统版本 （仅限 64 位）：

|SQL Server 驱动程序版本的 PHP&#8594;<br />&#8595; 操作系统|5.6|5.3|5.2|4.3|4.0|3.2|3.1|3.0|2.0|
|--|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|Ubuntu 18.10 （64 位）               |是  |   |   |   |   |   |   |   |   |
|Ubuntu 18.04 （64 位）               |是  |是  |   |   |   |   |   |   |   |
|Ubuntu 17.10 （64 位）               |   |是  |是  |   |   |   |   |   |   |
|Ubuntu 16.04 （64 位）               |是  |是  |是  |是  |是  |   |   |   |   |
|Ubuntu 15.10 （64 位）               |   |   |   |是  |   |   |   |   |   |
|Ubuntu 15.04 （64 位）               |   |   |   |   |是  |   |   |   |   |
|Debian 9 （64 位）                   |是  |是  |是  |   |   |   |   |   |   |
|Debian 8 （64 位）                   |是  |是  |是  |是  |   |   |   |   |   |
|Red Hat Enterprise Linux 7（64 位） |是  |是  |是  |是  |是  |   |   |   |   |
|Suse Enterprise Linux 15 （64 位）   |是  |   |   |   |   |   |   |   |   |
|Suse Enterprise Linux 12 （64 位）   |是  |是  |是  |   |   |   |   |   |   |
|macOS Mojave （64 位）               |是  |   |   |   |   |   |   |   |   |
|macOS High Sierra （64 位）          |是  |是  |   |   |   |   |   |   |   |
|macOS Sierra （64 位）               |是  |是  |是  |是  |   |   |   |   |   |
|macOS El Capitan （64 位）           |   |是  |是  |是  |   |   |   |   |   |
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |

## <a name="see-also"></a>另请参阅

[发行说明](../../connect/php/release-notes-php-sql-driver.md)

[支持资源](../../connect/php/support-resources-for-the-php-sql-driver.md)

[系统要求](../../connect/php/system-requirements-for-the-php-sql-driver.md)
