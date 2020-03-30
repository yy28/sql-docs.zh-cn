---
title: 如何：禁用多个活动的结果集 (MARS) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- multiple active result sets, disabling
- MARS, disabling
ms.assetid: 1912ad05-d0a4-40ff-8888-0d85bb36a807
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c5edf63a654b21d080e48f93c71553b8909ce8fd
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "67993556"
---
# <a name="how-to-disable-multiple-active-resultsets-mars"></a>如何：禁用多个活动的结果集 (MARS)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

如果你需要连接到不启用多个活动的结果集 (MARS) 的 SQL Server 数据源，可以使用 MultipleActiveResultSets 连接选项禁用或启用 MARS。  
  
## <a name="procedure"></a>过程  
  
#### <a name="to-disable-mars-support"></a>禁用 MARS 支持  
  
-   使用以下连接选项：  
  
    ```  
    'MultipleActiveResultSets'=>false  
    ```  
  
    如果应用程序尝试在具有开放的活动结果集的连接上执行查询，第二次查询尝试将返回以下错误信息：  
  
    连接无法处理此操作，因为存在具有挂起结果的语句。  若要使该连接可用于其他查询，请提取所有结果、取消或释放该语句。 有关 MultipleActiveResultSets 连接选项的详细信息，请参阅 [Connection Options](../../connect/php/connection-options.md)。  
  
## <a name="example"></a>示例  
以下示例显示如何使用 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]的 SQLSRV 驱动程序禁用 MARS 支持。  
  
```  
<?php  
/* Connect to the local server using Windows Authentication and  
specify the AdventureWorks database as the database in use. */  
$serverName = "MyServer";  
$connectionInfo = array( "Database"=>"AdventureWorks", 'MultipleActiveResultSets'=> false);  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
if( $conn === false )  
{  
   echo "Could not connect.\n";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="example"></a>示例  
以下示例显示如何使用 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 的 PDO_SQLSRV 驱动程序禁用 MARS 支持。  
  
```  
<?php  
// Connect to the local server using Windows Authentication and AdventureWorks database  
$serverName = "(local)";   
$database = "AdventureWorks";  
  
try {  
   $conn = new PDO(" sqlsrv:server=$serverName ; Database=$database ; MultipleActiveResultSets=false ", NULL, NULL);   
   $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );   
}  
  
catch( PDOException $e ) {  
   die( "Error connecting to SQL Server" );   
}  
  
$conn = null;   
?>  
```  
  
## <a name="see-also"></a>另请参阅  
[连接到服务器](../../connect/php/connecting-to-the-server.md)  
  
