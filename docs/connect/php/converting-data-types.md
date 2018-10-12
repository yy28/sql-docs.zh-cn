---
title: 转换数据类型 |Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 508542ec-cc28-4a17-80f4-52325d6a48db
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b6a7ed91da704fa81b0c8f101f8da5cd71ff48f9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47857195"
---
# <a name="converting-data-types"></a>转换数据类型
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

当向 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 发送数据或从其中检索数据时，[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 允许指定数据类型。 指定数据类型是可选的。 如果不指定数据类型，将使用默认类型。 此部分的主题介绍如何指定数据类型并提供有关默认数据类型的详细信息。  
  
## <a name="in-this-section"></a>本节内容  
  
|主题|描述|  
|---------|---------------|  
|[默认 SQL Server 数据类型](../../connect/php/default-sql-server-data-types.md)|在向服务器发送数据时，提供有关默认 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型的信息。|  
|[默认 PHP 数据类型](../../connect/php/default-php-data-types.md)|在从服务器检索数据时，提供有关默认 PHP 数据类型的信息。|  
|[如何：指定 SQL Server 数据类型](../../connect/php/how-to-specify-sql-server-data-types-when-using-the-sqlsrv-driver.md)|演示如何在向服务器发送数据时指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型。|  
|[如何：指定 PHP 数据类型](../../connect/php/how-to-specify-php-data-types.md)|演示如何在从服务器检索数据时指定 PHP 数据类型。|  
|[如何：使用内置 UTF-8 支持发送和检索 UTF-8 数据](../../connect/php/how-to-send-and-retrieve-utf-8-data-using-built-in-utf-8-support.md)|演示如何使用 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 对 UTF-8 数据的内置支持。<br /><br />已在 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 的版本 1.1 中添加了对 UTF-8 字符的支持。|  
|[如何：在 Linux 和 macOS 中发送和检索 ASCII 数据](../../connect/php/how-to-send-and-retrieve-ascii-data-in-linux-mac.md)|演示如何使用[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]的支持在 Linux 或 macOS 中的 ASCII 数据。<br /><br />5.2 版中添加了对 ASCII 字符在非 Windows 环境中支持[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]。|
  
## <a name="see-also"></a>另请参阅  
[适用于 SQL Server for PHP 编程 Microsoft 驱动程序的指南](../../connect/php/programming-guide-for-php-sql-driver.md)

[SQLSRV 驱动程序 API 参考](../../connect/php/sqlsrv-driver-api-reference.md)

[常量（Microsoft Drivers for PHP for SQL Server）](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)

[示例应用程序（SQLSRV 驱动程序）](../../connect/php/example-application-sqlsrv-driver.md)  
  
