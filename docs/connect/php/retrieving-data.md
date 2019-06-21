---
title: 检索数据 | Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 3414992c-61c0-4e7d-b509-72517e52c1bb
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 85fc9956e8e88398703adf283c91517972aa7e77
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66797064"
---
# <a name="retrieving-data"></a>检索数据
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

本主题和此部分中的主题将讨论如何检索数据。  
  
## <a name="sqlsrv-driver"></a>SQLSRV 驱动程序  
[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 的 SQLSRV 驱动程序提供以下选项来从某个结果集中检索数据：  
  
-   [sqlsrv_fetch_array](../../connect/php/sqlsrv-fetch-array.md)  
  
-   [sqlsrv_fetch_object](../../connect/php/sqlsrv-fetch-object.md)  
  
-   [sqlsrv_fetch](../../connect/php/sqlsrv-fetch.md)/[sqlsrv_get_field](../../connect/php/sqlsrv-get-field.md)  
  
> [!NOTE]  
> 当你使用上述任何函数时，请避免将 NULL 比较作为退出循环的条件。 因为 **sqlsrv** 函数在发生错误时会返回 false，所以在 [sqlsrv_fetch_array](../../connect/php/sqlsrv-fetch-array.md)中出现错误时，以下代码可能会导致无限循环：  
>   
> `/*``This code could result in an infinite loop. It is recommended that`  
>   
> `you do NOT use null comparisons as the criterion for exiting loops,`  
>   
> `as is done here. */`  
>   
> `do{`  
>   
> `$result = sqlsrv_fetch_array($stmt);`  
>   
> `} while( !is_null($result));`  
  
如果查询检索多个结果集，可以使用 [sqlsrv_next_result](../../connect/php/sqlsrv-next-result.md)移动至下一个结果集。  
  
从 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 的版本 1.1 开始，可以使用 [sqlsrv_has_rows](../../connect/php/sqlsrv-has-rows.md) 来查看结果集是否有行。  
  
## <a name="pdosqlsrv-driver"></a>PDO_SQLSRV 驱动程序  
[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 的 PDO_SQLSRV 驱动程序提供以下选项来从某个结果集中检索数据：  
  
-   [PDOStatement::fetch](../../connect/php/pdostatement-fetch.md)  
  
-   [PDOStatement::fetchAll](../../connect/php/pdostatement-fetchall.md)  
  
-   [PDOStatement::fetchColumn](../../connect/php/pdostatement-fetchcolumn.md)  
  
-   [PDOStatement::fetchObject](../../connect/php/pdostatement-fetchobject.md)  
  
如果查询检索多个结果集，可以使用 [PDOStatement::nextRowset](../../connect/php/pdostatement-nextrowset.md)移动至下一个结果集。  
  
你可以查看结果集中有多少行，前提是先指定可滚动游标，然后调用 [PDOStatement::rowCount](../../connect/php/pdostatement-rowcount.md)。  
  
[PDO::prepare](../../connect/php/pdo-prepare.md) 可让你指定游标类型。 然后，你可以使用 [PDOStatement::fetch](../../connect/php/pdostatement-fetch.md) 选择一行。 有关示例和详细信息，请参阅 [PDO::prepare](../../connect/php/pdo-prepare.md) 。  
  
## <a name="in-this-section"></a>本节内容  
  
|主题|描述|  
|---------|---------------|  
|[以流的形式检索数据](../../connect/php/retrieving-data-as-a-stream-using-the-sqlsrv-driver.md)|概述了如何从服务器中流式传输数据，并提供指向特定用例的链接。|  
|[使用方向参数](../../connect/php/using-directional-parameters.md)|介绍如何在调用存储过程时使用方向参数。|  
|[指定游标类型和选择行](../../connect/php/specifying-a-cursor-type-and-selecting-rows.md)|演示如何创建一个结果集，可以按任意顺序访问的行。|  
|[如何：使用 SQLSRV 驱动程序以字符串的形式检索日期和时间类型](../../connect/php/how-to-retrieve-date-and-time-type-as-strings-using-the-sqlsrv-driver.md)|介绍如何使用 SQLSRV 驱动程序以字符串的形式检索日期和时间类型。|  
|[如何：使用 PDO_SQLSRV 驱动程序以 PHP Datetime 对象形式检索日期和时间类型](../../connect/php/how-to-retrieve-datetime-objects-using-pdo-sqlsrv-driver.md)|介绍了如何使用 PDO_SQLSRV 驱动程序将日期和时间类型作为对象进行检索。|  
|[使用 SQLSRV 驱动程序的格式设置十进制字符串](../../connect/php/formatting-decimals-sqlsrv-driver.md)|演示如何设置使用 SQLSRV 驱动程序的十进制或货币值的格式。|  
|[使用 PDO_SQLSRV 驱动程序的格式设置十进制字符串](../../connect/php/formatting-decimals-pdo-sqlsrv-driver.md)|演示如何设置使用 PDO_SQLSRV 驱动程序的十进制或货币值的格式。|  
  
## <a name="related-sections"></a>相关章节  
[如何：指定 PHP 数据类型](../../connect/php/how-to-specify-php-data-types.md)  
  
## <a name="see-also"></a>另请参阅  
[适用于 SQL Server for PHP 编程 Microsoft 驱动程序的指南](../../connect/php/programming-guide-for-php-sql-driver.md)

[检索数据](../../connect/php/retrieving-data.md)  
  
