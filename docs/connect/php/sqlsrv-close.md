---
title: sqlsrv_close |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- sqlsrv_close
apitype: NA
helpviewer_keywords:
- sqlsrv_close
- API Reference, sqlsrv_close
ms.assetid: 6ac6209c-a134-4f8f-b88b-8eefaa1cbc7f
caps.latest.revision: 25
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e071fc2ac51931a52ba6672e97936dc60ee12072
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "38006839"
---
# <a name="sqlsrvclose"></a>sqlsrv_close
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

关闭指定的连接并释放关联的资源。  
  
## <a name="syntax"></a>语法  
  
```  
  
sqlsrv_close( resource $conn )  
```  
  
#### <a name="parameters"></a>Parameters  
*$conn*：要关闭的连接。  
  
## <a name="return-value"></a>返回值  
除非使用无效参数调用该函数，否则布尔值为 **true** 。 如果使用无效参数调用该函数，将返回 **False** 。  
  
> [!NOTE]  
> 对于此函数，**Null** 是有效参数。 这允许在脚本中调用该函数多次。 例如，当在错误条件中关闭某个连接，并且在脚本结尾再次关闭该连接时，第二次对 sqlsrv_close 的调用将返回 true，因为第一次对 sqlsrv_close 的调用（在错误条件中）将连接资源设置为 null。  
  
## <a name="example"></a>示例  
以下示例将关闭连接。 该示例假定已在本地计算机上安装了 SQL Server。 当从命令行运行该示例时，所有输出都将写入控制台。  
  
```  
<?php  
/*Connect to the local server using Windows Authentication and   
specify the AdventureWorks database as the database in use. */  
$serverName = "(local)";  
$conn = sqlsrv_connect( $serverName);  
if( $conn === false )  
{  
     echo "Could not connect.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
//-----------------------------------------------  
// Perform operations with connection here.  
//-----------------------------------------------  
  
/* Close the connection. */  
sqlsrv_close( $conn);  
echo "Connection closed.\n";  
?>  
```  
  
## <a name="see-also"></a>另请参阅  
[SQLSRV 驱动程序 API 参考](../../connect/php/sqlsrv-driver-api-reference.md)

[文档中相关的代码示例](../../connect/php/about-code-examples-in-the-documentation.md)  
  
