---
title: 默认 SQL Server 数据类型 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- default data types
- converting data types
ms.assetid: 65c7c211-96d3-4e65-a1de-1fe8d21348e7
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 69c138e7eb5d2c4f6dbace0db59ce235e1c0a5f9
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "67993658"
---
# <a name="default-sql-server-data-types"></a>默认 SQL Server 数据类型
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

在向服务器发送数据时，如果用户未指定任何 SQL Server 数据类型， [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 会将其 PHP 数据类型中的数据转换为 SQL Server 数据类型。 下表列出了 PHP 数据类型（向服务器发送的数据类型）和默认 SQL Server 数据类型（数据转换到的数据类型）。 有关如何在向服务器发送数据时指定数据类型的详细信息，请参阅[如何：在使用 SQLSRV 驱动程序时指定 SQL Server 数据类型](../../connect/php/how-to-specify-sql-server-data-types-when-using-the-sqlsrv-driver.md)。  
  
|PHP 数据类型|SQLSRV 驱动程序中的默认 SQL Server 类型|PDO_SQLSRV 驱动程序中的默认 SQL Server 类型|  
|-----------------|------------------------------------------------|-----------------------------------------------------|  
|Null|varchar(1)|不支持|  
|Boolean|bit|bit|  
|Integer|int|int|  
|Float|float(24)|不支持|  
|字符串（长度小于 8000 个字节）|varchar(<string length>)|varchar(<string length>)|  
|字符串（长度大于 8000 个字节）|varchar(max)|varchar(max)|  
|资源|不支持。|不支持。|  
|流（编码：不是二进制）|varchar(max)|varchar(max)|  
|流（编码：二进制）|varbinary|varbinary|  
|Array|不支持。|不支持。|  
|Object|不支持。|不支持。|  
|DateTime (1)|datetime|不支持。|  
  
## <a name="see-also"></a>另请参阅  
[常量（Microsoft Drivers for PHP for SQL Server）](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)

[转换数据类型](../../connect/php/converting-data-types.md)

[sqlsrv_field_metadata](../../connect/php/sqlsrv-field-metadata.md)

[PHP 类型](https://php.net/manual/language.types.php)

[数据类型 (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/data-types/data-types-transact-sql)  
  
