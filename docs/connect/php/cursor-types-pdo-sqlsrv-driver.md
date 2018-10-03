---
title: 游标类型 （PDO_SQLSRV 驱动程序） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 49ea6a6e-78d4-40f8-85eb-180b527f0537
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 621bfe1f20b9ca656bf442377b1f453503b86a8f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47833465"
---
# <a name="cursor-types-pdosqlsrv-driver"></a>游标类型（PDO_SQLSRV 驱动程序）
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

PDO_SQLSRV 驱动程序使您创建具有多个游标的一个可滚动结果集。  
  
有关如何指定使用 PDO_SQLSRV 驱动程序，游标的信息和代码示例，请参阅[pdo:: prepare](../../connect/php/pdo-prepare.md)。  
  
## <a name="pdosqlsrv-and-server-side-cursors"></a>PDO_SQLSRV 和服务器端游标  
之前的版本 3.0 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]，PDO_SQLSRV 驱动程序允许您创建的结果集与服务器端的只进的或静态游标。 从 3.0 版开始[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]，键集和动态游标均可用。  
  
可以通过使用 pdo:: prepare 或 pdostatement:: Setattribute 同时选择任一游标类型表示的服务器端游标的类型：  
  
-   PDO:: ATTR_CURSOR = &GT; PDO:: CURSOR_FWDONLY  
  
-   PDO:: ATTR_CURSOR = &GT; PDO:: CURSOR_SCROLL  
  
可以请求 keyset 或 dynamic 游标通过指定 pdo:: ATTR_CURSOR = > pdo:: CURSOR_SCROLL，然后将传递适当的值为 pdo:: SQLSRV_ATTR_CURSOR_SCROLL_TYPE。 可以传递给 pdo:: SQLSRV_ATTR_CURSOR_SCROLL_TYPE 的可能值有：  
  
-   PDO::SQLSRV_CURSOR_BUFFERED  
  
-   PDO::SQLSRV_CURSOR_DYNAMIC  
  
-   PDO::SQLSRV_CURSOR_KEYSET_DRIVEN  
  
-   PDO::SQLSRV_CURSOR_STATIC  
  
## <a name="pdosqlsrv-and-client-side-cursors"></a>PDO_SQLSRV 和客户端游标  
客户端游标已添加的版本 3.0 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] ，可用于缓存整个结果集在内存中。 一个优点是行计数可执行查询后。  
  
对于小型到中型的结果集，应使用客户端游标。 较大的结果集应使用服务器端游标。  
  
查询将返回 false，如果缓冲区足以容纳整个结果集时使用客户端游标。 可以增加缓冲区大小最大为 PHP 内存限制。  
  
可以配置用于保留结果集的 PDO::SQLSRV_ATTR_CLIENT_BUFFER_MAX_KB_SIZE 属性的缓冲区的大小[pdo:: setattribute](../../connect/php/pdo-setattribute.md)或[pdostatement:: Setattribute](../../connect/php/pdostatement-setattribute.md)。 此外可以在 php.ini 文件中使用 pdo_sqlsrv.client_buffer_max_kb_size 设置最大缓冲区大小 (例如，pdo_sqlsrv.client_buffer_max_kb_size = 1024年)。  
  
指示您希望使用 pdo:: prepare 或 pdostatement:: Setattribute 在客户端游标，并选择 pdo:: ATTR_CURSOR = > pdo:: CURSOR_SCROLL 游标类型。  然后，可以指定 pdo:: SQLSRV_ATTR_CURSOR_SCROLL_TYPE = > PDO::SQLSRV_CURSOR_BUFFERED。  
  
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
  
