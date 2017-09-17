---
title: "Pdo:: query |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f6f5e6d4-8ca9-4f06-89ed-de65ad3952a2
caps.latest.revision: 19
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 7495d5f3071e43e7eab2a1e9d49c105eff651a18
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="pdoquery"></a>PDO::query
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

执行 SQL 查询并返回一个结果集作为 PDOStatement 对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
PDOStatement PDO::query ($statement[, $fetch_style);  
```  
  
#### <a name="parameters"></a>Parameters  
*$statement*：要执行的 SQL 语句。  
  
*$fetch_style*： 有关如何执行查询的可选说明。 有关更多详细信息，请参阅“备注”部分。 $*fetch_style* pdo:: query 可以重写以 $*fetch_style* pdo:: fetch 中。  
  
## <a name="return-value"></a>返回值  
如果调用成功，PDO::query 将返回一个 PDOStatement 对象。 如果调用失败，PDO::query 将引发一个 PDOException 对象或者返回 False，具体取决于 PDO::ATTR_ERRMODE 的设置。  
  
## <a name="exceptions"></a>异常  
PDOException。  
  
## <a name="remarks"></a>注释  
使用 pdo:: query 执行的查询可以执行预定义的语句或直接，具体取决于 PDO::SQLSRV_ATTR_DIRECT_QUERY; 的设置请参阅[直接语句执行和已准备 PDO_SQLSRV 驱动程序中的语句执行](../../connect/php/direct-statement-execution-prepared-statement-execution-pdo-sqlsrv-driver.md)有关详细信息。  
  
PDO::SQLSRV_ATTR_QUERY_TIMEOUT 还会影响 pdo:: exec; 的行为请参阅[pdo:: setattribute](../../connect/php/pdo-setattribute.md)有关详细信息。  
  
你可以为 $ 指定以下选项*fetch_style*。  
  
|style|Description|  
|---------|---------------|  
|PDO::FETCH_COLUMN， *num*|在指定列中查询数据。 表中的第一列为列 0.|  
|Pdo:: FETCH_CLASS，*classname*，数组 ( *arglist* )|创建一个类的实例并给类中的属性分配列名称。 如果类构造函数采用一个或多个参数，你还可以传递 *arglist*。|  
|Pdo:: FETCH_CLASS，*classname*|给现有类中的属性分配列名称。|  
  
在再次调用 PDO::query 之前，请调用 PDOStatement::closeCursor 以释放与 PDOStatement 对象相关联的数据库资源。  
  
通过将 PDOStatement 对象设置为 NULL 来将其关闭。  
  
如果结果集中的所有数据都无法提取，下次调用 PDO::query 时将不会失败。  
  
已在 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]的版本 2.0 中添加了对 PDO 的支持。  
  
## <a name="example"></a>示例  
此示例显示多个查询。  
  
```  
<?php  
$database = "AdventureWorks";  
$conn = new PDO( "sqlsrv:server=(local) ; Database = $database", "", "");  
$conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );  
$conn->setAttribute( PDO::SQLSRV_ATTR_QUERY_TIMEOUT, 1 );  
  
$query = 'select * from Person.ContactType';  
  
// simple query  
$stmt = $conn->query( $query );  
while ( $row = $stmt->fetch( PDO::FETCH_ASSOC ) ){  
   print_r( $row['Name'] ."\n" );  
}  
  
echo "\n........ query for a column ............\n";  
  
// query for one column  
$stmt = $conn->query( $query, PDO::FETCH_COLUMN, 1 );  
while ( $row = $stmt->fetch() ){  
   echo "$row\n";  
}  
  
echo "\n........ query with a new class ............\n";  
$query = 'select * from HumanResources.Department order by GroupName';  
// query with a class  
class cc {  
   function __construct( $arg ) {  
      echo "$arg";  
   }  
  
   function __toString() {  
      return $this->DepartmentID . "; " . $this->Name . "; " . $this->GroupName;  
   }  
}  
  
$stmt = $conn->query( $query, PDO::FETCH_CLASS, 'cc', array( "arg1 " ));  
  
while ( $row = $stmt->fetch() ){  
   echo "$row\n";  
}  
  
echo "\n........ query into an existing class ............\n";  
$c_obj = new cc( '' );  
$stmt = $conn->query( $query, PDO::FETCH_INTO, $c_obj );  
while ( $stmt->fetch() ){  
   echo "$c_obj\n";  
}  
  
$stmt = null;  
?>  
```  
  
## <a name="see-also"></a>另请参阅  
[PDO 类](../../connect/php/pdo-class.md)  
[PDO](http://go.microsoft.com/fwlink/?LinkID=187441)  
  

