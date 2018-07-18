---
title: “高级编辑”（条件）对话框 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.dmf.condition.advancededit.f1
ms.assetid: a0bbe501-78c5-45ad-9087-965d04855663
caps.latest.revision: 42
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 2dc35e9080637129f69115a22e5f208be9ecad19
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37205407"
---
# <a name="advanced-edit-condition-dialog-box"></a>“高级编辑”（条件）对话框
  “高级编辑”对话框用于为基于策略的管理条件创建复杂表达式。  
  
## <a name="options"></a>“常规”  
 **单元值**  
 在创建用于单元值的函数或表达式时，显示相应的函数或表达式。 单击 **“确定”** 以后，在 **“常规”** 页的 **“创建新条件”** 对话框或 **“打开条件”** 对话框中，单元值就会出现在条件表达式框的 **“字段”** 单元或 **“值”** 单元。  
  
 **函数和属性**  
 显示可用的函数和属性。  
  
 **详细信息**  
 使用以下格式显示函数和属性的相关信息：函数签名、函数说明、返回值以及示例。  
  
## <a name="syntax"></a>语法  
 有效表达式必须采用以下格式：  
  
 `{property | function | constant}`  
  
 `{operator}`  
  
 `{property | function | constant}`  
  
## <a name="examples"></a>示例  
 下面是一些有效表达式示例：  
  
-   Property1> 5  
  
-   Property1=Property2  
  
-   Add(5, Multiply(.2,Property1))<Property2  
  
-   *Sometext* IN *Property1*  
  
-   *Property1* \< Fn (*Property2*)  
  
-   BitwiseAnd(Property1,Property2)= 0  
  
## <a name="additional-function-information"></a>其他函数信息  
 以下各节提供某些函数的附加信息，这些函数可用于为基于策略的管理条件创建复杂表达式。  
  
> [!IMPORTANT]  
>  可用于创建基于策略的管理条件的函数并不总是使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语法。 请务必遵从示例语法。 例如，使用`DateAdd`或`DatePart`函数，必须将*datepart*单引号中的参数。  
  
|函数|Description|参数|返回值|示例|  
|--------------|-----------------|---------------|------------------|-------------|  
|`Add()`|Numeric Add (Numeric expression1, Numeric expression2)<br /><br /> 两个数相加。|*expression1*并*expression2* -任何有效的表达式的任何一种数值类别中的数据类型为 except`bit`数据类型。 可以为常量、属性或返回数值类型的函数。|**返回值：** 返回优先级高的参数的数据类型。|**示例：** `Add(Property1, 5)`|  
|`Array()`|Array Array (VarArgs expression)<br /><br /> 根据值列表创建数组。 可与聚合函数（如 Sum() 和 Count()）配合使用。|expression - 将要转换为数组的表达式。|数组。|`Array(2,3,4,5,6)`|  
|`Avg()`|Numeric Avg (VarArgs)<br /><br /> 返回参数列表中各值的平均值。|*VarArgs* -除是精确数值或近似数值数据类型类别的变量表达式列表`bit`数据类型。|返回类型由表达式的计算结果类型确定。<br /><br /> 如果表达式结果为`integer`， `decimal`，`money`并`smallmoney`，`float`并`real`类别中，返回类型为`int`， `decimal`， `money`，和`float`;分别。|`Avg(1.0, 2.0, 3.0, 4.0, 5.0)` 返回 `3.0` 。|  
|`BitwiseAnd()`|Numeric BitwiseAnd (Numeric expression 1, Numeric expression2)<br /><br /> 在两个整数值之间执行“逻辑位与”运算。|expression1 和 expression2 – 整数数据类型类别的任意数据类型的任意有效表达式。|返回整数数据类型类别的值。|`BitwiseAnd(Property1, Property2)`|  
|`BitwiseOr()`|Numeric BitwiseOr (Numeric expression1, Numeric expression2)<br /><br /> 在两个指定的整数值之间执行“逻辑位或”运算。|expression1 和 expression2 – 整数数据类型类别的任意数据类型的任意有效表达式。|返回整数数据类型类别的值。|`BitwiseOr(Property1, Property2)`|  
|`Concatenate()`|String Concatenate (String string1, String string2)<br /><br /> 串联两个字符串。|string1 和 string2 - 要串联的两个字符串。 可以是任何有效的非空字符串。|串联的字符串，并且 *string1* 后跟有 *string2*。|`Concatenate("Hello", " World` `")` 返回“`Hello World`”。|  
|`Count()`|Numeric Count (VarArgs)<br /><br /> 返回参数列表中的项数。|*VarArgs* -以外任何类型的表达式`text`， `image`，和`ntext`。|返回整数数据类型类别的值。|`Count(1.0, 2.0, 3.0, 4.0, 5.0)` 返回 `5` 。|  
|`DateAdd()`|DateTime DateAdd (String datepart, Numeric number, DateTime date)<br /><br /> 返回一个新`datetime`根据向指定日期添加间隔的值。|datepart - 指定需要对日期中的哪一部分返回新值的参数。 支持的一些类型有 year(yy, yyyy)、month(mm, m) 和 dayofyear(dy, y)。 有关详细信息，请参阅 [DATEADD (Transact-SQL)](/sql/t-sql/functions/dateadd-transact-sql)。<br /><br /> number - 用于增加 datepart 的值。<br /><br /> *日期*-一个表达式，返回`datetime`值或日期格式的字符串。|是新`datetime`根据向指定日期添加间隔的值。|`DateAdd('day', 21, DateTime('2007-08-06 14:21:50'))` 返回 `'2007-08-27 14:21:50'` 。<br /><br /> 以下列表*dateparts*和缩写词对此函数支持：<br /><br /> **year**：yy、yyyy<br /><br /> **month**：mm、m<br /><br /> **dayofyear**：dy、y<br /><br /> **day**：dd、d<br /><br /> **week**：wk、ww<br /><br /> **weekday**：dw、w<br /><br /> **hour**：hh<br /><br /> **minute**：mi、n<br /><br /> **second**：ss、s<br /><br /> **millisecond**：ms|  
|`DatePart()`|Numeric DatePart (String datepart, DateTime date)<br /><br /> 返回表示指定日期的指定 *datepart* 的整数。|datepart -指定返回的日期部分的参数。 支持的一些类型有 year(yy, yyyy)、month(mm, m) 和 dayofyear(dy, y)。 有关详细信息，请参阅 [DATEPART (Transact-SQL)](/sql/t-sql/functions/datepart-transact-sql)。<br /><br /> *日期*-一个表达式，返回`datetime`值或日期格式的字符串。|返回一个整数数据类型类别的值，表示指定日期的指定 *datepart* 。|`DatePart('month', DateTime('2007-08-06 14:21:50.620'))` 返回 `8` 。|  
|`DateTime()`|DateTime DateTime (String dateString)<br /><br /> 根据字符串创建一个 datetime 值。|dateString - 字符串形式的 datetime 值。|返回一个根据输入字符串创建的 datatime 值。|`DateTime('3/12/2006')`|  
|`Divide()`|Numeric Divide (Numeric expression_dividend, Numeric expression_divisor)<br /><br /> 用一个数除以另一个数。|expression_dividend - 被除数的数值表达式。 被除数可以是具有数值数据类型类别中任一数据类型（`datetime` 数据类型除外）的任何有效表达式。<br /><br /> expression_divisor - 除数的数值表达式。 除数可以是具有数值数据类型类别中任一数据类型（`datetime` 数据类型除外）的任何有效表达式。|返回优先级高的参数的数据类型。|`Divide(Property1, 2)`<br /><br /> 注意：这是一个双精度运算。 若要进行整数比较，必须将结果与 `Round()`结合。 例如： `Round(Divide(10, 3), 0) = 3`。|  
|`Enum()`|Numeric Enum (String enumTypeName, String enumValueName)<br /><br /> 根据字符串创建枚举值。|enumTypeName - 枚举类型的名称。<br /><br /> enumValueName - 枚举的值。|返回数值类型的枚举值。|`Enum('CompatibilityLevel','Version100')`|  
|`Escape()`|String Escape (String replaceString, String stringToEscape, String escapeString)<br /><br /> 使用给定的转义字符串将输入字符串的子字符串转义。|*replaceString* – 输入字符串。<br /><br /> *stringToEscape* – *replaceString*的子字符串。 这是您要在前面添加转义字符串的字符串。<br /><br /> *escapeString* – 您要在每个 *stringToEscape*实例的前面添加的转义字符串。|返回修改的 *replaceString* ，其中 *stringToEscape* 的每个实例的前面都有 *escapeString*。|`Escape("Hello", "l", "[")` 返回“`He[l[lo`”。|  
|`ExecuteSQL()`|Variant ExecuteSQL (String returnType, String sqlQuery)<br /><br /> 对目标服务器执行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查询。<br /><br /> 有关 ExecuteSql() 的详细信息，请参阅 [ExecuteSql() 函数](http://blogs.msdn.com/b/sqlpbm/archive/2008/07/03/executesql.aspx)。|returnType - 指定 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句返回的数据类型。 有效文字*returnType*如下所示： `Numeric`， `String`， `Bool`， `DateTime`， `Array`，和`Guid`。<br /><br /> sqlQuery - 包含要执行的查询的字符串。||`ExecuteSQL ('Numeric', 'SELECT COUNT(*) FROM msdb.dbo.sysjobs') <> 0`<br /><br /> 针对 SQL Server 的目标实例运行一个标量值 TRANSACT-SQL 查询。 在 `SELECT` 语句中只能指定一列；第一列之外的其他列将被忽略。 生成的查询应只返回一行；第一行以外的其他行将被忽略。 如果查询返回空集，则围绕 `ExecuteSQL` 构建的条件表达式的计算结果将为 false。 `ExecuteSql` 支持 **按需** 和 **按计划** 计算模式。<br /><br /> `@@ObjectName` -对应于中的名称字段[sys.objects](/sql/relational-databases/system-catalog-views/sys-objects-transact-sql)。 该变量将替换为当前对象的名称。<br /><br /> `@@SchemaName` -对应于中的名称字段[sys.schemas](/sql/relational-databases/system-catalog-views/schemas-catalog-views-sys-schemas)。 该变量将替换为当前对象的架构名称（如果适用）。<br /><br /> <br /><br /> 注意：若要在 ExecuteSQL 语句中包含单引号，请再使用一个单引号将其转义。 例如，若要加入对用户 O'Brian 的引用，请键入 O''Brian。|  
|`ExecuteWQL()`|Variant ExecuteWQL (string returnType , string namespace, string wql)<br /><br /> 对提供的命名空间执行 WQL 脚本。 Select 语句只能包含一个返回列。 如果提供多个列，则会引发错误。|returnType - 指定 WQL 返回的数据的返回类型。 有效文字为`Numeric`， `String`， `Bool`， `DateTime`， `Array`，并`Guid`。<br /><br /> namespace - 要对其执行脚本的 WMI 命名空间。<br /><br /> wql - 包含要执行的 WQL 的字符串。||`ExecuteWQL('Numeric', 'root\CIMV2', 'select NumberOfProcessors from win32_ComputerSystem') <> 0`|  
|`False()`|Bool False()<br /><br /> 返回布尔值 FALSE。||返回布尔值 FALSE。|`IsDatabaseMailEnabled = False()`|  
|`GetDate()`|DateTime GetDate()<br /><br /> 返回系统日期。||返回 DateTime 类型的系统日期。|`@DateLastModified = GetDate()`|  
|`Guid()`|Guid Guid(String guidString)<br /><br /> 根据字符串返回 GUID。|guidString - 要创建的 GUID 的字符串表示形式。|返回根据字符串创建的 GUID。|`Guid('12340000-0000-3455-0000-000000000454')`|  
|`IsNull()`|Variant IsNull (Variant check_expression, Variant replacement_value)<br /><br /> 如果 check_expression 的值不为 NULL，则返回该值；否则返回 replacement_value。 如果类型不同，则将 replacement_value 隐式转换为 check_expression 类型。|check_expression - 将检查其是否为 NULL 的表达式。 check_expression 可以是基于策略的管理支持的任意类型：Numeric、String、Bool、DateTime、Array 和 Guid。<br /><br /> replacement_value - check_expression 为 NULL 时要返回的表达式。 replacement_value 必须是可隐式转换为 check_expression 类型的类型。|如果 check_expression 不为 NULL，则返回类型为 check_expression 的类型，否则将返回 replacement_value 的类型。||  
|`Len()`|Numeric Len (string_expression)<br /><br /> 返回给定字符串表达式的字符数（不包括尾随空格）。|string_expression – 要计算的字符串表达式。|返回整数数据类型类别的值。|`Len('Hello')` 返回 `5` 。|  
|`Lower()`|String Lower (String_expression)<br /><br /> 将所有大写字符转换为小写后返回字符串。|expression - 源字符串表达式。|返回一个字符串，它表示所有大写字符都已经转换为小写的源字符串表达式。|`Len('HeLlO')` 返回 `'hello'` 。|  
|`Mod()`|Numeric Mod (Numeric expression_dividend, Numeric expression_divisor)<br /><br /> 将第一个数据表达式的值除以第二个数据表达式的值后，提供整数余数。|expression_dividend - 被除数的数值表达式。 expression_dividend 必须为整数或数值数据类型类别中任意一种数据类型的有效表达式。<br /><br /> expression_divisor - 除数的数值表达式。 expression_divisor 必须为整数或数值数据类型类别中任意一种数据类型的任意有效表达式。|返回整数数据类型类别的值。|`Mod(Property1, 3)`|  
|`Multiply()`|Numeric Multiply (Numeric expression1, Numeric expression2)<br /><br /> 将两个表达式相乘。|*expression1*并*expression2* -任何有效的表达式的任何一种数值类别中的数据类型为 except`datetime`数据类型。|返回优先级高的参数的数据类型。|`Multiply(Property1, .20)`|  
|`Power()`|Numeric Power (Numeric numeric_expression, Numeric expression_power)<br /><br /> 返回指定表达式的指定幂的值。|numeric_expression - 精确或近似数值数据类型类别（bit 数据类型除外）的表达式。<br /><br /> expression_power - 对 numeric_expression 进行幂运算的幂值。 *expression_power*可以是精确数值或近似数值数据类型类别的表达式除外`bit`数据类型。|返回与 numeric_expression 相同的类型。|`Power(Property1, 3)`|  
|`Round()`|Numeric Round (Numeric expression, Numeric expression_precision)<br /><br /> 返回舍入到指定长度或精度的数值表达式。|*表达式*-是一个表达式属于精确数字或近似 numeric 数据类型类别中，除`bit`数据类型。<br /><br /> expression_precision - 表达式的舍入精度。 如果 expression_precision 为正数，则将 numeric_expression 舍入到按长度指定的小数位数。 如果 expression_precision 为负数，则将 numeric_expression 小数点左边部分舍入到 expression_precision 指定的长度。|返回与 numeric_expression 相同的类型。|`Round(5.333, 0)`|  
|`String()`|String String (Variant_expression)<br /><br /> 将变量转换为字符串。|expression - 要转换为字符串的变量表达式。|返回变量表达式的字符串值。|`String(4)`|  
|`Sum()`|Numeric Sum (VarArgs)<br /><br /> 返回参数列表中所有值的和。 Sum 可以与数值一起使用。|*VarArgs*-除是精确数值或近似数值数据类型类别的变量表达式列表`bit`数据类型。|以最精确的表达式数据类型返回所有表达式值的和。<br /><br /> 如果表达式结果为`integer`， `numeric`，`money`并`small money`，`float`并`real`类别中，返回类型为`int`， `numeric`， `money`，和`float`;分别。|`Sum(1.0, 2.0, 3.0, 4.0, 5.0)` 返回 `15` 。|  
|`True()`|Bool TRUE()<br /><br /> 返回布尔值 TRUE。||返回布尔值 TRUE。|`IsDatabaseMailEnabled = True()`|  
|`Upper()`|String Upper (String_expression)<br /><br /> 将所有小写字符转换为大写后返回字符串。|expression - 源字符串表达式。|返回一个字符串，它表示所有小写字符都已经转换为大写的源字符串表达式。|`Len('HeLlO')` 返回 `'HELLO'` 。|  
  
## <a name="see-also"></a>请参阅  
 [“创建新条件”或“打开条件”对话框，“常规”页](../../integration-services/general-page-of-integration-services-designers-options.md)   
 [使用基于策略的管理来管理服务器](administer-servers-by-using-policy-based-management.md)  
  
  
