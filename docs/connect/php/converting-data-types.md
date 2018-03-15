---
title: "转换数据类型 |Microsoft 文档"
ms.custom: 
ms.date: 01/16/2018
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
ms.assetid: 508542ec-cc28-4a17-80f4-52325d6a48db
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 177f4cc6c28a231fe37df65a46976c4c8836e912
ms.sourcegitcommit: 6b1618aa3b24bf6759b00a820e09c52c4996ca10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/15/2018
---
# <a name="converting-data-types"></a>转换数据类型
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

当向 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 发送数据或从其中检索数据时， [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]允许你指定数据类型。 指定数据类型是可选的。 如果不指定数据类型，将使用默认类型。 此部分的主题介绍如何指定数据类型并提供有关默认数据类型的详细信息。  
  
## <a name="in-this-section"></a>本節內容  
  
|主题|Description|  
|---------|---------------|  
|[默认 SQL Server 数据类型](../../connect/php/default-sql-server-data-types.md)|在向服务器发送数据时，提供有关默认 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 数据类型的信息。|  
|[默认 PHP 数据类型](../../connect/php/default-php-data-types.md)|在从服务器检索数据时，提供有关默认 PHP 数据类型的信息。|  
|[如何：指定 SQL Server 数据类型](../../connect/php/how-to-specify-sql-server-data-types-when-using-the-sqlsrv-driver.md)|演示如何在向服务器发送数据时指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 数据类型。|  
|[如何：指定 PHP 数据类型](../../connect/php/how-to-specify-php-data-types.md)|演示如何在从服务器检索数据时指定 PHP 数据类型。|  
|[如何：使用内置 UTF-8 支持发送和检索 UTF-8 数据](../../connect/php/how-to-send-and-retrieve-utf-8-data-using-built-in-utf-8-support.md)|演示如何使用[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]的 utf-8 数据的内置支持。<br /><br />版本 1.1 中添加了对 utf-8 字符支持[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]。|  
|[如何： 发送和检索在 Linux 和 macOS ASCII 数据](../../connect/php/how-to-send-and-retrieve-ascii-data-in-linux-mac.md)|演示如何使用[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]的 Linux 或 macOS 中 ASCII 数据支持。<br /><br />5.2 版中添加了对在非 Windows 环境中的 ASCII 字符支持[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]。|
  
## <a name="see-also"></a>另请参阅  
[PHP SQL 驱动程序的编程指南](../../connect/php/programming-guide-for-php-sql-driver.md)
[SQLSRV 驱动程序 API 参考](../../connect/php/sqlsrv-driver-api-reference.md)  
[常量（Microsoft Drivers for PHP for SQL Server）](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)  
[示例应用程序（SQLSRV 驱动程序）](../../connect/php/example-application-sqlsrv-driver.md)  
  
