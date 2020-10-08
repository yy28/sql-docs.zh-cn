---
title: PHP 驱动程序对 LocalDB 的支持
description: 了解 Microsoft Drivers for PHP for SQL Server 如何支持连接到 LocalDB 数据库实例。
ms.custom: ''
ms.date: 05/06/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d315ad6a-0d50-4093-80c2-2f11217237c2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 47bcfa16712e0ef227da7c7ae53de14aa42deacb
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91726763"
---
# <a name="support-for-localdb"></a>支持 LocalDB

[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

LocalDB 是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的轻量级版本，自 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 开始提供。 本主题介绍如何连接到 LocalDB 实例中的数据库。

## <a name="remarks"></a>备注

有关 LocalDB 的详细信息（包括如何安装 LocalDB 和配置 LocalDB 实例），请参阅 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Express LocalDB 上的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 联机丛书主题。

简而言之，通过 LocalDB，可以：

-   使用 sqllocaldb.exe  发现默认实例的名称。

-   使用 AttachDBFilename 连接字符串关键字指定服务器应附加的数据库文件  。 使用 AttachDBFilename 时，如果没有使用 Database 连接字符串关键字指定数据库的名称，则在应用程序关闭时，该数据库将从 LocalDB 实例中删除   。

-   在连接字符串中指定 LocalDB 实例。 例如，下面是一个示例 SQLSRV 连接字符串：

    ```php
    $conn = sqlsrv_connect( '(localdb)\\v11.0',
        array( 'Database'=>'myData'));

    $conn = sqlsrv_connect( '(localdb)\\v11.0',
        array('AttachDBFileName'=>'c:\\myData.MDF','Database'=>'myData'));

    $conn = sqlsrv_connect( '(localdb)\\v11.0',
        array('AttachDBFileName'=>'c:\\myData.MDF'));
    ```

    接下来是一个示例 PDO_SQLSRV 连接字符串：  

    ```php
    $conn = new PDO( 'sqlsrv:server=(localdb)\\v11.0;'
        . 'Database=myData', NULL, NULL);

    $conn = new PDO( 'sqlsrv:server=(localdb)\\v11.0;'
        . 'AttachDBFileName=c:\\myData.MDF;Database=myData ',
        NULL, NULL);

    $conn = new PDO( 'sqlsrv:server=(localdb)\\v11.0;'
        . 'AttachDBFileName=c:\\myData.MDF', NULL, NULL);  
    ```

如果需要，您可以使用 sqllocaldb.exe 创建 LocalDB 实例。 还可以使用 sqlcmd.exe 添加和修改 LocalDB 实例中的数据库。 例如，`sqlcmd -S (localdb)\v11.0` 。 （在 IIS 中运行时，需要使用正确的帐户运行才能获得与在命令行中运行时相同的结果；若要了解详细信息，请参阅[将 LocalDB 与完整的 IIS 结合使用，第 2 部分：实例所有权](/archive/blogs/sqlexpress/using-localdb-with-full-iis-part-2-instance-ownership)。）

下面的示例连接字符串演示如何使用 SQLSRV 驱动程序连接到名为 myInstance 的 LocalDB 命名实例中的数据库：

```php
$conn = sqlsrv_connect( '(localdb)\\myInstance',
    array( 'Database'=>'myData'));
```

下面的示例连接字符串演示如何使用 PDO_SQLSRV 驱动程序连接到名为 myInstance 的 LocalDB 命名实例中的数据库：  
  
```php
$conn = new PDO( 'sqlsrv:server=(localdb)\\myInstance;'
    . 'database=myData', NULL, NULL);
```

有关安装 LocalDB 的说明，请参阅 [LocalDB 文档](../../database-engine/configure-windows/sql-server-express-localdb.md)。 如果使用 sqlcmd.exe 修改 LocalDB 实例中的数据，则需要[sqlcmd 实用工具](../../tools/sqlcmd-utility.md)。

## <a name="see-also"></a>另请参阅

[连接到服务器](../../connect/php/connecting-to-the-server.md)