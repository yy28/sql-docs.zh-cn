---
title: "RAISERROR (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 02/21/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- RAISERROR
- RAISERROR_TSQL
- RAISEERROR_TSQL
dev_langs: TSQL
helpviewer_keywords:
- sysmessages system table
- errors [SQL Server], RAISERROR statement
- user-defined error messages [SQL Server]
- system flags
- generating errors [SQL Server]
- TRY block [SQL Server]
- recording errors
- ad hoc messages
- RAISERROR statement
- CATCH block
- messages [SQL Server], RAISERROR statement
ms.assetid: 483588bd-021b-4eae-b4ee-216268003e79
caps.latest.revision: "73"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: af9f82f9b550ecd366c10562199c606bf8ff0c9c
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="raiserror-transact-sql"></a>RAISERROR (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  生成错误消息并启动会话的错误处理。 RAISERROR 可以引用用户定义的消息存储在 sys.messages 目录视图或动态生成一条消息。 该消息作为服务器错误消息返回到调用应用程序，或返回到 TRY…CATCH 构造的关联 CATCH 块。 新的应用程序应使用[引发](../../t-sql/language-elements/throw-transact-sql.md)相反。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
RAISERROR ( { msg_id | msg_str | @local_variable }  
    { ,severity ,state }  
    [ ,argument [ ,...n ] ] )  
    [ WITH option [ ,...n ] ]  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
RAISERROR ( { msg_str | @local_variable }  
    { ,severity ,state }  
    [ ,argument [ ,...n ] ] )  
    [ WITH option [ ,...n ] ]  
```  
  
## <a name="arguments"></a>参数  
 *msg_id*  
 用户定义的错误消息号存储在使用 sp_addmessage sys.messages 目录视图中。 用户定义的错误消息的错误号应大于 50000。 当*msg_id*未指定，则 RAISERROR 引发一条错误消息，50000 错误号。  
  
 *msg_str*  
 是用户定义的消息格式必须为类似于**printf** C 标准库中的函数。 该错误消息最长可以有 2,047 个字符。 如果该消息包含的字符数等于或超过 2,048 个，则只能显示前 2,044 个并添加一个省略号以表示该消息已被截断。 请注意，由于内部存储行为的缘故，代替参数使用的字符数比输出所显示的字符数要多。 例如，替换参数的*%d*使用 2 赋的值实际生成的消息字符串中的一个字符，但却还内部占用的存储的三个其他字符。 此存储要求减少了可用于消息输出的字符数。  
  
 当*msg_str*指定，则 RAISERROR 引发一条错误消息，50000 错误号。  
  
 *msg_str*是使用可选的嵌入的转换规范的字符的字符串。 每个转换规范定义如何格式化和放入一个字段中的转换规范位置自变量列表中的值是*msg_str*。 转换规格的格式如下：  
  
 % [[*flag*] [*width*] [. *精度*] [{h | l}]]*类型*  
  
 可以在中使用的参数*msg_str*是：  
  
 *flag*  
  
 用于确定被替换值的间距和对齐的代码。  
  
|代码|前缀或对齐|Description|  
|----------|-----------------------------|-----------------|  
|-（减）|左对齐|在给定字段宽度内左对齐参数值。|  
|+ （加）|符号前缀|如果参数值为有符号类型，则在参数值的前面加上加号（+）或减号（-）。|  
|0（零）|零填充|在达到最小宽度之前在输出前面加上零。 如果出现 0 和减号 (-)，将忽略 0。|  
|#（数字）|对 x 或 X 的十六进制类型使用 0x 前缀|当使用 o、x 或 X 格式时，数字符号 (#) 标志在任何非零值的前面分别加上 0、0x 或 0X。 当 d、i 或 u 的前面有数字符号 (#) 标志时，将忽略该标志。|  
|' '（空白）|空格填充|如果输出值有符号且为正，则在该值前加空格。 如果包含在加号（+）标志中，则忽略该标志。|  
  
 *width*  
  
 定义放置参数值的字段的最小宽度的整数。 如果参数值的长度是等于还是长于*宽度*，没有空白打印值。 如果值为短于*宽度*，值填充到中指定的长度*宽度*。  
  
 星号 (*) 表示宽度由参数列表中的相关参数指定，该宽度必须为整数值。  
  
 *精度*  
  
 从字符串值的参数值中得到的最大字符数。 例如，如果一个字符串具有五个字符并且精度为 3，则只使用字符串值的前三个字符。  
  
 对于整数值，*精度*是最小位数打印。  
  
 星号 (*) 表示精度由参数列表中的相关参数指定，该精度必须为整数值。  
  
 {h | l}*类型*  
  
 用于字符类型 d i、 o、 s、 x、 X 或 u，并创建**shortint** (h) 或**longint** (l) 值。  
  
|类型规范|表示|  
|------------------------|----------------|  
|d 或 i|带符号的整数|  
|o|无符号的八进制数|  
|s|字符串|  
|u|无符号的整数|  
|x 或 X|无符号的十六进制数|  
  
> [!NOTE]  
>  在最初为定义的基于这些类型规范**printf** C 标准库中的函数。 在 RAISERROR 消息字符串映射到中使用的类型规范[!INCLUDE[tsql](../../includes/tsql-md.md)]数据类型，在中使用的规范时**printf**映射到 C 语言数据类型。 键入在中使用的规范**printf**不支持 RAISERROR 时[!INCLUDE[tsql](../../includes/tsql-md.md)]不具有类似于关联的 C 数据类型的数据类型。 例如， *%p*因为 RAISERROR 不支持指针的规范[!INCLUDE[tsql](../../includes/tsql-md.md)]没有指针数据类型。  
  
> [!NOTE]  
>  若要将值转换为[!INCLUDE[tsql](../../includes/tsql-md.md)] **bigint**数据类型，指定**%i64d**。  
  
 **@** *local_variable*  
 是任何有效的字符数据类型，包含与相同的方式在设置格式的字符串变量*msg_str*。 **@ * * * local_variable*必须**char**或**varchar**，或能够隐式转换为这些数据类型。  
  
 severity  
 用户定义的与该消息关联的严重级别。 使用时*msg_id*引发使用 sp_addmessage 创建用户定义消息，RAISERROR 上指定的严重性替代 sp_addmessage 中指定的严重性。  
  
 任何用户都可以指定 0 到 18 之间的严重级别。 只能由 sysadmin 固定服务器角色或用户具有 ALTER TRACE 权限的成员指定的严重性级别从 19 到 25。 若要使用 19 到 25 之间的严重级别，必须选择 WITH LOG 选项。 将小于 0 的严重级别解释为 0。 将大于 25 的严重级别解释为 25。  
  
> [!CAUTION]  
>  20 到 25 之间的严重级别被认为是致命的。 如果遇到致命的严重级别，客户端连接将在收到消息后终止，并将错误记录到错误日志和应用程序日志。  
  
 可以指定“-1”来返回与以下示例中所示的错误关联的严重性值。  
  
```  
RAISERROR (15600,-1,-1, 'mysp_CreateCustomer');  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 Msg 15600, Level 15, State 1, Line 1   
 An invalid parameter or option was specified for procedure 'mysp_CreateCustomer'.
 ```  
  
 State  
 0 到 255 之间的整数。 负值默认为 1。 不应使用值大于 255。 
  
 如果在多个位置引发相同的用户定义错误，则针对每个位置使用唯一的状态号有助于找到引发错误的代码段。  
  
 *argument*  
 是用于替换中定义的变量的参数*msg_str*或对应于的消息*msg_id*。 可以有 0 个或更多个替换参数，但替换参数的总数不能超过 20。 每个替换参数可以是本地的变量或任何这些数据类型： **tinyint**， **smallint**， **int**， **char**， **varchar**， **nchar**， **nvarchar**，**二进制**，或**varbinary**。 不支持其他数据类型。  
  
 *option*  
 错误的自定义选项，可以是下表中的任一值。  
  
|“值”|Description|  
|-----------|-----------------|  
|LOG|错误日志和实例的应用程序日志中记录错误[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)]。 记录到错误日志的错误目前被限定为最多 440 字节。 只有 sysadmin 固定的服务器角色或具有 ALTER TRACE 权限的用户的成员可以指定 WITH LOG。<br /><br /> [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], [!INCLUDE[ssSDS](../../includes/sssds-md.md)]|  
|NOWAIT|将消息立即发送给客户端。<br /><br /> [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], [!INCLUDE[ssSDS](../../includes/sssds-md.md)]|  
|SETERROR|集 @@ERROR和 ERROR_NUMBER 值到*msg_id*或 50000，而不考虑严重性级别。<br /><br /> [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], [!INCLUDE[ssSDS](../../includes/sssds-md.md)]|  
  
## <a name="remarks"></a>注释  
 RAISERROR 生成的错误与[!INCLUDE[ssDE](../../includes/ssde-md.md)]代码生成的错误的运行方式相同。 RAISERROR 指定的值报告的 ERROR_LINE、 ERROR_MESSAGE、 ERROR_NUMBER、 ERROR_PROCEDURE、 ERROR_SEVERITY、 ERROR_STATE 和 @@ERROR系统函数。 当 RAISERROR 在严重级别为 11 或更高的情况下在 TRY 块中运行，它便会将控制传输至关联的 CATCH 块。 如果 RAISERROR 在下列情况下运行，便会将错误返回到调用方：  
  
-   在任何 TRY 块的作用域之外运行。  
  
-   在严重级别为 10 或更低的情况下在 TRY 块中运行。  
  
-   在严重级别为 20 或更高的情况下终止数据库连接。  
  
 CATCH 块可以使用 RAISERROR 来再次引发调用 CATCH 块的错误，方法是使用 ERROR_NUMBER 和 ERROR_MESSAGE 之类的系统函数检索原始错误消息。 @@ERROR默认设置为 0 的严重级别的消息从 1 到 10。  
  
 当*msg_id*指定用户定义的消息可从 sys.messages 目录视图，RAISERROR 进程使用的相同规则被应用到指定用户定义消息的文本的文本列中的消息使用*msg_str*。 用户定义消息文本可以包含转换规格，并且 RAISERROR 将参数值映射到转换规格。 使用 sp_addmessage 添加用户定义的错误消息和 sp_dropmessage 删除用户定义的错误消息。  
  
 RAISERROR 可以代替 PRINT 将消息返回到调用应用程序。 RAISERROR 支持类似于的功能的字符替换**printf** C 标准库中的函数时[!INCLUDE[tsql](../../includes/tsql-md.md)]PRINT 语句却没有。 PRINT 语句不受 TRY 块的影响，而在严重级别为 11 到 19 的情况下在 TRY 块中运行的 RAISERROR 会将控制传输至关联的 CATCH 块。 指定严重级别为 10 或更低以使用 RAISERROR 返回 TRY 块中的消息，而不必调用 CATCH 块。  
  
 通常，连续的参数替换连续的转换规格；第一个参数替换第一个转换规格，第二个参数替换第二个转换规格，以此类推。 例如，在以下 `RAISERROR` 语句中，第一个参数 `N'number'` 替换第一个转换规格 `%s`，第二个参数 `5` 替换第二个转换规格 `%d.`。  
  
```  
RAISERROR (N'This is message %s %d.', -- Message text.  
           10, -- Severity,  
           1, -- State,  
           N'number', -- First argument.  
           5); -- Second argument.  
-- The message text returned is: This is message number 5.  
GO  
```  
  
 如果为转换规格的宽度或精度指定了星号 (*)，则要用于宽度或精度的值被指定为整数参数值。 在这种情况下，一个转换规格最多可以使用三个参数，分别用作宽度、精度和代替值。  
  
 例如，下列两个 `RAISERROR` 语句都返回相同的字符串。 一个指定参数列表中的宽度值和精度值；另一个指定转换规格中的宽度值和精度值。  
  
```  
RAISERROR (N'<\<%*.*s>>', -- Message text.  
           10, -- Severity,  
           1, -- State,  
           7, -- First argument used for width.  
           3, -- Second argument used for precision.  
           N'abcde'); -- Third argument supplies the string.  
-- The message text returned is: <<    abc>>.  
GO  
RAISERROR (N'<\<%7.3s>>', -- Message text.  
           10, -- Severity,  
           1, -- State,  
           N'abcde'); -- First argument supplies the string.  
-- The message text returned is: <<    abc>>.  
GO  
```  
  
## <a name="examples"></a>示例  
  
### <a name="a-returning-error-information-from-a-catch-block"></a>A. 从 CATCH 块返回错误消息  
 以下代码示例显示如何在 `RAISERROR` 块中使用 `TRY` 使执行跳至关联的 `CATCH` 块中。 它还显示如何使用 `RAISERROR` 返回有关调用 `CATCH` 块的错误的信息。  
  
> [!NOTE]  
>  RAISERROR 仅能生成状态为 1 到 127 的错误。 由于[!INCLUDE[ssDE](../../includes/ssde-md.md)]可能引发状态为 0 的错误，因此，建议您先检查由 ERROR_STATE 返回的错误状态，然后将它作为一个值传递给状态参数 RAISERROR。  
  
```  
BEGIN TRY  
    -- RAISERROR with severity 11-19 will cause execution to   
    -- jump to the CATCH block.  
    RAISERROR ('Error raised in TRY block.', -- Message text.  
               16, -- Severity.  
               1 -- State.  
               );  
END TRY  
BEGIN CATCH  
    DECLARE @ErrorMessage NVARCHAR(4000);  
    DECLARE @ErrorSeverity INT;  
    DECLARE @ErrorState INT;  
  
    SELECT   
        @ErrorMessage = ERROR_MESSAGE(),  
        @ErrorSeverity = ERROR_SEVERITY(),  
        @ErrorState = ERROR_STATE();  
  
    -- Use RAISERROR inside the CATCH block to return error  
    -- information about the original error that caused  
    -- execution to jump to the CATCH block.  
    RAISERROR (@ErrorMessage, -- Message text.  
               @ErrorSeverity, -- Severity.  
               @ErrorState -- State.  
               );  
END CATCH;  
```  
  
### <a name="b-creating-an-ad-hoc-message-in-sysmessages"></a>B. 在 sys.messages 中创建即席消息  
 下面的示例演示如何引发 sys.messages 目录视图中存储的消息。 通过使用消息添加到 sys.messages 目录视图`sp_addmessage`系统存储过程作为消息号`50005`。  
  
```  
sp_addmessage @msgnum = 50005,  
              @severity = 10,  
              @msgtext = N'<\<%7.3s>>';  
GO  
RAISERROR (50005, -- Message id.  
           10, -- Severity,  
           1, -- State,  
           N'abcde'); -- First argument supplies the string.  
-- The message text returned is: <<    abc>>.  
GO  
sp_dropmessage @msgnum = 50005;  
GO  
```  
  
### <a name="c-using-a-local-variable-to-supply-the-message-text"></a>C. 使用局部变量提供消息文本  
 以下代码示例显示如何使用局部变量为 `RAISERROR` 语句提供消息文本。  
  
```  
DECLARE @StringVariable NVARCHAR(50);  
SET @StringVariable = N'<\<%7.3s>>';  
  
RAISERROR (@StringVariable, -- Message text.  
           10, -- Severity,  
           1, -- State,  
           N'abcde'); -- First argument supplies the string.  
-- The message text returned is: <<    abc>>.  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [内置函数 (Transact-SQL)](~/t-sql/functions/functions.md)   
 [DECLARE @local_variable (Transact-SQL)](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [PRINT (Transact-SQL)](../../t-sql/language-elements/print-transact-sql.md)   
 [sp_addmessage &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmessage-transact-sql.md)   
 [sp_dropmessage &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-dropmessage-transact-sql.md)   
 [sys.messages (Transact-SQL)](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md)   
 [xp_logevent &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/xp-logevent-transact-sql.md)   
 [@@ERROR (Transact-SQL)](../../t-sql/functions/error-transact-sql.md)   
 [ERROR_LINE (Transact-SQL)](../../t-sql/functions/error-line-transact-sql.md)   
 [ERROR_MESSAGE (Transact-SQL)](../../t-sql/functions/error-message-transact-sql.md)   
 [ERROR_NUMBER (Transact-SQL)](../../t-sql/functions/error-number-transact-sql.md)   
 [ERROR_PROCEDURE (Transact-SQL)](../../t-sql/functions/error-procedure-transact-sql.md)   
 [ERROR_SEVERITY (Transact-SQL)](../../t-sql/functions/error-severity-transact-sql.md)   
 [ERROR_STATE &#40;Transact SQL &#41;](../../t-sql/functions/error-state-transact-sql.md)   
 [TRY...CATCH (Transact-SQL)](../../t-sql/language-elements/try-catch-transact-sql.md)  
  
  

