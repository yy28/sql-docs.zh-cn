---
title: 'Pdo:: setattribute |Microsoft 文档'
ms.custom: ''
ms.date: 07/13/2017
ms.prod: sql
ms.prod_service: connectivity
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 56f9ee96-e1d2-46cc-b137-38f06a251863
caps.latest.revision: 24
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c2a5bbd2370839cf1483d251f87588743994b081
ms.sourcegitcommit: 6e55a0a7b7eb6d455006916bc63f93ed2218eae1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/08/2018
ms.locfileid: "35239337"
---
# <a name="pdosetattribute"></a>PDO::setAttribute
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

设置预定义的 PDO 属性或自定义驱动程序属性。  
  
## <a name="syntax"></a>语法  
  
```  
  
bool PDO::setAttribute ( $attribute, $value );  
```  
  
#### <a name="parameters"></a>Parameters  
*$attribute*：要设置的属性。 请参阅受支持的属性列表的“备注”部分。  
  
*$value*: （混合类型） 的值。  
  
## <a name="return-value"></a>返回值  
如果成功，将返回 True；否则返回 False。  
  
## <a name="remarks"></a>Remarks  
  
|Attribute|处理对象|支持的值|Description|  
|-------------|----------------|--------------------|---------------|  
|PDO::ATTR_CASE|PDO|PDO::CASE_LOWER<br /><br />PDO::CASE_NATURAL<br /><br />PDO::CASE_UPPER|指定列名称的大小写。<br /><br />PDO::CASE_LOWER 会使列名称小写。<br /><br />PDO::CASE_NATURA（默认值）显示数据库返回的列名称。<br /><br />PDO::CASE_UPPER 会使列名称大写。<br /><br />可以使用 PDO::setAttribute 设置此属性。|  
|PDO::ATTR_DEFAULT_FETCH_MODE|PDO|请参阅 PDO 文档。|请参阅 PDO 文档。|  
|PDO::ATTR_ERRMODE|PDO|PDO::ERRMODE_SILENT<br /><br />PDO::ERRMODE_WARNING<br /><br />PDO::ERRMODE_EXCEPTION|指定如何在驱动程序报告失败。<br /><br />PDO::ERRMODE_SILENT（默认值）设置错误代码和信息。<br /><br />PDO::ERRMODE_WARNING 引发 E_WARNING。<br /><br />PDO::ERRMODE_EXCEPTION 会引发异常。<br /><br />可以使用 PDO::setAttribute 设置此属性。|  
|PDO::ATTR_ORACLE_NULLS|PDO|请参阅 PDO 文档。|指定应如何返回 NULL。<br /><br />PDO::NULL_NATURAL 不执行任何转换。<br /><br />PDO::NULL_EMPTY_STRING 将空字符串转换为 NULL。<br /><br />PDO::NULL_TO_STRING 将 NULL 转换为空字符串。|  
|PDO::ATTR_STATEMENT_CLASS|PDO|请参阅 PDO 文档。|设置派生自 PDOStatement 的用户提供的语句类。<br /><br />需要 `array(string classname, array(mixed constructor_args))`。<br /><br />有关详细信息，请参阅 PDO 文档。|  
|PDO::ATTR_STRINGIFY_FETCHES|PDO|True 或 False|检索数据时，将数值转换为字符串。|  
|PDO::SQLSRV_ATTR_CLIENT_BUFFER_MAX_KB_SIZE|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|1 到 PHP 内存限制。|配置用于保留结果集的缓冲区大小。<br /><br />默认值为 10240 KB (10 MB)。<br /><br />有关创建客户端游标的查询的详细信息，请参阅[游标类型&#40;PDO_SQLSRV 驱动程序&#41;](../../connect/php/cursor-types-pdo-sqlsrv-driver.md)。|  
|PDO::SQLSRV_ATTR_DIRECT_QUERY|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|true<br /><br />false|指定直接或已准备的查询执行。 有关详细信息，请参阅 [PDO_SQLSRV 驱动程序中的直接语句执行和预定语句执行](../../connect/php/direct-statement-execution-prepared-statement-execution-pdo-sqlsrv-driver.md)。|  
|PDO::SQLSRV_ATTR_ENCODING|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|PDO::SQLSRV_ENCODING_UTF8<br /><br />PDO::SQLSRV_ENCODING_SYSTEM。|设置驱动程序用于与服务器通信的字符集编码。<br /><br />不支持 PDO::SQLSRV_ENCODING_BINARY。<br /><br />默认值为 PDO::SQLSRV_ENCODING_UTF8。|  
|PDO::SQLSRV_ATTR_FETCHES_NUMERIC_TYPE|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|True 或 False|使用数值 SQL 类型 （位、 整数、 smallint、 tinyint、 float、 或实时） 处理数值列中的提取。<br /><br />打开连接选项标志 ATTR_STRINGIFY_FETCHES 时，返回值将是一个字符串，即使 SQLSRV_ATTR_FETCHES_NUMERIC_TYPE 位于上。<br /><br />PDO_PARAM_INT 绑定列中的返回的 PDO 类型时，为整数列中的返回值将是 int，即使 SQLSRV_ATTR_FETCHES_NUMERIC_TYPE 处于关闭状态。|  
|PDO::SQLSRV_ATTR_QUERY_TIMEOUT|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|integer|设置查询超时（以秒为单位）。<br /><br />默认值为 0，这意味着该驱动程序将无限期地等待结果。<br /><br />不允许使用负数。|  
|PDO::SQLSRV_CLIENT_BUFFER_MAX_SIZE|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|integer|设置查询缓冲区的大小。<br /><br />如果未在 php.ini 文件中指定，则默认值为 10240 KB。<br /><br />不允许零和负数。<br /><br />有关创建客户端游标的查询的详细信息，请参阅[游标类型&#40;PDO_SQLSRV 驱动程序&#41;](../../connect/php/cursor-types-pdo-sqlsrv-driver.md)。|  
  
PDO 将处理某些预定义的属性，并且需要驱动程序处理其他属性。 由驱动程序处理所有自定义属性和连接选项。 不支持的属性、 连接选项或不受支持的值将报告根据 PDO::ATTR_ERRMODE 的设置。  
  
已在 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]的版本 2.0 中添加了对 PDO 的支持。  
  
## <a name="example"></a>示例  
此示例演示如何设置 PDO::ATTR_ERRMODE 属性。  
  
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
?>  
```  
  
## <a name="see-also"></a>请参阅  
[PDO 类](../../connect/php/pdo-class.md)

[PDO](http://php.net/manual/book.pdo.php)  
  
