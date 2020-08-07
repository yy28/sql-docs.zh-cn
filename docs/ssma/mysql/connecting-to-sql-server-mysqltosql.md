---
title: 正在连接到 SQL Server (MySQLToSQL) |Microsoft Docs
description: 了解如何连接到 SQL Server 的目标实例以迁移 MySQL 数据库。 SSMA 获取有关 SQL Server 中的数据库的元数据。
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- connecting to SQL Server 2008, SQL Server permission
- connecting to SQL Server 2008, synchronization
ms.assetid: 08233267-693e-46e6-9ca3-3a3dfd3d2be7
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: f79784b6498f080b15f1ef370e8a3f31be81a871
ms.sourcegitcommit: 777704aefa7e574f4b7d62ad2a4c1b10ca1731ff
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/06/2020
ms.locfileid: "87823289"
---
# <a name="connecting-to-sql-server-mysqltosql"></a>连接到 SQL Server (MySQLToSQL)
若要将 MySQL 数据库迁移到 SQL Server，你必须连接到 SQL Server 的目标实例。 在连接时，SSMA 将获取 SQL Server 实例中所有数据库的元数据，并在 SQL Server 元数据资源管理器中显示数据库元数据。 SSMA 存储连接到但不存储密码的 SQL Server 实例的信息。  
  
到 SQL Server 的连接保持活动状态，直到关闭项目。 重新打开项目时，如果需要与服务器建立活动连接，则必须重新连接到 SQL Server。 在将数据库对象加载到 SQL Server 和迁移数据之前，可以脱机工作。  
  
与 SQL Server 实例有关的元数据不会自动同步。 相反，若要更新 SQL Server 元数据资源管理器中的元数据，必须手动更新 SQL Server 元数据。 有关详细信息，请参阅本主题后面的 "同步 SQL Server 元数据" 一节。  
  
## <a name="required-sql-server-permissions"></a>必需的 SQL Server 权限  
用于连接 SQL Server 的帐户需要不同的权限，具体取决于帐户执行的操作：  
  
-   若要将 MySQL 对象转换为 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语法、从 SQL Server 更新元数据，或者将转换的语法保存到脚本中，该帐户必须有权登录到 SQL Server 实例。  
  
-   若要将数据库对象加载到 SQL Server 中，最低权限要求是目标数据库中**db_owner**数据库角色的成员身份。  
  
## <a name="establishing-a-sql-server-connection"></a>建立 SQL Server 连接  
在将 MySQL 数据库对象转换为 SQL Server 语法之前，必须与要迁移 MySQL 数据库的 SQL Server 实例建立连接。  
  
定义连接属性时，还可以指定要将对象和数据迁移到的数据库。 连接到 SQL Server 后，你可以在 MySQL 架构级别自定义此映射。 有关详细信息，请参阅[将 MySQL 数据库映射到 SQL Server 架构 &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md)  
  
> [!IMPORTANT]  
> 尝试连接到 SQL Server 之前，请确保 SQL Server 的实例正在运行，并且可以接受连接。  
  
**连接到 SQL Server**  
  
1.  在 "**文件**" 菜单上，选择 "**连接到 SQL Server** (在创建项目) 后启用此选项。  
  
    如果以前已连接到 SQL Server，则命令名称将**重新连接到 SQL Server**。  
  
2.  在 "连接" 对话框中，输入或选择 SQL Server 实例的名称。  
  
    -   如果要连接到本地计算机上的默认实例，则可以输入**localhost**或点 (**。**) 。  
  
    -   如果要连接到另一台计算机上的默认实例，请输入计算机的名称。  
  
    -   如果要连接到另一台计算机上的命名实例，请输入计算机名称后跟反斜杠和实例名称，如 MyServer\MyInstance。  
  
3.  如果 SQL Server 的实例配置为接受非默认端口上的连接，请在 "**服务器端口**" 框中输入用于 SQL Server 连接的端口号。 对于 SQL Server 的默认实例，默认端口号为1433。 对于命名实例，SSMA 将尝试从 SQL Server Browser 服务获取端口号。  
  
4.  在 "**身份验证**" 框中，选择要用于连接的身份验证类型。 若要使用当前的 Windows 帐户，请选择 " **Windows 身份验证**"。 若要使用 SQL Server 登录名，请选择 "SQL Server 身份验证"，然后提供登录名和密码。  
  
5.  对于安全连接，将添加两个控件，即 "**加密连接**" 和 " **TrustServerCertificate** " 复选框。 只有在选中 "**加密连接**" 时，" **TrustServerCertificate** " 复选框才可见。 选中 "**加密连接**" (true) 并取消选中 " **TrustServerCertificate** " (false) ，它将验证 SQL Server SSL 证书。 验证服务器证书是 SSL 握手过程的一部分，这可确保服务器是要连接到的正确服务器。 为了确保这一点，证书必须安装在客户端和服务器端。  
  
6.  单击“连接”。  
  
**更高版本兼容性**  
  
允许连接/重新连接到 SQL Server 的更高版本。  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 如果创建的项目是 "2005"，则可以连接到2008或2012、2014或 2016 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
2.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]如果创建的项目为2008，则可以连接到2012或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 但不允许连接到较低的版本，即 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005。  
  
3.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 如果创建的项目是2012，你将能够连接到2012或2014或 2016 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
4.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 如果创建的项目为2014，你将只能连接到2014或 2016 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
5.  较高的版本兼容性对于 "SQL Azure" 无效。  
  
|项目类型与目标服务器版本|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005<br />  (版本： 1.x) |[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008<br />  (版本： 8.x) |[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012<br /> (版本： 11. x) |[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014<br /> (版本： 12. x) |[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016<br /> (版本：十三) |SQL Azure|  
|-|-|-|-|-|-|-|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005|是|是|是|是|是||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008||是|是|是|是||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012|||是|是|是||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014||||是|是||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2016|||||是||  
|SQL Azure||||||是|  
  
> [!IMPORTANT]  
> 数据库对象的转换是根据项目类型执行的，而不是按连接到的的版本执行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 如果项目为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 即使连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQL Server 2008/SQL Server 2012/SQL Server 2014/SQL Server 2016)  (的更高版本，也会按照2005执行转换。  
  
## <a name="synchronizing-sql-server-metadata"></a>同步 SQL Server 元数据  
不会自动更新与 SQL Server 数据库有关的元数据。 SQL Server 元数据资源管理器中的元数据是首次连接到 SQL Server 或上次手动更新元数据时的元数据的快照。 您可以为所有数据库或任何单个数据库或数据库对象手动更新元数据。  
  
**同步元数据**  
  
1.  请确保已连接到 SQL Server。  
  
2.  在 SQL Server 元数据资源管理器 "中，选中要更新的数据库或数据库架构旁边的复选框。  
  
    例如，若要更新所有数据库的元数据，请选中 "数据库" 旁边的复选框。  
  
3.  右键单击 "数据库"、"数据库" 或 "数据库架构"，然后选择 "**与数据库同步**"。  
  
## <a name="next-step"></a>下一步  
迁移的下一步取决于你的项目需求：  
  
-   若要自定义 MySQL 架构与 SQL Server 数据库和架构之间的映射，请参阅[将 Mysql 数据库映射到 SQL Server 架构 &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md)  
  
-   若要自定义项目的配置选项，请参阅[设置项目选项 &#40;MySQLToSQL&#41;](../../ssma/mysql/setting-project-options-mysqltosql.md)  
  
-   若要自定义源和目标数据类型的映射，请参阅[&#40;MySQLToSQL 映射 MySQL 和 SQL Server 数据类型&#41;](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md)  
  
-   如果不需要执行这些任务中的任何一种，可以将 MySQL 数据库对象定义转换为 SQL Server 对象定义。 有关详细信息，请参阅将[MySQL 数据库转换 &#40;MySQLToSQL&#41;](../../ssma/mysql/converting-mysql-databases-mysqltosql.md)  
  
## <a name="see-also"></a>另请参阅  
[将 MySQL 数据库迁移到 SQL Server-Azure SQL 数据库 &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
