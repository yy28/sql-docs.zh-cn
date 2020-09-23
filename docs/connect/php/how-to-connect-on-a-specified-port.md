---
title: 如何：在指定端口上连接
description: 了解如何使用用于 SQL Server 的 PHP 的 Microsoft SQLSRV 和 PDO_SQLSRV 驱动程序连接到特定端口上配置的数据库。
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connecting to the server, specifying a port
ms.assetid: 65a154d1-375c-439b-a653-7815c9d70ff3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b55f12bbfe4bbe255af2d62c2ed0c5ab3f968e98
ms.sourcegitcommit: 129f8574eba201eb6ade1f1620c6b80dfe63b331
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/30/2020
ms.locfileid: "87435232"
---
# <a name="how-to-connect-on-a-specified-port"></a>如何：在指定端口上连接
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

本主题介绍如何使用 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]在指定端口上连接到 SQL Server。  
  
### <a name="to-connect-on-a-specified-port"></a>在指定端口上连接  
  
1.  对服务器配置为接受连接的端口进行验证。 若要了解如何将服务器配置为接受指定端口上的连接，请参阅[如何：配置服务器以侦听特定 TCP 端口（SQL Server 配置管理器）](../../database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port.md)。  
  
2.  将所需端口添加到 sqlsrv_connect 函数的 [$serverName](../../connect/php/sqlsrv-connect.md) 参数。 用逗号分隔服务器名称和端口。 例如，以下代码行使用 SQLSRV 驱动程序来演示如何在端口 1521 上连接到名为 *myServer* 的服务器：  
  
    ```  
    $serverName = "myServer, 1521";  
    sqlsrv_connect( $serverName );  
    ```  
  
    以下代码行使用 PDO_SQLSRV 驱动程序来演示如何在端口 1521 上连接到名为 myServer 的服务器：  
  
    ```  
    $serverName = "(local), 1521";  
    $database = "AdventureWorks";  
    $conn = new PDO( "sqlsrv:server=$serverName;Database=$database", "", "");  
    ```  
  
## <a name="see-also"></a>另请参阅  
[连接到服务器](../../connect/php/connecting-to-the-server.md)

[Microsoft Drivers for PHP for SQL Server 编程指南](../../connect/php/programming-guide-for-php-sql-driver.md)

[开始使用 Microsoft Drivers for PHP for SQL Server](../../connect/php/getting-started-with-the-php-sql-driver.md)

[SQLSRV 驱动程序 API 参考](../../connect/php/sqlsrv-driver-api-reference.md)

[PDO_SQLSRV 驱动程序参考](../../connect/php/pdo-sqlsrv-driver-reference.md)  
  
