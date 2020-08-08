---
title: " (转换的项目设置)  (SybaseToSQL) |Microsoft Docs"
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: eeb80fa5-f530-4f21-beee-25f5a4b8ace6
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 1d2f1c02b9a9400236381cdd30fb3deb570500c1
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2020
ms.locfileid: "87934646"
---
# <a name="project-settings-conversion-sybasetosql"></a>项目设置（转换）(SybaseToSQL)
"**项目设置**" 对话框的 "转换" 页包含用于自定义 SSMA 将 Sybase 自适应服务器企业 (ASE) 语法转换为或 SQL Azure 语法的方式的设置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
"**项目设置**" 和 "**默认项目设置**" 对话框中提供了 "转换" 窗格：  
  
-   如果要指定所有 SSMA 项目的设置，请在 "**工具**" 菜单上，选择 "**默认项目设置**"，单击左侧窗格底部的 "**常规**"，然后单击 "**转换**"。  
  
-   若要指定当前项目的设置，请在 "**工具**" 菜单上选择 "**项目设置**"，单击左侧窗格底部的 "**常规**"，然后单击 "**转换**"。  
  
## <a name="miscellaneous-options"></a>其他选项  
**@@ERROR**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL Azure 和 ASE 使用不同的错误代码。  
  
使用此设置来指定消息的类型 (警告或错误) 当在 ASE 代码中遇到对 **@ @ERROR **的引用时，SSMA 在输出或错误列表窗格中显示。  
  
-   如果选择 "**转换" 并标记**为 "警告"，则 SSMA 将转换这些语句，并将其标记为警告注释。  
  
-   如果选择 "**标记并出错**"，则 SSMA 将跳过转换，并将语句标记为错误注释。  
  
在 "**模式**" 框中选择转换模式时，SSMA 将应用以下设置：  
  
**默认/乐观模式：** 转换并标记警告  
  
**完整模式：** 标记有错误  
  
**LIKE 运算符的转换**  
指定是否转换 LIKE 操作数，使其与 Sybase ASE 行为匹配。 要点是，Sybase 会以类似模式修整尾随空格。 解决方法是将右侧表达式强制转换为固定长度的数据类型，并具有最大精度。  
  
-   选择 "**简单转换**" 可在不进行任何更正的情况下转换表达式。  
  
-   若要使用 ASE 行为，请选择 "**强制转换为固定长度"。**  
  
在 "模式" 框中选择转换模式时，SSMA 将应用以下设置：  
  
**默认/乐观模式**：简单转换  
  
**完整模式**：强制转换为固定长度  
  
**将空字符串转换或强制转换为数值类型**  
指定如何处理数值类型为 datatype 参数的转换或强制转换表达式中的空字符串。 此设置可使用以下选项：  
  
-   选择 "**简单转换**" 可在不进行任何更正的情况下转换表达式。  
  
-   如果选择**空字符串作为零数字**，则字符串参数 {s} 将替换为区分大小写 (rtrim ( {s}，当为 0 else {s} 结束表达式时，将替换 ) # A3  
  
在 "模式" 框中选择转换模式时，SSMA 将应用以下设置：  
  
**默认/乐观模式**：简单转换  
  
**完整模式**：空字符串（零数字）  
  
**空值的串联**  
此设置指定如何转换字符串与 NULL 的串联。 可以为此特定设置设置以下选项：  
  
-   **用 ISNULL 函数 Wrap：** 如果设置了此选项，则串联中的每个非常量 "string_expression" 将用 ISNULL () string_expression 进行包装，并将 Null 替换为空字符串。  
  
-   **保留当前语法**  
  
在 "**模式**" 框中选择转换模式时，SSMA 将应用以下设置：  
  
**默认/乐观模式：** 保留当前语法  
  
**完整模式：** 用 ISNULL 函数换行  
  
**空字符串的转换**  
此设置指定如何转换空字符串。 可以为此特定设置设置以下选项：  
  
-   **将所有字符串表达式替换为空格**  
  
-   **用空格替换空字符串常量**  
  
-   若要使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /SQL Azure 行为，请选择 "**保留当前的语法**"。  
  
在 "**模式**" 框中选择转换模式时，SSMA 将应用以下设置：  
  
**默认/乐观模式：** 保留当前语法  
  
**完整模式：** 将所有字符串表达式替换为空格  
  
**转换和强制转换二进制字符串转换**  
二进制值到数字的转换可能会在不同的平台上返回不同的值。 例如，在 x86 处理器上，转换 (整数，0x00000100) 将在 ASE 中返回65536，在中返回 256 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 ASE 还根据字节顺序返回不同的值。  
  
使用此设置可控制 SSMA 如何转换包含二进制值的转换和 CASE 表达式：  
  
-   选择 "**简单转换**" 可以转换表达式，而无需任何警告或更正。 如果你知道 ASE 服务器的字节顺序不需要二进制值的任何更改，请使用此设置。  
  
-   选择 "**转换" 和 "更正**"，让 SSMA 转换和更正表达式以便在上使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 文本常量中的字节顺序将会反转。 所有其他二进制值 (如二进制变量和列) 将被标记为有错误。 如果你知道 ASE 服务器的字节顺序需要更改二进制值，请使用此值。  
  
-   选择 "**转换" 并标记**为 "警告"，让 SSMA 转换和更正表达式，并将所有已转换的表达式标记为警告注释。  
  
在 "**模式**" 框中选择转换模式时，SSMA 将应用以下设置：  
  
**默认模式：** 转换并标记警告  
  
**乐观模式：** 简单转换  
  
**完整模式：** 转换和更正  
  
**动态 SQL**  
使用此设置来指定消息的类型 (警告或错误) 在 ASE 代码中遇到动态 SQL 时，SSMA 在输出或错误列表窗格中显示。  
  
-   如果选择 "**转换" 并标记**为 "警告"，则 SSMA 将转换动态 SQL，并将语句标记为警告注释。  
  
-   如果选择 "**标记并出错**"，则 SSMA 将跳过转换，并将语句标记为错误注释。  
  
在 "**模式**" 框中选择转换模式时，SSMA 将应用以下设置：  
  
**默认/乐观模式：** 转换并标记警告  
  
**完整模式：** 标记有错误  
  
**相等性检查转换**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]如果 ANSI_NULLS 设置为 on/SQL Azure，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 当任何相等比较包含 null 值时，/SQL AZURE 返回未知。 如果 ANSI_NULLS 为 off，则当比较的列和表达式或两个表达式均为 null 时，包含 null 值的相等比较将返回 true。 默认情况下 (ANSINULL 关闭) Sybase ASE 相等比较的行为类似于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /SQL Azure ANSI_NULLS 关闭。  
  
-   如果选择**简单转换**，则 SSMA 会将 ASE 代码转换为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /SQL Azure 语法，而不会对 null 值进行额外检查。 如果 ANSI_NULLS 在/SQL Azure 中处于关闭状态， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或如果你想要根据每个大小修订相等性比较，请使用此设置。  
  
-   如果选择 "**考虑 null 值**"，则 SSMA 将使用 is NULL 和 IS NOT null 子句来添加对 null 值的检查。  
  
在 "**模式**" 框中选择转换模式时，SSMA 将应用以下设置：  
  
**默认/乐观模式：** 简单转换  
  
**完整模式：** 考虑 NULL 值  
  
**格式字符串**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL Azure 不再支持 PRINT 和 RAISERROR 语句中的*format_string*参数。 支持在字符串中直接放置可替换参数，然后在运行时替换参数的*format_string*变量。 相反， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 需要使用字符串文字或使用变量生成的字符串的完整字符串。 有关详细信息，请参阅联机丛书中的 "打印 ( [!INCLUDE[tsql](../../includes/tsql-md.md)]) " 主题 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
当 SSMA 遇到*format_string*参数时，它可以使用变量生成字符串文本，或创建新变量并使用该变量生成字符串。  
  
-   若要为 PRINT 和 RAISERROR 函数使用字符串文字，请选择 "**创建新字符串**"。  
  
    在此模式下，如果 PRINT 或 RAISERROR 语句未使用占位符和局部变量，则语句将保持不变。 %% (%% ) 的双百分比字符将更改为打印字符串文本中的单个百分号字符%。  
  
    如果 PRINT 或 RAISERROR 语句使用占位符和一个或多个局部变量，如以下示例中所示：  
  
    ```  
    PRINT 'Total: %1!%%', @percent  
    ```  
    SSMA 会将其转换为以下语法：  
  
    ```  
    PRINT 'Total: '+ CAST(@percent AS varchar(max)) + '%'  
    ```  
    如果*format_string*是一个变量，如以下语句中所示：  
  
    ```  
    PRINT @fmt, @arg1, @arg2  
    ```  
    SSMA 无法执行简单的字符串转换，必须创建新的变量：  
  
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
    当使用**Create new string** mode 时，SSMA 假设 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 选项 CONCAT_NULL_YIELDS_NULL 为 OFF。 因此，SSMA 不检查空参数。  
  
-   若要让 SSMA 为每个 PRINT 和 RAISERROR 语句生成一个新变量，并将该变量用于字符串值，请选择 "新建**变量**"。  
  
    在此模式下，如果 PRINT 或 RAISERROR 语句未使用占位符和局部变量，则 SSMA 会将所有双精度百分比 )  ( 字符替换为单百分比字符，以符合 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /SQL Azure 语法。  
  
    如果 PRINT 或 RAISERROR 语句使用占位符和一个或多个局部变量，如以下示例中所示：  
  
    ```  
    PRINT 'Total: %1!%%', @percent  
    ```  
    SSMA 会将其转换为以下语法：  
  
    ```  
    DECLARE @print_format_1 varchar(max)  
    SET @print_format_1 = 'Total: %1!%'  
    SET @print_format_1  =   
        REPLACE (@print_format_1, '%1!',   
        ISNULL(CAST (@percent AS VARCHAR(max)), ''))  
    PRINT @print_format_1  
    ```  
    如果*format_string*是一个变量，如以下语句中所示：  
  
    ```  
    PRINT @fmt, @arg1, @arg2  
    ```  
    SSMA 创建一个新变量，如下所示，检查每个参数中是否有 null 值：  
  
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
  
在 "**模式**" 框中选择转换模式时，SSMA 将应用以下设置：  
  
**默认/乐观模式：** 创建新字符串  
  
**完整模式：** 创建新变量  
  
**将显式值插入时间戳列**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL Azure 不支持将显式值插入时间戳列。  
  
-   若要从 INSERT 语句中排除时间戳列，请选择 "**排除列**"。  
  
-   若要在每次在 INSERT 语句中使用 timestamp 列时打印一条错误消息，请选择 "**标记并显示错误**"。 在此模式下，不会转换 INSERT 语句，并将其标记为错误注释。  
  
在 "**模式**" 框中选择转换模式时，SSMA 将应用以下设置：  
  
**默认/乐观模式：** 排除列  
  
**完整模式：** 标记有错误  
  
**存储过程中定义的临时对象**  
此设置指定在转换过程中出现在过程中的临时对象定义是否应存储在源元数据中。  
  
-   选择 **"是"** 以存储到元数据。  
  
-   如果不需要存储对象，请选择 "**否**"。  
  
**默认/乐观模式：** 是的  
  
**完整模式：** 不  
  
**代理表转换**  
指定 ASE 代理表是否转换为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /SQL Azure 表，或是否不进行转换以及代码是否标记有错误注释。  
  
-   选择 "**转换**" 将代理表转换为常规表。  
  
-   选择 "**标记为错误**"，以便只需将代理表代码标记为 "错误注释"。  
  
在 "**模式**" 框中选择转换模式时，SSMA 将应用以下设置：  
  
**默认/乐观/完整模式：** 标记有错误  
  
**RAISERROR 基本消息编号**  
ASE 用户消息存储在每个数据库中。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]用户消息集中存储，并通过**sys.databases**目录视图提供。 此外，ASE 用户消息从20000开始，但从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 50001 开始的错误消息。  
  
此设置指定要添加到 ASE 用户消息编号的数字，以将其转换为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用户消息。 如果在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **sys.databases**目录视图中有用户消息，则可能需要将此数字更改为较高的值。 这是因为，转换后的消息数不会与现有消息号冲突。  
  
注意以下事项：  
  
-   范围17000-19999 中的 ASE 消息来自 sysmessages 系统表，不进行转换。  
  
-   如果 RAISERROR 语句中引用的消息号是常量，则 SSMA 会将基本消息号添加到常量，以确定新的用户消息号。  
  
-   如果引用的消息号是变量或表达式，则 SSMA 将创建一个中间局部变量。  
  
-   在乐观模式下，SSMA 假设 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 选项 CONCAT_NULL_YIELDS_NULL 关闭，不会检查是否存在 NULL 参数。  
  
-   在完整模式下，SSMA 将检查是否有空参数。  
  
-   不转换具有 ERRORDATA*列表*的 RAISERROR。  
  
在 "**模式**" 框中选择转换模式时，SSMA 将应用以下设置：  
  
**默认/乐观/完整模式：** 30001  
  
**系统对象**  
使用此设置来指定消息的类型 (警告或错误，在该消息使用 ASE 系统对象时，将在输出或错误列表窗格中显示 SSMA) 。  
  
-   如果选择 "**转换" 并标记**为 "警告"，则 SSMA 会将引用转换为系统对象，并将带有警告注释的语句标记为。  
  
-   如果选择 "**标记并出错**"，则 SSMA 将不会将引用转换为系统对象，并且会将语句标记为带有错误注释。  
  
在 "**模式**" 框中选择转换模式时，SSMA 将应用以下设置：  
  
**默认/乐观模式：** 转换并标记警告  
  
**完整模式：** 标记有错误  
  
**解析的标识符**  
使用此设置可指定在无法解析标识符时 SSMA 显示在输出或错误列表窗格中 (警告或错误) 消息的类型。  
  
-   如果选择 "**转换" 并标记**为 "警告"，则 SSMA 将尝试将引用转换为未解析的标识符，并将语句标记为带有警告注释。  
  
-   如果选择 "**标记并出错**"，则 SSMA 将不会将引用转换为未解析的标识符，并将标记语句替换为错误注释。  
  
在 "**模式**" 框中选择转换模式时，SSMA 将应用以下设置：  
  
**默认/乐观模式：** 转换并标记警告  
  
**完整模式：** 标记有错误  
  
## <a name="system-function-options"></a>系统函数选项  
**CHARINDEX 函数**  
在 ASE 中，仅当所有输入表达式均为 NULL 时，CHARINDEX 才返回 NULL。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL Azure 如果任何输入表达式为 NULL，则返回 NULL。  
  
-   若要使用 ASE 行为，请选择 " **Replace function**"。 所有对 CHARINDEX 函数的调用都将替换为对 CHARINDEX_VARCHAR 或 CHARINDEX_NVARCHAR 用户定义函数的调用，该函数基于在架构名称的 2ss ' ) 下的用户数据库中创建的 (参数类型，以模拟 Sybase ASE 行为。  
  
-   若要使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /SQL Azure 行为，请选择 "**保留当前的语法**"。  
  
在 "**模式**" 框中选择转换模式时，SSMA 将应用以下设置：  
  
**默认/乐观模式：** 保留当前语法  
  
**完整模式：** Replace 函数  
  
**DATALENGTH 函数**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]当 DATALENGTH 函数返回的值为单个空格时，/SQL Azure 和 ASE 的值不同。 在这种情况下， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /SQL Azure 返回0，ASE 返回1。  
  
-   若要使用 ASE 行为，请选择 " **Replace function**"。 对 DATALENGTH 函数的所有调用都将替换为 CASE 表达式，以模拟 Sybase ASE 行为。  
  
-   若要使用默认 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /SQL Azure 行为，请选择 "**保留当前的语法**"。  
  
在 "**模式**" 框中选择转换模式时，SSMA 将应用以下设置：  
  
**默认/乐观模式：** 保留当前语法  
  
**完整模式：** Replace 函数  
  
**INDEX_COL 函数**  
ASE 支持 INDEX_COL 函数的可选*user_id*参数;但 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQL Azure 不支持此参数。 如果使用*user_id*参数，则此函数不能转换为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /SQL Azure 语法。  
  
-   若要使用 ASE 行为，请选择 "**转换函数**"。 如果代码包含*user_id*参数，SSMA 将显示错误。  
  
-   若要在每次遇到 INDEX_COL 时显示错误消息，请选择 "**标记并显示错误**"。 SSMA 不会将引用转换为函数，并且会将语句标记为带有错误注释。  
  
**默认/乐观/完整模式：** 标记有错误  
  
**INDEX_COLORDER 函数**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL Azure 没有 INDEX_COLORDER 的系统函数。  
  
-   若要使用 ASE 行为，请选择 "**转换函数**"。 对 INDEX_COLORDER 函数的所有调用都将被替换为具有相同名称的用户定义函数的调用， (在用户 ) 数据库中创建的同名 INDEX_COLORDER 将模拟 Sybase ASE 行为。  
  
-   若要在每次遇到 INDEX_COLORDER 时打印错误消息，请选择 "**标记并显示错误**"。 SSMA 不会将引用转换为函数，并且会将语句标记为带有错误注释。  
  
在 "**模式**" 框中选择转换模式时，SSMA 将应用以下设置：  
  
**默认/乐观/完整模式：** 标记有错误  
  
**左函数和右函数**  
Sybase 中的左函数和右函数对于负值长度参数的行为有所不同。  
  
-   若要使用 ASE 行为，请选择 " **Replace Function**"。 然后，将 length 参数替换为 CASE 表达式，该表达式将为负值返回 null 值。  
  
-   若要使用 SQL Server 行为，请选择 "**保留当前语法**"  
  
在 "**模式**" 框中选择转换模式时，SSMA 将应用以下设置：  
  
**默认/乐观模式：** 保留当前语法  
  
**完整模式：** Replace 函数  
  
> [!NOTE]  
> 如果 length 参数是文本值而不是复杂表达式，则无论项目设置如何，长度值始终替换为 null。  
  
**NEXT_IDENTITY 函数**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL Azure 没有 NEXT_IDENTITY 的系统函数。  
  
-   若要使用 ASE 行为，请选择 "**转换函数**"。 对 NEXT_IDENTITY 函数的所有调用都将替换为 expression (IDENT_CURRENT (参数值) + IDENT_INCR (参数值) 用于模拟 Sybase ASE 的行为。  
  
-   若要在每次遇到 NEXT_IDENTITY 时打印错误消息，请选择 "**标记并显示错误**"。 SSMA 不会将引用转换为函数，并且会将语句标记为带有错误注释。  
  
在 "**模式**" 框中选择转换模式时，SSMA 将应用以下设置：  
  
**默认/乐观/完整模式：** 标记有错误  
  
**PATINDEX 函数**  
指定是否转换 PATINDEX 函数以匹配 Sybase ASE 行为。 要点是，Sybase 修整搜索模式中的尾随空格。 解决方法是将值表达式强制转换为固定长度的数据类型，该类型具有最大精度，并将 rtrim 函数应用到搜索模式。  
  
-   若要使用 ASE 行为，请选择 "**使用**"。  
  
-   若要使用默认 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /SQL Azure 行为，请选择 "不**使用**"。  
  
在 "**模式**" 框中选择转换模式时，SSMA 将应用以下设置：  
  
**默认/乐观模式：** 不要使用  
  
**完整模式：** 用法  
  
**REPLICATE 函数**  
复制函数重复指定次数的字符串。 在 ASE 中，如果指定将字符串重复零次，则结果为 null。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /SQL Azure 中，结果为空字符串。  
  
-   若要使用 ASE 行为，请选择 " **Replace function**"。 对复制函数的所有调用都将被替换为对 REPLICATE_VARCHAR 或 REPLICATE_NVARCHAR 用户定义函数的调用，该函数基于在架构名称 2ss ' ) 下的用户数据库中创建的 (参数类型，以模拟 Sybase ASE 行为。  
  
-   若要使用默认 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /SQL Azure 行为，请选择 "**替换函数**"。  
  
在 "**模式**" 框中选择转换模式时，SSMA 将应用以下设置：  
  
**默认/乐观模式/完整模式：** Replace 函数  
  
**TRIM (LTRIM，RTRIM) 函数**  
此设置指定是否用 Sybase ASE 等效语法函数替换对剪裁 (LTRIM、RTRIM) 函数的调用或保留当前语法。 此特定设置有以下选项：  
  
-   **Replace 函数**  
  
-   **保留当前语法**  
  
在 "**模式**" 框中选择转换模式时，SSMA 将应用以下设置：  
  
**默认/乐观模式/完整模式：** Replace 函数  
  
**SUBSTRING 函数**  
在 ASE 中， `SUBSTRING(expression, start, length)` 如果指定的起始值大于表达式中的字符数，或者长度等于零，则函数返回 NULL。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /SQL Azure 中，等效表达式返回空字符串。  
  
-   若要使用 ASE 行为，请选择 " **Replace function**"。 对 SUBSTRING 函数的所有调用都将替换为对 SUBSTRING_VARCHAR 或 SUBSTRING_NVARCHAR 或 SUBSTRING_VARBINARY 用户定义函数的调用，该函数基于在用户数据库中在架构名称 2ss ' ) 中创建的 (参数类型来模拟 Sybase ASE 行为。  
  
-   若要使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /SQL Azure 行为，请选择 "**保留当前的语法**"。  
  
在 "**模式**" 框中选择转换模式时，SSMA 将应用以下设置：  
  
**默认/乐观模式：** 保留当前语法  
  
**完整模式：** Replace 函数  
  
## <a name="tables"></a>TABLES  
**添加主密钥**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]如果访问表没有主键或唯一索引，则在或 SQL Azure 表中创建新的主键。  
  
-   **默认模式**： False  
  
-   **乐观模式**： False  
  
-   **完整模式**： True  
  
> [!NOTE]  
> 连接到 SQL Azure 时，默认情况下为 True。  
  
## <a name="see-also"></a>另请参阅  
[用户界面参考 &#40;SybaseToSQL&#41;](../../ssma/sybase/user-interface-reference-sybasetosql.md)  
  
