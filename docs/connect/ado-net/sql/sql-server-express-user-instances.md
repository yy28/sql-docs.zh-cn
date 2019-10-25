---
title: SQL Server Express 用户实例
description: 描述对 SQL Server Express 用户实例的支持。
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 00c12376-cb26-4317-86ad-e6e9c089be57
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 3b3ac1e395cc1240693ca0dc27324766964e0cfa
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452010"
---
# <a name="sql-server-express-user-instances"></a>SQL Server Express 用户实例

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[下载 ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

Microsoft SQL Server Express Edition （SQL Server Express）支持用户实例功能，仅当使用适用于 SQL Server 的 Microsoft SqlClient 数据提供程序时，该功能才可用。 用户实例是由父实例生成的 SQL Server Express 数据库引擎的单独实例。 用户实例允许非管理员计算机上的用户连接到 SQL Server Express 数据库并连接到该数据库。 每个实例在单个用户的安全上下文下运行，每个用户一个实例。  
  
## <a name="user-instance-capabilities"></a>用户实例功能  
用户实例适用于在最低权限用户帐户（LUA）下运行 Windows 的用户，因为每个用户对其计算机上运行的实例具有 SQL Server 系统管理员（`sysadmin`）权限，而无需作为 Windows 运行管理员。 在具有有限权限的用户实例上执行的软件无法进行系统范围的更改，因为 SQL Server Express 的实例是在用户的非管理员 Windows 帐户下运行，而不是以服务的形式运行。 用户实例独立于父实例和该计算机上运行的任何其他用户实例。 在用户实例上运行的数据库仅以单用户模式打开，多个用户无法连接到在用户实例上运行的数据库。 还会为用户实例禁用复制和分布式查询。  
  
有关详细信息，请参阅 SQL Server 联机丛书中的“用户实例”。  
  
> [!NOTE]
>  对于已经在自己的计算机上具有管理员权限的用户，或在涉及多个数据库用户的方案中，用户实例不是必需的。  
  
## <a name="enabling-user-instances"></a>启用用户实例  
若要生成用户实例，SQL Server Express 的父实例必须正在运行。 安装 SQL Server Express 后，默认情况下将启用用户实例，且对父实例执行 sp_configure 系统存储过程的系统管理员可以显式启用或禁用用户实例  。  
  
```sql
-- Enable user instances.  
sp_configure 'user instances enabled','1'   
  
-- Disable user instances.  
sp_configure 'user instances enabled','0'  
```  
  
用户实例的网络协议必须为本地命名管道。 用户实例无法在 SQL Server 的远程实例上启动，不允许 SQL Server 登录名。  
  
## <a name="connecting-to-a-user-instance"></a>连接到用户实例  
`User Instance` 和 `AttachDBFilename`<xref:Microsoft.Data.SqlClient.SqlConnection.ConnectionString%2A> 关键字允许 <xref:Microsoft.Data.SqlClient.SqlConnection> 连接到用户实例。 @No__t_0 `UserInstance` 和 `AttachDBFilename` 属性还支持用户实例。  
  
请注意下面所示的示例连接字符串：  
  
- @No__t_0 关键字引用正在生成用户实例的 SQL Server Express 的父实例。 默认实例为 .\sqlexpress。  
  
- `Integrated Security` 设置为 `true`。 若要连接到用户实例，需要 Windows 身份验证;不支持 SQL Server 登录名。  
  
- @No__t_0 设置为 `true`，这将调用一个用户实例。 （默认值为 `false`。）  
  
- @No__t_0 连接字符串关键字用于附加主数据库文件（.mdf），该文件必须包含完整路径名。 `AttachDbFileName` 还对应于 <xref:Microsoft.Data.SqlClient.SqlConnection> 连接字符串中的 "扩展属性" 和 "初始文件名" 密钥。  
  
- 管道符号中包含的 `|DataDirectory|` 替换字符串是指打开连接的应用程序的数据目录，并提供指示 .mdf 和 .ldf 数据库和日志文件位置的相对路径。 如果要在其他位置查找这些文件，则必须提供文件的完整路径。  
  
```console
Data Source=.\\SQLExpress;Integrated Security=true;  
User Instance=true;AttachDBFilename=|DataDirectory|\InstanceDB.mdf;  
Initial Catalog=InstanceDB;  
```  
  
> [!NOTE]
>  你还可以使用 <xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder> <xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder.UserInstance%2A> 和 <xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder.AttachDBFilename%2A> 属性在运行时生成连接字符串。  
  
### <a name="using-the-124datadirectory124-substitution-string"></a>使用&#124;DataDirectory&#124;替换字符串  
`DataDirectory` 与 `AttachDbFileName` 结合使用可指示数据文件的相对路径，从而允许开发人员创建基于数据源的相对路径（而无需指定完整路径）的连接字符串。  
  
@No__t_0 指向的物理位置取决于应用程序的类型。 在此示例中，要附加的 Northwind .mdf 文件位于应用程序的 \app_data 文件夹中。  
  
```console
Data Source=.\\SQLExpress;Integrated Security=true;  
User Instance=true;  
AttachDBFilename=|DataDirectory|\app_data\Northwind.mdf;  
Initial Catalog=Northwind;  
```  
  
使用 `DataDirectory` 时，生成的文件路径在目录结构中不能比替换字符串指向的目录更高。 例如，如果完全展开的 `DataDirectory` 为 C:\AppDirectory\app_data，则上面显示的示例连接字符串将起作用，因为它低于 c:\AppDirectory。 但是，如果尝试将 `DataDirectory` 指定为 `|DataDirectory|\..\data`，将会产生一个错误，因为 \data 不是 \AppDirectory 的子目录。  
  
如果连接字符串的替换字符串格式不正确，则会引发 <xref:System.ArgumentException>。  
  
> [!NOTE]
>  <xref:Microsoft.Data.SqlClient> 将替换字符串解析为本地计算机文件系统的完整路径。 因此，不支持远程服务器、HTTP 和 UNC 路径名称。 如果未在本地计算机上打开连接，则会引发异常。  
  
打开 <xref:Microsoft.Data.SqlClient.SqlConnection> 时，它将从默认的 SQL Server Express 实例重定向到在调用方帐户下运行的运行时启动的实例。  
  
> [!NOTE]
>  可能需要增加 <xref:Microsoft.Data.SqlClient.SqlConnection.ConnectionTimeout%2A> 值，因为加载用户实例所需的时间可能比常规实例需要更长的时间。  
  
以下代码段将打开一个新的 `SqlConnection`，在控制台窗口中显示连接字符串，然后在退出 `using` 代码块时关闭连接。  
  
```csharp  
private static void OpenSqlConnection()  
{  
    // Retrieve the connection string.  
    string connectionString = GetConnectionString();  
  
    using (SqlConnection connection =   
        new SqlConnection(connectionString))  
    {  
        connection.Open();  
        Console.WriteLine("ConnectionString: {0}",   
             connection.ConnectionString);  
    }  
}  
```  
  
> [!NOTE]
>  在 SQL Server 中运行的公共语言运行时（CLR）代码不支持用户实例。 如果在连接字符串中有 `User Instance=true` 的 <xref:Microsoft.Data.SqlClient.SqlConnection> 调用 `Open`，则会引发 <xref:System.InvalidOperationException>。  
  
## <a name="lifetime-of-a-user-instance-connection"></a>用户实例连接的生存期  
与作为服务运行的 SQL Server 版本不同，SQL Server Express 实例无需手动启动和停止。 用户每次登录并连接到用户实例时，如果用户实例尚未运行，则启动该用户实例。 用户实例数据库设置了 "`AutoClose`" 选项，以便在一段非活动期后自动关闭数据库。 在最后一次连接到实例后，启动的 sqlservr.exe 进程保持运行状态，因此，如果在超时过期之前打开了另一个连接，则无需重新启动。 如果在超时期限过期之前没有打开新连接，用户实例将自动关闭。 父实例的系统管理员可为用户实例设置超时期限的持续时间，方法为：使用 sp_configure 更改“用户实例超时”选项   。 默认值为 60 分钟。  
  
> [!NOTE]
>  如果在连接字符串中使用大于零的 `Min Pool Size`，则连接池将始终保持几个打开的连接，并且用户实例不会自动关闭。  
  
## <a name="how-user-instances-work"></a>用户实例的工作方式  
为每个用户首次生成用户实例时，系统会将 master 和 msdb 系统数据库从模板数据文件夹复制到用户的本地应用程序数据存储库目录下的某个路径中，供用户实例专用   。 此路径通常 `C:\Documents and Settings\<UserName>\Local Settings\Application Data\Microsoft\Microsoft SQL Server Data\SQLEXPRESS`。 启动用户实例时，tempdb、日志和跟踪文件也将被写入到此目录中  。 为实例生成一个名称，该名称保证对每个用户都是唯一的。  
  
默认情况下，Windows Builtin\Users 组的所有成员都被授予连接本地实例的权限，以及对 SQL Server 二进制文件的读取和执行权限。 在对承载用户实例的调用用户的凭据进行验证后，该用户将成为该实例上的 `sysadmin`。 只为用户实例启用共享内存，这意味着只能在本地计算机上执行操作。  
  
必须为用户授予对在连接字符串中指定的 .mdf 和 .ldf 文件的读取和写入权限。  
  
> [!NOTE]
>  .Mdf 和 .ldf 文件分别表示数据库和日志文件。 这两个文件是一个匹配的集，因此在备份和还原操作期间必须小心谨慎。 数据库文件包含有关日志文件的确切版本的信息，如果数据库与错误的日志文件耦合，则该数据库将不会打开。  
  
若要避免数据损坏，用户实例中的数据库将以独占访问权限打开。 如果两个不同的用户实例共享同一台计算机上的同一个数据库，则第一个实例上的用户必须关闭该数据库，然后才能在第二个实例中打开该数据库。  
  
## <a name="user-instance-scenarios"></a>用户实例方案  
用户实例为数据库应用程序开发人员提供了一个 SQL Server 数据存储区，该存储区不依赖于在其开发计算机上具有管理帐户的开发人员。 用户实例基于 Access/Jet 模型，在该模型中，数据库应用程序只连接到一个文件，用户自动对所有数据库对象具有完全权限，而无需系统管理员介入即可授予访问. 它在以下情况下运行：用户在最低特权用户帐户（LUA）下运行，并且在服务器或本地计算机上没有管理权限，但需要创建数据库对象和应用程序。 用户实例允许用户在运行时创建在用户自己的安全上下文中运行的实例，而不是在具有更高权限的系统服务的安全上下文中运行的实例。  
  
> [!IMPORTANT]
>  用户实例仅应在所有使用该应用程序的应用程序完全受信任的情况下使用。  
  
用户实例方案包括：  
  
- 不需要共享数据的任何单用户应用程序。  
  
- ClickOnce 部署。 如果 .NET Framework 2.0（或更高版本）或 .NET Core 1.0（或更高版本），以及 SQL Server Express 已安装在目标计算机上，则可以由非管理员用户安装并使用因 ClickOnce 操作而下载的安装程序包。 请注意，如果是安装程序的一部分，则管理员必须安装 SQL Server Express。 有关详细信息，请参阅[ClickOnce Deployment for Windows 窗体](https://docs.microsoft.com/dotnet/framework/winforms/clickonce-deployment-for-windows-forms)。
  
- 使用 Windows 身份验证的专用 ASP.NET 托管。 单个 SQL Server Express 实例可以承载在 intranet 上。 应用程序使用 ASPNET Windows 帐户进行连接，而不是使用模拟。 用户实例不应用于第三方或共享主机方案，在这些方案中，所有应用程序将共享同一个用户实例，且不再彼此隔离。  
  
## <a name="next-steps"></a>后续步骤
- [SQL Server 和 ADO.NET](index.md)
