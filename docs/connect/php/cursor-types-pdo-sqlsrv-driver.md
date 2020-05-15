---
title: 游标类型（PDO_SQLSRV 驱动程序） | Microsoft Docs
ms.custom: ''
ms.date: 05/03/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 49ea6a6e-78d4-40f8-85eb-180b527f0537
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c62c2a35123e77f5366dd5348fd51b3c50c85605
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "67993691"
---
# <a name="cursor-types-pdo_sqlsrv-driver"></a>游标类型（PDO_SQLSRV 驱动程序）
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

可通过 PDO_SQLSRV 驱动程序创建一个具有多个游标的可滚动结果集。

有关如何使用 PDO_SQLSRV 驱动程序指定游标的信息和代码示例，请参阅 [PDO::prepare](../../connect/php/pdo-prepare.md)。

## <a name="pdo_sqlsrv-and-server-side-cursors"></a>PDO_SQLSRV 和服务器端游标
在 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 3.0 版本之前，PDO_SQLSRV 驱动程序允许使用服务器端只进或静态游标创建结果集。 从 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 的 3.0 版开始，还可以使用键集和动态游标。

可以使用 [PDO::prepare](../../connect/php/pdo-prepare.md) 选择下列游标类型之一，从而指示服务器端游标的类型：

-   `PDO::ATTR_CURSOR => PDO::CURSOR_FWDONLY`

-   `PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL`

可以通过指定 `PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL` 并将适当的值传递给 `PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE` 来请求动态、静态或键集游标。 可以传递给服务器端游标 `PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE` 的可能的值包括：

-   `PDO::SQLSRV_CURSOR_DYNAMIC`

-   `PDO::SQLSRV_CURSOR_STATIC`

-   `PDO::SQLSRV_CURSOR_KEYSET`

## <a name="pdo_sqlsrv-and-client-side-cursors"></a>PDO_SQLSRV 和客户端游标
[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 3.0 版本中添加了客户端游标，允许在内存中缓存整个结果集。 一个优点是，在执行查询之后，行计数将可用。

客户端游标应用于中小型结果集。 较大的结果集应使用服务器端游标。

如果使用客户端游标时缓冲区不够大，无法容纳整个结果集，则查询将返回 false。 可以将缓冲区大小增加到 PHP 内存限制。

可以使用 `PDO::SQLSRV_ATTR_CLIENT_BUFFER_MAX_KB_SIZE`PDO::setAttribute[ 或 ](../../connect/php/pdo-setattribute.md)PDOStatement::setAttribute[ 的 ](../../connect/php/pdostatement-setattribute.md) 属性配置保留结果集的缓冲区的大小。 还可以使用 pdo_sqlsrv.client_buffer_max_kb_size 在 php.ini 文件中设置最大缓冲区大小（例如，pdo_sqlsrv.client_buffer_max_kb_size = 1024）。

可以使用 [PDO::prepare](../../connect/php/pdo-prepare.md) 来请求客户端游标，指定 `PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL` 游标类型，然后指定 `PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE => PDO::SQLSRV_CURSOR_BUFFERED`。

## <a name="example"></a>示例
以下示例显示如何指定缓冲游标。
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

