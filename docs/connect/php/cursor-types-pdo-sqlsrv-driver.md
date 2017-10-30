---
title: "游标类型 （PDO_SQLSRV 驱动程序） |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 49ea6a6e-78d4-40f8-85eb-180b527f0537
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 77a8050977a85ff825b872b21557f4bd3a282639
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="cursor-types-pdosqlsrv-driver"></a>游标类型 （PDO_SQLSRV 驱动程序）
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

PDO_SQLSRV 驱动程序，可以使用多个游标之一创建可滚动的结果集。  
  
有关如何指定使用 PDO_SQLSRV 驱动程序，游标的信息和代码示例，请参阅[pdo:: prepare](../../connect/php/pdo-prepare.md)。  
  
## <a name="pdosqlsrv-and-server-side-cursors"></a>PDO_SQLSRV 和服务器端游标  
之前的版本 3.0 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]，PDO_SQLSRV 驱动程序允许你创建具有服务器端只进或静态游标的结果集。 从 3.0 版开始[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]，键集和动态游标也是可用。  
  
可以通过使用 pdo:: prepare 或 pdostatement:: Setattribute 来选择任一游标类型来指示服务器端游标的类型：  
  
-   PDO::ATTR_CURSOR = > PDO::CURSOR_FWDONLY  
  
-   PDO::ATTR_CURSOR = > PDO::CURSOR_SCROLL  
  
你可以通过指定 PDO::ATTR_CURSOR 请求键集或动态游标 = > PDO::CURSOR_SCROLL，然后传入适当的值与 PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE。 你可以将其传递到 PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE 的可能值有：  
  
-   PDO::SQLSRV_CURSOR_BUFFERED  
  
-   PDO::SQLSRV_CURSOR_DYNAMIC  
  
-   PDO::SQLSRV_CURSOR_KEYSET_DRIVEN  
  
-   PDO::SQLSRV_CURSOR_STATIC  
  
## <a name="pdosqlsrv-and-client-side-cursors"></a>PDO_SQLSRV 和客户端游标  
客户端游标已添加的版本 3.0 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] ，使你能够整个结果集在内存中高速缓存。 优点之一是执行查询后，行计数可用。  
  
对于小型到中型的结果集，应使用客户端游标。 大型结果集应使用服务器端游标。  
  
查询将返回 false 缓冲区是否不大到能够容纳整个结果集时使用的客户端游标。 你可以增加最大 PHP 内存限制为缓冲区大小。  
  
你可以配置用于保留结果集的 PDO::SQLSRV_ATTR_CLIENT_BUFFER_MAX_KB_SIZE 属性的缓冲区的大小[pdo:: setattribute](../../connect/php/pdo-setattribute.md)或[pdostatement:: Setattribute](../../connect/php/pdostatement-setattribute.md)。 此外可以在 php.ini 文件中使用 pdo_sqlsrv.client_buffer_max_kb_size 设置最大缓冲区大小 (例如，pdo_sqlsrv.client_buffer_max_kb_size = 1024年)。  
  
指示你希望通过使用 pdo:: prepare 或 pdostatement:: Setattribute 在客户端游标，并选择 PDO::ATTR_CURSOR = > PDO::CURSOR_SCROLL 游标类型。  然后指定 PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE = > PDO::SQLSRV_CURSOR_BUFFERED。  
  
```  
<?php  
$database = "AdventureWorks";  
$server = "(local)";  
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");  
  
$query = "select * from Person.ContactType";  
$stmt = $conn->prepare( $query, array(PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL, PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE => PDO::SQLSRV_CURSOR_BUFFERED));  
$stmt->execute();  
print $stmt->rowCount();  
  
echo "\n";  
  
while ( $row = $stmt->fetch( PDO::FETCH_ASSOC ) ){  
   print "$row[Name]\n";  
}  
echo "\n..\n";  
  
$row = $stmt->fetch( PDO::FETCH_BOTH, PDO::FETCH_ORI_FIRST );  
print_r($row);  
  
$row = $stmt->fetch( PDO::FETCH_ASSOC, PDO::FETCH_ORI_REL, 1 );  
print "$row[Name]\n";  
  
$row = $stmt->fetch( PDO::FETCH_NUM, PDO::FETCH_ORI_NEXT );  
print "$row[1]\n";  
  
$row = $stmt->fetch( PDO::FETCH_NUM, PDO::FETCH_ORI_PRIOR );  
print "$row[1]..\n";  
  
$row = $stmt->fetch( PDO::FETCH_NUM, PDO::FETCH_ORI_ABS, 0 );  
print_r($row);  
  
$row = $stmt->fetch( PDO::FETCH_NUM, PDO::FETCH_ORI_LAST );  
print_r($row);  
?>  
```  
  
## <a name="see-also"></a>另请参阅  
[指定游标类型和选择行](../../connect/php/specifying-a-cursor-type-and-selecting-rows.md)  
  

