---
title: 连接到 Sybase ASE (SybaseToSQL) |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Connecting to Sybase ASE
ms.assetid: a45a2330-9175-4c9e-af38-ef920e350614
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: d9c76a33a650284fde21b28af3a61b197829ef98
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63298534"
---
# <a name="connecting-to-sybase-ase-sybasetosql"></a>连接到 Sybase ASE (SybaseToSQL)
以自适应服务器 Sybase 企业 (ASE) 将数据库迁移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure，您必须连接到包含要迁移的数据库的自适应服务器。 连接时，SSMA 获得有关自适应服务器上所有数据库的元数据并在 Sybase 的元数据资源管理器窗格中显示数据库元数据。 SSMA 存储信息，数据库服务器中，但不存储密码。  
  
您连接到 ASE 将保持活动状态，直到您关闭该项目。 当您重新打开项目时，则必须重新连接到 ASE 中，如果要到服务器的活动连接。  
  
关于自适应服务器的元数据不会自动更新。 相反，如果您想要更新 Sybase 的元数据资源管理器中的元数据，您必须手动更新元数据，如本主题后面部分中的"刷新 Sybase ASE 元数据"部分中所述。  
  
## <a name="required-ase-permissions"></a>所需的 ASE 的权限  
用于连接到 ASE 的帐户必须至少**公用**访问 master 数据库以及任何源数据库迁移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure。 此外，若要选择要迁移的表的权限，用户必须选择 权限上以下系统表：  
  
-   [source_db].dbo.sysobjects  
  
-   [source_db].dbo.syscolumns  
  
-   [source_db].dbo.sysusers  
  
-   [source_db].dbo.systypes  
  
-   [source_db].dbo.sysconstraints  
  
-   [source_db].dbo.syscomments  
  
-   [source_db].dbo.sysindexes  
  
-   [source_db].dbo.sysreferences  
  
-   master.dbo.sysdatabases  
  
## <a name="establishing-a-connection-to-ase"></a>建立连接到 ASE  
当您连接到一个自适应的服务器时，SSMA 读取数据库元数据在数据库服务器中，，然后将此元数据添加到项目文件。 它将转换为对象时，使用此元数据 SSMA 通过[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 语法时，它将迁移到数据和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure。 可以浏览此元数据在 Sybase 的元数据资源管理器窗格中，查看单个数据库对象的属性。  
  
> [!IMPORTANT]  
> 您尝试连接到数据库服务器之前，请确保数据库服务器正在运行且可以接受的连接。  
  
**若要连接到 Sybase ASE**  
  
1.  在**文件**菜单中，选择**连接到 Sybase**。  
  
    如果您以前连接到 Sybase，命令名称将**与 Sybase 重新连接**。  
  
2.  在**提供程序**框中，选择任何已安装的提供程序的计算机上连接到 Sybase 服务器。  
  
3.  在**模式**框中，选择**标准模式**或**高级的模式**。  
  
    使用标准模式来指定服务器名称、 端口、 用户名和密码。 使用高级的模式提供的连接字符串。 此模式通常是仅用于故障排除，或与技术支持工作。  
  
4.  如果您选择**标准模式**，提供下列值：  
  
    1.  在**服务器名称**框中，输入或选择的名称或 IP 地址数据库服务器。  
  
    2.  如果数据库服务器没有配置为接受连接默认端口 (5000)，输入用于在 Sybase 连接的端口号**服务器端口**框。  
  
    3.  在**用户名**框中，输入一个 Sybase 帐户具有所需的权限。  
  
    4.  在**密码**框中，输入指定的用户名的密码。  
  
5.  如果您选择**高级的模式**，提供中的连接字符串**连接字符串**框。  
  
    不同的连接字符串的示例如下所示：  
  
    1.  **Sybase OLE DB 提供程序的连接字符串：**  
  
        对于 Sybase ASE OLE DB 12.5，连接字符串的示例如下所示：  
  
        `Server Name=sybserver;User ID=MyUserID;Password=MyP@$$word;Provider=Sybase.ASEOLEDBProvider;`  
  
        Sybase ASE OLE DB 15 个，连接字符串的示例如下所示：  
  
        `Server=sybserver;User ID=MyUserID;Password=MyP@$$word;Provider= ASEOLEDB;Port=5000;`  
  
    2.  **Sybase ODBC 提供程序的连接字符串：**  
  
        `Driver=Adaptive Server Enterprise;Server=sybserver;uid=MyUserID;pwd=MyP@$$word;Port=5000;`  
  
    3.  **Sybase ADO.NET 提供程序的连接字符串：**  
  
        `Server=sybserver;Port=5000;uid=MyUserID;pwd=MyP@$$word;`  
  
    有关详细信息，请参阅[连接到 Sybase &#40;SybaseToSQL&#41;](../../ssma/sybase/connect-to-sybase-sybasetosql.md)。  
  
## <a name="reconnecting-to-sybase-ase"></a>重新连接到 ASE Sybase  
与数据库服务器的连接将保持活动状态，直到您关闭该项目。 当您重新打开项目时，则必须重新连接如果您希望与自适应服务器的活动连接。 您可以脱机处理直到您要更新元数据，加载到数据库对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 和迁移数据。  
  
## <a name="refreshing-sybase-ase-metadata"></a>正在刷新 Sybase ASE 元数据  
有关 ASE 数据库的元数据不会自动刷新。 Sybase 元数据资源管理器中的元数据是元数据的快照，首次连接到自适应的服务器或在手动刷新元数据的最后一个时间时。 您可以手动更新单个数据库中，单个数据库架构或所有数据库的元数据。  
  
**若要刷新元数据**  
  
1.  请确保连接到自适应的服务器。  
  
2.  Sybase 元数据资源管理器中选择你想要更新的数据库架构的数据库旁边的复选框。  
  
3.  右键单击数据库或单个数据库或数据库架构，然后选择**从数据库刷新**。  
  
4.  如果您要求检查当前的对象，请单击**是**。  
  
## <a name="next-step"></a>下一步  
  
-   迁移过程中的下一步是[连接到 SQL Server 的实例](connecting-to-sql-server-sybasetosql.md) / [连接到 SQL Azure 实例](connecting-to-azure-sql-db-sybasetosql.md)  
  
## <a name="see-also"></a>请参阅  
[将 Sybase ASE 数据库迁移到 SQL Server-Azure SQL 数据库&#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
