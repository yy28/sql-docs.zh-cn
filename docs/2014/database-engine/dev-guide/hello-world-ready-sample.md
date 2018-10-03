---
title: Hello World Ready 示例 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
ms.assetid: 1cb94266-f702-4a57-a1ae-689a89c98757
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: cc2ba0e196fa2440152fe1bd7415feeeb6f4e079
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48079637"
---
# <a name="hello-world-ready-sample"></a>Hello World Ready 示例
  Hello World Ready 示例说明了创建、部署和测试基于公共语言运行时 (CLR) 集成的简单且全球通用存储过程所涉及的基本操作。 不用更改全球通用组件的源代码就可以将它轻松地本地化为全世界各个市场的各种语言。 此示例还说明了如何通过输出参数和记录返回由存储过程动态构建并返回到客户端的数据。此示例与 Hello World 示例基本相同，只不过在对此应用程序进行本地化时，此示例更容易且更安全。 更改已本地化的文本需要执行下列操作：  
  
1.  更改 XML 文件 (。`resx` 文件） 的资源目录中的特定区域性  
  
2.  使用 `resgen` 生成该语言的资源文件  
  
3.  生成该区域性的最新附属 DLL  
  
4.  在 SQL Server 中删除和添加该程序集  
  
 CLR 存储过程本身的源代码和程序集并不更改。 提供了 `build.cmd` 脚本，用来说明如何编译和链接资源程序集。尽管应用程序的源代码基于当前执行的程序集创建了资源管理器，但是您不必在包含存储过程的 DLL 中嵌入独立于区域性的资源。 `System.Resources.NeutralResourcesLanguage attribute` 允许附属 DLL 中存在独立于区域性的资源。 因此，最好使用单独的 DLL，以便在需要添加或更改本地化文本时，不必更改包含 CLR 存储过程的主 DLL。 这对于可能含有列和其他相关性，造成类型难以删除和重新添加的 CLR 用户定义类型而言，尤为有用。通常，附属 DLL 版本必须与主程序集版本相同。 但是，使用 `SatelliteContractVersion` 属性可以允许仅更新主程序集，而不更新附属程序集。 有关详细信息，请参阅 Microsoft .NET 文档中的 `ResourceManager` 类。  
  
## <a name="prerequisites"></a>必要條件  
 此示例仅适用于 SQL Server 2005 和更高版本。  
  
 若要创建和运行此项目，必须安装下列软件：  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Express。 可以从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Express 文档和示例[网站](http://go.microsoft.com/fwlink/?LinkId=31046)免费获取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Express  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]开发人员[网站](http://go.microsoft.com/fwlink/?linkid=62796)提供的 AdventureWorks 数据库  
  
-   .NET Framework SDK 2.0 或更高版本，或 Microsoft Visual Studio 2005 或更高版本。 您可以免费获取 .NET Framework SDK。  
  
-   此外，还必须满足以下条件：  
  
-   使用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例必须已启用 CLR 集成。  
  
-   若要启用 CLR 集成，请执行以下步骤：  
  
    #### <a name="enabling-clr-integration"></a>启用 CLR 集成  
  
    -   执行以下 [!INCLUDE[tsql](../../includes/tsql-md.md)] 命令：  
  
     `sp_configure 'clr enabled', 1`  
  
     `GO`  
  
     `RECONFIGURE`  
  
     `GO`  
  
    > [!NOTE]  
    >  若要启用 CLR，必须具有`ALTER SETTINGS`服务器级权限，其中的成员隐式拥有`sysadmin`和`serveradmin`固定服务器角色的成员。  
  
-   必须在您使用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例上安装 AdventureWorks 数据库。  
  
-   如果你不是要使用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的管理员，必须请管理员授予你 **CreateAssembly** 权限，才能完成安装。  
  
## <a name="building-the-sample"></a>生成示例  
  
#### <a name="create-and-run-the-sample-by-using-the-following-instructions"></a>按照以下说明创建和运行该示例：  
  
1.  打开 Visual Studio 或 .NET Framework 命令提示符。  
  
2.  如有必要，为您的示例创建目录。 对于此示例，我们将使用 C:\MySample。  
  
3.  在 c:\MySample 中，创建 `HelloWorld.vb`（用于 Visual Basic 示例）或 `HelloWorld.cs`（用于 C# 示例），并将相应的 Visual Basic 或 C# 示例代码（如下所示）复制到该文件中。  
  
4.  在 c:\MySample，创建文件`messages.resx`和示例代码复制到的文件。  
  
5.  在 c:\MySample，创建在文件`messages.de.resx`将文件保存`messages.resx`作为`messages.de.resx`后将行  
  
    -   `<value xml:space="preserve">Hello, World!</value>`  
  
    -   更改为   
  
    -   `<value xml:space="preserve">Hallo Welt!</value>`  
  
6.  在 c:\MySample，创建在文件`messages.es.resx`将文件保存`messages.resx`作为`messages.es.resx`后将行  
  
    -   `<value xml:space="preserve">Hello, World!</value>`  
  
    -   更改为   
  
    -   `<value xml:space="preserve">Hola a todos</value>`  
  
7.  在 c:\MySample，创建在文件`messages.fr.resx`将文件保存`messages.resx`作为`messages.fr.resx`后将行  
  
    -   `<value xml:space="preserve">Hello, World!</value>`  
  
    -   更改为   
  
    -   `<value xml:space="preserve">BonjourÂ !</value>`  
  
8.  在 c:\MySample，创建在文件`messages.fr-FR.resx`将文件保存`messages.resx`作为`messages.fr-FR.resx`后将行  
  
    -   `<value xml:space="preserve">Hello, World!</value>`  
  
    -   更改为   
  
    -   `<value xml:space="preserve">Bonjour de France!</value>`  
  
9. 在 c:\MySample，创建在文件`messages.it.resx`将文件保存`messages.resx`作为`messages.it.resx`后将行  
  
    -   `<value xml:space="preserve">Hello, World!</value>`  
  
    -   更改为   
  
    -   `<value xml:space="preserve">Buongiorno</value>`  
  
10. 在 c:\MySample，创建在文件`messages.ja.resx`将文件保存`messages.resx`作为`messages.ja.resx`后将行  
  
    -   `<value xml:space="preserve">Hello, World!</value>`  
  
    -   更改为   
  
    -   `<value xml:space="preserve">` `ã“ã‚“ã«ã¡ã¯</value>`  
  
11. 在 c:\MySample 中，创建文件 `build.com` 并将示例代码复制到该文件中。  
  
12. 通过在命令提示符处执行文件生成操作来生成附属程序集。  
  
13. 通过在命令行提示符处执行以下命令之一来编译示例代码：  
  
    -   `Vbc /reference:C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.Data.dll,C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.dll,C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.Xml.dll /out:HelloWorldReady.dll /target:library HelloWorld.vb`  
  
    -   `Csc /reference:C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.Data.dll /reference:C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.dll /reference:C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.XML.dll /out:HelloWorldReady.dll /target:library Hello.csCopy the tsql installation code into a file and save it as Install.sql in the sample directory.`  
  
14. 如果示例安装在 `C:\MySample\` 之外的目录中，请按说明编辑文件 `Install.sql` 以指向该位置。  
  
15. 通过执行以下命令部署程序集和存储过程：  
  
    -   `sqlcmd -E -I -i install.sql`  
  
16. 复制[!INCLUDE[tsql](../../includes/tsql-md.md)]到一个文件测试命令脚本并将其保存为`test.sql`示例目录中。  
  
17. 使用以下命令执行测试脚本：  
  
    -   `sqlcmd -E -I -i test.sql`  
  
18. 将 [!INCLUDE[tsql](../../includes/tsql-md.md)] 清除脚本复制到一个文件中，并在示例目录中将其另存为 `cleanup.sql`。  
  
19. 使用以下命令执行该脚本：  
  
    -   `sqlcmd -E -I -i cleanup.sql`  
  
## <a name="sample-code"></a>示例代码  
 下面是此示例的代码列表。  
  
 C#  
  
```  
using System;  
using System.Data;  
using System.Data.Sql;  
using System.Data.SqlTypes;  
using Microsoft.SqlServer.Server;  
using System.Globalization;  
using System.Threading;  
using System.Resources;  
using System.Reflection;  
using System.Runtime.CompilerServices;  
  
[assembly: System.Resources.NeutralResourcesLanguage("", System.Resources.UltimateResourceFallbackLocation.Satellite)]  
[assembly: System.Security.Permissions.SecurityPermissionAttribute(System.Security.Permissions.SecurityAction.RequestMinimum)]  
[assembly: System.Runtime.ConstrainedExecution.ReliabilityContract(System.Runtime.ConstrainedExecution.Consistency.MayCorruptInstance, System.Runtime.ConstrainedExecution.Cer.None)]  
  
    public sealed partial class StoredProcedures  
    {  
        private StoredProcedures()  
        {  
        }  
  
        [System.Diagnostics.CodeAnalysis.SuppressMessage("Microsoft.Design", "CA1021:AvoidOutParameters"), Microsoft.SqlServer.Server.SqlProcedure]  
        public static void HelloWorldReady(string culture, out string greeting)  
        {  
ResourceManager rm   
= new ResourceManager("Messages",   
Assembly.GetExecutingAssembly());  
  
string message = rm.GetString("HelloWorld", CultureInfo.GetCultureInfo(culture));  
  
            Microsoft.SqlServer.Server.SqlMetaData columnInfo  
                = new Microsoft.SqlServer.Server.SqlMetaData("Column1", SqlDbType.NVarChar, 24);  
            SqlDataRecord greetingRecord  
                = new SqlDataRecord(new Microsoft.SqlServer.Server.SqlMetaData[] { columnInfo });  
            greetingRecord.SetString(0, message);  
            SqlContext.Pipe.Send(greetingRecord);  
            greeting = message;  
        }  
    }  
  
```  
  
 Visual Basic  
  
```  
Imports System  
Imports System.Data  
Imports System.Data.Sql  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
Imports System.Globalization  
Imports System.Resources  
Imports System.Reflection  
Imports System.Runtime.InteropServices  
<Assembly: AssemblyVersion("1.0.*")>   
<Assembly: System.Runtime.InteropServices.ComVisible(False)>   
<Assembly: System.CLSCompliant(True)>   
<Assembly: System.Resources.NeutralResourcesLanguage("", System.Resources.UltimateResourceFallbackLocation.Satellite)>   
<Assembly: System.Security.Permissions.SecurityPermissionAttribute(System.Security.Permissions.SecurityAction.RequestMinimum)>   
<Assembly: System.Runtime.ConstrainedExecution.ReliabilityContract(System.Runtime.ConstrainedExecution.Consistency.WillNotCorruptState, Runtime.ConstrainedExecution.Cer.None)>   
  
Partial Public NotInheritable Class StoredProcedures  
    Private Sub New()  
    End Sub  
    <Microsoft.SqlServer.Server.SqlProcedure()> _  
    Public Shared Sub HelloWorldReady(ByVal culture As String, ByRef greeting As String)  
        Dim rm As New ResourceManager("Messages", Assembly.GetExecutingAssembly())  
        Dim message As String = rm.GetString("HelloWorld", CultureInfo.GetCultureInfo(culture))  
        Dim columnInfo As New Microsoft.SqlServer.Server.SqlMetaData("Column1", _  
            SqlDbType.NVarChar, 24)  
        Dim greetingRecord As New SqlDataRecord(New  _  
            Microsoft.SqlServer.Server.SqlMetaData() {columnInfo})  
        greetingRecord.SetString(0, message)  
        SqlContext.Pipe.Send(greetingRecord)  
        greeting = message  
    End Sub  
End Class  
  
```  
  
 这是用于生成附属程序集的 `build.com`。  
  
```  
resgen Messages.resx  
resgen Messages.de.resx  
resgen Messages.es.resx  
resgen Messages.fr.resx  
resgen Messages.fr-Fr.resx  
resgen Messages.it.resx  
resgen Messages.ja.resx  
if not exist de/ mkdir de  
if not exist es/ mkdir es  
if not exist fr/ mkdir fr  
if not exist fr-FR/ mkdir fr-FR  
if not exist it/ mkdir it  
if not exist ja/ mkdir ja  
al /t:lib /culture:de /embed:Messages.de.resources /out:de\HelloWorldReady.resources.dll  
al /t:lib /culture:es /embed:Messages.es.resources /out:es\HelloWorldReady.resources.dll  
al /t:lib /culture:fr /embed:Messages.fr.resources /out:fr\HelloWorldReady.resources.dll  
al /t:lib /culture:fr-FR /embed:Messages.fr-FR.resources /out:fr-FR\HelloWorldReady.resources.dll  
al /t:lib /culture:it /embed:Messages.it.resources /out:it\HelloWorldReady.resources.dll  
al /t:lib /culture:ja /embed:Messages.ja.resources /out:ja\HelloWorldReady.resources.dll  
al /t:lib /culture:"" /embed:Messages.resources /out:HelloWorldReady.resources.dll  
```  
  
 这是 [!INCLUDE[tsql](../../includes/tsql-md.md)] 安装脚本 (`Install.sql`)，该脚本在数据库中部署程序集并创建存储过程。  
  
```  
USE AdventureWorks  
GO  
  
-- Drop existing sproc and assembly if any.  
  
IF EXISTS (SELECT * FROM sys.procedures WHERE [name] = 'usp_HelloWorldReady')  
DROP PROCEDURE usp_HelloWorldReady;  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE [name] = 'HelloWorldReady')  
DROP ASSEMBLY HelloWorldReady;  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE [name] = 'HelloWorldReady.resources.neutral')  
DROP ASSEMBLY [HelloWorldReady.resources.neutral]  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE [name] = 'HelloWorldReady.resources.de')  
DROP ASSEMBLY [HelloWorldReady.resources.de]  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE [name] = 'HelloWorldReady.resources.es')  
DROP ASSEMBLY [HelloWorldReady.resources.es]  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE [name] = 'HelloWorldReady.resources.fr')  
DROP ASSEMBLY [HelloWorldReady.resources.fr]  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE [name] = 'HelloWorldReady.resources.fr-FR')  
DROP ASSEMBLY [HelloWorldReady.resources.fr-FR]  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE [name] = 'HelloWorldReady.resources.it')  
DROP ASSEMBLY [HelloWorldReady.resources.it]  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE [name] = 'HelloWorldReady.resources.ja')  
DROP ASSEMBLY [HelloWorldReady.resources.ja]  
GO  
  
DECLARE @SamplesPath nvarchar(1024)  
-- You may need to modify the value of this variable if you have installed the sample someplace other than the default location.  
Set @SamplesPath = N'C:\MySample\'  
  
-- Add the assembly and CLR integration based stored procedure  
  
CREATE ASSEMBLY HelloWorldReady  
FROM @SamplesPath + 'HelloWorldReady.dll'  
WITH permission_set = Safe;  
  
CREATE ASSEMBLY [HelloWorldReady.resources.neutral]  
FROM @SamplesPath + 'HelloWorldReady.resources.dll'  
WITH permission_set = Safe;   
  
CREATE ASSEMBLY [HelloWorldReady.resources.de]  
FROM @SamplesPath + '\de\HelloWorldReady.resources.dll'  
WITH permission_set = Safe;  
  
CREATE ASSEMBLY [HelloWorldReady.resources.es]  
FROM @SamplesPath + '\es\HelloWorldReady.resources.dll'  
WITH permission_set = Safe;  
  
CREATE ASSEMBLY [HelloWorldReady.resources.fr]  
FROM @SamplesPath + '\fr\HelloWorldReady.resources.dll'  
WITH permission_set = Safe;  
  
CREATE ASSEMBLY [HelloWorldReady.resources.fr-FR]  
FROM @SamplesPath + '\fr-FR\HelloWorldReady.resources.dll'  
WITH permission_set = Safe;  
  
CREATE ASSEMBLY [HelloWorldReady.resources.it]  
FROM @SamplesPath + '\it\HelloWorldReady.resources.dll'  
WITH permission_set = Safe;  
  
CREATE ASSEMBLY [HelloWorldReady.resources.ja]  
FROM @SamplesPath + '\ja\HelloWorldReady.resources.dll'  
WITH permission_set = Safe;  
GO  
  
CREATE PROCEDURE usp_HelloWorldReady  
(  
@Culture NVarchar(12),  
@Greeting NVarchar(24) OUTPUT  
)  
AS EXTERNAL NAME HelloWorldReady.StoredProcedures.HelloWorldReady;  
GO  
  
USE master;  
GO  
```  
  
 这是 `test.sql`，该脚本通过对各个区域设置执行函数来测试该示例。  
  
```  
USE AdventureWorks  
GO  
  
DECLARE @GreetingDe nvarchar(24);  
DECLARE @GreetingDe_CH nvarchar(24);  
DECLARE @GreetingEn nvarchar(24);  
DECLARE @GreetingEs nvarchar(24);  
DECLARE @GreetingFr nvarchar(24);  
DECLARE @GreetingFr_FR nvarchar(24);  
DECLARE @GreetingIt nvarchar(24);  
DECLARE @GreetingJa nvarchar(24);  
  
--German as spoken anywhere in the world (the neutral German culture)  
EXEC usp_HelloWorldReady 'de', @GreetingDe OUTPUT;  
--German as spoken in Switzerland.  Because we don't have a specific assembly  
--for this case, the .NET Framework will automatically fall back to the neutral German culture DLL.  
EXEC usp_HelloWorldReady 'de-CH', @GreetingDe_CH OUTPUT;  
EXEC usp_HelloWorldReady 'en', @GreetingEn OUTPUT;  
EXEC usp_HelloWorldReady 'es', @GreetingEs OUTPUT;  
--French as spoken anywhere in the world (the neutral French culture)  
EXEC usp_HelloWorldReady 'fr', @GreetingFr OUTPUT  
--French as spoken in France.  Since we do have a specific assembly for this case, a specific   
--greeting is provided from that DLL.  The neutral French culture DLL is not used in this case.  
EXEC usp_HelloWorldReady 'fr-FR', @GreetingFr_FR OUTPUT  
EXEC usp_HelloWorldReady 'it', @GreetingIt OUTPUT;  
EXEC usp_HelloWorldReady 'ja', @GreetingJa OUTPUT;  
  
SELECT @GreetingDe AS OUTPUT_PARAMETER_DE;  
SELECT @GreetingDe_CH AS OUTPUT_PARAMETER_De_CH;  
SELECT @GreetingEn AS OUTPUT_PARAMETER_EN;  
SELECT @GreetingEs AS OUTPUT_PARAMETER_ES;  
SELECT @GreetingFr AS OUTPUT_PARAMETER_FR;  
SELECT @GreetingFr_FR AS OUTPUT_PARAMETER_Fr_FR;  
SELECT @GreetingIt AS OUTPUT_PARAMETER_IT;  
SELECT @GreetingJa AS OUTPUT_PARAMETER_JA;  
  
GO  
```  
  
 下面的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 从数据库中删除程序集和存储过程。  
  
```  
USE AdventureWorks;  
GO  
  
-- Drop existing sproc and assembly if any.  
  
IF EXISTS (SELECT * FROM sys.procedures WHERE [name] = 'usp_HelloWorldReady')  
DROP PROCEDURE usp_HelloWorldReady;  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE [name] = 'HelloWorldReady')  
DROP ASSEMBLY HelloWorldReady;  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE [name] = 'HelloWorldReady.resources.neutral')  
DROP ASSEMBLY [HelloWorldReady.resources.neutral]  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE [name] = 'HelloWorldReady.resources.de')  
DROP ASSEMBLY [HelloWorldReady.resources.de]  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE [name] = 'HelloWorldReady.resources.es')  
DROP ASSEMBLY [HelloWorldReady.resources.es]  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE [name] = 'HelloWorldReady.resources.fr')  
DROP ASSEMBLY [HelloWorldReady.resources.fr]  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE [name] = 'HelloWorldReady.resources.fr-FR')  
DROP ASSEMBLY [HelloWorldReady.resources.fr-FR]  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE [name] = 'HelloWorldReady.resources.it')  
DROP ASSEMBLY [HelloWorldReady.resources.it]  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE [name] = 'HelloWorldReady.resources.ja')  
DROP ASSEMBLY [HelloWorldReady.resources.ja]  
GO  
  
USE master;  
GO  
```  
  
## <a name="see-also"></a>请参阅  
 [公共语言运行时 (CLR) 集成的使用方案和示例](../../../2014/database-engine/dev-guide/usage-scenarios-and-examples-for-common-language-runtime-clr-integration.md)  
  
  
