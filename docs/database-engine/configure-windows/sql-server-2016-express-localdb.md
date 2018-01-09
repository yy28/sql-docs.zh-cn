---
title: SQL Server 2016 Express LocalDB | Microsoft Docs
ms.custom: 
ms.date: 08/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: configure-windows
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- user instances
- LocalDB, described
- local database runtime
- file database
- LocalDB
ms.assetid: 5a641a46-7cfb-4d7b-a90d-6e4625719d74
caps.latest.revision: "42"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 8e9500bdeffd9c7e9e9480f30a87e1678074cc57
ms.sourcegitcommit: 6e016a4ffd28b09456008f40ff88aef3d911c7ba
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2017
---
# <a name="sql-server-2016-express-localdb"></a>SQL Server 2016 Express LocalDB
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
 > 有关与以前版本的 SQL Server 相关的内容，请参阅 [SQL Server 2014 Express LocalDB](https://msdn.microsoft.com/en-US/library/hh510202(SQL.120).aspx)。

Microsoft SQL Server 2016 Express **LocalDB** 是一种面向开发人员的 [SQL Server Express](https://msdn.microsoft.com/library/ms144275(SQL.130).aspx) 功能。 它在具有高级服务的 SQL Server 2016 Express 上可用。  

 **LocalDB** 安装将复制启动 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]所需的最少的文件集。 安装 LocalDB 后，你可以使用特定连接字符串来启动连接。 连接时，将自动创建并启动所需的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 基础结构，从而使应用程序无需执行复杂的配置任务即可使用数据库。 开发人员工具可以向开发人员提供 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] ，使其不必管理 [!INCLUDE[tsql](../../includes/tsql-md.md)] 的完整服务器实例即可撰写和测试 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代码。 
 
 
 ## <a name="try-it-out"></a>进行试用： 
  
-   若要下载并安装 SQL Server 2016 Express，请转到 [SQL Server 下载](https://www.microsoft.com/en-us/sql-server/sql-server-downloads)。 LocalDB 是在安装过程中选择的一项功能，可在下载该媒体时使用。 如果下载媒体，则选择“Express Advanced”或“LocalDB”包。 
  
-   是否拥有 Azure 帐户？  然后转到 **[此处](https://azure.microsoft.com/en-us/services/virtual-machines/sql-server/)** ，以加速已安装有 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 的虚拟机。  
  
## <a name="install-localdb"></a>安装 LocalDB  
 通过安装向导或使用 SqlLocalDB.msi 程序安装 **LocalDB** 。 **LocalDB** 是安装 [!INCLUDE[ssExpCurrent](../../includes/ssexpcurrent-md.md)] 时的一个选项。 
 
在安装过程中，在“功能选择/共享功能”页上选择 **LocalDB**。 对于每个主要 **版本，只能存在** LocalDB [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 二进制文件的一个安装。 可以启动多个 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 进程，并且这些进程都将使用相同的二进制文件。 作为 LocalDB 启动的 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 实例与 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 具有相同的限制。  

 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] **LocalDB** 的实例通过 **SqlLocalDB.exe** 实用工具进行托管。 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] **LocalDB** 应该用于代替已弃用的 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 用户实例功能。 
  
## <a name="description"></a>Description  
 **LocalDB** 安装程序使用 SqlLocalDB.msi 程序在计算机上安装所需文件。 安装后， **LocalDB** 是可以创建和打开 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 数据库的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。 数据库的系统数据库文件存储于用户本地 AppData 路径中，这个路径通常是隐藏的。 例如 **C:\Users\\<user\>\AppData\Local\Microsoft\Microsoft SQL Server Local DB\Instances\LocalDBApp1\\**。 用户数据库文件存储在用户指定的位置，通常为 **C:\Users\\<user\>\Documents\\** 文件夹中的某个位置。  
  
 有关在应用程序中包含 **LocalDB** 的详细信息，请参阅 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 文档[本地数据概述](http://msdn.microsoft.com/library/ms233817\(VS.110\).aspx)、[演练：创建 SQL Server LocalDB 数据库](http://msdn.microsoft.com/library/ms233763\(VS.110\).aspx)和[演练：连接到 SQL Server LocalDB 数据库中的数据（Windows 窗体）](http://msdn.microsoft.com/library/ms171890\(VS.110\).aspx)。  
  
 有关 **LocalDB** API 的详细信息，请参阅 [SQL Server Express LocalDB 实例 API 参考](http://msdn.microsoft.com/library/hh234692\(SQL.110\).aspx) 和 [LocalDBStartInstance 函数](http://msdn.microsoft.com/library/hh217143\(SQL.110\).aspx)。  
  
 SqlLocalDb 实用工具可以创建 **LocalDB**的新实例，启动和停止 **LocalDB**的实例，并且包含可帮助你管理 **LocalDB**的选项。  有关 SqlLocalDb 实用工具的详细信息，请参阅 [SqlLocalDB 实用工具](../../tools/sqllocaldb-utility.md)。  
  
 将 **LocalDB** 的实例排序规则设置为 SQL_Latin1_General_CP1_CI_AS，并且不能更改它。 通常支持数据库级、列级和表达式级排序规则。 包含数据库遵循 [Contained Database Collations](../../relational-databases/databases/contained-database-collations.md)所定义的元数据和 tempdb 排序规则。  
  
### <a name="restrictions"></a>限制  
 **LocalDB** 不能是合并复制订阅服务器。  
  
 **LocalDB** 不支持 FILESTREAM。  
  
 **LocalDB** 仅允许 Service Broker 的本地队列。  
  
 由于 Windows 文件系统重定向，NT AUTHORITY\SYSTEM 等内置帐户拥有的 **LocalDB** 的一个实例可能具有管理性问题；请改用常规 Windows 帐户作为所有者。  
  
### <a name="automatic-and-named-instances"></a>自动实例和命名实例  
 **LocalDB** 支持两种类型的实例：自动实例和命名实例。  
  
-   **LocalDB** 的自动实例是公共的。 系统自动为用户创建和管理此类实例，并可由任何应用程序使用。 安装在用户计算机上的每个 **LocalDB** 版本都存在一个自动 **LocalDB** 实例。 自动 **LocalDB** 实例提供无缝的实例管理。 无需创建实例；它可以自动执行工作。 这使得应用程序可以轻松地安装和迁移到另一台计算机。 如果目标计算机已安装指定版本的 **LocalDB** ，则目标计算机也提供此版本的自动 **LocalDB** 实例。 自动 **LocalDB** 实例具有属于保留命名空间的特殊实例名称模式。 这可以防止名称与 **LocalDB**的命名实例发生冲突。 自动实例的名称为 **MSSQLLocalDB**。  
  
-   **LocalDB** 的命名实例是专用的。 这些命名实例由负责创建和管理该实例的单个应用程序所拥有。 命名实例提供与其他实例的隔离，并可以通过减少与其他数据库用户的资源争用来提高性能。 命名实例必须由用户通过 **LocalDB** 管理 API 显式创建，或者通过托管应用程序的 app.config 文件隐式创建（尽管托管应用程序也会在需要时使用 API）。 **LocalDB** 的每个命名实例都具有关联的 **LocalDB** 版本，指向相应的 **LocalDB** 二进制文件集。 **LocalDB** 的命名实例为 **sysname** 数据类型并且可具有最多 128 个字符。 （这不同于常规的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 命名实例，此类命名实例将名称限制为 16 个 ASCII 字符的常规 NetBIOS 名称。）**LocalDB** 实例名称可包含在文件名内合法的任何 Unicode 字符。  使用自动实例名称的命名实例将成为自动实例。  
  
 不同的计算机用户可具有同名的实例。 每个实例都是以不同的用户身份运行的不同的进程。  
  
## <a name="shared-instances-of-localdb"></a>LocalDB 的共享实例  
 为了支持多个计算机用户需要连接到单个 **LocalDB**实例的方案， **LocalDB** 支持实例共享。 实例所有者可以选择允许计算机上的其他用户连接到其实例。 **LocalDB** 的自动实例和命名实例都可以共享。 若要共享 **LocalDB** 的某个实例，用户需要为其选择一个共享名称（别名）。 因为该共享名称对于该计算机的所有用户都是可见的，则此共享名称在计算机上必须唯一。 **LocalDB** 实例的共享名称具有与 **LocalDB**的命名实例相同的格式。  
  
 只有计算机上的管理员才能创建 **LocalDB**的共享实例。 **LocalDB** 的共享实例可由管理员或 **LocalDB**共享实例的所有者取消共享。 若要共享和取消共享某一 **LocalDB**实例，请使用 `LocalDBShareInstance` LocalDB `LocalDBUnShareInstance` API 的 **和** 方法，或者使用 SqlLocalDb 实用工具的共享和取消共享选项。  
  
## <a name="starting-localdb-and-connecting-to-localdb"></a>启动 LocalDB 和连接到 LocalDB  
  
### <a name="connecting-to-the-automatic-instance"></a>连接到自动实例  
 使用 **LocalDB** 的最简单方法是通过使用连接字符串 **"Server=(localdb)\MSSQLLocalDB;Integrated Security=true"**连接到当前用户拥有的自动实例。 若要使用文件名连接到特定数据库，则使用类似于 **"Server=(LocalDB)\MSSQLLocalDB; Integrated Security=true ;AttachDbFileName=D:\Data\MyDB1.mdf"**的连接字符串进行连接。  
  
> [!NOTE]  
>  在计算机上的用户首次尝试连接到 **LocalDB**时，必须创建并启动该自动实例。 创建实例所用的额外时间可能会导致连接尝试失败并且具有超时消息。 在发生此情况时，等待几秒钟以便让创建过程完成，然后再次连接。  
  
### <a name="creating-and-connecting-to-a-named-instances"></a>创建和连接到命名实例  
 除了自动实例之外， **LocalDB** 还支持命名实例。 使用 SqlLocalDB.exe 程序可以创建、启动和停止 **LocalDB**的命名实例。 有关 SqlLocalDB.exe 的详细信息，请参阅 [SqlLocalDB 实用工具](../../tools/sqllocaldb-utility.md)。  
  
```ms-dos  
REM Create an instance of LocalDB  
"C:\Program Files\Microsoft SQL Server\130\Tools\Binn\SqlLocalDB.exe" create LocalDBApp1  
REM Start the instance of LocalDB  
"C:\Program Files\Microsoft SQL Server\130\Tools\Binn\SqlLocalDB.exe" start LocalDBApp1  
REM Gather information about the instance of LocalDB  
"C:\Program Files\Microsoft SQL Server\130\Tools\Binn\SqlLocalDB.exe" info LocalDBApp1  
```  
  
 上面的最后一行将返回如下信息。  
  
|||  
|-|-|  
|“属性”|"LocalDBApp1"|  
|版本|\<当前版本>|  
|共享名称|""|  
|“所有者”|"\<你的 Windows 用户>"|  
|自动创建|是|  
|State|运行|  
|上次启动时间|\<日期和时间>|  
|实例管道名称|np:\\\\.\pipe\LOCALDB#F365A78E\tsql\query|  
  
> [!NOTE]  
>  如果您的应用程序使用早于 .NET 4.0.2 的版本，您必须直接连接到 **LocalDB**的命名管道。 实例管道名称值为 **LocalDB** 的实例正在侦听的命名管道。 LOCALDB# 之后的实例管道名称部分将在每次启动 **LocalDB** 实例时更改。 若要通过使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 连接到 **LocalDB** 实例，请在“连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]”对话框的“服务器名称”框中键入实例管道名称。 从您的自定义程序，您可以通过使用类似于 **LocalDB** LocalDB `SqlConnection conn = new SqlConnection(@"Server=np:\\.\pipe\LOCALDB#F365A78E\tsql\query");`  
  
### <a name="connecting-to-a-shared-instance-of-localdb"></a>连接到 LocalDB 的共享实例  
 若要连接到某一 LocalDB 共享实例，请将“.\\”（句点 + 反斜杠）添加到连接字符串以便引用为共享实例保留的命名空间。 例如，若要连接到名为 **的** LocalDB `AppData` 的共享实例，可使用连接字符串（例如 `(localdb)\.\AppData` ）作为连接字符串的一部分。 连接到用户不拥有的 **LocalDB** 共享实例的用户必须具有 Windows 身份验证或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证登录名。  
  
## <a name="troubleshooting"></a>故障排除  
 有关排除 **LocalDB**问题的信息，请参阅 [排除 SQL Server 2012 Express LocalDB 问题](http://social.technet.microsoft.com/wiki/contents/articles/4609.aspx)。  
  
## <a name="permissions"></a>权限  
 由于 Windows 文件系统重定向，NT AUTHORITY\SYSTEM 等内置帐户拥有的 [!INCLUDE[ssExpCurrent](../../includes/ssexpcurrent-md.md)]**LocalDB** 的实例是用户为其使用而创建的实例。 计算机上的任何用户都可以使用 **LocalDB**实例创建数据库，在用户配置文件下存储文件并使用凭据来运行进程。 默认情况下，对 **LocalDB** 实例的访问仅限于其所有者。 **LocalDB** 中包含的数据受到对数据库文件的文件系统访问的保护。 如果用户数据库文件存储于某一共享位置，则通过使用他们自己拥有的 **LocalDB** 实例对该位置具有文件系统访问权限的任何人都可以打开该数据库。 如果数据库文件处于某一受保护的位置，例如用户数据文件夹，则只有该用户以及有权访问该文件夹的任何管理员才能打开该数据库。 **LocalDB** 文件只能一次通过一个 **LocalDB** 实例来打开。  
  
> [!NOTE]  
>  **LocalDB** 始终在用户安全上下文中运行；即 **LocalDB** 从不使用本地 Administrator 组的凭据来运行。 这意味着 **LocalDB** 实例使用的所有数据库文件必须可以通过拥有的用户的 Windows 帐户来访问，而不必考虑本地 Administrators 组中的成员资格。  
  
## <a name="see-also"></a>另请参阅  
 [SqlLocalDB 实用工具](../../tools/sqllocaldb-utility.md)  
  
  
