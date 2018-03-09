---
title: "连接到 DB2 数据库 (DB2ToSQL) |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-db2
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 5eb5801d-f0c3-4127-97c0-0b1ef49f4844
caps.latest.revision: "7"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f718f75a750d376bdae9ff7bfab10f298107822d
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="connecting-to-db2-database-db2tosql"></a>连接到 DB2 数据库 (DB2ToSQL)
迁移到 DB2 数据库[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，你必须连接到你想要迁移的 DB2 数据库。 连接时，SSMA 获取有关所有的 DB2 架构的元数据，然后在 DB2 元数据资源管理器窗格中显示内容。 SSMA 存储有关数据库服务器的信息，但不会存储密码。  
  
数据库的连接将保持活动状态，直到关闭该项目。 当你重新打开项目时，你必须重新连接，如果你想与数据库的活动连接。  
  
有关 DB2 数据库的元数据不自动更新。 相反，如果你想要更新 DB2 元数据资源管理器中的元数据，则必须手动更新它。 有关详细信息，请参阅本主题后面的"刷新 DB2 元数据"部分。  
  
## <a name="required-db2-permissions"></a>所需的 DB2 权限  
用户授权定义的命令和可用于用户的对象的列表。 此列表从而控制用户操作。 在 DB2，有的权限来进行授权，同时在实例级别和 DB2 数据库的级别的预定义的组。 这使 SSMA 从连接的用户拥有的架构中获取元数据。 获取其他架构中的对象的元数据，然后转换这些架构中的对象，该帐户必须具有以下权限：  
  
-   除非限制关键字用在创建通常向 PUBLIC 授予架构迁移架构访问权限  
  
-   对于数据迁移的数据访问要求 DATAACCESS  
  
## <a name="establishing-a-connection-to-db2"></a>建立与 DB2 的连接  
当你连接到数据库时，SSMA 读取数据库元数据，然后将此元数据添加到项目文件。 此元数据转换到的对象时，SSMA 使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]语法中，当它迁移到的数据和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 你可以浏览此元数据在 DB2 元数据资源管理器窗格中，并检查各个数据库对象的属性。  
  
> [!IMPORTANT]  
> 你尝试进行连接之前，请确保数据库服务器正在运行，并且可以接受连接。  
  
**若要连接到 DB2**  
  
1.  上**文件**菜单上，选择**连接到 DB2**。  
  
    如果你以前连接到 DB2，命令名称将**重新连接到 DB2**。  
  
2.  在**提供程序**框中，你将看到**OLE DB 访问接口**这当前是唯一的 DB2 客户端访问接口。  
  
3.  在**Manager**你可以选择框**zOs 的 Db2**，或**LUW 的 DB2**  
  
4.  在**模式**框中，选择**标准模式**，或**连接字符串模式**。  
  
    使用标准的模式来指定服务器名称和端口。 使用服务名称模式，若要手动指定 DB2 服务名称。 使用连接字符串模式来提供完整连接字符串。  
  
5.  如果你选择**标准模式**，提供以下值：  
  
    -   在**服务器名称**框中，输入或选择的名称或数据库服务器的 IP 地址。  
  
    -   如果数据库服务器未配置为接受连接上默认端口 (1521) 中，输入用于在 DB2 连接的端口号**服务器端口**框。  
  
    -   在**服务器端口**框中，输入的 TCP/IP 端口号。  
  
    -   在**初始目录**框中，输入数据库名称  
  
    -   在**用户名**框中，输入具有所需的权限的 DB2 帐户。  
  
    -   在**密码**框中，指定的用户名称中输入的密码。  
  
6.  如果你选择**连接字符串模式**，提供连接字符串中的**连接字符串**框。  
  
    下面的示例演示一个 OLE DB 连接字符串：  
  
    `Provider=OraOLEDB.DB2;Data Source=MyDB2DB;User Id=myUsername;Password=myPassword;`  
  
    下面的示例演示一个使用集成的安全性的 DB2 客户端连接字符串：  
  
    `Data Source=MyDB2DB;Integrated Security=yes;`  
  
    有关详细信息，请参阅[连接到 Oracle &#40; OracleToSQL &#41;](../../ssma/oracle/connect-to-oracle-oracletosql.md)。  
  
## <a name="reconnecting-to-db2"></a>重新连接到 DB2  
与数据库服务器的连接将保持活动状态，直到关闭该项目。 当你重新打开项目时，你必须重新连接，如果你想与数据库的活动连接。 您可以离线工作之前你想要更新元数据，数据库将对象加载到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，并迁移数据。  
  
## <a name="refreshing-db2-metadata"></a>正在刷新 DB2 元数据  
有关 DB2 数据库的元数据不会自动刷新。 DB2 元数据资源管理器中的元数据是首次连接时的元数据或最后一次你手动刷新元数据的快照。 你可以手动更新所有架构、 单个架构或单独的数据库对象的元数据。  
  
**若要刷新元数据**  
  
1.  请确保你已连接到数据库。  
  
2.  在 DB2 元数据资源管理器，选择你想要更新每个架构或数据库对象旁边的复选框。  
  
3.  右键单击**架构**，或单个架构或数据库对象，，然后选择**从数据库刷新**。  
  
    如果没有活动连接，将显示 SSMA**连接到 DB2**对话框中，因此您可以连接。  
  
4.  在从数据库对话框刷新中，指定要刷新的对象。  
  
    -   若要刷新的对象，请单击**Active**字段旁边的对象之前会出现一个箭头。  
  
    -   若要防止对象被刷新，请单击**Active**字段旁边的对象，直到**X**显示。  
  
    -   若要刷新或拒绝的对象的类别，请单击**Active**字段旁边的类别文件夹。  
  
    若要查看的颜色编码定义，请单击**图例**按钮。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok_md.md)]  
  
## <a name="next-step"></a>下一步  
  
-   迁移过程的下一步是[连接到 SQL Server](http://msdn.microsoft.com/en-us/b59803cb-3cc6-41cc-8553-faf90851410e)。  
  
## <a name="see-also"></a>另请参阅  
[将 DB2 数据库迁移到 SQL Server &#40; DB2ToSQL &#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)  
  
