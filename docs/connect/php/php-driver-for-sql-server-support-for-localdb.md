---
title: 对 LocalDB 的支持 |Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d315ad6a-0d50-4093-80c2-2f11217237c2
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 48c9955733672699e16cb4a00e28fa2f59717b80
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2019
ms.locfileid: "66797088"
---
# <a name="support-for-localdb"></a>支持 LocalDB

[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

LocalDB 是轻型版本，其中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，这也是可用以来[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]。 本主题介绍如何连接到 LocalDB 实例中的数据库。

## <a name="remarks"></a>Remarks

有关 LocalDB，包括如何安装 LocalDB 和配置 LocalDB 实例，请参阅[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]上的联机丛书主题[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]Express LocalDB。

简单地说，LocalDB，您可以：

-   使用**sqllocaldb.exe 我**发现的默认实例的名称。

-   使用 AttachDBFilename 连接字符串关键字指定服务器应附加的数据库文件  。 使用 AttachDBFilename 时，如果没有使用 Database 连接字符串关键字指定数据库的名称，则在应用程序关闭时，该数据库将从 LocalDB 实例中删除   。

-   在连接字符串中指定 LocalDB 实例。 例如，下面是一个 SQLSRV 连接字符串示例：

    ```php
    $conn = sqlsrv_connect( '(localdb)\\v11.0',
        array( 'Database'=>'myData'));

    $conn = sqlsrv_connect( '(localdb)\\v11.0',
        array('AttachDBFileName'=>'c:\\myData.MDF','Database'=>'myData'));

    $conn = sqlsrv_connect( '(localdb)\\v11.0',
        array('AttachDBFileName'=>'c:\\myData.MDF'));
    ```

    接下来是一个 PDO_SQLSRV 连接字符串示例：  

    ```php
    $conn = new PDO( 'sqlsrv:server=(localdb)\\v11.0;'
        . 'Database=myData', NULL, NULL);

    $conn = new PDO( 'sqlsrv:server=(localdb)\\v11.0;'
        . 'AttachDBFileName=c:\\myData.MDF;Database=myData ',
        NULL, NULL);

    $conn = new PDO( 'sqlsrv:server=(localdb)\\v11.0;'
        . 'AttachDBFileName=c:\\myData.MDF', NULL, NULL);  
    ```

如果需要，您可以使用 sqllocaldb.exe 创建 LocalDB 实例。 还可以使用 sqlcmd.exe 添加和修改 LocalDB 实例中的数据库。 例如， `sqlcmd -S (localdb)\v11.0`。 (需要以获取与在命令行中; 运行时相同的结果在正确的帐户下运行时在 IIS 中运行，请参阅[将 localdb 与完整 IIS，第 2 部分结合： 实例所有权](https://blogs.msdn.com/b/sqlexpress/archive/2011/12/09/using-localdb-with-full-iis-part-2-instance-ownership.aspx)有关详细信息。)

以下是连接到 LocalDB 命名名为 myInstance 的实例中的数据库的示例连接字符串使用 SQLSRV 驱动程序：

```php
$conn = sqlsrv_connect( '(localdb)\\myInstance',
    array( 'Database'=>'myData'));
```

以下是连接到 LocalDB 命名名为 myInstance 的实例中的数据库的示例连接字符串使用 PDO_SQLSRV 驱动程序：  
  
```php
$conn = new PDO( 'sqlsrv:server=(localdb)\\myInstance;'
    . 'database=myData', NULL, NULL);
```

有关安装 LocalDB 的说明，请参阅[LocalDB 文档](../../database-engine/configure-windows/sql-server-2016-express-localdb.md)。 如果使用 sqlcmd.exe 来修改 LocalDB 实例中的数据，则需要[sqlcmd 实用工具](../../tools/sqlcmd-utility.md)。

## <a name="see-also"></a>另请参阅

[连接到服务器](../../connect/php/connecting-to-the-server.md)
