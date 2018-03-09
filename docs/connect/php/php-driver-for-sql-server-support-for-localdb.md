---
title: "PHP Driver for SQL Server Support for LocalDB |Microsoft 文档"
ms.custom: 
ms.date: 02/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: sql
ms.prod_service: drivers
ms.component: php
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d315ad6a-0d50-4093-80c2-2f11217237c2
caps.latest.revision: "14"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4dcf9e36eb3928bc606053bdfda441520155864a
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="php-driver-for-sql-server-support-for-localdb"></a>PHP Driver for SQL Server 对 LocalDB 的支持

[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

从[!INCLUDE[ssSQL11](../../includes/sssql11_md.md)]的轻量版本[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]、 称为 LocalDB、 将可用。 本主题介绍如何连接到 LocalDB 实例中的数据库。

## <a name="remarks"></a>Remarks

有关 LocalDB，包括如何安装 LocalDB 和配置 LocalDB 实例，请参阅[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]上的联机丛书主题[!INCLUDE[ssSQL11](../../includes/sssql11_md.md)]Express LocalDB。

总之，通过 LocalDB，您可以：

-   使用**sqllocaldb.exe 我**来发现的默认实例的名称。

-   使用**AttachDBFilename**应附加连接字符串关键字来指定的数据库文件服务器。 使用时**AttachDBFilename**，如果不指定与数据库的名称**数据库**连接字符串关键字，数据库将从 LocalDB 实例时应用程序关闭。

-   连接字符串中指定的 LocalDB 实例。 例如，下面是一个 SQLSRV 连接字符串示例：

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

如果需要，您可以使用 sqllocaldb.exe 创建 LocalDB 实例。 还可以使用 sqlcmd.exe 添加和修改 LocalDB 实例中的数据库。 例如， `sqlcmd -S (localdb)\v11.0`。 (当在 IIS 中运行，你需要在要获取与你在命令行中; 上的运行时相同的结果的正确帐户下运行请参阅[使用 LocalDB 完整 iis，第 2 部分： 实例所有权](http://blogs.msdn.com/b/sqlexpress/archive/2011/12/09/using-localdb-with-full-iis-part-2-instance-ownership.aspx)有关详细信息。)

以下是连接到命名实例名为 myInstance LocalDB 中的数据库的示例连接字符串使用 SQLSRV 驱动程序：

```php
$conn = sqlsrv_connect( '(localdb)\\myInstance',
    array( 'Database'=>'myData'));
```

以下是连接到命名实例名为 myInstance LocalDB 中的数据库的示例连接字符串使用 PDO_SQLSRV 驱动程序：  
  
```php
$conn = new PDO( 'sqlsrv:server=(localdb)\\myInstance;'
    . 'database=myData', NULL, NULL);
```

你可以下载 LocalDB 从[SQL Server 2012 功能包页](http://go.microsoft.com/fwlink/?LinkID=236805)，或从[!INCLUDE[ssSQL11](../../includes/sssql11_md.md)]Express edition。 如果将使用 sqlcmd.exe 来修改 LocalDB 实例中的数据，你将需要从 sqlcmd [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)]，你可以通过在命令行实用工具下载[!INCLUDE[ssSQL11](../../includes/sssql11_md.md)]功能包页。

## <a name="see-also"></a>另请参阅

[连接到服务器](../../connect/php/connecting-to-the-server.md)
