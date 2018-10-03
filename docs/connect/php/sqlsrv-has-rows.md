---
title: sqlsrv_has_rows |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- API Reference, sqlsrv_has_rows
- sqlsrv_has_rows
ms.assetid: 4da7f640-cf12-409f-9e00-95b30a8d5e17
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9cc449b6aa47024d9d38af1870dfa370f8a59896
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47772765"
---
# <a name="sqlsrvhasrows"></a>sqlsrv_has_rows
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

指示结果集具有一行还是具有多行。  
  
## <a name="syntax"></a>语法  
  
```  
  
sqlsrv_has_rows( resource $stmt )  
```  
  
#### <a name="parameters"></a>Parameters  
*$stmt*：已执行的语句。  
  
## <a name="return-value"></a>返回值  
如果结果集中存在行，该返回值将为 **True**。 如果没有任何行，或者如果函数调用失败，该返回值将为 **False**。  
  
## <a name="example"></a>示例  
  
```  
<?php  
   $server = "server_name";  
   $conn = sqlsrv_connect( $server, array( 'Database' => 'Northwind' ) );  
  
   $stmt = sqlsrv_query( $conn, "select * from orders where CustomerID = 'VINET'" , array());  
  
   if ($stmt !== NULL) {  
      $rows = sqlsrv_has_rows( $stmt );  
  
      if ($rows === true)  
         echo "\nthere are rows\n";  
      else   
         echo "\nno rows\n";  
   }  
?>  
```  
  
## <a name="see-also"></a>另请参阅  
[SQLSRV 驱动程序 API 参考](../../connect/php/sqlsrv-driver-api-reference.md)  
  
