---
title: 连接到 SQL Server (MySQLToSQL) |Microsoft Docs
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
helpviewer_keywords:
- connecting to SQL Server 2008, SQL Server permission
- connecting to SQL Server 2008, synchronization
ms.assetid: 08233267-693e-46e6-9ca3-3a3dfd3d2be7
caps.latest.revision: 18
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 08744f04acbc5ad066be78b90f8880459ce74629
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2018
ms.locfileid: "40396227"
---
# <a name="connecting-to-sql-server-mysqltosql"></a>连接到 SQL Server (MySQLToSQL)
若要将 MySQL 数据库迁移到 SQL Server，必须连接到 SQL Server 目标实例。 连接时，SSMA 获取有关 SQL Server 实例中的所有数据库的元数据，并在 SQL Server 元数据资源管理器中显示数据库元数据。 SSMA 存储的连接，但不存储密码的 SQL Server 实例的信息。  
  
与 SQL Server 的连接保持活动状态，直到关闭该项目。 当你重新打开该项目时，你必须重新连接到 SQL Server 中，如果想要的活动连接到服务器。 加载到 SQL Server 数据库对象并将数据迁移之前，您可以脱机工作。  
  
有关 SQL Server 实例的元数据不会自动同步。 相反，若要更新 SQL Server 元数据资源管理器中的元数据，必须手动更新 SQL Server 元数据。 有关详细信息，请参阅本主题后面的"同步 SQL Server 元数据"部分。  
  
## <a name="required-sql-server-permissions"></a>所需的 SQL Server 权限  
用于连接到 SQL Server 的帐户需要不同的权限，具体取决于该帐户执行的操作：  
  
-   要转换到 MySQL 对象[!INCLUDE[tsql](../../includes/tsql-md.md)]语法中，更新元数据从 SQL Server，或者将保存到转换后的语法编写的脚本，该帐户必须有权登录到 SQL Server 实例。  
  
-   若要将数据库对象加载到 SQL Server，最小权限要求是中的成员身份**db_owner**目标数据库中的数据库角色。  
  
## <a name="establishing-a-sql-server-connection"></a>建立 SQL Server 连接  
将 MySQL 数据库对象转换为 SQL Server 语法之前，必须建立与想要迁移或多个 MySQL 数据库的 SQL server 实例的连接。  
  
在定义的连接属性时，还可以指定对象和数据将迁移的数据库。 连接到 SQL Server 后，可以自定义此映射 MySQL 架构级别上。 有关详细信息，请参阅[映射到 SQL Server 架构的 MySQL 数据库&#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md)  
  
> [!IMPORTANT]  
> 在尝试连接到 SQL Server 之前，请确保 SQL Server 实例正在运行，并且可接受连接。  
  
**若要连接到 SQL Server**  
  
1.  上**文件**菜单中，选择**连接到 SQL Server** （在创建项目后启用此选项）。  
  
    如果你之前已连接到 SQL Server，命令名称将是**重新连接到 SQL Server**。  
  
2.  在连接对话框中，输入或选择的 SQL Server 实例的名称。  
  
    -   如果要连接到本地计算机上的默认实例，则可以输入**localhost**或句点 (**。**)。  
  
    -   如果要连接到另一台计算机上的默认实例，输入的计算机的名称。  
  
    -   如果要连接到另一台计算机上的命名实例，输入计算机名称后跟反斜杠，然后该实例名称，例如 MyServer\MyInstance。  
  
3.  如果你的 SQL Server 实例配置为接受非默认端口上的连接，输入用于中的 SQL Server 连接的端口号**服务器端口**框。 对于 SQL Server 默认实例，则默认端口号为 1433年。 对于命名实例，SSMA 将尝试从 SQL Server Browser 服务来获取端口号。  
  
4.  在中**身份验证**框中，选择要用于连接的身份验证类型。 若要使用当前 Windows 帐户，请选择**Windows 身份验证**。 若要使用的 SQL Server 登录名，选择 SQL Server 身份验证，并提供登录名和密码。  
  
5.  对于安全的连接，将添加两个控件，**加密连接**并**TrustServerCertificate**复选框。 仅当**加密连接**处于选中状态， **TrustServerCertificate**复选框是否可见。 当**加密连接**已选中 (true) 和**TrustServerCertificate**处于未选中状态 (false)，它将验证 SQL Server SSL 证书。 验证服务器证书是 SSL 握手过程的一部分，这可确保服务器是要连接到的正确服务器。 若要确保这一点，必须在客户端和服务器端上安装证书。  
  
6.  单击连接。  
  
**更高版本兼容性**  
  
它允许连接/重新连接到更高版本的 SQL Server。  
  
1.  你将能够连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2008年或[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2012年或[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014年或[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2016 时创建的项目是[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2005年。  
  
2.  你将能够连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2012年或[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014年或[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2016 时创建的项目是[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2008年，但它不允许即连接到较低版本[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005.  
  
3.  你将能够连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2012年或[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014年或[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2016 时创建的项目是[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2012年。  
  
4.  你将能够连接到仅[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014年或[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2016 时创建的项目是[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014年。  
  
5.  更高版本兼容性不能用于"SQL Azure"。  
  
||||||||  
|-|-|-|-|-|-|-|  
|**项目类型与目标服务器版本**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005<br /> (版本： 9.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008<br /> (版本： 10.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012<br />(Version:11.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014<br />(Version:12.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016<br />(Version:13.x)|SQL Azure|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005|用户帐户控制|是|是|是|用户帐户控制||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008||用户帐户控制|是|是|用户帐户控制||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012|||用户帐户控制|是|用户帐户控制||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014||||用户帐户控制|用户帐户控制||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2016|||||用户帐户控制||  
|SQL Azure||||||用户帐户控制|  
  
> [!IMPORTANT]  
> 根据项目类型，但不是根据版本的数据库对象的转换执行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]相连。 情况下[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2005年项目中，执行转换为每个[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2005 即使你已连接到更高版本的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)](SQL Server 2008/SQL Server 2012/SQL Server 2014/SQL Server 2016)。  
  
## <a name="synchronizing-sql-server-metadata"></a>同步 SQL Server 元数据  
有关 SQL Server 数据库的元数据不会自动更新。 SQL Server 元数据资源管理器中的元数据是快照元数据时首次连接到 SQL Server，或上一次你手动更新元数据。 您可以手动更新所有数据库，或任何单个数据库或数据库对象的元数据。  
  
**同步元数据**  
  
1.  请确保连接到 SQL Server。  
  
2.  SQL Server 元数据资源管理器中，选择你想要更新的数据库架构的数据库旁边的复选框。  
  
    例如，若要更新的所有数据库的元数据，请选择数据库旁边的框。  
  
3.  右键单击数据库，或单个数据库或数据库架构，然后选择**与数据库同步**。  
  
## <a name="next-step"></a>下一步  
迁移的下一步取决于您的项目需求：  
  
-   若要自定义 MySQL 架构和 SQL Server 数据库和架构之间的映射，请参阅[映射到 SQL Server 架构的 MySQL 数据库&#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md)  
  
-   若要自定义项目的配置选项，请参阅[设置项目选项&#40;MySQLToSQL&#41;](../../ssma/mysql/setting-project-options-mysqltosql.md)  
  
-   若要自定义源和目标数据类型的映射，请参阅[映射 MySQL 和 SQL Server 数据类型&#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md)  
  
-   如果不需要执行任何这些任务，你可以将 SQL Server 对象定义转换的 MySQL 数据库对象定义。 有关详细信息，请参阅[转换 MySQL 数据库&#40;MySQLToSQL&#41;](../../ssma/mysql/converting-mysql-databases-mysqltosql.md)  
  
## <a name="see-also"></a>请参阅  
[迁移 MySQL 数据库移到 SQL Server-Azure SQL 数据库&#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
