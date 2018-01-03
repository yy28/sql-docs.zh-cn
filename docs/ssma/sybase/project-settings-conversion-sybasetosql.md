---
title: "项目设置 （转换） (SybaseToSQL) |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-sybase
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: eeb80fa5-f530-4f21-beee-25f5a4b8ace6
caps.latest.revision: "8"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 64845d9450c412ca975d541f1171a725271ec502
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="project-settings-conversion-sybasetosql"></a>项目设置 （转换） (SybaseToSQL)
转换页**项目设置**对话框中包含自定义如何 SSMA 将转换到的 Sybase 自适应 Server Enterprise (ASE) 语法的设置[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 语法。  
  
转换窗格位于**项目设置**和**默认项目设置**对话框：  
  
-   如果你想要对指定的所有的 SSMA 项目设置**工具**菜单上，选择**默认项目设置**，单击**常规**中左窗格中，然后单击底部**转换**。  
  
-   若要对指定为当前项目中，设置**工具**菜单上，选择**项目设置**，单击**常规**中左窗格中，然后单击底部**转换**。  
  
## <a name="miscellaneous-options"></a>其他选项  
**@@ERROR**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ SQL Azure 和 ASE 使用不同的错误代码。  
  
此设置用于指定当它遇到的引用，SSMA 显示在输出或错误列表窗格中的消息 （警告或错误） 的类型**@@ERROR**  ASE 代码中。  
  
-   如果你选择**转换并将标记警告**，SSMA 将转换语句并将其标记警告注释。  
  
-   如果你选择**出现错误的标记**，SSMA 将跳过转换并将标记与错误注释语句。  
  
当选择中的转换模式**模式**框，SSMA 适用以下设置：  
  
**默认/Optimistic 模式：**转换并将警告标记  
  
**完整模式：**出现错误的标记  
  
**LIKE 运算符的转换**  
指定是否将操作数与匹配 Sybase ASE 行为类似。 不同之处在于，Sybase 修剪 like 模式中的尾随空格。 解决方法是使右侧表达式的强制转换为固定的长度数据类型最大精度。  
  
-   选择**简单转换**将转换表达式而无需任何更正。  
  
-   若要使用 ASE 行为选择**强制转换为固定长度。**  
  
当在模式框中选择转换模式时，SSMA 适用以下设置：  
  
**默认/Optimistic 模式**： 简单的转换  
  
**完整模式**： 强制转换为固定长度  
  
**将转换或强制转换为数字类型的空字符串**  
指定如何处理与作为数据类型参数的数值类型的 CONVERT 或 CAST 表达式内的空或空白字符串。 将此设置提供以下选项：  
  
-   选择**简单转换**将转换表达式而无需任何更正。  
  
-   如果**空字符串为零数字**选中，那么字符串参数 {s} 将替换为事例 ltrim(rtrim({s})) 时""然后 0 else {s} 端表达式  
  
当在模式框中选择转换模式时，SSMA 适用以下设置：  
  
**默认/Optimistic 模式**： 简单的转换  
  
**完整模式**： 空字符串为零数值  
  
**串联的 NULL**  
此设置指定如何将转换为 null 的字符串串联。 为此特定设置，可以设置以下选项：  
  
-   **使用 ISNULL 函数包装：**如果此选项设置、 将与 ISNULL(string_expression) 包装每个非常量串联 string_expression 和 null 值将替换为空字符串。  
  
-   **保留当前的语法**  
  
当选择中的转换模式**模式**框，SSMA 适用以下设置：  
  
**默认/Optimistic 模式：**保留当前的语法  
  
**完整模式：**包装使用 ISNULL 函数  
  
**空字符串转换**  
此设置指定如何将空字符串转换。 为此特定设置，可以设置以下选项：  
  
-   **将替换为空间的所有字符串表达式**  
  
-   **空字符串常量替换空间**  
  
-   若要使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ SQL Azure 行为，选择**保留当前语法**。  
  
当选择中的转换模式**模式**框，SSMA 适用以下设置：  
  
**默认/Optimistic 模式：**保留当前的语法  
  
**完整模式：**替换空间的所有字符串表达式  
  
**转换和转换二进制字符串转换**  
二进制值转换为数字可以在不同平台上返回不同的值。 例如，在 x86 处理器，转换 （整数、 0x00000100） 返回 65536 ASE 中的，将在 256 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 ASE 也会返回不同的值，具体取决于字节顺序。  
  
使用此设置来控制如何 SSMA 将转换和包含二进制值的 CASE 表达式：  
  
-   选择**简单转换**要转换的表达式没有任何警告或更正。 如果您知道 ASE 服务器不需要任何更改的二进制值的字节顺序，请使用此设置。  
  
-   选择**转换和更正**能够将转换和更正上使用的表达式的 SSMA [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 将反转文本常量中的字节顺序。 所有其他二进制值 （如二进制变量和列） 都标有错误。 如果你知道 ASE 服务器需要更改为二进制值的字节顺序，请使用此值。  
  
-   选择**转换并将标记警告**能够将转换和更正表达式，并将所有标记的 SSMA 转换表达式与警告注释。  
  
当选择中的转换模式**模式**框，SSMA 适用以下设置：  
  
**默认模式：**转换并将警告标记  
  
**开放式模式：**简单转换  
  
**完整模式：**转换和更正  
  
**动态 SQL**  
此设置用于指定当它遇到 ASE 代码中的动态 SQL，SSMA 输出或错误列表窗格中显示的消息 （警告或错误） 的类型。  
  
-   如果你选择**转换并将标记警告**，SSMA 将转换动态 SQL，并将标记与警告注释语句。  
  
-   如果你选择**出现错误的标记**，SSMA 将跳过转换并将标记与错误注释语句。  
  
当选择中的转换模式**模式**框，SSMA 适用以下设置：  
  
**默认/Optimistic 模式：**转换并将警告标记  
  
**完整模式：**出现错误的标记  
  
**相等性检查转换**  
在[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ SQL Azure，ANSI_NULLS 设置处于打开状态，如果[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ SQL Azure 返回未知时任何相等性比较包含一个 null 值。 如果 ANSI_NULLS 为 off，包含 null 值的相等性比较返回 true 时比较的列和表达式或两个表达式都是 null。 通过默认 （ANSINULL 关闭） Sybase ASE 相等比较的行为类似于[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ 具有 ANSI_NULLS OFF 的 SQL Azure。  
  
-   如果你选择**简单转换**，SSMA 会将转换到的 ASE 代码[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ SQL Azure 而无需额外检查是否有空值的语法。 使用此设置，如果 ANSI_NULLS 处于关闭状态中[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ SQL Azure 或如果你想要修改的每个用例基础上的相等性比较。  
  
-   如果你选择**考虑 NULL 值**，SSMA 将通过使用 IS NULL 和 IS NOT NULL 子句中添加 null 值的检查。  
  
当选择中的转换模式**模式**框，SSMA 适用以下设置：  
  
**默认/Optimistic 模式：**简单转换  
  
**完整模式：**请考虑 NULL 值  
  
**格式字符串**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ SQL Azure 不再支持*format_string* PRINT 和 RAISERROR 语句中的自变量。 *Format_string*变量支持直接在字符串中，将可替换参数，然后替换在运行时的参数。 相反，[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]需要通过使用字符串文本或使用的变量基于生成的字符串的完整字符串。 有关详细信息，请参阅"打印 ([!INCLUDE[tsql](../../includes/tsql_md.md)])"中的主题[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]联机丛书。  
  
当 SSMA 遇到*format_string*自变量，它可以生成字符串文本使用变量或创建一个新的变量和生成通过使用该变量的字符串。  
  
-   若要为 PRINT 和 RAISERROR 函数使用字符串文本，请选择**创建新的字符串**。  
  
    在此模式下，如果打印或 RAISERROR 语句不使用占位符和本地变量，该语句不变。 Double 百分比字符 （%） 都会更改为打印字符串文本中的单个百分比字符 %。  
  
    如果打印或 RAISERROR 语句使用占位符和一个或多个本地变量，如如以下示例所示：  
  
    ```  
    PRINT 'Total: %1!%%', @percent  
    ```  
    SSMA 会将它转换为以下语法：  
  
    ```  
    PRINT 'Total: '+ CAST(@percent AS varchar(max)) + '%'  
    ```  
    如果*format_string*是变量，如以下语句所示：  
  
    ```  
    PRINT @fmt, @arg1, @arg2  
    ```  
    SSMA 不能执行简单的字符串转换，而且必须创建一个新的变量：  
  
    ```  
    DECLARE @print_format_1 varchar(max)  
    SET @print_format_1  =   
        REPLACE (@fmt, '%%', '%')  
    SET @print_format_1  =   
        REPLACE (@print_format_1, '%1!',   
        CAST (@arg1 AS varchar(max)))  
    SET @print_format_1  =   
        REPLACE (@print_format_1, '%2!',   
        CAST (@arg2 AS varchar(max)))  
    PRINT @print_format_1  
    ```  
    当它使用**创建新的字符串**模式下，SSMA 假定[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]选项 CONCAT_NULL_YIELDS_NULL 为 OFF。 因此，SSMA 不检查空参数。  
  
-   如果希望 SSMA 生成一个新的变量为每个 PRINT 和 RAISERROR 语句，以及如何将该变量的字符串值，请选择**创建新变量**。  
  
    在此模式下，如果打印或 RAISERROR 语句不使用占位符和局部变量，SSMA 所有 double 百分比字符 （%） 将使用替换单个百分比字符，以符合[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ SQL Azure 语法。  
  
    如果打印或 RAISERROR 语句使用占位符和一个或多个本地变量，如如以下示例所示：  
  
    ```  
    PRINT 'Total: %1!%%', @percent  
    ```  
    SSMA 会将它转换为以下语法：  
  
    ```  
    DECLARE @print_format_1 varchar(max)  
    SET @print_format_1 = 'Total: %1!%'  
    SET @print_format_1  =   
        REPLACE (@print_format_1, '%1!',   
        ISNULL(CAST (@percent AS VARCHAR(max)), ''))  
    PRINT @print_format_1  
    ```  
    如果*format_string*是变量，如以下语句所示：  
  
    ```  
    PRINT @fmt, @arg1, @arg2  
    ```  
    SSMA 检查每个自变量中的 null 值，如下所示，创建一个新变量：  
  
    ```  
    DECLARE @print_format_1 varchar(max)  
    SET @print_format_1  =   
        REPLACE (@fmt, '%%', '%')  
    SET @print_format_1  =   
        REPLACE (@print_format_1, '%1!',   
        ISNULL(CAST (@arg1 AS varchar(max)),''))  
    SET @print_format_1  =   
        REPLACE (@print_format_1, '%2!',   
        ISNULL(CAST (@arg2 AS varchar(max)),''))  
    PRINT @print_format_1  
    ```  
  
当选择中的转换模式**模式**框，SSMA 适用以下设置：  
  
**默认/Optimistic 模式：**创建新的字符串  
  
**完整模式：**创建新变量  
  
**将显式值插入时间戳列**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ SQL Azure 不支持将显式值插入时间戳列。  
  
-   若要从 INSERT 语句中排除时间戳列，选择**排除列**。  
  
-   若要打印一条错误消息时间戳列是 INSERT 语句中每个时间，请选择**出现错误的标记**。 在此模式下，INSERT 语句将不会转换，并将使用错误注释标记。  
  
当选择中的转换模式**模式**框，SSMA 适用以下设置：  
  
**默认/Optimistic 模式：**排除列  
  
**完整模式：**出现错误的标记  
  
**存储过程中定义的临时对象**  
此设置指定是否应在转换期间的源元数据中存储的临时对象定义在过程中显示的。  
  
-   选择**是**将存储到元数据。  
  
-   选择**否**如果不需要存储对象。  
  
**默认/开放式模式：**是  
  
**完整模式：**否  
  
**代理表转换**  
指定是否 ASE 代理表将转换为[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ SQL Azure 表或是否不转换，并带有错误注释标记的代码。  
  
-   选择**转换**将代理表转换为普通表。  
  
-   选择**出现错误的标记**只需将标记带有错误注释的代理表代码。  
  
当选择中的转换模式**模式**框，SSMA 适用以下设置：  
  
**默认/Optimistic/完整模式：**出现错误的标记  
  
**RAISERROR 基消息号**  
ASE 用户消息存储在每个数据库。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]用户消息集中存储和可用于通过**sys.messages**目录视图。 此外 ASE 用户消息开始 20000，但[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]错误消息开始 50001。  
  
此设置指定的编号，以将添加到 ASE 用户消息编号，以将其转换为[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]用户消息。 如果你[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]有用户消息**sys.messages**目录视图中，你可能需要将此数字更改为较高的值。 这是因此转换后的消息号不与现有消息号冲突。  
  
请注意以下事项：  
  
-   在范围内 17000 19999 ASE 消息来自 sysmessages 系统表，不进行转换。  
  
-   如果 RAISERROR 语句中引用的消息数为常量，SSMA 将向常量，以确定新的用户消息号添加基本的消息数。  
  
-   如果变量或表达式，被引用的消息数，SSMA 将创建一个中间的本地变量。  
  
-   在乐观模式下，SSMA 假定[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]选项 CONCAT_NULL_YIELDS_NULL 处于关闭状态，并不使任何检查 null 自变量。  
  
-   在完全模式下，SSMA 检查 null 参数。  
  
-   RAISERROR 与 ERRORDATA*列表*不会进行转换。  
  
当选择中的转换模式**模式**框，SSMA 适用以下设置：  
  
**默认/开放式/完整模式：** 30001  
  
**系统对象**  
此设置用于指定当它遇到 ASE 系统对象的使用，SSMA 将显示在输出或错误列表窗格中的消息 （警告或错误） 的类型。  
  
-   如果你选择**转换并将标记警告**，SSMA 会将转换对系统对象的引用，并将标记与警告注释语句。  
  
-   如果你选择**出现错误的标记**，SSMA 不会将对系统对象的引用转换并将标记与错误注释语句。  
  
当选择中的转换模式**模式**框，SSMA 适用以下设置：  
  
**默认/Optimistic 模式：**转换并将警告标记  
  
**完整模式：**出现错误的标记  
  
**未解析的标识符**  
此设置用于指定当它不能解析标识符，SSMA 输出或错误列表窗格中显示的消息 （警告或错误） 的类型。  
  
-   如果你选择**转换并将标记警告**，SSMA 将尝试将引用转换为未解析的标识符，并且会将标记为警告注释语句。  
  
-   如果你选择**出现错误的标记**，SSMA 不会将对未解析的标识符的引用转换并将标记与错误注释语句。  
  
当选择中的转换模式**模式**框，SSMA 适用以下设置：  
  
**默认/Optimistic 模式：**转换并将警告标记  
  
**完整模式：**出现错误的标记  
  
## <a name="system-function-options"></a>系统函数选项  
**CHARINDEX 函数**  
在 ASE，CHARINDEX 返回 NULL，仅当输入的所有表达式都都为 NULL。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ 如果任何输入的表达式为 NULL，则 SQL Azure 将返回 NULL。  
  
-   若要使用的 ASE 行为，请选择**将函数**。 对 CHARINDEX 函数的所有调用都替换对 CHARINDEX_VARCHAR 或 CHARINDEX_NVARCHAR 基于传递的参数的类型 （用户在数据库中创建架构名称 s2ss 下） 来模拟 Sybase ASE 行为的用户定义函数的调用。  
  
-   若要使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ SQL Azure 行为，选择**保留当前语法**。  
  
当选择中的转换模式**模式**框，SSMA 适用以下设置：  
  
**默认/Optimistic 模式：**保留当前的语法  
  
**完整模式：**将函数  
  
**Datalength 之外函数**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ SQL Azure 和 ASE 不同的值为一个空格时 datalength 之外函数返回的值中。 在这种情况下， [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ SQL Azure，则返回 0 并 ASE 返回 1。  
  
-   若要使用的 ASE 行为，请选择**将函数**。 对 datalength 之外函数的所有调用将都替换与用例表达式模拟 Sybase ASE 行为。  
  
-   若要使用默认[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ SQL Azure 行为，选择**保留当前语法**。  
  
当选择中的转换模式**模式**框，SSMA 适用以下设置：  
  
**默认/Optimistic 模式：**保留当前的语法  
  
**完整模式：**将函数  
  
**INDEX_COL 函数**  
ASE 支持一个可选*user_id*参数 INDEX_COL 函数中; 但是， [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ SQL Azure 不支持此参数。 如果你使用*user_id* ，此函数不能将参数转换为[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ SQL Azure 语法。  
  
-   若要使用的 ASE 行为，请选择**转换函数**。 如果代码包含*user_id*自变量，SSMA 将显示错误。  
  
-   若要在每次遇到该 INDEX_COL，则显示一条错误消息，请选择**出现错误的标记**。 SSMA 不会将对该函数的引用转换，并将标记与错误注释语句。  
  
**默认/Optimistic/完整模式：**出现错误的标记  
  
**INDEX_COLORDER 函数**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ SQL Azure 没有 INDEX_COLORDER 系统函数。  
  
-   若要使用的 ASE 行为，请选择**转换函数**。 对 INDEX_COLORDER 函数的所有调用都替换对具有相同名称 （在采用架构名称 s2ss 的用户数据库中创建） 的 INDEX_COLORDER 它们模拟 Sybase ASE 行为的用户定义函数的调用。  
  
-   若要在每次遇到该 INDEX_COLORDER 打印一条错误消息，请选择**出现错误的标记**。 SSMA 不会将对该函数的引用转换，并将标记与错误注释语句。  
  
当选择中的转换模式**模式**框，SSMA 适用以下设置：  
  
**默认/Optimistic/完整模式：**出现错误的标记  
  
**LEFT 和 RIGHT 函数**  
左侧和右侧函数中 Sybase 负长度参数行为不同。  
  
-   若要使用的 ASE 行为，请选择**Replace 函数**。 长度参数然后替换 CASE 表达式将返回 null 作为负数的值。  
  
-   若要使用的 SQL Server 行为，请选择**保留当前的语法**  
  
当选择中的转换模式**模式**框，SSMA 适用以下设置：  
  
**默认/Optimistic 模式：**保留当前的语法  
  
**完整模式：**将函数  
  
> [!NOTE]  
> 如果长度参数为文字值而不是复杂的表达式，则长度值将始终替换 null 而不考虑项目设置。  
  
**NEXT_IDENTITY 函数**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ SQL Azure 没有 NEXT_IDENTITY 系统函数。  
  
-   若要使用的 ASE 行为，请选择**转换函数**。 对 NEXT_IDENTITY 函数的所有调用都替换表达式 （IDENT_CURRENT(parameter Value) + IDENT_INCR(parameter Value) 它们模拟 Sybase ASE 行为。  
  
-   若要在每次遇到该 NEXT_IDENTITY 打印一条错误消息，请选择**出现错误的标记**。 SSMA 不会将对该函数的引用转换，并将标记与错误注释语句。  
  
当选择中的转换模式**模式**框，SSMA 适用以下设置：  
  
**默认/Optimistic/完整模式：**出现错误的标记  
  
**PATINDEX 函数**  
指定是否将转换 PATINDEX 函数，以匹配 Sybase ASE 行为。 不同之处在于，Sybase 修剪搜索模式中的尾随空格。 解决方法是使强制转换为固定长度数据类型和最大精度和应用 rtrim 函数要搜索模式的值表达式。  
  
-   若要使用 ASE 行为选择**使用**。  
  
-   若要使用默认[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ SQL Azure 行为，选择**不使用**。  
  
当选择中的转换模式**模式**框，SSMA 适用以下设置：  
  
**默认/Optimistic 模式：**不使用  
  
**完整模式：**使用  
  
**REPLICATE 函数**  
REPLICATE 函数重复指定次数的字符串。 在 ASE 中，如果指定要重复字符串零次，结果为 null。 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ SQL Azure，结果为空字符串。  
  
-   若要使用的 ASE 行为，请选择**将函数**。 对复制的函数的所有调用都替换对 REPLICATE_VARCHAR 或 REPLICATE_NVARCHAR 基于传递的参数的类型 （用户在数据库中创建架构名称 s2ss 下） 来模拟 Sybase ASE 行为的用户定义函数的调用。  
  
-   若要使用默认[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ SQL Azure 行为，选择**Replace 函数**。  
  
当选择中的转换模式**模式**框，SSMA 适用以下设置：  
  
**默认/Optimistic 模式/完整模式：**将函数  
  
**TRIM （LTRIM、 RTRIM） 函数**  
此设置指定是否将对 Trim （LTRIM、 RTRIM） 函数的调用替换为 Sybase ASE 等效语法函数，或要保留当前语法。 存在为此特定的设置提供了以下选项：  
  
-   **将函数**  
  
-   **保留当前的语法**  
  
当选择中的转换模式**模式**框，SSMA 适用以下设置：  
  
**默认/Optimistic 模式/完整模式：**将函数  
  
**子字符串函数**  
ASE，该函数中`SUBSTRING(expression, start, length)`如果指定开始值大于表达式中的字符数，或如果长度等于零，则返回 NULL。 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ SQL Azure 的等效表达式返回一个空字符串。  
  
-   若要使用的 ASE 行为，请选择**将函数**。 对 SUBSTRING 函数的所有调用都替换对 SUBSTRING_VARCHAR 或 SUBSTRING_NVARCHAR 或 SUBSTRING_VARBINARY 基于传递的参数的类型 （用户在数据库中创建架构名称 s2ss 下） 来模拟 Sybase ASE 行为的用户定义函数的调用。  
  
-   若要使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ SQL Azure 行为，选择**保留当前语法**。  
  
当选择中的转换模式**模式**框，SSMA 适用以下设置：  
  
**默认/Optimistic 模式：**保留当前的语法  
  
**完整模式：**将函数  
  
## <a name="tables"></a>TABLES  
**添加主键**  
创建中的新主键[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 表，如果访问表没有主键或唯一索引。  
  
-   **默认模式**: False  
  
-   **开放式模式**: False  
  
-   **完整模式**: True  
  
> [!NOTE]  
> 当连接到 SQL Azure，它是默认情况下，True。  
  
## <a name="see-also"></a>另请参阅  
[用户界面参考 &#40;SybaseToSQL &#41;](../../ssma/sybase/user-interface-reference-sybasetosql.md)  
  
