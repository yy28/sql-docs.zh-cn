---
title: SQL Server 2014 Express LocalDB |Microsoft Docs
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- user instances
- LocalDB, described
- local database runtime
- file database
- LocalDB
ms.assetid: 5a641a46-7cfb-4d7b-a90d-6e4625719d74
caps.latest.revision: 30
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: d87a85927751b12e3f86d5ce2bc908da9d063b21
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37243247"
---
# <a name="sql-server-2014-express-localdb"></a>SQL Server 2014 Express LocalDB
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssExpCurrent](../../includes/ssexpcurrent-md.md)] `LocalDB` 是的执行模式[!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]面向程序开发人员。 `LocalDB` 安装将复制启动所需的文件的最小集[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]。 一次`LocalDB`是安装了，开发人员通过使用特殊的连接字符串中启动的连接。 在连接时，所需[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]基础结构会自动创建并启动，使应用程序以使用无需复杂或耗时的配置任务的数据库。 开发人员工具可以向开发人员提供 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] ，使其不必管理 [!INCLUDE[tsql](../../includes/tsql-md.md)] 的完整服务器实例即可撰写和测试 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代码。 实例[!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]`LocalDB`由使用`SqlLocalDB.exe`实用程序。 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]`LocalDB` 应使用来代替[!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]用户实例功能已弃用。  
  
## <a name="installing-localdb"></a>安装 LocalDB  
 安装的主要方法`LocalDB`是使用 SqlLocalDB.msi 程序。 `LocalDB` 安装的任何 SKU 时，是一个选项[!INCLUDE[ssExpCurrent](../../includes/ssexpcurrent-md.md)]。 选择`LocalDB`上**功能选择**安装过程中的页[!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]。 可以有只能安装一个`LocalDB`对于每个主要的二进制文件[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]版本。 可以启动多个 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 进程，并且这些进程都将使用相同的二进制文件。 实例[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]作为启动`LocalDB`具有相同的限制 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]  
  
## <a name="description"></a>Description  
 `LocalDB`安装程序使用 SqlLocalDB.msi 程序安装在计算机上的所需文件。 安装后，`LocalDB`的实例[!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]可以创建和打开[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库。 数据库的系统数据库文件存储于用户本地 AppData 路径中，这个路径通常是隐藏的。 例如 **C:\Users\\<user\>\AppData\Local\Microsoft\Microsoft SQL Server Local DB\Instances\LocalDBApp1\\**。 用户数据库文件存储在用户指定的位置，通常为 **C:\Users\\<user\>\Documents\\** 文件夹中的某个位置。  
  
 有关详细信息，包括有关`LocalDB`在应用程序，请参阅[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]文档[本地数据概述](http://msdn.microsoft.com/library/ms233817\(VS.110\).aspx)，[演练： 创建 SQL Server LocalDB 数据库](http://msdn.microsoft.com/library/ms233763\(VS.110\).aspx)，和[演练： 连接到 SQL Server LocalDB 数据库 （Windows 窗体） 中的数据](http://msdn.microsoft.com/library/ms171890\(VS.110\).aspx)。  
  
 有关详细信息`LocalDB`API，请参阅[SQL Server Express LocalDB 实例 API 参考](http://msdn.microsoft.com/library/hh234692\(SQL.110\).aspx)并[LocalDBStartInstance 函数](http://msdn.microsoft.com/library/hh217143\(SQL.110\).aspx)。  
  
 SqlLocalDb 实用工具可以创建的新实例`LocalDB`，启动和停止的实例`LocalDB`，并包括选项来帮助你管理`LocalDB`。  有关 SqlLocalDb 实用工具的详细信息，请参阅 [SqlLocalDB 实用工具](../../tools/sqllocaldb-utility.md)。  
  
 实例排序规则`LocalDB`被设置为 SQL_Latin1_General_CP1_CI_AS 且不能更改。 一般支持数据库级、列级和表达式级排序规则。 包含数据库遵循 [Contained Database Collations](../../relational-databases/databases/contained-database-collations.md)所定义的元数据和 tempdb 排序规则。  
  
### <a name="restrictions"></a>限制  
 `LocalDB` 不能为合并复制订阅服务器。  
  
 `LocalDB` 不支持 FILESTREAM。  
  
 `LocalDB` 仅允许 Service broker 的本地队列。  
  
 实例`LocalDB`拥有的内置帐户，例如 NT AUTHORITY\SYSTEM 可以具有可管理性问题由于 windows 文件系统重定向;改用常规 windows 帐户作为所有者。  
  
### <a name="automatic-and-named-instances"></a>自动实例和命名实例  
 `LocalDB` 支持两种类型的实例： 自动实例和命名的实例。  
  
-   自动实例`LocalDB`是公共的。 系统自动为用户创建和管理此类实例，并可由任何应用程序使用。 一个自动实例`LocalDB`存在的每一版本`LocalDB`用户的计算机上安装。 自动实例`LocalDB`提供无缝的实例管理。 无需创建实例；它可以自动执行工作。 这使得应用程序可以轻松地安装和迁移到另一台计算机。 如果目标计算机上存在指定的版本的`LocalDB`安装的自动实例`LocalDB`该版本为目标计算机也可用。 自动实例`LocalDB`具有属于保留命名空间的实例名称的特殊模式。 这可以防止名称冲突的命名实例，并用`LocalDB`。 自动实例的名称为 **MSSQLLocalDB**。  
  
-   命名实例`LocalDB`是私有的。 这些命名实例由负责创建和管理该实例的单个应用程序所拥有。 命名实例提供与其他实例的隔离，并可以通过减少与其他数据库用户的资源争用来提高性能。 命名的实例必须由用户通过显式创建`LocalDB`管理 API 或隐式通过 app.config 文件的托管应用程序 （尽管托管应用程序也会使用此 API，如果需要）。 每个命名的实例`LocalDB`都有一个关联`LocalDB`指向各自的集的版本`LocalDB`二进制文件。 实例名称`LocalDB`是`sysname`数据类型并且可具有最多为 128 个字符。 （这不同于常规的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 命名实例，此类命名实例将名称限制为 16 个 ASCII 字符的常规 NetBIOS 名称。）实例的名称`LocalDB`可以包含在文件名内合法的任何 Unicode 字符。  使用自动实例名称的命名实例将成为自动实例。  
  
 不同的计算机用户可具有同名的实例。 每个实例都是以不同的用户身份运行的不同的进程。  
  
## <a name="shared-instances-of-localdb"></a>LocalDB 的共享实例  
 若要支持多个用户的计算机需要连接到的单个实例的方案`LocalDB`，`LocalDB`支持实例共享。 实例所有者可以选择允许计算机上的其他用户连接到其实例。 同时自动实例和命名实例的`LocalDB`可以共享。 若要共享的实例`LocalDB`用户选择该共享的名称 （别名）。 因为该共享名称对于该计算机的所有用户都是可见的，则此共享名称在计算机上必须唯一。 实例的共享的名称`LocalDB`具有相同的格式为命名实例的`LocalDB`。  
  
 只有在计算机上的管理员可以创建的共享的实例`LocalDB`。 共享的实例`LocalDB`可以是由管理员或由共享实例的所有者取消共享`LocalDB`。 若要共享的且不共享的实例`LocalDB`，使用`LocalDBShareInstance`和`LocalDBUnShareInstance`方法的`LocalDB`API，或共享和取消共享的选项 SqlLocalDb 实用工具。  
  
## <a name="starting-localdb-and-connecting-to-localdb"></a>启动 LocalDB 和连接到 LocalDB  
  
### <a name="connecting-to-the-automatic-instance"></a>连接到自动实例  
 若要使用的最简单方法`LocalDB`是连接到由当前用户拥有使用连接字符串的自动实例 **"Server = (localdb) \MSSQLLocalDB;Integrated Security = true"**。 若要使用文件名连接到特定数据库，则使用类似于 **"Server=(LocalDB)\MSSQLLocalDB; Integrated Security=true ;AttachDbFileName=D:\Data\MyDB1.mdf"** 的连接字符串进行连接。  
  
> [!NOTE]  
>  首次在计算机上的用户尝试连接到`LocalDB`，必须将同时创建并启动该自动实例。 创建实例所用的额外时间可能会导致连接尝试失败并且具有超时消息。 在发生此情况时，等待几秒钟以便让创建过程完成，然后再次连接。  
  
### <a name="creating-and-connecting-to-a-named-instances"></a>创建和连接到命名实例  
 除了自动实例`LocalDB`还支持命名实例。 使用 SqlLocalDB.exe 程序来创建、 启动和停止的命名的实例`LocalDB`。 有关 SqlLocalDB.exe 的详细信息，请参阅 [SqlLocalDB 实用工具](../../tools/sqllocaldb-utility.md)。  
  
```ms-dos  
REM Create an instance of LocalDB  
"C:\Program Files\Microsoft SQL Server\120\Tools\Binn\SqlLocalDB.exe" create LocalDBApp1  
REM Start the instance of LocalDB  
"C:\Program Files\Microsoft SQL Server\120\Tools\Binn\SqlLocalDB.exe" start LocalDBApp1  
REM Gather information about the instance of LocalDB  
"C:\Program Files\Microsoft SQL Server\120\Tools\Binn\SqlLocalDB.exe" info LocalDBApp1  
```  
  
 上面的最后一行将返回如下信息。  
  
|||  
|-|-|  
|“属性”|"LocalDBApp1"|  
|版本|\<当前版本>|  
|共享名称|""|  
|“所有者”|"\<你的 Windows 用户>"|  
|自动创建|“否”|  
|State|运行|  
|上次启动时间|\<日期和时间>|  
|实例管道名称|np:\\\\.\pipe\LOCALDB#F365A78E\tsql\query|  
  
> [!NOTE]  
>  如果应用程序使用.NET 4.0.2 的版本，必须直接连接到的命名管道`LocalDB`。 实例管道名称值是命名管道的实例`LocalDB`上侦听。 实例管道名称后 LOCALDB # 将更改每个部分的时间的实例`LocalDB`已启动。 若要连接到的实例`LocalDB`通过使用[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，键入实例管道名称**服务器名称**框**连接到[!INCLUDE[ssDE](../../includes/ssde-md.md)]** 对话框。 可以从自定义程序建立连接到的实例`LocalDB`使用类似于连接字符串 `SqlConnection conn = new SqlConnection(@"Server=np:\\.\pipe\LOCALDB#F365A78E\tsql\query");`  
  
### <a name="connecting-to-a-shared-instance-of-localdb"></a>连接到 LocalDB 的共享实例  
 若要连接到的共享实例`LocalDB`添加 **。\\** （句点 + 反斜杠） 到连接字符串以便引用为共享实例保留的命名空间。 例如，若要连接到的共享实例`LocalDB`名为`AppData`使用的连接字符串，如`(localdb)\.\AppData`作为连接字符串的一部分。 连接到的共享实例的用户`LocalDB`它们尚未拥有必须具有 Windows 身份验证或[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]身份验证登录名。  
  
## <a name="troubleshooting"></a>故障排除  
 有关故障排除信息`LocalDB`，请参阅[故障排除 SQL Server 2012 Express LocalDB](http://social.technet.microsoft.com/wiki/contents/articles/4609.aspx)。  
  
## <a name="permissions"></a>权限  
 实例[!INCLUDE[ssExpCurrent](../../includes/ssexpcurrent-md.md)]`LocalDB`是其使用的用户创建的实例。 在计算机上的任何用户可以使用创建数据库的实例`LocalDB`、 其用户配置文件下存储文件并运行其凭据进程。 默认情况下，访问到的实例`LocalDB`仅限于其所有者。 中包含的数据`LocalDB`受到对数据库文件的文件系统访问。 如果用户数据库文件存储于某一共享位置，可以使用的实例打开具有到该位置的文件系统访问权限的任何人都数据库`LocalDB`他们拥有。 如果数据库文件处于某一受保护的位置，例如用户数据文件夹，则只有该用户以及有权访问该文件夹的任何管理员才能打开该数据库。 `LocalDB`文件只能打开的一个实例`LocalDB`一次。  
  
> [!NOTE]  
>  `LocalDB` 始终运行的用户安全上下文;也就是说，`LocalDB`从不使用的凭据运行从本地管理员组。 这意味着所有数据库使用的文件`LocalDB`实例必须使用拥有的用户的 Windows 帐户，而无需考虑本地 Administrators 组中的成员身份可以访问。  
  
## <a name="see-also"></a>请参阅  
 [SqlLocalDB 实用工具](../../tools/sqllocaldb-utility.md)  
  
  
