---
title: 正在连接到 SQL Server （AccessToSQL） |Microsoft Docs
description: 了解如何连接到 SQL 数据库的目标实例以迁移 Access 数据库。 SSMA 获取有关 SQL 数据库中的数据库的元数据。
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- authentication
- instance of SQL Server
- metadata, refreshing
- ports
- refreshing metadata
- spaces in database names
- special characters
- SQL Server
- SQL Server, connecting
- SQL Server, connecting to
- SQL Server, reconnecting
ms.assetid: f84cf007-ddf1-4396-a07c-3e0729abc769
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 6266eb0596b351a7ef54baed6a7a76a7a655ac60
ms.sourcegitcommit: 59cda5a481cfdb4268b2744edc341172e53dede4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/02/2020
ms.locfileid: "84293084"
---
# <a name="connecting-to-sql-server-accesstosql"></a>连接到 SQL Server （AccessToSQL）
若要将 Access 数据库迁移到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，你必须连接到的目标实例 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 在连接时，SSMA 将获取实例中的数据库的元数据， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 并在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元数据资源管理器中显示数据库元数据。 SSMA 存储有关您连接到的实例的信息 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，但不存储密码。  
  
到 SQL Server 的连接保持活动状态，直到关闭项目。 重新打开项目时，如果需要与服务器建立活动连接，则必须重新连接到 SQL Server。 在将数据库对象加载到 SQL Server 和迁移数据之前，可以脱机工作。  
  
与 SQL Server 实例有关的元数据不会自动同步。 相反，若要更新 SQL Server 元数据资源管理器中的元数据，必须手动更新 SQL Server 元数据。 有关详细信息，请参阅本主题后面的 "同步 SQL Server 元数据" 一节。  
  
## <a name="required-sql-server-permissions"></a>必需的 SQL Server 权限  
用于连接到的帐户 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 需要不同的权限，具体取决于该帐户执行的操作。  
  
-   若要将 Access 对象转换为 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语法、刷新中的元数据 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或将转换后的语法保存到脚本中，该帐户必须有权登录到的实例 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
-   若要将数据库对象加载到中 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 并且要将数据迁移到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，最低权限要求是目标数据库中**db_owner**数据库角色的成员身份。  
  
## <a name="establishing-a-sql-server-connection"></a>建立 SQL Server 连接  
在将 Access 数据库对象转换为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 语法之前，必须建立与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 要将 access 数据库迁移到的实例的连接。  
  
定义连接属性时，还可以指定要将对象和数据迁移到的数据库。 在连接到之后，可以在访问数据库级别自定义此映射 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 有关详细信息，请参阅[映射源和目标数据库](mapping-source-and-target-databases-accesstosql.md)。  
  
> [!IMPORTANT]  
> 在连接到之前 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，请确保的实例正在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 运行，并且可以接受连接。 有关详细信息，请参阅联机丛书中的 "连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库引擎" [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
**连接到 SQL Server**  
  
1.  在 "**文件**" 菜单上，选择 "**连接到 SQL Server**"。  
  
    如果以前连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，则命令名称将**重新连接到 SQL Server**。  
  
2.  在 "**服务器名称**" 框中，输入或选择实例的名称 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
    -   如果要连接到本地计算机上的默认实例，则可以输入**localhost**或点（**.**）。  
  
    -   如果要连接到另一台计算机上的默认实例，请输入计算机的名称。  
  
    -   如果要连接到命名实例，请输入计算机名称、反斜杠和实例名称。 例如： MyServer\MyInstance。  
  
    -   若要连接到的活动用户实例 [!INCLUDE[ssExpress](../../includes/ssexpress_md.md)] ，请使用 named pipes 协议进行连接，并指定管道名称，如 \\ \\ .\pipe\sql\query。 有关详细信息，请参阅 [!INCLUDE[ssExpress](../../includes/ssexpress_md.md)] 文档。  
  
3.  如果实例 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置为接受非默认端口上的连接，请 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在 "**服务器端口**" 框中输入用于连接的端口号。 对于的默认实例 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，默认端口号为1433。 对于命名实例，SSMA 将尝试从 Browser 服务获取端口号 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
4.  在 "**数据库**" 框中，输入用于对象和数据迁移的目标数据库的名称。  
  
    当重新连接到时，此选项不可用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
    目标数据库名称不能包含空格或特殊字符。 例如，可以将 Access 数据库迁移到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 名为 "abc" 的数据库。 但不能将 Access 数据库迁移到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 名为 "a b c" 的数据库。  
  
    连接后，可以为每个数据库自定义此映射。 有关详细信息，请参阅[映射源和目标数据库](mapping-source-and-target-databases-accesstosql.md)  
  
5.  在 "**身份验证**" 下拉菜单中，选择要用于连接的身份验证类型。 若要使用当前的 Windows 帐户，请选择 " **Windows 身份验证**"。 若要使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名，请选择 " **SQL Server 身份验证**"，然后提供用户名和密码。  
  
6.  对于安全连接，将添加两个控件： "**加密连接**" 复选框和 " **TrustServerCertificate** " 复选框。 仅当 "**加密连接**" 复选框处于选中状态时**TrustServerCertificate**复选框可见。 选中 "**加密连接**" （true）并取消选中**TrustServerCertificate** （false）后，将验证 SQL Server SSL 证书。 验证服务器证书是 SSL 握手过程的一部分，这可确保服务器是要连接到的正确服务器。 为了确保这一点，证书必须安装在客户端和服务器端。  
  
7.  单击“连接”。  
  
**更高版本兼容性**  
  
允许连接/重新连接到 SQL Server 的更高版本。  
  
1.  当创建的项目 SQL Server 2005 时，你将能够连接到 SQL Server 2008 或 SQL Server 2012。  
  
2.  如果创建的项目为 SQL Server 2008，则可以连接到 SQL Server 2012，但不允许将其连接到更低的版本，即 SQL Server 2005。  
  
3.  如果创建的项目 SQL Server 2012，你将只能连接到 SQL Server 2012。  
  
4.  版本兼容性对于 SQL Azure 无效。  
  
||||||||
|-|-|-|-|-|-|-|
|**项目类型 Vs 目标服务器版本**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2005（版本：1.x）|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2008（版本：8.x）|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2012（版本： 11. x）|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014（版本： 12. x）|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2016（版本： 13. x）|SQL Azure|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005|是|是|是|是|是||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008||是|是|是|是||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012|||是|是|是||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014||||是|是||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016|||||是||
|SQL Azure||||||是|
  
> [!IMPORTANT]  
> 数据库对象的转换是根据项目类型执行的，而不是按连接到的 SQL Server 版本来执行的。 在 SQL Server 2005 项目的情况下，即使你连接到 SQL Server 的更高版本（SQL Server 2008/SQL Server 2012/SQL Server 2014/SQL Server 2016），也会按 SQL Server 2005 执行转换。  
  
## <a name="synchronizing-sql-server-metadata"></a>同步 SQL Server 元数据  
如果在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 连接后架构发生更改，则可以将元数据与服务器同步。  
  
**同步 SQL Server 元数据**  
  
-   在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元数据资源管理器中，右键单击 "**数据库**"，然后选择 "**与数据库同步**"。  
  
## <a name="reconnecting-to-sql-server"></a>正在重新连接到 SQL Server  
你的连接将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 保持活动状态，直到你关闭项目。 重新打开项目时， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 如果想要与服务器建立活动连接，则必须重新连接到。 在将数据库对象加载到和迁移数据之前，可以脱机工作 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
重新连接到的过程与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 建立连接的过程相同。  
  
## <a name="next-steps"></a>后续步骤  
如果要自定义源和目标数据库之间的映射，请参阅[映射源和目标数据库](mapping-source-and-target-databases-accesstosql.md); 否则，下一步是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用[转换数据库对象](converting-access-database-objects-accesstosql.md)将数据库对象转换为语法  
  
## <a name="see-also"></a>另请参阅  
[将 Access 数据库迁移到 SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
