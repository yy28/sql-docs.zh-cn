---
title: 连接池 (Microsoft Drivers for PHP for SQL Server)
ms.custom: ''
ms.date: 07/10/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- connection pooling support
ms.assetid: 4d9a83d4-08de-43a1-975c-0a94005edc94
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2a332153e4e2651079198dac5b4390c3b56d550d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MTE
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="connection-pooling-microsoft-drivers-for-php-for-sql-server"></a>连接池 (Microsoft Drivers for PHP for SQL Server)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

有关 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]中的连接池，需要注意以下要点：  
  
-   [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 使用 ODBC 连接池。  
  
-   默认情况下，启用连接池。 在 Linux 和 Mac OS X 中，连接建立池连接才适用于 ODBC 启用连接池。 启用连接池后，连接到服务器时的驱动程序将尝试使用已入池的连接，然后它会创建一个新。 如果在池中未找到等效连接，将创建新的连接，并将其添加到该池中。 该驱动程序将基于连接字符串的比较结果确定连接是否等效。  
  
-   当使用池中的某个连接时，会重置该连接状态。  
  
-   关闭连接会将该连接返回到池。  
  
有关连接池的详细信息，请参阅 [驱动程序管理器连接池](../../odbc/reference/develop-app/driver-manager-connection-pooling.md)。  
  
## <a name="enablingdisabling-connection-pooling"></a>启用/禁用连接池
### <a name="windows"></a>Windows
可以通过将连接字符串中的 **ConnectionPooling** 属性值设置为 false（或 0），强制驱动程序创建新连接（而不是在连接池中查找等效连接）。  
  
如果连接字符串中省略了 *ConnectionPooling* 属性，或如果该属性设置为 **true**（或 1），仅当连接池中不存在等效连接时，该驱动程序才会创建新连接。  
  
有关其他连接属性的信息，请参阅 [Connection Options](../../connect/php/connection-options.md)。  
### <a name="linux-and-mac-os-x"></a>Linux 和 Mac OS X
*ConnectionPooling*属性不能用于启用/禁用连接池。 

连接池可启用/禁用通过编辑 odbcinst.ini 配置文件。 以使更改生效，应重新加载驱动程序。

设置`Pooling`到`Yes`和一个值为正`CPTimeout`odbcinst.ini 中的值，将启用连接池。 
```
[ODBC]
Pooling=Yes

[ODBC Driver 13 for SQL Server]
CPTimeout=<int value>
```
设置`Pooling`到`No`odbcinst.ini 中强制驱动程序来创建新的连接。
```
[ODBC]
Pooling=No
```
  
## <a name="see-also"></a>另请参阅  
[如何：使用 Windows 身份验证进行连接](../../connect/php/how-to-connect-using-windows-authentication.md)

[如何：使用 SQL Server 身份验证进行连接](../../connect/php/how-to-connect-using-sql-server-authentication.md)  
  
