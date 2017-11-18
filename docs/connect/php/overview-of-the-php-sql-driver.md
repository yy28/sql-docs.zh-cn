---
title: "PHP SQL 驱动程序概述 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: php
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 66559249-34c0-409d-b919-9b5bf0c4c9ec
caps.latest.revision: 73
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 4badc426f6dbff44784bd8487b04bc0665d959ad
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="overview-of-the-php-sql-driver"></a>PHP SQL 驱动程序概述

![下载向下箭头带圆圈](../../ssdt/media/download.png)[下载适用于 SQL Server PHP 驱动程序](../sql-connection-libraries.md#anchor-20-drivers-relational-access)

[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]是一个 PHP 扩展，提供对 SQL Server 2005 和更高版本包括 Azure SQL Database 数据访问。 扩展提供的过程接口 （SQLSRV 驱动程序） 和面向对象的接口 （PDO_SQLSRV 驱动程序） 用于访问所有版本 （包括 Express） 中的数据从 SQL Server 2005 （支持 for PHP for SQL Server 版本 3.1 和更高版本开始开始使用 SQL Server 2008）。 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] API 包括对 Windows 身份验证、事务、参数绑定、流式传输、元数据访问和错误处理的支持。  
  
若要使用[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]必须具有正确版本的 SQL Server Native Client 或运行 PHP 的同一台计算机上安装的 Microsoft ODBC 驱动程序。  有关详细信息，请参阅 [PHP SQL 驱动程序的系统要求](../../connect/php/system-requirements-for-the-php-sql-driver.md)。  
  
## <a name="in-this-section"></a>本节内容  
  
|主题|Description|  
|---------|---------------|  
| ![下载向下箭头带圆圈](../../ssdt/media/download.png)[下载适用于 SQL Server PHP 驱动程序](../sql-connection-libraries.md#anchor-20-drivers-relational-access) | Microsoft SQL Server PHP 驱动程序的源代码下载链接。 |
|[PHP SQL 驱动程序的发行说明](../../connect/php/release-notes-for-the-php-sql-driver.md)|列出已添加版本 4.0、 3.2、 3.1、 3.0 和 2.0 的功能。|  
|[PHP SQL 驱动程序支持资源](../../connect/php/support-resources-for-the-php-sql-driver.md)|在开发使用 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]的应用程序时，提供可能有用的资源的链接。|  
|[文档中相关的代码示例](../../connect/php/about-code-examples-in-the-documentation.md)|在运行本文档中的代码示例时，提供可能有用的信息。|  
  
## <a name="reference"></a>参考  
[SQLSRV 驱动程序 API 参考](../../connect/php/sqlsrv-driver-api-reference.md)  
[PDO_SQLSRV 驱动程序参考](../../connect/php/pdo-sqlsrv-driver-reference.md)  
[常量（Microsoft Drivers for PHP for SQL Server）](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)  
  
## <a name="see-also"></a>另请参阅  
[PHP SQL 驱动程序入门](../../connect/php/getting-started-with-the-php-sql-driver.md)
[PHP SQL 驱动程序编程指南](../../connect/php/programming-guide-for-php-sql-driver.md)
[示例应用程序 &#40;SQLSRV 驱动程序 &#41;](../../connect/php/example-application-sqlsrv-driver.md)

