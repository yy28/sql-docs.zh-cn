---
title: SQL Server 2014 Express LocalDB |Microsoft Docs
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- user instances
- LocalDB, described
- local database runtime
- file database
- LocalDB
ms.assetid: 5a641a46-7cfb-4d7b-a90d-6e4625719d74
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 224facf54b0cde09f97010be472e3cc28754e94b
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "62756986"
---
# <a name="sql-server-2014-express-localdb"></a>SQL Server 2014 Express LocalDB
  [!INCLUDE[msCoName](../../includes/msconame-md.md)]是面向程序开发人员[!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]的执行模式。 [!INCLUDE[ssExpCurrent](../../includes/ssexpcurrent-md.md)] `LocalDB` `LocalDB`安装将复制启动所需的最小文件集[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]。 安装`LocalDB`后，开发人员通过使用特殊的连接字符串来启动连接。 连接时，将自动创建并启动所需的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 基础结构，从而使应用程序无需执行复杂或耗时的配置任务即可使用数据库。 开发人员工具可以向开发人员提供 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] ，使其不必管理 [!INCLUDE[tsql](../../includes/tsql-md.md)] 的完整服务器实例即可撰写和测试 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代码。 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] `LocalDB`使用`SqlLocalDB.exe`实用工具管理的实例。 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]`LocalDB`应该用于代替已弃用的[!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]用户实例功能。  
  
## <a name="installing-localdb"></a>安装 LocalDB  
 主要的安装`LocalDB`方法是使用 SqlLocalDB 程序。 `LocalDB`是安装的[!INCLUDE[ssExpCurrent](../../includes/ssexpcurrent-md.md)]任何 SKU 时的一个选项。 在`LocalDB`的安装过程中，在 "**功能选择**" 页上选择[!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]。 对于每个主`LocalDB` [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]版本，只能有一个二进制文件安装。 可以启动多个 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 进程，并且这些进程都将使用相同的二进制文件。 作为[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]启动的实例与`LocalDB`具有相同的限制[!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]  
  
## <a name="description"></a>说明  
 `LocalDB`安装程序使用 SqlLocalDB 程序在计算机上安装所需的文件。 安装之后， `LocalDB`是可以创建和[!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]打开[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库的实例。 数据库的系统数据库文件存储于用户本地 AppData 路径中，这个路径通常是隐藏的。 例如 **C:\Users\\<user\>\AppData\Local\Microsoft\Microsoft SQL Server Local DB\Instances\LocalDBApp1\\**。 用户数据库文件存储在用户指定的位置，通常为 **C:\Users\\<user\>\Documents\\** 文件夹中的某个位置。  
  
 有关在应用程序中`LocalDB`包括的详细信息，请[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]参阅文档[本地数据概述](https://msdn.microsoft.com/library/ms233817\(VS.110\).aspx)、[演练：创建 SQL Server LocalDB 数据库](https://msdn.microsoft.com/library/ms233763\(VS.110\).aspx)和[演练：连接到 SQL Server LocalDB 数据库中的数据（Windows 窗体）](https://msdn.microsoft.com/library/ms171890\(VS.110\).aspx)。  
  
 有关`LocalDB` API 的详细信息，请参阅[SQL SERVER EXPRESS LocalDB 实例 API 参考](https://msdn.microsoft.com/library/hh234692\(SQL.110\).aspx)和[LocalDBStartInstance 函数](https://msdn.microsoft.com/library/hh217143\(SQL.110\).aspx)。  
  
 SqlLocalDb 实用工具可以创建的`LocalDB`新实例，启动和停止实例`LocalDB`，并包含可帮助您管理`LocalDB`的选项。  有关 SqlLocalDb 实用工具的详细信息，请参阅 [SqlLocalDB 实用工具](../../tools/sqllocaldb-utility.md)。  
  
 的实例排序规则`LocalDB`设置为 SQL_Latin1_General_CP1_CI_AS 并且无法更改。 一般支持数据库级、列级和表达式级排序规则。 包含的数据库遵循 [Contained Database Collations](../../relational-databases/databases/contained-database-collations.md) 所定义的元数据和 tempdb 排序规则。  
  
### <a name="restrictions"></a>限制  
 `LocalDB`不能是合并复制订阅服务器。  
  
 `LocalDB`不支持 FILESTREAM。  
  
 `LocalDB`仅允许 Service Broker 的本地队列。  
  
 由于 windows 文件`LocalDB`系统重定向，NT AUTHORITY\SYSTEM 等内置帐户拥有的一个实例可能具有管理性问题;改为使用普通的 windows 帐户作为所有者。  
  
### <a name="automatic-and-named-instances"></a>自动实例和命名实例  
 `LocalDB`支持两种类型的实例：自动实例和命名实例。  
  
-   的自动实例`LocalDB`是公共的。 系统自动为用户创建和管理此类实例，并可由任何应用程序使用。 对于`LocalDB`安装在用户`LocalDB`计算机上的每个版本，都存在一个自动实例。 自动实例提供`LocalDB`无缝的实例管理。 无需创建实例；它可以自动执行工作。 这使得应用程序可以轻松地安装和迁移到另一台计算机。 如果目标计算机已安装指定版本的 `LocalDB`，则目标计算机也提供此版本的自动 `LocalDB` 实例。 的`LocalDB`自动实例对于属于保留命名空间的实例名称有特殊的模式。 这可以防止名称与的`LocalDB`命名实例发生冲突。 自动实例的名称为 **MSSQLLocalDB**。  
  
-   的命名实例`LocalDB`是专用的。 这些命名实例由负责创建和管理该实例的单个应用程序所拥有。 命名实例提供与其他实例的隔离，并可以通过减少与其他数据库用户的资源争用来提高性能。 命名实例必须由用户通过`LocalDB`管理 API 显式创建，或者通过托管应用程序的 app.config 文件隐式创建（尽管托管应用程序也可以使用 API，如需要）。 的`LocalDB`每个命名实例都具有`LocalDB`指向各自的`LocalDB`二进制文件集的关联版本。 的实例名称的数据`LocalDB`类型`sysname`为，最多可包含128个字符。 （这不同于常规的命名实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，后者将名称限制为16个 ASCII 字符的常规 NetBIOS 名称。）实例的名称`LocalDB`可包含在文件名内合法的任何 Unicode 字符。  使用自动实例名称的命名实例将成为自动实例。  
  
 不同的计算机用户可具有同名的实例。 每个实例都是以不同的用户身份运行的不同的进程。  
  
## <a name="shared-instances-of-localdb"></a>LocalDB 的共享实例  
 为了支持多个计算机用户需要连接到单个实例的`LocalDB`方案， `LocalDB`支持实例共享。 实例所有者可以选择允许计算机上的其他用户连接到其实例。 的`LocalDB`自动实例和命名实例都可以共享。 若要共享 `LocalDB` 的某个实例，用户需要为其选择一个共享名称（别名）。 因为该共享名称对于该计算机的所有用户都是可见的，则此共享名称在计算机上必须唯一。 实例的共享名称`LocalDB`具有与的命名实例相同的格式。 `LocalDB`  
  
 只有计算机上的管理员才能创建的`LocalDB`共享实例。 的`LocalDB`共享实例可由管理员或共享实例的所有者取消共享`LocalDB`。 若要共享和取消共享实例`LocalDB`，请使用`LocalDBShareInstance` `LocalDB` API `LocalDBUnShareInstance`的和方法，或者使用 SqlLocalDb 实用工具的共享和非共享选项。  
  
## <a name="starting-localdb-and-connecting-to-localdb"></a>启动 LocalDB 和连接到 LocalDB  
  
### <a name="connecting-to-the-automatic-instance"></a>连接到自动实例  
 使用`LocalDB`的最简单方法是使用连接字符串 **"Server = （localdb） \MSSQLLocalDB; 集成安全性 = true"** 连接到当前用户拥有的自动实例。 若要使用文件名连接到特定数据库，则使用类似于 **"Server=(LocalDB)\MSSQLLocalDB; Integrated Security=true ;AttachDbFileName=D:\Data\MyDB1.mdf"** 的连接字符串进行连接。  
  
> [!NOTE]  
>  计算机上的用户首次尝试连接到`LocalDB`时，必须创建并启动自动实例。 创建实例所用的额外时间可能会导致连接尝试失败并且具有超时消息。 在发生此情况时，等待几秒钟以便让创建过程完成，然后再次连接。  
  
### <a name="creating-and-connecting-to-a-named-instances"></a>创建和连接到命名实例  
 除了自动实例， `LocalDB`还支持命名实例。 使用 SqlLocalDB 程序可以创建、启动和停止的命名实例`LocalDB`。 有关 SqlLocalDB.exe 的详细信息，请参阅 [SqlLocalDB 实用工具](../../tools/sqllocaldb-utility.md)。  
  
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
|名称|"LocalDBApp1"|  
|版本|\<当前版本>|  
|共享名称|""|  
|“所有者”|"\<你的 Windows 用户>"|  
|自动创建|否|  
|状态|“正在运行”|  
|上次启动时间|\<日期和时间>|  
|实例管道名称|np:\\\\.\pipe\LOCALDB#F365A78E\tsql\query|  
  
> [!NOTE]  
>  如果应用程序使用4.0.2 之前的 .NET 版本，则必须直接连接到的命名管道`LocalDB`。 实例管道名称值是实例`LocalDB`正在侦听的命名管道。 LOCALDB # 之后的实例管道名称部分将在每次启动实例`LocalDB`时更改。 若要[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]使用连接到实例`LocalDB` ，请在 "**连接到[!INCLUDE[ssDE](../../includes/ssde-md.md)] ** " 对话框的 "**服务器名称**" 框中键入实例管道名称。 通过自定义程序，可以使用类似于的连接字符串`LocalDB`建立与实例的连接。`SqlConnection conn = new SqlConnection(@"Server=np:\\.\pipe\LOCALDB#F365A78E\tsql\query");`  
  
### <a name="connecting-to-a-shared-instance-of-localdb"></a>连接到 LocalDB 的共享实例  
 若为，则连接到连接`LocalDB`字符串的共享**\\实例（点**+ 反斜杠），以引用为共享实例保留的命名空间。 例如，若要连接到`LocalDB`名为`AppData`的共享实例，请使用连接字符串（ `(localdb)\.\AppData`例如）作为连接字符串的一部分。 连接到其不拥有的共享实例`LocalDB`的用户必须具有 Windows 身份验证或[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]身份验证登录名。  
  
## <a name="troubleshooting"></a>故障排除  
 有关故障排除`LocalDB`的详细信息，请参阅[SQL Server 2012 Express LocalDB 疑难解答](https://social.technet.microsoft.com/wiki/contents/articles/4609.aspx)。  
  
## <a name="permissions"></a>权限  
 的[!INCLUDE[ssExpCurrent](../../includes/ssexpcurrent-md.md)] `LocalDB`实例是用户创建的一个实例，供用户使用。 计算机上的任何用户都可以使用实例创建数据库`LocalDB`，在用户配置文件下存储文件并在其凭据下运行该进程。 默认情况下，对实例的`LocalDB`访问仅限于其所有者。 中包含的`LocalDB`数据受到对数据库文件的文件系统访问的保护。 如果用户数据库文件存储在共享位置，则对该位置具有文件系统访问权限的任何人都可以打开该数据库，方法是使用`LocalDB`它们所拥有的实例。 如果数据库文件处于某一受保护的位置，例如用户数据文件夹，则只有该用户以及有权访问该文件夹的任何管理员才能打开该数据库。 `LocalDB`文件一次只能由一个实例`LocalDB`打开。  
  
> [!NOTE]  
>  `LocalDB`始终在用户安全上下文中运行;也就是说， `LocalDB`绝不会用本地管理员组中的凭据运行。 这意味着， `LocalDB`实例使用的所有数据库文件必须可以使用拥有用户的 Windows 帐户进行访问，而无需考虑本地 Administrators 组的成员身份。  
  
## <a name="see-also"></a>另请参阅  
 [SqlLocalDB 实用工具](../../tools/sqllocaldb-utility.md)  
  
  
