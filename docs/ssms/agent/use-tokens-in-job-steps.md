---
title: 在作业步骤中使用标记 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms-agent
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- job steps [SQL Server Agent]
- security [SQL Server Agent], enabling alert job step tokens
- SQL Server Agent jobs, job steps
- tokens [SQL Server]
- escape macros [SQL Server Agent]
ms.assetid: 105bbb66-0ade-4b46-b8e4-f849e5fc4d43
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 01eb7c21ff82d25e49982d5acd700ed9226f53bd
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "37971359"
---
# <a name="use-tokens-in-job-steps"></a>在作业步骤中使用标记
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL 数据库托管实例](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支持大多数但并非所有 SQL Server 代理功能。 有关详细信息，请参阅 [Azure SQL 数据库托管实例与 SQL Server 之间的 T-SQL 差异](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 通过代理，你可以在 [!INCLUDE[tsql](../../includes/tsql_md.md)] 作业步骤脚本中使用标记。 如果在编写作业步骤时使用标记，则可以为您提供编写软件程序时使用变量所提供的灵活性。 在作业步骤脚本中插入令牌之后， [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理便会在运行时 [!INCLUDE[tsql](../../includes/tsql_md.md)] 子系统执行作业步骤之前替换此不标记。  
  
> [!IMPORTANT]  
> 从 [!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)] Service Pack 1 开始， [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理作业步骤的标记语法已发生更改。 因此，作业步骤中使用的所有标记现在必须附带转义宏，否则，这些作业步骤将会失败。 下列部分说明了使用转义宏和更新使用标记的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理作业步骤：“了解标记用法”、“[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理标记和宏”以及“更新作业步骤以使用宏”。 此外，使用方括号调用 [!INCLUDE[ssVersion2000](../../includes/ssversion2000_md.md)] 代理作业步骤标记的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 语法（例如，“`[DATE]`”）也已发生更改。 现在，必须用括号将令牌名称括起来，并在令牌语法的开头加上美元符号 (`$`)。 例如：  
>   
> `$(ESCAPE_`*宏名*`(DATE))`  
  
## <a name="understanding-using-tokens"></a>了解标记用法  
  
> [!IMPORTANT]  
> 对 Windows 事件日志拥有写入权限的任何 Windows 用户都可以访问由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理警报或 WMI 警报激活的作业步骤。 为了防范此安全隐患，默认情况下，可以在由警报激活的作业中使用的特定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理标记已被禁用。 这些标记包括：A-DBN、A-SVR、A-ERR、A-SEV、A-MSG 和 WMI(property)****。 请注意，在此版本中，对标记的使用扩展至所有警报。  
>   
> 如果您需要使用这些标记，请首先确保只有可信任的 Windows 安全组（如 Administrators 组）成员才对安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 的计算机的事件日志拥有写入权限。 然后在对象资源管理器中右键单击“SQL Server 代理”，选择“属性”，并在“警报系统”页上选择“为警报的所有作业响应替换标记”以启用这些标记。  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理标记替换简单且有效： [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理以准确的文字字符串值替换标记。 所有标记都是区分大小写的。 您的作业步骤必须考虑到这一点，并且将所用标记正确地用引号引起来或将替换字符串转换为正确的数据类型。  
  
例如，您可以在作业步骤中使用以下语句输出数据库的名称：  
  
`PRINT N'Current database name is $(ESCAPE_SQUOTE(A-DBN))' ;`  
  
在此示例中，针对 **A-DBN** 标记插入 **ESCAPE_SQUOTE** 宏。 运行时， **A-DBN** 标记将替换为相应的数据库名称。 转义宏将转义可能会在标记替换字符串中意外传递的任何单引号。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理在最终字符串中将一个单引号替换为两个单引号。  
  
例如，如果用来替换标记的已传递字符串为 `AdventureWorks2012'SELECT @@VERSION --`，则由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理作业步骤执行的命令将为：  
  
`PRINT N'Current database name is AdventureWorks2012''SELECT @@VERSION --' ;`  
  
在这种情况下，不会执行已插入的语句 `SELECT @@VERSION`。 相反，多余的单引号会导致服务器将已插入语句作为字符串进行分析。 如果标记替换字符串不包含单引号，则不会转义任何字符，并且包含此标记的作业步骤会按预期方式执行。  
  
若要在作业步骤中调试标记使用，请使用 `PRINT N'$(ESCAPE_SQUOTE(SQLDIR))'` 之类的输出语句并将作业步骤输出保存到文件或表。 可以使用“作业步骤属性”对话框的“高级”页指定作业步骤输出文件或表。  
  
## <a name="sql-server-agent-tokens-and-macros"></a>SQL Server 代理标记和宏  
下列各表列出并说明了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理支持的标记和宏。  
  
### <a name="sql-server-agent-tokens"></a>SQL Server 代理标记  
  
|标记|描述|  
|---------|---------------|  
|**(A-DBN)**|数据库名称。 如果作业由某个警报运行，则在作业步骤中，数据库名称值将自动替换此标记。|  
|**(A-SVR)**|服务器名称。 如果作业由某个警报运行，则在作业步骤中，服务器名称值将自动替换此标记。|  
|**(A-ERR)**|错误号。 如果作业由某个警报运行，则在作业步骤中，错误号值将自动替换此标记。|  
|**(A-SEV)**|错误严重性。 如果作业由某个警报运行，则在作业步骤中，错误严重性值将自动替换此标记。|  
|**(A-MSG)**|消息正文。 如果作业由某个警报运行，则在作业步骤中，消息正文值将自动替换此标记。|  
|**(JOBNAME)**|作业的名称。|  
|**(STEPNAME)**|步骤的名称。|  
|**(DATE)**|当前日期（以 YYYYMMDD 格式表示）。|  
|**(INST)**|实例名。 对于默认实例，此标记将具有默认实例名称：MSSQLSERVER。|  
|**(JOBID)**|作业 ID。|  
|**(MACH)**|计算机名称。|  
|**(MSSA)**|主 SQLServerAgent 服务名称。|  
|**(OSCMD)**|用于运行 **CmdExec** 作业步骤的程序的前缀。|  
|**(SQLDIR)**|安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 的目录。 默认情况下，此值为 C:\Program Files\Microsoft SQL Server\MSSQL。|  
|**(SQLLOGDIR)**|SQL Server 错误日志文件夹路径的替换标记 – 例如 $(ESCAPE_SQUOTE(SQLLOGDIR))。|  
|**(STEPCT)**|此步骤已执行的次数（不包括重试）。 步骤命令可以使用它来强制终止多步骤循环。|  
|**(STEPID)**|步骤 ID。|  
|**(SRVR)**|运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]的计算机的名称。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 实例是命名实例，此值将包含实例名。|  
|**(TIME)**|当前时间（以 HHMMSS 格式表示）。|  
|**(STRTTM)**|作业开始执行的时间（以 HHMMSS 格式表示）。|  
|**(STRTDT)**|作业开始执行的日期（以 YYYYMMDD 格式表示）。|  
|(WMI(property))****|对于为响应 WMI 警报而运行的作业，属性值由 property 指定。 例如，`$(WMI(DatabaseName))` 为导致警报运行的 WMI 事件提供 **DatabaseName** 属性值。|  
  
### <a name="sql-server-agent-escape-macros"></a>SQL Server 代理转义宏  
  
|转义宏|描述|  
|-----------------|---------------|  
|**$(ESCAPE_SQUOTE(***token_name***))**|转义标记替换字符串中的单引号 (')。 将一个单引号替换为两个单引号。|  
|**$(ESCAPE_DQUOTE(***token_name***))**|转义标记替换字符串中的双引号 (")。 将一个双引号替换为两个双引号。|  
|**$(ESCAPE_RBRACKET(***token_name***))**|转义标记替换字符串中的右方括号 (])。 将一个右方括号替换为两个右方括号。|  
|**$(ESCAPE_NONE(***token_name***))**|替换标记而不转义字符串中的任何字符。 提供此宏是为了在仅需要来自受信任用户的标记替换字符串的环境中支持向后兼容。 有关详细信息，请参阅本主题后面的“更新作业步骤以使用宏”。|  
  
## <a name="updating-job-steps-to-use-macros"></a>更新作业步骤以使用宏  
从 [!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)] Service Pack 1 开始，包含不带转义宏的标记的作业步骤将失败，并返回错误消息，指示作业步骤包含一个或多个必须在作业运行之前使用宏进行更新的标记。  
  
[!INCLUDE[msCoName](../../includes/msconame_md.md)] 知识库文章 915845： [在 SQL Server 2005 Service Pack 1 中使用标记的 SQL Server 代理作业步骤将失败](http://support.microsoft.com/kb/915845)提供的脚本。可以使用此脚本通过 **ESCAPE_NONE** 宏更新所有使用标记的作业步骤。 使用此脚本之后，我们建议你尽快查看使用标记的作业步骤，并将 **ESCAPE_NONE** 宏替换为适用于作业步骤上下文的转义宏。  
  
下表说明 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理如何处理标记替换。 若要启用或禁用警报标记替换，请在对象资源管理器中右键单击“SQL Server 代理”，选择“属性”，然后在“警报系统”页上选中或清除“为警报的所有作业响应替换标记”复选框。  
  
|标记语法|启用警报标记替换|禁用警报标记替换|  
|----------------|------------------------------|-------------------------------|  
|使用转义宏|成功替换作业中的所有标记。|不替换由警报激活的标记。 这些标记包括 A-DBN、A-SVR、A-ERR、A-SEV、A-MSG 和 WMI(property)****。 成功替换其他静态标记。|  
|不使用转义宏|任何包含标记的作业均失败。|任何包含标记的作业均失败。|  
  
## <a name="token-syntax-update-examples"></a>标记语法更新示例  
  
### <a name="a-using-tokens-in-non-nested-strings"></a>A. 在非嵌套字符串中使用标记  
以下示例显示如何使用相应的转义宏更新简单的非嵌套脚本。 在运行更新脚本之前，以下作业步骤脚本使用作业步骤标记输出相应的数据库名称：  
  
`PRINT N'Current database name is $(A-DBN)' ;`  
  
在运行更新脚本之后，在 `ESCAPE_NONE` 标记之前插入 `A-DBN` 宏。 由于使用单引号分隔输出字符串，因此必须通过插入 `ESCAPE_SQUOTE` 宏来更新作业步骤，如下所示：  
  
`PRINT N'Current database name is $(ESCAPE_SQUOTE(A-DBN))' ;`  
  
### <a name="b-using-tokens-in-nested-strings"></a>B. 在嵌套字符串中使用标记  
对于在嵌套字符串或语句中使用标记的作业步骤脚本，应将嵌套语句重写为多个语句，然后插入相应的转义宏。  
  
例如，请看以下作业步骤，此步骤使用 `A-MSG` 标记并且尚未使用转义宏进行更新：  
  
`PRINT N'Print ''$(A-MSG)''' ;`  
  
在运行更新脚本之后，针对此标记插入 `ESCAPE_NONE` 宏。 但在这种情况下，必须按如下方式在不使用嵌套的情况下重写脚本，并插入 `ESCAPE_SQUOTE` 宏以正确转义可能在标记替换字符串中传递的分隔符：  
  
<pre>DECLARE @msgString nvarchar(max)  
SET @msgString = '$(ESCAPE_SQUOTE(A-MSG))'  
SET @msgString = QUOTENAME(@msgString,'''')  
PRINT N'Print ' + @msgString ;</pre>  
  
另请注意，在此示例中 QUOTENAME 函数设置引号字符。  
  
### <a name="c-using-tokens-with-the-escapenone-macro"></a>C. 将标记与 ESCAPE_NONE 宏配合使用  
以下示例是从 `job_id` 表中检索 `sysjobs` 并使用 `JOBID` 标记填充 `@JobID` 变量（在脚本的前面部分已声明为 binary 数据类型）的脚本的一部分。 注意，由于 binary 数据类型不需要分隔符，因此将 `ESCAPE_NONE` 宏与 `JOBID` 标记配合使用。 运行更新脚本之后，无需更新此作业步骤。  
  
<pre>SELECT * FROM msdb.dbo.sysjobs  
WHERE @JobID = CONVERT(uniqueidentifier, $(ESCAPE_NONE(JOBID))) ;</pre>  
  
## <a name="see-also"></a>另请参阅  
[执行作业](../../ssms/agent/implement-jobs.md)  
[管理作业步骤](../../ssms/agent/manage-job-steps.md)  
  
