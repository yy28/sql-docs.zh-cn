---
title: 连接到 SQL Server (AccessToSQL) |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 0bedb8ba74d7965df34a102fb0d53a0cbdb248dc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63139017"
---
# <a name="connecting-to-sql-server-accesstosql"></a>连接到 SQL Server (AccessToSQL)
将 Access 数据库迁移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，必须连接到的目标实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 SSMA 连接时，获取有关的实例中的数据库的元数据[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，并显示数据库中的元数据[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]元数据资源管理器。 SSMA 存储信息的哪些实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]您连接到，但不存储密码。  
  
与 SQL Server 的连接保持活动状态，直到关闭该项目。 当你重新打开该项目时，你必须重新连接到 SQL Server 中，如果想要的活动连接到服务器。 加载到 SQL Server 数据库对象并将数据迁移之前，您可以脱机工作。  
  
有关 SQL Server 实例的元数据不会自动同步。 相反，若要更新 SQL Server 元数据资源管理器中的元数据，必须手动更新 SQL Server 元数据。 有关详细信息，请参阅本主题后面的"同步 SQL Server 元数据"部分。  
  
## <a name="required-sql-server-permissions"></a>所需的 SQL Server 权限  
用于连接到的帐户[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]需要不同的权限，具体取决于该帐户执行的操作。  
  
-   要转换的对象访问[!INCLUDE[tsql](../../includes/tsql-md.md)]语法中，若要刷新从元数据[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，或将保存到脚本转换后的语法，该帐户必须有权登录到的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
-   若要加载到数据库对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]并将数据迁移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，最小权限要求是中的成员身份**db_owner**目标数据库中的数据库角色。  
  
## <a name="establishing-a-sql-server-connection"></a>建立 SQL Server 连接  
在转换到访问数据库对象之前[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]语法，必须建立的实例的连接[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]想要迁移的 Access 数据库。  
  
在定义的连接属性时，还可以指定对象和数据将迁移的数据库。 连接到后，您可以自定义此映射在访问数据库级别[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 有关详细信息，请参阅[映射源和目标数据库](mapping-source-and-target-databases-accesstosql.md)。  
  
> [!IMPORTANT]  
> 连接到之前[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，请确保实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]正在运行，并且可以接受连接。 有关详细信息，请参阅"连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库引擎"中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]联机丛书。  
  
**若要连接到 SQL Server**  
  
1.  上**文件**菜单中，选择**连接到 SQL Server**。  
  
    如果你以前连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，命令名称将是**重新连接到 SQL Server**。  
  
2.  在中**服务器名称**框中，输入或选择的实例的名称[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
    -   如果要连接到本地计算机上的默认实例，则可以输入**localhost**或句点 ( **。** )。  
  
    -   如果要连接到另一台计算机上的默认实例，输入的计算机的名称。  
  
    -   如果要连接到命名实例，则输入计算机名称、 一个反斜杠和实例名称。 例如：MyServer\MyInstance。  
  
    -   若要连接到的活动用户实例[!INCLUDE[ssExpress](../../includes/ssexpress_md.md)]，使用命名管道连接协议和指定管道名称，例如\\ \\.\pipe\sql\query。 有关详细信息，请参阅[!INCLUDE[ssExpress](../../includes/ssexpress_md.md)]文档。  
  
3.  如果你的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]配置为接受非默认端口上的连接，请输入用于的端口号[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中的连接**服务器端口**框。 对于默认实例的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，默认端口号为 1433年。 对于命名实例，SSMA 会尝试获取端口号从[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]浏览器服务。  
  
4.  在中**数据库**框中，输入对象和数据迁移的目标数据库的名称。  
  
    此选项不可用时重新连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
    目标数据库名称不能包含空格或特殊字符。 例如，你可以迁移到 Access 数据库[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]名为"abc"的数据库。 但无法迁移到 Access 数据库[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库命名为"b c"。  
  
    连接后，可以自定义此映射每个数据库。 有关详细信息，请参阅[映射源和目标数据库](mapping-source-and-target-databases-accesstosql.md)  
  
5.  在中**身份验证**下拉列表菜单中，选择要使用的连接身份验证类型。 若要使用当前 Windows 帐户，请选择**Windows 身份验证**。 若要使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登录名，选择**SQL Server 身份验证**，然后提供用户名和密码。  
  
6.  对于安全的连接，将添加两个控件，**加密连接**复选框并**TrustServerCertificate**复选框。 仅当**加密连接**选中复选框**TrustServerCertificate**复选框是否可见。 当**加密连接**是 checked(true) 和**TrustServerCertificate** unchecked(false)，将验证 SQL Server SSL 证书。 验证服务器证书是 SSL 握手过程的一部分，这可确保服务器是要连接到的正确服务器。 若要确保这一点，必须在客户端和服务器端上安装证书。  
  
7.  单击 **“连接”** 。  
  
**更高版本兼容性**  
  
它允许连接/重新连接到更高版本的 SQL Server。  
  
1.  你将能够连接到 SQL Server 2008 或 SQL Server 2012 时创建的项目是 SQL Server 2005。  
  
2.  你将能够连接到 SQL Server 2012 创建的项目是 SQL Server 2008 不允许连接到较低版本即 SQL Server 2005 时。  
  
3.  你将能够连接到仅 SQL Server 2012 时创建的项目是 SQL Server 2012。  
  
4.  更高版本兼容性不是有效的 SQL Azure。  
  
||||||||
|-|-|-|-|-|-|-|
|**项目类型与目标服务器版本**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 (版本：9.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008 (版本：10.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 (Version:11.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 (Version:12.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 (Version:13.x)|SQL Azure|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005|是|是|是|是|是||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008||是|是|是|是||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012|||是|是|是||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014||||是|是||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016|||||是||
|SQL Azure||||||是|
  
> [!IMPORTANT]  
> 根据项目类型，但根据连接到的 SQL Server 的版本不被执行数据库对象的转换。 对于 SQL Server 2005 项目，转换被执行根据 SQL Server 2005 即使你已连接到更高版本的 SQL Server (SQL Server 2008/SQL Server 2012/SQL Server 2014/SQL Server 2016)。  
  
## <a name="synchronizing-sql-server-metadata"></a>同步 SQL Server 元数据  
如果[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]架构更改连接后，可以与服务器同步元数据。  
  
**若要将 SQL Server 元数据同步**  
  
-   在中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]元数据资源管理器，右键单击**数据库**，然后选择**与数据库同步**。  
  
## <a name="reconnecting-to-sql-server"></a>重新连接到 SQL Server  
与连接[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]保持活动状态，直到关闭该项目。 当你重新打开该项目时，您必须重新连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]如果想要的活动连接到服务器。 您可以脱机处理之前加载到的数据库对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]并将数据迁移。  
  
重新连接到的过程[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]建立连接的过程相同。  
  
## <a name="next-steps"></a>后续步骤  
如果你想要自定义源和目标数据库之间的映射，请参阅[映射源和目标数据库](mapping-source-and-target-databases-accesstosql.md)否则为下一步是将转换到的数据库对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]语法使用[转换数据库对象](converting-access-database-objects-accesstosql.md)  
  
## <a name="see-also"></a>请参阅  
[Access 数据库迁移到 SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
