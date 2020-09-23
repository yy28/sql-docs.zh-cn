---
title: 游标类型（PDO_SQLSRV 驱动程序）
description: 了解各种服务器端和客户端游标，以及用户在使用 Microsoft PDO_SQLSRV Driver for PHP for SQL Server 时如何指定游标类型。
ms.custom: ''
ms.date: 08/10/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 49ea6a6e-78d4-40f8-85eb-180b527f0537
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7660f71ba8a288840210734b85ac551a0770fc81
ms.sourcegitcommit: d1051f05a7db81ec62d9785bb6af572408f3d4e0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2020
ms.locfileid: "88680582"
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

可以使用 [PDO::setAttribute](../../connect/php/pdo-setattribute.md) 或 [PDOStatement::setAttribute](../../connect/php/pdostatement-setattribute.md) 的 `PDO::SQLSRV_ATTR_CLIENT_BUFFER_MAX_KB_SIZE` 属性配置保留结果集的缓冲区的大小。 还可以使用 pdo_sqlsrv.client_buffer_max_kb_size 在 php.ini 文件中设置最大缓冲区大小（例如，pdo_sqlsrv.client_buffer_max_kb_size = 1024）。

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

