---
title: 对 LocalDB 的支持 |Microsoft 文档
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: d315ad6a-0d50-4093-80c2-2f11217237c2
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 438802c4645ff3acdc1bed42af22e4e32786e1d0
ms.sourcegitcommit: f16003fd1ca28b5e06d5700e730f681720006816
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/11/2018
ms.locfileid: "35308746"
---
# <a name="support-for-localdb"></a>对 LocalDB 的支持

[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

LocalDB 是轻量版本[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，这也是可用自[!INCLUDE[ssSQL11](../../includes/sssql11_md.md)]。 本主题介绍如何连接到 LocalDB 实例中的数据库。

## <a name="remarks"></a>Remarks

有关 LocalDB，包括如何安装 LocalDB 和配置 LocalDB 实例，请参阅[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]上的联机丛书主题[!INCLUDE[ssSQL11](../../includes/sssql11_md.md)]Express LocalDB。

简单地说，LocalDB，你可以：

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

有关安装 LocalDB 的说明，请参阅[LocalDB 文档](../../database-engine/configure-windows/sql-server-2016-express-localdb.md)。 如果使用 sqlcmd.exe 来修改 LocalDB 实例中的数据，你将需要[sqlcmd 实用工具](../../tools/sqlcmd-utility.md)。

## <a name="see-also"></a>请参阅

[连接到服务器](../../connect/php/connecting-to-the-server.md)
