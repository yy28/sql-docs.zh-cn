---
title: 项目设置 （转换） (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: eeb80fa5-f530-4f21-beee-25f5a4b8ace6
caps.latest.revision: 8
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: dc51a7149b1af55db3a79bc1dae811a2480e351f
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2018
ms.locfileid: "40395027"
---
# <a name="project-settings-conversion-sybasetosql"></a>项目设置（转换）(SybaseToSQL)
转换页**项目设置**对话框中包含自定义如何 SSMA 将转换 Sybase Adaptive Server Enterprise (ASE) 语法来设置[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 的语法。  
  
转换窗格中现已推出**项目设置**并**默认项目设置**对话框：  
  
-   如果你想要在指定的所有的 SSMA 项目设置**工具**菜单中，选择**默认项目设置**，单击**常规**底部的左窗格中，然后单击**转换**。  
  
-   若要在指定的当前项目中，设置**工具**菜单中，选择**项目设置**，单击**常规**底部的左窗格中，然后单击**转换**。  
  
## <a name="miscellaneous-options"></a>其他选项  
**@@ERROR**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/ SQL Azure 和 ASE 使用不同的错误代码。  
  
使用此设置指定的消息 （警告或错误） 时遇到的引用，SSMA 显示输出或错误列表窗格中的类型 **@@ERROR**  ASE 代码中。  
  
-   如果选择**转换并将标记为具有警告**，SSMA 将转换语句并将其标记具有警告注释。  
  
-   如果选择**含有错误标记**，SSMA 将跳过转换并将标记具有错误的注释语句。  
  
当选择中的转换模式**模式下**框，SSMA 适用以下设置：  
  
**默认/Optimistic 模式：** 转换并将标记为警告  
  
**完整模式：** 含有错误标记  
  
**LIKE 运算符的转换**  
指定是否将操作数以匹配 Sybase ASE 行为等。 不同之处在于 Sybase 修剪 like 模式中的尾随空格。 解决方法是使右侧表达式的强制转换为固定的长度数据类型最大精度。  
  
-   选择**简单的转换**转换表达式而无需任何更正。  
  
-   若要使用 ASE 行为选择**强制转换为固定长度。**  
  
在模式框中选择转换模式，SSMA 将应用以下设置：  
  
**默认/Optimistic 模式**： 简单的转换  
  
**完整模式**： 强制转换为固定长度  
  
**将转换或强制转换为数字类型的空字符串**  
指定如何处理空或空白字符串与数值类型作为数据类型参数的 CONVERT 或 CAST 表达式内。 此设置有以下选项：  
  
-   选择**简单的转换**转换表达式而无需任何更正。  
  
-   如果**空字符串为零的数字**选中，则将字符串参数 {s} 将替换事例 ltrim(rtrim({s})) 时""然后 0 其他 {s} 结束表达式  
  
在模式框中选择转换模式，SSMA 将应用以下设置：  
  
**默认/Optimistic 模式**： 简单的转换  
  
**完整模式**： 空字符串为零的数字  
  
**串联的 NULL**  
此设置指定如何将转换字符串串联为 null。 为此特定设置，可以设置以下选项：  
  
-   **使用 ISNULL 函数包装：** 如果设置此选项，将使用 ISNULL(string_expression) 包装每个非常量在串联中的 string_expression 和 null 值将替换为空字符串。  
  
-   **保留当前的语法**  
  
当选择中的转换模式**模式下**框，SSMA 适用以下设置：  
  
**默认/Optimistic 模式：** 保留当前的语法  
  
**完整模式：** 使用 ISNULL 函数包装  
  
**将空字符串转换**  
此设置指定如何将空字符串转换。 为此特定设置，可以设置以下选项：  
  
-   **所有字符串表达式都替换为空格**  
  
-   **替换空间为空字符串常量**  
  
-   若要使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/ SQL Azure 行为，选择**保留当前语法**。  
  
当选择中的转换模式**模式下**框，SSMA 适用以下设置：  
  
**默认/Optimistic 模式：** 保留当前的语法  
  
**完整模式：** 替换空间的所有字符串表达式  
  
**转换和强制转换二进制字符串转换**  
为数字的二进制值的转换可以在不同平台上返回不同的值。 例如，在 x86 处理器，CONVERT (integer，0x00000100) 返回 65536 ASE 中的，将在 256 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 ASE 还会返回不同的值，具体取决于字节顺序。  
  
使用此设置以控制如何 SSMA 将转换和包含二进制值的 CASE 表达式：  
  
-   选择**简单的转换**转换表达式而无需任何警告或更正。 如果您知道 ASE 服务器具有不需要任何更改的二进制值的字节顺序，请使用此设置。  
  
-   选择**转换和更正**能够转换和更正上使用的表达式的 SSMA [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 将反转文本常量中的字节顺序。 所有其他二进制值 （如二进制变量和列） 都标有错误。 如果知道 ASE 服务器需要对二进制值的更改的字节顺序，请使用此值。  
  
-   选择**转换并将标记为具有警告**具有 SSMA 转换和更正表达式，并将所有标记已转换警告注释使用的表达式。  
  
当选择中的转换模式**模式下**框，SSMA 适用以下设置：  
  
**默认模式：** 转换并将标记为警告  
  
**乐观模式：** 简单的转换  
  
**完整模式：** 转换和更正  
  
**动态 SQL**  
使用此设置指定的 SSMA 显示时遇到的 ASE 代码中的动态 SQL 中输出或错误列表窗格中的消息 （警告或错误） 的类型。  
  
-   如果选择**转换并将标记为具有警告**，SSMA 将转换的动态 SQL，并将标记与警告注释语句。  
  
-   如果选择**含有错误标记**，SSMA 将跳过转换并将标记具有错误的注释语句。  
  
当选择中的转换模式**模式下**框，SSMA 适用以下设置：  
  
**默认/Optimistic 模式：** 转换并将标记为警告  
  
**完整模式：** 含有错误标记  
  
**相等性检查转换**  
在中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/ SQL Azure，ANSI_NULLS 设置为 on 时，如果[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/ 任何相等性比较包含 null 值时，SQL Azure 将返回 UNKNOWN。 如果 ANSI_NULLS 为 off，包含 null 值的相等性比较返回 true 时的比较列和表达式或两个表达式都是 null。 通过 Sybase ASE (ANSINULL OFF) 的默认相等比较的行为类似于[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/ SQL Azure 与 ANSI_NULLS OFF。  
  
-   如果选择**简单的转换**，SSMA 会将转换到 ASE 代码[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/ SQL Azure 而无需额外检查 null 值的语法。 当 ANSI_NULLS 为 off 中使用此设置[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/ SQL Azure 或你想要修改的每个用例的基础上的相等性比较。  
  
-   如果选择**考虑 NULL 值**，SSMA 使用 IS NULL 和 IS NOT NULL 子句将添加检查 null 值。  
  
当选择中的转换模式**模式下**框，SSMA 适用以下设置：  
  
**默认/Optimistic 模式：** 简单的转换  
  
**完整模式：** 请考虑为 NULL 值  
  
**格式字符串**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/ 不再支持 SQL Azure *format_string* PRINT 和 RAISERROR 语句中的参数。 *Format_string*变量支持直接在字符串中，将可替换参数，然后替换在运行时参数。 相反，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]需要通过使用字符串文字或使用变量来生成一个字符串的完整字符串。 有关详细信息，请参阅"打印 ([!INCLUDE[tsql](../../includes/tsql-md.md)])"中的主题[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]联机丛书。  
  
当遇到 SSMA *format_string*参数，它可以是生成字符串文本使用的变量或者创建新的变量，然后使用该变量生成的字符串。  
  
-   若要为 PRINT 和 RAISERROR 函数使用字符串文本，请选择**创建新的字符串**。  
  
    在此模式下，如果 PRINT 或 RAISERROR 语句不使用占位符和本地变量，该语句不变。 双精度百分比字符 （%） 都会更改为打印字符串文本中的单个百分比字符 %。  
  
    如果 PRINT 或 RAISERROR 语句使用占位符和一个或多个本地变量，例如如以下示例所示：  
  
    ```  
    PRINT 'Total: %1!%%', @percent  
    ```  
    SSMA 会将其转换为以下语法：  
  
    ```  
    PRINT 'Total: '+ CAST(@percent AS varchar(max)) + '%'  
    ```  
    如果*format_string*是变量，如下面的语句中：  
  
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
    当使用**创建新的字符串**模式下，SSMA 假定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]选项 CONCAT_NULL_YIELDS_NULL 为 OFF。 因此，SSMA 不会检查 null 参数。  
  
-   SSMA 生成新的变量为每个 PRINT 和 RAISERROR 语句，以及如何将该变量的字符串值，请选中**创建新变量**。  
  
    在此模式下，如果 PRINT 或 RAISERROR 语句不使用占位符和局部变量，SSMA 替换所有的双精度百分比字符 （%） 百分比的单个字符以符合[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/ SQL Azure 语法。  
  
    如果 PRINT 或 RAISERROR 语句使用占位符和一个或多个本地变量，例如如以下示例所示：  
  
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
    如果*format_string*是变量，如下面的语句中：  
  
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
  
当选择中的转换模式**模式下**框，SSMA 适用以下设置：  
  
**默认/Optimistic 模式：** 创建新的字符串  
  
**完整模式：** 创建新变量  
  
**将显式值插入时间戳列**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/ SQL Azure 不支持将显式值插入时间戳列。  
  
-   若要从 INSERT 语句中排除时间戳列，请选择**排除列**。  
  
-   若要在 INSERT 语句中的时间戳列是每次打印一条错误消息，请选择**含有错误标记**。 在此模式下，INSERT 语句不会进行转换，并且将标有错误的注释。  
  
当选择中的转换模式**模式下**框，SSMA 适用以下设置：  
  
**默认/Optimistic 模式：** 排除列  
  
**完整模式：** 含有错误标记  
  
**存储过程中定义的临时对象**  
此设置指定是否应在转换期间源元数据中存储的临时对象定义的过程中出现。  
  
-   选择**是**将存储到元数据。  
  
-   选择**否**如果不需要存储对象。  
  
**默认/乐观模式：** 是  
  
**完整模式：** 否  
  
**代理表转换**  
指定是否 ASE 代理表将转换为[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/ SQL Azure 表，或者不会转换并使用错误注释标记代码。  
  
-   选择**转换**若要将代理表转换为常规表。  
  
-   选择**含有错误标记**只需将代理表代码与错误的注释标记。  
  
当选择中的转换模式**模式下**框，SSMA 适用以下设置：  
  
**默认/Optimistic/Full 模式：** 含有错误标记  
  
**RAISERROR 基本消息数**  
ASE 用户消息存储在每个数据库。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用户消息集中存储和可通过**sys.messages**目录视图。 除了 ASE 用户消息开始 20000，但[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]错误消息开始 50001。  
  
此设置指定的编号，以将添加到 ASE 用户消息号将其转换为[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]用户消息。 如果你[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中具有用户消息**sys.messages**目录视图中，您可能需要将此数字更改为较高的值。 这是转换后的消息号不与现有消息号冲突。  
  
请注意以下事项：  
  
-   在范围内 17000 19999 ASE 消息来自 sysmessages 系统表，不进行转换。  
  
-   如果 RAISERROR 语句中引用的消息数为常量，SSMA 将添加到要确定新的用户消息号的常量的基本消息号。  
  
-   如果引用的消息数是变量或表达式，SSMA 将创建一个中间的本地变量。  
  
-   在乐观模式下，SSMA 假定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]CONCAT_NULL_YIELDS_NULL 选项处于关闭状态，并使任何 null 参数检查。  
  
-   在完整模式下，SSMA 检查 null 参数。  
  
-   RAISERROR 与 ERRORDATA*列表*不转换。  
  
当选择中的转换模式**模式下**框，SSMA 适用以下设置：  
  
**默认/乐观/Full 模式：** 30001  
  
**系统对象**  
使用此设置指定的 SSMA 显示时遇到 ASE 系统对象的使用输出或错误列表窗格中的消息 （警告或错误） 的类型。  
  
-   如果选择**转换并将标记为具有警告**，SSMA 将转换对系统对象的引用，并会将标记为警告注释语句。  
  
-   如果选择**含有错误标记**，SSMA 不会对系统对象的引用将转换并将标记具有错误的注释语句。  
  
当选择中的转换模式**模式下**框，SSMA 适用以下设置：  
  
**默认/Optimistic 模式：** 转换并将标记为警告  
  
**完整模式：** 含有错误标记  
  
**未解析的标识符**  
使用此设置指定的 SSMA 显示在输出或错误列表窗格中时无法解析标识符的消息 （警告或错误） 的类型。  
  
-   如果选择**转换并将标记为具有警告**，SSMA 将尝试将引用转换为无法解析标识符，并且会将标记为警告注释语句。  
  
-   如果选择**含有错误标记**，SSMA 将不转换对无法解析标识符的引用，并会将标记为具有错误的注释语句。  
  
当选择中的转换模式**模式下**框，SSMA 适用以下设置：  
  
**默认/Optimistic 模式：** 转换并将标记为警告  
  
**完整模式：** 含有错误标记  
  
## <a name="system-function-options"></a>系统函数选项  
**CHARINDEX 函数**  
在 ASE 中，则 CHARINDEX 返回 NULL，仅当输入的所有表达式都均为 NULL。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/ 如果任何输入的表达式为 NULL SQL Azure 将返回 NULL。  
  
-   若要使用 ASE 行为，请选择**替换为函数**。 对 CHARINDEX 函数的所有调用都替换对 CHARINDEX_VARCHAR 或 CHARINDEX_NVARCHAR 基于传递的参数类型 （在数据库中创建用户架构名称 's2ss 下） 来模拟 Sybase ASE 行为的用户定义函数的调用。  
  
-   若要使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/ SQL Azure 行为，选择**保留当前语法**。  
  
当选择中的转换模式**模式下**框，SSMA 适用以下设置：  
  
**默认/Optimistic 模式：** 保留当前的语法  
  
**完整模式：** 替换函数  
  
**DATALENGTH 函数**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] / SQL Azure 和 ASE 中的值为单个空格时，DATALENGTH 函数返回的值不同。 在这种情况下， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/ SQL Azure，则返回 0 和 ASE 返回 1。  
  
-   若要使用 ASE 行为，请选择**替换为函数**。 使用 CASE 表达式，以模拟 Sybase ASE 行为来替换对 DATALENGTH 函数的所有调用。  
  
-   若要使用默认[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/ SQL Azure 行为，选择**保留当前语法**。  
  
当选择中的转换模式**模式下**框，SSMA 适用以下设置：  
  
**默认/Optimistic 模式：** 保留当前的语法  
  
**完整模式：** 替换函数  
  
**INDEX_COL 函数**  
ASE 支持一个可选*user_id*参数 INDEX_COL 函数中; 但是， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/ SQL Azure 不支持此参数。 如果您使用*user_id*参数，此函数不能转换为[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/ SQL Azure 语法。  
  
-   若要使用 ASE 行为，请选择**将函数转换**。 如果代码包含*user_id*参数，SSMA 将显示错误。  
  
-   若要每次遇到该 INDEX_COL 显示一条错误消息，请选择**含有错误标记**。 SSMA 将不转换对函数的引用，并将标记与错误注释语句。  
  
**默认/Optimistic/Full 模式：** 含有错误标记  
  
**INDEX_COLORDER 函数**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/ SQL Azure 不具有 INDEX_COLORDER 系统函数。  
  
-   若要使用 ASE 行为，请选择**将函数转换**。 对 INDEX_COLORDER 函数的所有调用都替换对具有相同名称 （在进行架构名称 's2ss 的用户数据库中创建） 的 INDEX_COLORDER 它们模拟 Sybase ASE 行为的用户定义函数的调用。  
  
-   若要打印一条错误消息，每次遇到该 INDEX_COLORDER，选择**含有错误标记**。 SSMA 将不转换对函数的引用，并将标记与错误注释语句。  
  
当选择中的转换模式**模式下**框，SSMA 适用以下设置：  
  
**默认/Optimistic/Full 模式：** 含有错误标记  
  
**LEFT 和 RIGHT 函数**  
Left 和 Right 函数在 Sybase 中的行为不同负长度参数。  
  
-   若要使用 ASE 行为，请选择**替换为函数**。 长度参数然后替换 CASE 表达式将返回负的值为 null。  
  
-   若要使用 SQL Server 行为，请选择**保留当前的语法**  
  
当选择中的转换模式**模式下**框，SSMA 适用以下设置：  
  
**默认/Optimistic 模式：** 保留当前的语法  
  
**完整模式：** 替换函数  
  
> [!NOTE]  
> 如果长度参数为文本值而不是复杂表达式，长度值始终被替换而不考虑项目设置为 null。  
  
**NEXT_IDENTITY 函数**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/ SQL Azure 不具有 NEXT_IDENTITY 系统函数。  
  
-   若要使用 ASE 行为，请选择**转换函数**。 对 NEXT_IDENTITY 函数的所有调用将被都替换表达式 （IDENT_CURRENT(parameter Value) + IDENT_INCR(parameter Value) 它们模拟 Sybase ASE 行为。  
  
-   若要打印一条错误消息，每次遇到该 NEXT_IDENTITY，选择**含有错误标记**。 SSMA 将不转换对函数的引用，并将标记与错误注释语句。  
  
当选择中的转换模式**模式下**框，SSMA 适用以下设置：  
  
**默认/Optimistic/Full 模式：** 含有错误标记  
  
**PATINDEX 函数**  
指定是否将转换 PATINDEX 函数以匹配 Sybase ASE 行为。 不同之处在于 Sybase 修剪搜索模式中的尾随空格。 解决方法是进行强制转换为固定长度数据类型最大精度，并应用 rtrim 函数要搜索模式的值表达式。  
  
-   若要使用 ASE 行为选择**使用**。  
  
-   若要使用默认[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/ SQL Azure 行为，选择**不要使用**。  
  
当选择中的转换模式**模式下**框，SSMA 适用以下设置：  
  
**默认/Optimistic 模式：** 不使用  
  
**完整模式：** 使用  
  
**REPLICATE 函数**  
REPLICATE 函数重复指定次数的字符串。 在 ASE 中，如果指定要重复字符串零次，则结果为 null。 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/ SQL Azure，则结果为空字符串。  
  
-   若要使用 ASE 行为，请选择**替换为函数**。 对复制函数的所有调用都替换对 REPLICATE_VARCHAR 或 REPLICATE_NVARCHAR 基于传递的参数类型 （在数据库中创建用户架构名称 's2ss 下） 来模拟 Sybase ASE 行为的用户定义函数的调用。  
  
-   若要使用默认[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/ SQL Azure 行为，选择**Replace 函数**。  
  
当选择中的转换模式**模式下**框，SSMA 适用以下设置：  
  
**默认/Optimistic 模式/完整模式：** 替换函数  
  
**TRIM （LTRIM、 RTRIM） 函数**  
此设置指定是否对 Trim （LTRIM、 RTRIM） 函数的调用替换为 Sybase ASE 等效语法函数或者保留当前的语法。 以下选项将存在对于此特定的设置：  
  
-   **Replace 函数**  
  
-   **保留当前的语法**  
  
当选择中的转换模式**模式下**框，SSMA 适用以下设置：  
  
**默认/Optimistic 模式/完整模式：** 替换函数  
  
**SUBSTRING 函数**  
在 ASE 中，该函数`SUBSTRING(expression, start, length)`如果指定的开始值的表达式中的字符数比大，或如果长度等于零，则返回 NULL。 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/ SQL Azure 的等效表达式将返回一个空字符串。  
  
-   若要使用 ASE 行为，请选择**替换为函数**。 对 SUBSTRING 函数的所有调用都替换对 SUBSTRING_VARCHAR 或 SUBSTRING_NVARCHAR 或 SUBSTRING_VARBINARY 基于类型参数传递 （在架构名称 's2ss 的用户数据库中创建） 来模拟的用户定义函数的调用Sybase ASE 行为。  
  
-   若要使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/ SQL Azure 行为，选择**保留当前语法**。  
  
当选择中的转换模式**模式下**框，SSMA 适用以下设置：  
  
**默认/Optimistic 模式：** 保留当前的语法  
  
**完整模式：** 替换函数  
  
## <a name="tables"></a>TABLES  
**添加主键**  
创建新的主密钥中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 表，如果访问表没有主键或唯一索引。  
  
-   **默认模式**: False  
  
-   **乐观模式**: False  
  
-   **完整模式**: True  
  
> [!NOTE]  
> 连接到 SQL Azure 时，它是默认情况下 True。  
  
## <a name="see-also"></a>请参阅  
[用户界面参考&#40;SybaseToSQL&#41;](../../ssma/sybase/user-interface-reference-sybasetosql.md)  
  
