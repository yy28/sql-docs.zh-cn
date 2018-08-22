---
title: 连接到 DB2 数据库 (DB2ToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 5eb5801d-f0c3-4127-97c0-0b1ef49f4844
caps.latest.revision: 7
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 2228a08c2985f4e683ff860cd77e68159a0ecd0a
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2018
ms.locfileid: "40394590"
---
# <a name="connecting-to-db2-database-db2tosql"></a>连接到 DB2 数据库 (DB2ToSQL)
将 DB2 数据库迁移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，必须连接到你想要迁移的 DB2 数据库。 连接时，SSMA 中获取所有的 DB2 架构有关的元数据，然后在 DB2 元数据资源管理器窗格中显示。 SSMA 存储信息，数据库服务器中，但不存储密码。  
  
与数据库的连接保持活动状态，直到关闭该项目。 重新打开该项目，必须重新连接如果想要的活动连接到数据库。  
  
DB2 数据库的元数据不会自动更新。 相反，如果你想要更新 DB2 元数据资源管理器中的元数据，则必须手动更新它。 有关详细信息，请参阅本主题后面的"刷新 DB2 元数据"部分。  
  
## <a name="required-db2-permissions"></a>所需的 DB2 权限  
用户授权中定义的命令和可用的用户对象的列表。 因此，此列表控制用户操作。 在 DB2，有预先确定的来进行授权，在实例级别和 DB2 数据库级别的权限的组。 这使 SSMA 从连接的用户拥有的架构中获取元数据。 若要获取的其他架构中的对象元数据，然后将转换这些架构中的对象，该帐户必须具有以下权限：  
  
-   除非在创建中使用了限制关键字通常为 PUBLIC 授予架构迁移架构访问权限  
  
-   数据迁移的数据访问要求 DATAACCESS  
  
## <a name="establishing-a-connection-to-db2"></a>建立连接到 DB2  
当连接到数据库时，SSMA 读取数据库元数据，然后将此元数据添加到项目文件。 它将转换到的对象时，使用此元数据的 SSMA[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]语法，并当它会将数据迁移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 您可以浏览此 DB2 元数据资源管理器窗格中的元数据，并查看单独的数据库对象的属性。  
  
> [!IMPORTANT]  
> 尝试连接之前，请确保数据库服务器正在运行，并且可以接受连接。  
  
**若要连接到 DB2**  
  
1.  上**文件**菜单中，选择**连接到 DB2**。  
  
    如果你之前连接到 DB2，命令名称将是**重新连接到 DB2**。  
  
2.  在中**提供程序**框中，将看到**OLE DB 访问接口**这当前是唯一的 DB2 客户端访问提供程序。  
  
3.  在中**管理器**框，您可以选择任一**zOs 的 Db2**，或**DB2 for luw 提供**  
  
4.  在中**模式下**框中，选择**标准模式**，或**连接字符串模式**。  
  
    使用标准模式来指定服务器名称和端口。 使用服务名称模式，若要手动指定 DB2 服务名称。 使用连接字符串模式来提供完整的连接字符串。  
  
5.  如果您选择**标准模式**，提供下列值：  
  
    -   在**服务器名称**框中，输入或选择的名称或 IP 地址数据库服务器。  
  
    -   如果数据库服务器未配置为接受连接上默认端口 (1521) 中，输入用于在 DB2 连接的端口号**服务器端口**框。  
  
    -   在中**服务器端口**框中，输入的 TCP/IP 端口号。  
  
    -   在中**Initial Catalog**框中，输入数据库名称  
  
    -   在中**用户名**框中，输入具有所需的权限的 DB2 帐户。  
  
    -   在**密码**框中，输入指定的用户名的密码。  
  
6.  如果选择**连接字符串模式**，提供连接字符串**连接字符串**框。  
  
    下面的示例演示的 OLE DB 连接字符串：  
  
    `Provider=OraOLEDB.DB2;Data Source=MyDB2DB;User Id=myUsername;Password=myPassword;`  
  
    下面的示例显示了使用集成的安全性的 DB2 客户端连接字符串：  
  
    `Data Source=MyDB2DB;Integrated Security=yes;`  
  
    有关详细信息，请参阅[连接到 Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/connect-to-oracle-oracletosql.md)。  
  
## <a name="reconnecting-to-db2"></a>重新连接到 DB2  
与数据库服务器的连接将保持活动状态，直到您关闭该项目。 重新打开该项目，必须重新连接如果想要的活动连接到数据库。 您可以脱机处理直到您要更新元数据，加载到数据库对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，和迁移数据。  
  
## <a name="refreshing-db2-metadata"></a>正在刷新 DB2 元数据  
DB2 数据库的元数据不会自动刷新。 DB2 的元数据资源管理器中的元数据是元数据，当您首次连接或上次您手动刷新元数据的快照。 您可以手动更新所有架构、 单一架构或单独的数据库对象的元数据。  
  
**若要刷新元数据**  
  
1.  请确保您已连接到数据库。  
  
2.  在 DB2 的元数据资源管理器中，选择您要更新的每个架构或数据库对象旁边的复选框。  
  
3.  用鼠标右键单击**架构**，或者单个架构或数据库对象，然后再选择**从数据库刷新**。  
  
    如果没有活动的连接，将显示 SSMA**连接到 DB2**对话框，以便您可以连接。  
  
4.  在刷新数据库对话框中，指定要刷新的对象。  
  
    -   若要刷新对象，请单击**活动**字段旁边会显示一个箭头，直到该对象。  
  
    -   若要禁止刷新对象，请单击**活动**字段相邻的对象，直到**X**出现。  
  
    -   若要刷新或拒绝的对象类别，请单击**活动**类别文件夹旁边的字段。  
  
    若要查看的颜色代码定义，请单击**图例**按钮。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="next-step"></a>下一步  
  
-   迁移过程的下一步是为[连接到 SQL Server](http://msdn.microsoft.com/b59803cb-3cc6-41cc-8553-faf90851410e)。  
  
## <a name="see-also"></a>请参阅  
[迁移的 DB2 数据库移到 SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)  
  
