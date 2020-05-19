---
title: 使用 sqlcmd 实用工具
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- Transact-SQL statements, executing
- command prompt utilities [SQL Server], sqlcmd
- statements [SQL Server], executing
- sqlcmd utility, about sqlcmd utility
ms.assetid: 3ec89119-7314-43ef-9e91-12e72bb63d62
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 35f7bcf1c8e5ebcb225a9198944cf4144321bad3
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/01/2020
ms.locfileid: "82703693"
---
# <a name="use-the-sqlcmd-utility"></a>使用 sqlcmd 实用工具
  `sqlcmd` 实用工具是一个命令行实用工具，用于 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句和脚本的即席、交互执行以及自动执行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 脚本撰写任务。 若要以交互方式使用 `sqlcmd`，或要生成可使用 `sqlcmd` 运行的脚本文件，用户需要了解 [!INCLUDE[tsql](../../includes/tsql-md.md)]。 `sqlcmd`实用程序通常按以下方式使用：  
  
-   用户以交互方式输入 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句，输入方式与在命令提示符下输入的方式类似。 结果将显示在命令提示符处。 若要打开命令提示符窗口，依次单击 **“开始”**、 **“所有程序”**，指向 **“附件”**，然后单击 **“命令提示符”**。 在命令提示符处，键入 `sqlcmd`，后面跟随所需的选项列表。 有关支持的选项的完整列表 `sqlcmd` ，请参阅[sqlcmd 实用工具](../../tools/sqlcmd-utility.md)。  
  
-   用户通过下列方式提交 `sqlcmd` 作业：指定要执行的单个 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句，或将实用工具指向要执行的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句所在的文本文件。 输出通常定向到一个文本文件，但也可以显示在命令提示符处。  
  
-   [查询编辑器中的](edit-sqlcmd-scripts-with-query-editor.md) SQLCMD 模式 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 。  
  
-   SQL Server 管理对象 (SMO)  
  
-   SQL Server 代理 CmdExec 作业。  
  
## <a name="typically-used-sqlcmd-options"></a>常用 sqlcmd 选项  
 最常用的选项如下：  
  
-   服务器选项（**-S**），用于标识 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 要连接的的实例 `sqlcmd` 。  
  
-   身份验证选项（**-E**、 **-U**和 **-P**），用于指定用于 `sqlcmd` 连接到实例的凭据 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
    > [!NOTE]  
    >  **-E** 选项为默认选项，毋须指定。  
  
-   输入选项（**-q**、 **-q**和 **-i**），用于标识输入的位置 `sqlcmd` 。  
  
-   输出选项（**-o**），用于指定在其中 `sqlcmd` 放置输出的文件。  
  
## <a name="connecting-to-the-sqlcmd-utility"></a>连接到 sqlcmd 实用工具  
 以下是 `sqlcmd` 实用工具的常见用法：  
  
-   使用 Windows 身份验证连接到默认实例，以交互方式运行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句：  
  
    ```  
    sqlcmd -S <ComputerName>  
    ```  
  
    > [!NOTE]  
    >  在前面的示例中，未指定 **-E** ，因为它是默认值，并且 `sqlcmd` 通过使用 Windows 身份验证连接到默认实例。  
  
-   使用 Windows 身份验证连接到命名实例，以交互方式运行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句：  
  
    ```  
    sqlcmd -S <ComputerName>\<InstanceName>  
    ```  
  
     or  
  
    ```  
    sqlcmd -S .\<InstanceName>  
    ```  
  
-   使用 Windows 身份验证连接到命名实例，并指定输入和输出文件：  
  
    ```  
    sqlcmd -S <ComputerName>\<InstanceName> -i <MyScript.sql> -o <MyOutput.rpt>  
    ```  
  
-   使用 Windows 身份验证连接到本地计算机上的默认实例，执行查询，并在查询运行完毕后使 `sqlcmd` 保持运行状态：  
  
    ```  
    sqlcmd -q "SELECT * FROM AdventureWorks2012.Person.Person"  
    ```  
  
-   使用 Windows 身份验证连接到本地计算机上的默认实例，执行查询，将输出定向到某个文件，并在查询运行完毕后使 `sqlcmd` 退出：  
  
    ```  
    sqlcmd -Q "SELECT * FROM AdventureWorks2012.Person.Person" -o MyOutput.txt  
    ```  
  
-   使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证连接到命名实例，以交互方式运行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句，并由 `sqlcmd` 提示输入密码：  
  
    ```  
    sqlcmd -U MyLogin -S <ComputerName>\<InstanceName>  
    ```  
  
    > [!NOTE]  
    >  若要查看 `sqlcmd` 实用工具所支持选项的列表，请运行：`sqlcmd -?`。  
  
## <a name="running-transact-sql-statements-interactively-by-using-sqlcmd"></a>使用 sqlcmd 以交互方式运行 Transact-SQL 语句  
 您可以使用 `sqlcmd` 实用工具以交互方式在命令提示符窗口中执行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句。 若要使用以交互方式执行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句 `sqlcmd` ，请在不使用 **-q**、 **-q**、 **-Z**或 **-i**选项指定任何输入文件或查询的情况下运行实用工具。 例如：  
  
 `sqlcmd -S <ComputerName>\<InstanceName>`  
  
 在未指定输入文件或查询的情况下执行命令时，`sqlcmd` 连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的指定实例，然后显示一个新行，其中包含 `1>` 并且后面跟着一个闪烁的下划线（称为 `sqlcmd` 提示符）。 `1` 表示这是 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句的第一行，而 `sqlcmd` 提示符则是您键入 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句的起点。  
  
 在 `sqlcmd` 提示符中，可以键入 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句和 `sqlcmd` 命令，如 `GO` 和 `EXIT`。 每个 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句放在称为“语句缓存”的缓冲区中。 键入 `GO` 命令并按 Enter 键后，这些语句将发送到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 若要退出 `sqlcmd` ， `EXIT` 请 `QUIT` 在新行的开头键入或。  
  
 若要清除语句缓存，请键入 `:RESET`。 键入 `^C` `sqlcmd` 将导致退出。 在发出 `^C` 命令后，还可以用 `GO` 停止语句缓存的执行。  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)]可以通过输入 **： ED**命令和提示符来编辑在交互式会话中输入的语句 `sqlcmd` 。 编辑器将打开，编辑 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句并关闭编辑器后，修改后的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句将显示于命令窗口中。 输入 `GO` 以运行 therevised [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句。  
  
## <a name="quoted-strings"></a>带引号的字符串  
 用引号引起来的字符无需任何额外的预处理即可使用。例外，输入两个连续的引号可以将引号插入字符串中。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将这种字符序列视作一个引号。 （但在服务器上会进行转换。）当脚本变量出现在字符串中时，不会展开它们。  
  
 例如：  
  
 `sqlcmd`  
  
 `PRINT "Length: 5"" 7'";`  
  
 `GO`  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `Length: 5" 7'`  
  
## <a name="strings-that-span-multiple-lines"></a>跨多行的字符串  
 `sqlcmd` 支持包含跨多行的字符串的脚本。 例如，下面的 `SELECT` 语句跨多行，但键入 `GO`并按 Enter 键后，将执行单个字符串。  
  
 `SELECT First line`  
  
 `FROM Second line`  
  
 `WHERE Third line;`  
  
 `GO`  
  
## <a name="interactive-sqlcmd-example"></a>交互式 sqlcmd 示例  
 本示例说明了以交互方式运行 `sqlcmd` 的过程。  
  
 打开命令提示符窗口时，出现如下一行内容：  
  
 `C:\> _`  
  
 这表示文件夹 `C:\` 为当前文件夹，如果您指定文件名，则 Windows 将在此文件夹中查找这个文件。  
  
 键入 `sqlcmd` 连接到本地计算机上的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 默认实例，命令提示符窗口的内容为：  
  
 `C:\>sqlcmd`  
  
 `1> _`  
  
 这表示您已连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例，并且 `sqlcmd` 现在已可以接受 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句和 `sqlcmd` 命令。 `1>` 后闪烁的下划线是 `sqlcmd` 提示符，它标明了所键入语句和命令的显示位置。 现在，键入 `USE AdventureWorks2012` 并按 enter，然后键入 `GO` 并按 enter。 命令提示符窗口的内容如下：  
  
 `sqlcmd`  
  
 `USE AdventureWorks2012;`  
  
 `GO`  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `Changed database context to 'AdventureWorks2012'.`  
  
 `1> _`  
  
 输入 `USE AdventureWorks2012` 后按 Enter 键，即向 `sqlcmd` 发出换行信号。 键入 `GO,` 后按 Enter 键，即向 `sqlcmd` 发出信号将 `USE AdventureWorks2012` 语句发送到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的实例。 `sqlcmd` 随后返回一条消息，指示 `USE` 语句已成功完成并显示新的 `1>` 提示符作为输入新语句或命令的信号。  
  
 下面的示例说明了键入 `SELECT` 语句和 `GO` 执行 `SELECT`以及键入 `EXIT` 退出 `sqlcmd`时命令提示符窗口包含的内容：  
  
 `sqlcmd`  
  
 `USE AdventureWorks2012;`  
  
 `GO`  
  
 `SELECT TOP (3) BusinessEntityID, FirstName, LastName`  
  
 `FROM Person.Person;`  
  
 `GO`  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `BusinessEntityID   FirstName                 LastName`  
  
 `----------- -------------------------------- -----------`  
  
 `1           Syed                             Abbas`  
  
 `2           Catherine                        Abel`  
  
 `3           Kim                              Abercrombie`  
  
 `(3 rows affected)`  
  
 `1> EXIT`  
  
 `C:\>`  
  
 行 `3> GO` 后的几行内容为 `SELECT` 语句的输出。 生成输出后， `sqlcmd` 重置 `sqlcmd` 提示符并显示 `1>`。 在 `EXIT` 行输入 `1>`后，命令提示符窗口显示第一次打开时显示的行。 它指示 `sqlcmd` 已退出会话。 现在可以再键入一个 `EXIT` 命令关闭命令提示符窗口。  
  
## <a name="running-transact-sql-script-files-by-using-sqlcmd"></a>使用 sqlcmd 运行 Transact-SQL 脚本文件  
 可以使用 `sqlcmd` 执行数据库脚本文件。 脚本文件是包含 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句、 `sqlcmd` 命令和脚本变量混合的文本文件。 有关如何使用脚本变量的详细信息，请参阅 [将 sqlcmd 与脚本变量结合使用](sqlcmd-use-with-scripting-variables.md)。 `sqlcmd` 与脚本文件中语句、命令和脚本变量的配合方式类似于它与交互输入的语句和命令的配合方式。 主要区别在于 `sqlcmd` 从输入文件连续读取内容，而不是等待用户输入语句、命令和脚本变量。  
  
 可以通过几种不同的方式创建数据库脚本文件：  
  
-   可以在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中以交互方式生成和调试一组 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]语句，然后将“查询”窗口中的内容另存为脚本文件。  
  
-   可以使用记事本等文本编辑器创建包含 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句的文本文件。  
  
## <a name="examples"></a>示例  
  
### <a name="a-running-a-script-by-using-sqlcmd"></a>A. 使用 sqlcmd 运行脚本  
 启动记事本并键入以下 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句：  
  
 `USE AdventureWorks2012;`  
  
 `GO`  
  
 `SELECT TOP (3) BusinessEntityID, FirstName, LastName`  
  
 `FROM Person.Person;`  
  
 `GO`  
  
 创建一个名为 `MyFolder` 的文件夹，然后将脚本另存为文件夹 `MyScript.sql` 中的文件 `C:\MyFolder`。 在命令提示符处输入以下命令运行脚本，并将输出放入 `MyOutput.txt` 的 `MyFolder`中：  
  
 `sqlcmd -i C:\MyFolder\MyScript.sql -o C:\MyFolder\MyOutput.txt`  
  
 在记事本中查看 `MyOutput.txt` 的内容时，将看到以下内容：  
  
 `Changed database context to 'AdventureWorks2012'.`  
  
 `BusinessEntityID FirstName   LastName`  
  
 `---------------- ----------- -----------`  
  
 `1                Syed        Abbas`  
  
 `2                Catherine   Abel`  
  
 `3                Kim         Abercrombie`  
  
 `(3 rows affected)`  
  
### <a name="b-using-sqlcmd-with-a-dedicated-administrative-connection"></a>B. 通过专用管理连接使用 sqlcmd  
 在下面的示例中， `sqlcmd` 通过专用管理员连接 (DAC) 连接到一台具有阻塞问题的服务器。  
  
 `C:\>sqlcmd -S ServerName -A`  
  
 `1> SELECT blocked FROM sys.dm_exec_requests WHERE blocked <> 0;`  
  
 `2> GO`  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `spid   blocked`  
  
 `------ -------`  
  
 `62       64`  
  
 `(1 rows affected)`  
  
 使用 `sqlcmd` 结束阻塞进程。  
  
 `1> KILL 64;`  
  
 `2> GO`  
  
### <a name="c-using-sqlcmd-to-execute-a-stored-procedure"></a>C. 使用 sqlcmd 执行存储过程  
 下面的示例说明如何使用 `sqlcmd`执行存储过程。 创建以下存储过程。  
  
 `USE AdventureWorks2012;`  
  
 `IF OBJECT_ID ( ' dbo.ContactEmailAddress, 'P' ) IS NOT NULL`  
  
 `DROP PROCEDURE dbo.ContactEmailAddress;`  
  
 `GO`  
  
 `CREATE PROCEDURE dbo.ContactEmailAddress`  
  
 `(`  
  
 `@FirstName nvarchar(50)`  
  
 `,@LastName nvarchar(50)`  
  
 `)`  
  
 `AS`  
  
 `SET NOCOUNT ON`  
  
 `SELECT EmailAddress`  
  
 `FROM Person.Person`  
  
 `WHERE FirstName = @FirstName`  
  
 `AND LastName = @LastName;`  
  
 `SET NOCOUNT OFF`  
  
 在 `sqlcmd` 提示符下，输入以下内容：  
  
 `C:\sqlcmd`  
  
 `1> :Setvar FirstName Gustavo`  
  
 `1> :Setvar LastName Achong`  
  
 `1> EXEC dbo.ContactEmailAddress $(Gustavo),$(Achong)`  
  
 `2> GO`  
  
 `EmailAddress`  
  
 `-----------------------------`  
  
 `gustavo0@adventure-works.com`  
  
### <a name="d-using-sqlcmd-for-database-maintenance"></a>D. 使用 sqlcmd 进行数据库维护  
 下面的示例说明了如何将 `sqlcmd` 用于数据库维护任务。 使用以下代码创建 `C:\BackupTemplate.sql` 。  
  
 `USE master;`  
  
 `BACKUP DATABASE [$(db)] TO DISK='$(bakfile)';`  
  
 在 `sqlcmd` 提示符下，输入以下内容：  
  
 `C:\ >sqlcmd`  
  
 `1> :connect <server>`  
  
 `Sqlcmd: Successfully connected to server <server>.`  
  
 `1> :setvar db msdb`  
  
 `1> :setvar bakfile c:\msdb.bak`  
  
 `1> :r c:\BackupTemplate.sql`  
  
 `2> GO`  
  
 `Changed database context to 'master'.`  
  
 `Processed 688 pages for database 'msdb', file 'MSDBData' on file 2.`  
  
 `Processed 5 pages for database 'msdb', file 'MSDBLog' on file 2.`  
  
 `BACKUP DATABASE successfully processed 693 pages in 0.725 seconds (7.830 MB/sec)`  
  
### <a name="e-using-sqlcmd-to-execute-code-on-multiple-instances"></a>E. 使用 sqlcmd 对多个实例执行代码  
 某文件中的以下代码表示一个连接到两个实例的脚本。 请注意连接到第二个实例之前的 `GO` 。  
  
 `:CONNECT <server>\,<instance1>`  
  
 `EXEC dbo.SomeProcedure`  
  
 `GO`  
  
 `:CONNECT <server>\,<instance2>`  
  
 `EXEC dbo.SomeProcedure`  
  
 `GO`  
  
### <a name="e-returning-xml-output"></a>E. 返回 XML 输出  
 下面的示例说明了如何以连续流返回未格式化的 XML 输出。  
  
 `C:\>sqlcmd -d AdventureWorks2012`  
  
 `1> :XML ON`  
  
 `1> SELECT TOP 3 FirstName + ' ' + LastName + ', '`  
  
 `2> FROM Person.Person`  
  
 `3> GO`  
  
 `Syed Abbas, Catherine Abel, Kim Abercrombie,`  
  
### <a name="f-using-sqlcmd-in-a-windows-script-file"></a>F. 在 Windows 脚本文件中使用 sqlcmd  
 `sqlcmd`命令（如） `sqlcmd -i C:\InputFile.txt -o C:\OutputFile.txt,` 可以与 VBScript 一起在 .bat 文件中执行。 此时，不要使用交互选项。 执行 .bat 文件的计算机上必须安装 `sqlcmd`。  
  
 首先，创建以下四个文件：  
  
-   C:\badscript.sql  
  
    ```  
    SELECT batch_1_this_is_an_error  
    GO  
    SELECT 'batch #2'  
    GO  
    ```  
  
-   C:\goodscript.sql  
  
    ```  
    SELECT 'batch #1'  
    GO  
    SELECT 'batch #2'  
    GO  
    ```  
  
-   C:\returnvalue.sql  
  
    ```  
    :exit(select 100)  
    @echo off  
    C:\windowsscript.bat  
    @echo off  
  
    echo Running badscript.sql  
    sqlcmd -i badscript.sql -b -o out.log  
    if not errorlevel 1 goto next1  
    echo == An error occurred   
  
    :next1  
  
    echo Running goodscript.sql  
    sqlcmd -i goodscript.sql -b -o out.log  
    if not errorlevel 1 goto next2  
    echo == An error occurred   
  
    :next2  
    echo Running returnvalue.sql  
    sqlcmd -i returnvalue.sql -o out.log  
    echo SQLCMD returned %errorlevel% to the command shell  
  
    :exit  
    ```  
  
-   C:\windowsscript.bat  
  
    ```  
    @echo off  
  
    echo Running badscript.sql  
    sqlcmd -i badscript.sql -b -o out.log  
    if not errorlevel 1 goto next1  
    echo == An error occurred   
  
    :next1  
  
    echo Running goodscript.sql  
    sqlcmd -i goodscript.sql -b -o out.log  
    if not errorlevel 1 goto next2  
    echo == An error occurred   
  
    :next2  
    echo Running returnvalue.sql  
    sqlcmd -i returnvalue.sql -o out.log  
    echo SQLCMD returned %errorlevel% to the command shell  
  
    :exit  
    ```  
  
 然后，在命令提示符处运行 `C:\windowsscript.bat`：  
  
 `C:\>windowsscript.bat`  
  
 `Running badscript.sql`  
  
 `== An error occurred`  
  
 `Running goodscript.sql`  
  
 `Running returnvalue.sql`  
  
 `SQLCMD returned 100 to the command shell`  
  
### <a name="g-using-sqlcmd-to-set-encryption-on-azure-sql-database"></a>G. 使用 sqlcmd 在 Azure SQL 数据库上设置加密  
 `sqlcmd`可以在与上的数据的连接上执行， [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 以指定加密和证书信任。 提供两个 "sqlcmd" 选项：  
  
-   -N 开关，客户端使用它来请求加密连接。 此选项等同于 ADO.net 选项 `ENCRYPT = true`。  
  
-   -C 开关，客户端用来将其配置为隐式信任服务器证书且不对其进行验证。 此选项等同于 ADO.net 选项 `TRUSTSERVERCERTIFICATE = true`。  
  
 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 服务并不支持 SQL Server 实例上所有可用的 `SET` 选项。 当将相应的 `SET` 选项设置为 `ON` 或 `OFF`时，下面的选项将引发错误：  
  
-   SET ANSI_DEFAULTS  
  
-   SET ANSI_NULLS  
  
-   SET REMOTE_PROC_TRANSACTIONS  
  
-   SET ANSI_NULL_DEFAULT  
  
 下面的 SET 选项虽然不会引发异常，但无法使用。 不推荐使用这些选项：  
  
-   SET CONCAT_NULL_YIELDS_NULL  
  
-   SET ANSI_PADDING  
  
-   SET QUERY_GOVERNOR_COST_LIMIT  
  
#### <a name="syntax"></a>语法  
 以下示例介绍了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 访问接口设置包括的情况： `ForceProtocolEncryption = False`、 `Trust Server Certificate = No`  
  
 使用 Windows 凭据进行连接并对通信加密：  
  
```  
SQLCMD -E -N  
  
```  
  
 使用 Windows 凭据进行连接并信任服务器证书：  
  
```  
SQLCMD -E -C  
  
```  
  
 使用 Windows 凭据进行连接、对通信加密并信任服务器证书：  
  
```  
SQLCMD -E -N -C  
  
```  
  
 以下示例介绍了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 访问接口设置包括的情况： `ForceProtocolEncryption = True`、 `TrustServerCertificate = Yes`。  
  
 使用 Windows 凭据进行连接、对通信加密并信任服务器证书：  
  
```  
SQLCMD -E  
  
```  
  
 使用 Windows 凭据进行连接、对通信加密并信任服务器证书：  
  
```  
SQLCMD -E -N  
  
```  
  
 使用 Windows 凭据进行连接、对通信加密并信任服务器证书：  
  
```  
SQLCMD -E -T  
  
```  
  
 使用 Windows 凭据进行连接、对通信加密并信任服务器证书：  
  
```  
SQLCMD -E -N -C  
  
```  
  
 如果访问接口指定了 `ForceProtocolEncryption = True` ，则启用加密，即使连接字符串中具有 `Encrypt=No` 。  
  
## <a name="see-also"></a>另请参阅  
 [sqlcmd 实用工具](../../tools/sqlcmd-utility.md)   
 [将 sqlcmd 与脚本变量结合使用](sqlcmd-use-with-scripting-variables.md)   
 [在查询编辑器中编辑 SQLCMD 脚本](edit-sqlcmd-scripts-with-query-editor.md)   
 [管理作业步骤](../../ssms/agent/manage-job-steps.md)   
 [创建 CmdExec 作业步骤](../../ssms/agent/create-a-cmdexec-job-step.md)  
  
  
