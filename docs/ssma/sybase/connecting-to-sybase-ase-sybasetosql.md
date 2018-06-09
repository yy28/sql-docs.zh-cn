---
title: 连接到 Sybase ASE (SybaseToSQL) |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Connecting to Sybase ASE
ms.assetid: a45a2330-9175-4c9e-af38-ef920e350614
caps.latest.revision: 8
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 2fb1bb6047dca0965d71e80b1042d9fe1d8bca97
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2018
ms.locfileid: "34778453"
---
# <a name="connecting-to-sybase-ase-sybasetosql"></a>连接到 Sybase ASE (SybaseToSQL)
若要 Sybase 自适应 Server Enterprise (ASE) 将数据库迁移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure，你必须连接到包含你想要迁移的数据库的自适应服务器。 连接时，SSMA 获取自适应的服务器上所有数据库有关的元数据，并在 Sybase 元数据资源管理器窗格中显示数据库元数据。 SSMA 存储有关数据库服务器的信息，但不会存储密码。  
  
与 ASE 的连接将保持活动状态，直到关闭该项目。 当你重新打开项目时，你必须重新连接到 ASE 中，如果你想与服务器的活动连接。  
  
有关自适应的服务器的元数据不会自动更新。 相反，如果你想要更新 Sybase 元数据资源管理器中的元数据，则必须手动更新元数据，如本主题后面的"刷新 Sybase ASE 元数据"一节中所述。  
  
## <a name="required-ase-permissions"></a>所需的 ASE 权限  
用于连接到 ASE 的帐户必须至少具有**公共**到 master 数据库和要迁移到任何源数据库的访问[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。 此外，若要选择所要迁移的表的权限，用户必须具有 SELECT 权限下的系统表：  
  
-   [source_db].dbo.sysobjects  
  
-   [source_db].dbo.syscolumns  
  
-   [source_db].dbo.sysusers  
  
-   [source_db].dbo.systypes  
  
-   [source_db].dbo.sysconstraints  
  
-   [source_db].dbo.syscomments  
  
-   [source_db].dbo.sysindexes  
  
-   [source_db].dbo.sysreferences  
  
-   master.dbo.sysdatabases  
  
## <a name="establishing-a-connection-to-ase"></a>建立与 ASE 的连接  
当你连接到自适应的服务器时，SSMA 读取数据库元数据在数据库服务器上，然后将此元数据添加到项目文件。 此元数据转换到的对象时，SSMA 使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 语法时，它将迁移到的数据和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。 你可以浏览此元数据的 Sybase 元数据资源管理器窗格中，并检查各个数据库对象的属性。  
  
> [!IMPORTANT]  
> 你尝试连接到数据库服务器之前，请确保数据库服务器正在运行，并且可以接受连接。  
  
**若要连接到 Sybase ASE**  
  
1.  上**文件**菜单上，选择**连接到 Sybase**。  
  
    如果你以前连接到 Sybase，命令名称将**重新连接到 Sybase**。  
  
2.  在**提供程序**框中，选择任何已安装提供程序计算机上连接到 Sybase 服务器。  
  
3.  在**模式**框中，选择**标准模式**或**高级的模式**。  
  
    使用标准的模式来指定服务器名称、 端口、 用户名称和密码。 使用高级的模式来提供连接字符串。 此模式通常是仅用于故障排除或与技术支持工作。  
  
4.  如果你选择**标准模式**，提供以下值：  
  
    1.  在**服务器名称**框中，输入或选择的名称或数据库服务器的 IP 地址。  
  
    2.  如果数据库服务器未配置为接受连接上默认端口 (5000)，请输入中的 Sybase 连接使用的端口号**服务器端口**框。  
  
    3.  在**用户名**框中，输入 Sybase 帐户具有所需的权限。  
  
    4.  在**密码**框中，指定的用户名称中输入的密码。  
  
5.  如果你选择**高级的模式**，提供连接字符串中的**连接字符串**框。  
  
    不同的连接字符串的示例如下所示：  
  
    1.  **Sybase OLE DB 访问接口的连接字符串：**  
  
        Sybase ASE OLE DB 12.5，对于一个示例连接字符串，如下所示是：  
  
        `Server Name=sybserver;User ID=MyUserID;Password=MyP@$$word;Provider=Sybase.ASEOLEDBProvider;`  
  
        Sybase ASE OLE DB 15 个，一个示例连接字符串如下所示：  
  
        `Server=sybserver;User ID=MyUserID;Password=MyP@$$word;Provider= ASEOLEDB;Port=5000;`  
  
    2.  **Sybase ODBC 提供程序的连接字符串：**  
  
        `Driver=Adaptive Server Enterprise;Server=sybserver;uid=MyUserID;pwd=MyP@$$word;Port=5000;`  
  
    3.  **Sybase ADO.NET 提供程序的连接字符串：**  
  
        `Server=sybserver;Port=5000;uid=MyUserID;pwd=MyP@$$word;`  
  
    有关详细信息，请参阅[连接到 Sybase &#40;SybaseToSQL&#41;](../../ssma/sybase/connect-to-sybase-sybasetosql.md)。  
  
## <a name="reconnecting-to-sybase-ase"></a>重新连接到 Sybase ASE  
与数据库服务器的连接将保持活动状态，直到关闭该项目。 当你重新打开项目时，你必须重新连接，如果你想与自适应的服务器的活动连接。 您可以离线工作之前你想要更新元数据，数据库将对象加载到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure，并迁移数据。  
  
## <a name="refreshing-sybase-ase-metadata"></a>正在刷新 Sybase ASE 元数据  
不会自动刷新 ASE 数据库有关的元数据。 Sybase 元数据资源管理器中的元数据是元数据的快照，首次连接到自适应的服务器或您手动刷新元数据的最后一个时间时。 你可以手动更新单个数据库，单个数据库架构或所有数据库的元数据。  
  
**若要刷新元数据**  
  
1.  请确保你已连接到自适应的服务器。  
  
2.  在 Sybase 元数据资源管理器，选择你想要更新的数据库架构的数据库旁边的复选框。  
  
3.  右键单击数据库或单个数据库或数据库架构，然后选择**从数据库刷新**。  
  
4.  如果系统询问是否要检查当前对象，单击**是**。  
  
## <a name="next-step"></a>下一步  
  
-   迁移过程的下一步是[连接到的 SQL Server 实例](http://msdn.microsoft.com/en-us/dd368a1a-45b0-40e9-b4d3-5cdb48c26606) / [连接到 SQL Azure 的实例](http://msdn.microsoft.com/en-us/9e77e4b0-40c0-455c-8431-ca5d43849aa7)  
  
## <a name="see-also"></a>请参阅  
[将 Sybase ASE 数据库迁移到 SQL Server 的 Azure SQL DB &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
