---
title: 'Pdo:: getattribute |Microsoft 文档'
ms.custom: ''
ms.date: 07/13/2017
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
ms.assetid: c81833ea-8b8a-459d-8f24-920098da994d
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4f281a512c64aeb5c777882565961c7e4fb71061
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="pdogetattribute"></a>PDO::getAttribute
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

检索预定义 PDO 或驱动程序属性的值。  
  
## <a name="syntax"></a>语法  
  
```  
  
mixed PDO::getAttribute ( $attribute )  
```  
  
#### <a name="parameters"></a>Parameters  
*$attribute*：受支持的属性之一。 请参阅受支持的属性列表的“备注”部分。  
  
## <a name="return-value"></a>返回值  
如果成功，返回连接选项的值、预定义 PDO 属性或自定义驱动程序属性。 如果失败，返回 null。  
  
## <a name="remarks"></a>注释  
下表包含受支持的属性列表。  
  
|Attribute|由以下值处理|支持的值|Description|  
|-------------|----------------|--------------------|---------------|  
|PDO::ATTR_CASE|PDO|PDO::CASE_LOWER<br /><br />PDO::CASE_NATURAL<br /><br />PDO::CASE_UPPER|指定列名称是否应使用特定格式。 PDO::CASE_LOWER 强制使用小写列名称，PDO::CASE_NATURAL 保留数据库返回的列名称，而PDO::CASE_UPPER 强制使用大写列名称。<br /><br />默认值为 PDO::CASE_NATURAL。<br /><br />还可以使用 PDO::setAttribute 设置此属性。|  
|PDO::ATTR_CLIENT_VERSION|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|字符串数组|介绍驱动程序和相关库的版本。 返回包含以下元素的数组： ODBC 版本 (*MajorVer*。*MinorVer*)， [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Native Client DLL 名称和版本、[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]版本 (*MajorVer*。*MinorVer*。*BuildNumber*。*修订*)|  
|PDO::ATTR_DRIVER_NAME|PDO|字符串|始终返回“sqlsrv”。|  
|PDO::ATTR_DRIVER_VERSION|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|字符串|指示[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]版本 (*MajorVer*。*MinorVer*。*BuildNumber*。*修订*)|  
|PDO::ATTR_ERRMODE|PDO|PDO::ERRMODE_SILENT<br /><br />PDO::ERRMODE_WARNING<br /><br />PDO::ERRMODE_EXCEPTION|指定驱动程序应如何处理失败。<br /><br />PDO::ERRMODE_SILENT（默认值）设置错误代码和信息。<br /><br />PDO::ERRMODE_WARNING 引发 E_WARNING。<br /><br />PDO::ERRMODE_EXCEPTION 引发异常。<br /><br />还可以使用 PDO::setAttribute 设置此属性。|  
|PDO::ATTR_ORACLE_NULLS|PDO|请参阅 PDO 文档。|请参阅 PDO 文档。|  
|PDO::ATTR_SERVER_INFO|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|3 个元素的数组|返回当前数据库、SQL Server 版本和 SQL Server 实例。|  
|PDO::ATTR_SERVER_VERSION|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|字符串|指示 SQL Server 版本 (*主要*。*次要*。*BuildNumber*)|  
|PDO::ATTR_STRINGIFY_FETCHES|PDO|请参阅 PDO 文档|请参阅 PDO 文档。|  
|PDO::SQLSRV_ATTR_CLIENT_BUFFER_MAX_KB_SIZE|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|1 到 PHP 内存限制。|配置保留客户端游标的结果集的缓冲区大小。<br /><br />默认值为 10240 KB (10 MB)。<br /><br />有关客户端游标的详细信息，请参阅[游标类型&#40;SQLSRV 驱动程序&#41;](../../connect/php/cursor-types-sqlsrv-driver.md)。|  
|PDO::SQLSRV_ATTR_DIRECT_QUERY|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|true<br /><br />false|指定直接或已准备的查询执行。 有关详细信息，请参阅 [PDO_SQLSRV 驱动程序中的直接语句执行和预定语句执行](../../connect/php/direct-statement-execution-prepared-statement-execution-pdo-sqlsrv-driver.md)。|  
|PDO::SQLSRV_ATTR_ENCODING|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|PDO::SQLSRV_ENCODING_UTF8<br /><br />PDO::SQLSRV_ENCODING_SYSTEM|指定驱动程序用于与服务器通信的字符集编码。<br /><br />默认值为 PDO::SQLSRV_ENCODING_UTF8。|  
|PDO::SQLSRV_ATTR_FETCHES_NUMERIC_TYPE|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|True 或 False|使用数值 SQL 类型 （位、 整数、 smallint、 tinyint、 float、 或实时） 处理数值列中的提取。<br /><br />打开连接选项标志 ATTR_STRINGIFY_FETCHES 时，即使 SQLSRV_ATTR_FETCHES_NUMERIC_TYPE 处于打开状态，则返回值是一个字符串。<br /><br />PDO_PARAM_INT 绑定列中的返回的 PDO 类型时，为整数列中的返回值将是 int，即使 SQLSRV_ATTR_FETCHES_NUMERIC_TYPE 处于关闭状态。|  
|PDO::SQLSRV_ATTR_QUERY_TIMEOUT|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|integer|设置查询超时（以秒为单位）。<br /><br />默认值为 0，这意味着该驱动程序将无限期地等待结果。<br /><br />不允许使用负数。|  

  
PDO 将处理某些预定义的属性，同时它需要驱动程序处理其他属性。 由驱动程序处理所有自定义属性和连接选项，则返回 null 的不受支持的属性或连接选项。  
  
已在 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]的版本 2.0 中添加了对 PDO 的支持。  
  
## <a name="example"></a>示例  
此示例显示在更改其值之前和之后的 PDO::ATTR_ERRMODE 属性的值。  
  
```  
<?php  
$database = "AdventureWorks";  
$conn = new PDO( "sqlsrv:server=(local) ; Database = $database", "", "");  
  
$attributes1 = array( "ERRMODE" );  
foreach ( $attributes1 as $val ) {  
     echo "PDO::ATTR_$val: ";  
     var_dump ($conn->getAttribute( constant( "PDO::ATTR_$val" ) ));  
}  
  
$conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );  
  
$attributes1 = array( "ERRMODE" );  
foreach ( $attributes1 as $val ) {  
     echo "PDO::ATTR_$val: ";  
     var_dump ($conn->getAttribute( constant( "PDO::ATTR_$val" ) ));  
}  
  
// An example using PDO::ATTR_CLIENT_VERSION  
print_r($conn->getAttribute( PDO::ATTR_CLIENT_VERSION ));  
?>  
```  
  
## <a name="see-also"></a>另请参阅  
[PDO 类](../../connect/php/pdo-class.md)

[PDO](http://php.net/manual/book.pdo.php)  
  
