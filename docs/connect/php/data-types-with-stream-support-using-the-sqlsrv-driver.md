---
title: 使用 SQLSRV 驱动程序时支持流的数据类型
description: 本主题列出了在使用 Microsoft SQLSRV Driver for PHP for SQL Server 时可作为流检索的 SQL Server 数据类型
ms.custom: ''
ms.date: 08/10/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- streaming data
ms.assetid: a16fe7da-e4c8-45f5-be54-aad03c4fa168
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5ca74b31b55fd0cb8a0c8405ac3303d041c38478
ms.sourcegitcommit: d1051f05a7db81ec62d9785bb6af572408f3d4e0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2020
ms.locfileid: "88680802"
---
# <a name="data-types-with-stream-support-using-the-sqlsrv-driver"></a>使用 SQLSRV 驱动程序时支持流的数据类型
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

以流的形式检索数据仅在 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 的 SQLSRV 驱动程序中可用，在 PDO_SQLSRV 驱动程序中不可用。  
  
以下 SQL Server 数据类型可以通过 SQLSRV 驱动程序以流的形式检索：  
  
-   binary  
  
-   char  
  
-   image  
  
-   nchar  
  
-   ntext  
  
-   nvarchar  
  
-   text  
  
-   UDT  
  
-   varbinary  
  
-   varchar  
  
-   XML  
  
## <a name="see-also"></a>另请参阅  
[使用 SQLSRV 驱动程序以流的形式检索数据](../../connect/php/retrieving-data-as-a-stream-using-the-sqlsrv-driver.md)

[默认 PHP 数据类型](../../connect/php/default-php-data-types.md)

[如何：指定 PHP 数据类型](../../connect/php/how-to-specify-php-data-types.md)  
  
