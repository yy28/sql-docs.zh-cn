---
title: 连接到 SQL Server (AccessToSQL) |Microsoft 文档
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-access
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
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
caps.latest.revision: 24
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 572c516cfac93f3122814cdc93a3eed4f2b9c291
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
# <a name="connecting-to-sql-server-accesstosql"></a>连接到 SQL Server (AccessToSQL)
若要访问将数据库迁移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，你必须连接到的目标实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 SSMA 连接时，获取有关中的实例的数据库的元数据[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]并显示在数据库元数据[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]元数据资源管理器。 SSMA 存储的哪个实例有关的信息[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]你连接到，但不会存储密码。  
  
与 SQL 服务器的连接将保持活动状态，直到关闭该项目。 当你重新打开项目时，你必须重新连接到 SQL Server 中，如果你想与服务器的活动连接。 加载到 SQL Server 数据库对象并迁移数据之前，你可以脱机工作。  
  
有关 SQL Server 实例的元数据将不自动同步。 相反，若要更新 SQL 服务器元数据资源管理器中的元数据，你必须手动更新 SQL Server 元数据。 有关详细信息，请参阅本主题后面的"同步 SQL 服务器元数据"部分。  
  
## <a name="required-sql-server-permissions"></a>所需的 SQL Server 权限  
用于连接到的帐户[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]需要不同的权限，具体取决于该帐户通过执行的操作。  
  
-   要转换到的访问对象[!INCLUDE[tsql](../../includes/tsql_md.md)]语法，刷新从元数据[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，若要将已转换的语法保存到脚本中，帐户必须有权登录到的实例或[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
-   若要加载到的数据库对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]和将数据迁移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，最小权限要求是中的成员身份**db_owner**目标数据库中的数据库角色。  
  
## <a name="establishing-a-sql-server-connection"></a>建立 SQL Server 连接  
在转换到的访问数据库对象之前[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]语法，必须建立连接到的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]想要迁移的 Access 数据库。  
  
在定义的连接属性时，你还指定对象和数据将迁移的数据库。 连接到后，你可以自定义数据库级别的访问的文件的此映射[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 有关详细信息，请参阅[映射源和目标数据库](http://msdn.microsoft.com/en-us/69bee937-7b2c-49ee-8866-7518c683fad4)  
  
> [!IMPORTANT]  
> 连接到之前[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，请确保实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]正在运行并且可以接受连接。 有关详细信息，请参阅"连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据库引擎"在[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]联机丛书。  
  
**若要连接到 SQL Server**  
  
1.  上**文件**菜单上，选择**连接到 SQL Server**。  
  
    如果你以前连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，命令名称将**重新连接到 SQL Server**。  
  
2.  在**服务器名称**框中，输入或选择的实例的名称[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
    -   如果你要连接到本地计算机上的默认实例，则可以输入**localhost**或句点 (**。**)。  
  
    -   如果你要连接到另一台计算机上的默认实例，输入的计算机的名称。  
  
    -   如果你要连接到命名实例，输入计算机名称、 反斜杠和实例名称。 例如： MyServer\MyInstance。  
  
    -   若要连接到的活动用户实例[!INCLUDE[ssExpress](../../includes/ssexpress_md.md)]，使用命名管道连接协议和指定的管道名称，例如\\ \\.\pipe\sql\query。 有关详细信息，请参阅 [!INCLUDE[ssExpress](../../includes/ssexpress_md.md)] 文档。  
  
3.  如果你的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]配置为接受非默认端口上的连接，请输入端口号用于[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]中的连接**服务器端口**框。 对于默认实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，默认端口号为 1433年。 对于命名实例，SSMA 将尝试获取中的端口号[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]浏览器服务。  
  
4.  在**数据库**框中，输入对象和数据迁移的目标数据库的名称。  
  
    此选项不可用，当重新连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
    目标数据库名称不能包含空格或特殊字符。 例如，你可以访问将数据库迁移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]名为"abc"的数据库。 但你无法迁移到 Access 数据库[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据库名为"b c"。  
  
    连接后，你可以自定义每个数据库的此映射。 有关详细信息，请参阅[映射源和目标数据库](http://msdn.microsoft.com/en-us/69bee937-7b2c-49ee-8866-7518c683fad4)  
  
5.  在**身份验证**下拉菜单中，选择要用于连接的身份验证类型。 若要使用当前的 Windows 帐户，请选择**Windows 身份验证**。 若要使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]登录名选择**SQL Server 身份验证**，然后提供用户名和密码。  
  
6.  对于安全的连接，将添加两个控件，**加密连接**复选框和**TrustServerCertificate**复选框。 仅当**加密连接**复选框已选中**TrustServerCertificate**复选框是可见。 当**加密连接**是 checked(true) 和**TrustServerCertificate** unchecked(false)，将验证 SQL Server SSL 证书。 验证服务器证书是 SSL 握手过程的一部分，这可确保服务器是要连接到的正确服务器。 若要确保这一点，必须在客户端上以及在服务器端中安装证书。  
  
7.  单击 **“连接”**。  
  
**更高版本兼容性**  
  
它允许连接/重新连接到的 SQL Server 的更高版本。  
  
1.  你将能够连接到 SQL Server 2008 或 SQL Server 2012，SQL Server 2005 创建的项目时。  
  
2.  你将能够连接到 SQL Server 2012，如果创建的项目为 SQL Server 2008，但它不允许连接到较低版本即 SQL Server 2005。  
  
3.  你将能够连接到仅 SQL Server 2012，SQL Server 2012 创建的项目时。  
  
4.  更高版本兼容性不是有效的 SQL Azure。  
  
||||||||
|-|-|-|-|-|-|-|
|**项目类型与目标服务器版本**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005 (版本： 9.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008 (版本： 10.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012 (Version:11.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014 (Version:12.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2016 (Version:13.x)|SQL Azure|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005|是|用户帐户控制|用户帐户控制|用户帐户控制|是||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008||是|用户帐户控制|用户帐户控制|是||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012|||是|用户帐户控制|是||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014||||是|是||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2016|||||是||
|SQL Azure||||||是|
  
> [!IMPORTANT]  
> 根据项目类型，但根据连接到 SQL Server 的版本不会执行的数据库对象的转换。 如果 SQL Server 2005 项目转换会执行根据 SQL Server 2005 即使你已连接到更高版本的 SQL Server (SQL Server 2008/SQL Server 2012/SQL Server 2014/SQL Server 2016)。  
  
## <a name="synchronizing-sql-server-metadata"></a>SQL Server 元数据同步  
如果[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]架构更改连接后，你可以与服务器同步元数据。  
  
**若要将 SQL Server 元数据同步**  
  
-   在[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]元数据资源管理器，右键单击**数据库**，然后选择**与数据库的同步**。  
  
## <a name="reconnecting-to-sql-server"></a>重新连接到 SQL Server  
与连接[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]将保持活动状态，直到关闭该项目。 当你重新打开项目时，你必须重新连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]如果想与服务器的活动连接。 您可以离线工作之前加载到的数据库对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]并迁移数据。  
  
重新连接到的过程[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]建立的连接的过程相同。  
  
## <a name="next-steps"></a>后续步骤  
如果你想要自定义数据库源和目标数据库之间的映射，请参阅[映射源和目标数据库](http://msdn.microsoft.com/en-us/69bee937-7b2c-49ee-8866-7518c683fad4)否则下, 一步是将转换到的数据库对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]语法使用[转换数据库对象](http://msdn.microsoft.com/en-us/e0ef67bf-80a6-4e6c-a82d-5d46e0623c6c)  
  
## <a name="see-also"></a>另请参阅  
[将访问数据库迁移到 SQL Server](http://msdn.microsoft.com/en-us/76a3abcf-2998-4712-9490-fe8d872c89ca)  
  
