---
title: "使用 SQLSRV 驱动程序流的形式检索数据 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 17dc9129-04cd-430c-b5b3-82824116425d
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8fa189273eeb236d30f7f9ed9f01f00f14c6f70d
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="retrieving-data-as-a-stream-using-the-sqlsrv-driver"></a>使用 SQLSRV 驱动程序以流的形式检索数据
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

流选项仅适用于的 SQLSRV 驱动程序的形式检索数据[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]，并在 PDO_SQLSRV 驱动程序中不可用。  
  
[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 将流用于检索大量数据。 本部分中的主题详细介绍了如何以流的形式检索数据。  
  
以下步骤总结了如何以流的形式检索数据：  
  
1.  准备并执行 Transact SQL 查询使用[sqlsrv_query](../../connect/php/sqlsrv-query.md)或的组合[sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md)/[sqlsrv_execute](../../connect/php/sqlsrv-execute.md)。  
  
2.  使用 [sqlsrv_fetch](../../connect/php/sqlsrv-fetch.md) 在结果集中移动到下一行。  
  
3.  使用 [sqlsrv_get_field](../../connect/php/sqlsrv-get-field.md) 从行中检索字段。 指定要使用的流的形式检索数据**SQLSRV_PHPTYPE_STREAM (<encoding>)**作为函数调用中的第三个参数。 此表列出了用于指定编码及其描述符的常量：  
  
    |SQLSRV 常量|Description|  
    |-------------------|---------------|  
    |SQLSRV_ENC_BINARY|数据以原始字节流的形式从服务器返回，无需执行编码或转换。|  
    |SQLSRV_ENC_CHAR|数据以在系统上设置的 Windows 区域设置代码页中指定的 8 位字符的形式返回。 任何多字节字符或未映射到此代码页中的字符都会替换为单字节问号 (?) 字符。|  
  
> [!NOTE]  
> 某些数据类型默认情况下以流的形式返回。 有关详细信息，请参阅 [Default PHP Data Types](../../connect/php/default-php-data-types.md)。  
  
## <a name="in-this-section"></a>本节内容  
  
|主题|说明|  
|---------|---------------|  
|[使用 SQLSRV 驱动程序时支持流的数据类型](../../connect/php/data-types-with-stream-support-using-the-sqlsrv-driver.md)|列出可以流的形式进行检索的 SQL Server 数据类型。|  
|[如何：使用 SQLSRV 驱动程序以流的形式检索字符数据](../../connect/php/how-to-retrieve-character-data-as-a-stream-using-the-sqlsrv-driver.md)|演示如何以流的形式检索字符数据。|  
|[如何：使用 SQLSRV 驱动程序以流的形式检索二进制数据](../../connect/php/how-to-retrieve-binary-data-as-a-stream-using-the-sqlsrv-driver.md)|演示如何以流的形式检索二进制数据。|  
  
## <a name="see-also"></a>另请参阅  
[检索数据](../../connect/php/retrieving-data.md)  
[常量（Microsoft Drivers for PHP for SQL Server）](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)  
  

