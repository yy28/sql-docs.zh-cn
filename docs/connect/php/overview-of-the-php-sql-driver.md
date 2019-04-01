---
title: Microsoft Drivers for PHP for SQL Server 概述 | Microsoft Docs
ms.custom: ''
ms.date: 03/27/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 66559249-34c0-409d-b919-9b5bf0c4c9ec
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f2129745a8732fba882da6da1caf22e80df11f47
ms.sourcegitcommit: c60784d1099875a865fd37af2fb9b0414a8c9550
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2019
ms.locfileid: "58645479"
---
# <a name="overview-of-the-microsoft-drivers-for-php-for-sql-server"></a>Microsoft Drivers for PHP for SQL Server 概述

[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 是 PHP 扩展，用于提供对 SQL Server 2005 及更高版本（包括 Azure SQL 数据库）的数据访问。 扩展提供过程接口使用 SQLSRV 驱动程序和面向对象的接口使用 PDO_SQLSRV 驱动程序用于访问中的 SQL Server，包括 Express，从 SQL Server 2005 开始的所有版本的数据。 SQL Server 2008 开始支持版本 3.1 和更高版本的驱动程序。 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] API 包括对 Windows 身份验证、事务、参数绑定、流式传输、元数据访问和错误处理的支持。  
  
若要使用[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]、 必须具有正确版本的 SQL Server Native Client 或 Microsoft ODBC 驱动程序安装在同一台计算机 PHP 上运行。  有关详细信息，请参阅[Microsoft Drivers for PHP for SQL Server 的系统要求](../../connect/php/system-requirements-for-the-php-sql-driver.md)。  
  
## <a name="in-this-section"></a>本节内容  
  
|主题|描述|  
|---------|---------------|  
| ![下载向下箭头线圈出](../../ssdt/media/download.png)[若要下载驱动程序 for PHP for SQL Server](download-drivers-php-sql-server.md) | 下载 Microsoft Drivers for PHP for SQL Server 的链接。 |
|[Microsoft Drivers for PHP for SQL Server 发行说明](../../connect/php/release-notes-php-sql-driver.md)|列出版本 4.0、3.2、3.1、3.0 和 2.0 中的新增功能。|  
|[Microsoft Drivers for PHP for SQL Server 的支持资源](../../connect/php/support-resources-for-the-php-sql-driver.md)|在开发使用 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]的应用程序时，提供可能有用的资源的链接。|  
|[文档中相关的代码示例](../../connect/php/about-code-examples-in-the-documentation.md)|在运行本文档中的代码示例时，提供可能有用的信息。|  
| &nbsp; | &nbsp; |

## <a name="reference"></a>参考

[SQLSRV 驱动程序 API 参考](../../connect/php/sqlsrv-driver-api-reference.md)  
[PDO_SQLSRV 驱动程序参考](../../connect/php/pdo-sqlsrv-driver-reference.md)  
[常量（Microsoft Drivers for PHP for SQL Server）](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)  

## <a name="see-also"></a>另请参阅

[开始使用 Microsoft Drivers for PHP for SQL Server](../../connect/php/getting-started-with-the-php-sql-driver.md)

[适用于 SQL Server for PHP 编程 Microsoft 驱动程序的指南](../../connect/php/programming-guide-for-php-sql-driver.md)

[示例应用程序（SQLSRV 驱动程序）](../../connect/php/example-application-sqlsrv-driver.md)
