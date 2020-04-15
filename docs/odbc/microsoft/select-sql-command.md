---
title: 选择 - SQL 命令 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- select [ODBC]
ms.assetid: 2149c3ca-3a71-446d-8d53-3d056e2f301a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 640189a5a31d0c21642b037e906bd6361690a9a5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300937"
---
# <a name="select---sql-command"></a>SELECT - SQL 命令
从一个或多个表检索数据。  
  
 Visual FoxPro ODBC 驱动程序支持此命令的本机 Visual FoxPro 语言语法。 有关特定于驱动程序的信息，请参阅**驱动程序备注**。  
  
## <a name="syntax"></a>语法  
  
```  
  
SELECT [ALL | DISTINCT]  
   [Alias.] Select_Item [AS Column_Name]  
   [, [Alias.] Select_Item [AS Column_Name] ...]   
FROM [DatabaseName!]Table [Local_Alias]  
   [, [DatabaseName!]Table [Local_Alias] ...]   
[WHERE JoinCondition [AND JoinCondition  
...]  
   [AND | OR FilterCondition [AND | OR FilterCondition ...]]]  
[GROUP BY GroupColumn [, GroupColumn ...]]  
[HAVING FilterCondition]  
[UNION [ALL] SELECTCommand]  
[ORDER BY Order_Item [ASC | DESC] [, Order_Item [ASC | DESC] ...]]  
```  
  
## <a name="arguments"></a>参数  
  
> [!NOTE]  
>  *子查询*（在以下参数中引用）是 SELECT 中的 SELECT，必须包含在括号中。 在 WHERE 子句中，可以在同一级别（未嵌套）最多具有两个子查询。 （请参阅参数的该部分。子查询可以包含多个联接条件。  
  
 [所有&#124;  [*别名*].*Select_Item* [as *Column_Name*] [ ， [*别名*. ]*Select_Item* [as *Column_Name*]  
 SELECT 子句指定查询结果中显示的字段、常量和表达式。  
  
 默认情况下，ALL 显示查询结果中的所有行。  
  
 从查询结果中排除任何行的重复项。  
  
> [!NOTE]  
>  每个 SELECT 子句只能使用一次"保留"。  
  
 *别名*. 限定匹配项名称。 使用*Select_Item*指定的每个项目都会生成查询结果的一列。 如果两个或多个项具有相同的名称，请包括表别名和项名称前的句点，以防止重复列。  
  
 *Select_Item*指定要包含在查询结果中的项。 项可以是以下项之一：  
  
-   FROM 子句表中表中的字段的名称。  
  
-   指定相同的常量值的常量值将显示在查询结果的每一行中。  
  
-   可以是用户定义的函数名称的表达式。  
  
 **具有 SELECT 的用户定义函数**  
  
 尽管在 SELECT 子句中使用用户定义的函数有明显的好处，但您还应考虑以下限制：  
  
-   使用 SELECT 执行的操作速度可能受执行此类用户定义的函数的速度的限制。 通过使用用 C 或汇编语言编写的 API 和用户定义的函数，可以更好地完成涉及用户定义函数的高容量操作。  
  
-   将值传递给从 SELECT 调用的用户定义的函数的唯一可靠方法是在调用函数时传递给该函数的参数列表。  
  
-   即使您试验并发现一个据称被禁止的操作，在 FoxPro 的特定版本中工作正常，也不能保证它将继续在更高版本中工作。  
  
 除了这些限制之外，选择子句中可以接受用户定义的函数。 但是，请记住，使用 SELECT 可能会降低性能。  
  
 以下字段函数可用于涉及字段的字段或表达式的选择项：  
  
-   *AVG（Select_Item*）-平均一列数字数据。  
  
-   *COUNT（Select_Item*）- 计算列中选定项的数量。 COUNT（*） 计算查询输出中的行数。  
  
-   *MIN（Select_Item*）-确定列中*Select_Item*的最小值。  
  
-   *MAX（Select_Item*）-确定列中*Select_Item*的最大值。  
  
-   *SUM（Select_Item*）-总计一列数值数据。  
  
 不能嵌套字段函数。  
  
 如*Column_Name*  
 指定查询输出中列的标题。 当*Select_Item*是表达式或包含字段函数并且您希望为列指定有意义的名称时，这非常有用。 *Column_Name*可以是表达式，但不能包含表字段名称中不允许的字符（例如空格）。  
  
 从 [*数据库名称*！ ]*表*[*Local_Alias*] [ ] [ [*数据库名称*！ ]*表*[*Local_Alias*]  
 列出包含查询检索数据的表。 如果没有打开任何表，Visual FoxPro 将显示 **"打开**"对话框，以便您可以指定文件位置。 打开后，该表在查询完成后保持打开状态。  
  
 *数据库名称*！ 指定数据库的名称，而不是使用数据源指定的数据库。 如果未使用数据源指定数据库，则必须包含包含表的数据库的名称。 包括数据库名称后和表名称之前的感叹号 （！） 分隔符。  
  
 *Local_Alias*指定*表*中指定的表的临时名称。 如果指定本地别名，则必须在整个 SELECT 语句中使用本地别名而不是表名。 本地别名不会影响 Visual FoxPro 环境。  
  
 WHERE*加入条件*[和*加入条件*...]   [和&#124;或*筛选条件*[和&#124; 或*筛选条件*...]  
 告诉 Visual FoxPro 在查询结果中仅包含某些记录。 从多个表中检索数据需要 WHERE。  
  
 *Join条件*指定链接 FROM 子句中表的字段。 如果在查询中包含多个表，则应为第一个表之后的每个表指定联接条件。  
  
> [!IMPORTANT]  
>  创建联接条件时请考虑以下信息：  
  
-   如果在查询中包含两个表，并且未指定联接条件，则只要满足筛选器条件，第一个表中的每个记录都将联接到第二个表中的每个记录。 此类查询可以产生冗长的结果。  
  
-   将表与空字段联接时要小心，因为 Visual FoxPro 匹配空字段。 例如，如果您加入 CUSTOMER。邮编和发票。ZIP，如果 CUSTOMER 包含 100 个空邮政编码，并且 INVOICE 包含 400 个空邮政编码，则查询输出包含由空字段产生的额外记录 40，000 条。 使用**EMPTY（ 函数**从查询输出中消除空记录）。  
  
-   您必须使用 AND 运算符连接多个联接条件。 每个联接条件都有以下形式：  
  
     *字段名称1 比较字段名称2*  
  
     *FieldName1*是一个表中的字段的名称 *，FieldName2*是另一个表中的字段的名称，*比较*是下表中描述的运算符之一。  
  
|操作员|比较|  
|--------------|----------------|  
|=|等于|  
|==|完全相等|  
|LIKE|SQL 喜欢|  
|<>，！，##|不等于|  
|>|超过|  
|>=|超过或等于|  
|<|小于|  
|<=|小于或等于|  
  
 使用带有字符串的 + 运算符时，它的作用会有所不同，具体取决于 SET ANSI 的设置。 当 SET ANSI 设置为 OFF 时，Visual FoxPro 会以 Xbase 用户熟悉的方式处理字符串比较。 当 SET ANSI 设置为 ON 时，Visual FoxPro 遵循用于字符串比较的 ANSI 标准。 有关 Visual FoxPro 如何执行字符串比较的详细信息，请参阅[SET ANSI](../../odbc/microsoft/set-ansi-command.md)和[SET EXACT。](../../odbc/microsoft/set-exact-command.md)  
  
 *筛选器条件*指定记录必须满足的条件才能包含在查询结果中。 您可以在查询中根据需要包含尽可能多的筛选器条件，将它们与 AND 或 OR 运算符连接。 您还可以使用 NOT 运算符反转逻辑表达式的值，也可以使用**EMPTY（ ）** 检查空字段。 *筛选器条件*可以采用以下示例中的任何窗体：  
  
 **示例 1** *字段名称1 比较字段名称2*  
  
 `customer.cust_id = orders.cust_id`  
  
 **示例 2** *字段名称比较表达式*  
  
 `payments.amount >= 1000`  
  
 **示例 3** *字段名称比较*全部 （*子查询*）  
  
 `company < ALL ;`  
  
 `(SELECT company FROM customer WHERE country = "USA")`  
  
 当筛选器条件包含 ALL 时，该字段必须满足子查询生成的所有值的比较条件，然后才能将其记录包含在查询结果中。  
  
 **示例 4** *字段名称比较*任何&#124; A（*子查询*）  
  
 `company < ANY ;`  
  
 `(SELECT company FROM customer WHERE country = "USA")`  
  
 当筛选器条件包括 ANY 或 SOME 时，该字段必须满足子查询生成的至少一个值的比较条件。  
  
 以下示例检查字段中的值是否在指定的值范围内：  
  
 **示例 5***字段名称*[不是] *Start_Range*和*End_Range*  
  
 `customer.postalcode BETWEEN 90000 AND 99999`  
  
 下面的示例检查至少一行是否符合子查询中的条件。 当筛选器条件包括 EXISTS 时，筛选器条件将评估为 True （。T.），除非子查询计算为空集。  
  
 **示例 6** [NOT] 存在 （*子查询*）  
  
 `EXISTS ;`  
  
 `(SELECT * FROM orders WHERE customer.postalcode =`  
  
 `orders.postalcode)`  
  
 **示例 7** *字段名称*[不] *Value_Set*  
  
 `customer.postalcode NOT IN ("98052","98072","98034")`  
  
 当筛选器条件包含 IN 时，该字段必须包含其中一个值，然后才能将其记录包含在查询结果中。  
  
 **示例 8** *字段名称*[NOT] IN （*子查询*）  
  
 `customer.cust_id IN ;`  
  
 `(SELECT orders.cust_id FROM orders WHERE orders.city="Seattle")`  
  
 此处，该字段必须包含子查询返回的值之一，然后才能将其记录包含在查询结果中。  
  
 **示例 9** *字段名称*[NOT] 喜欢*c 表达式*  
  
 `customer.country NOT LIKE "USA"`  
  
 此筛选器条件搜索与*cExpression*匹配的每个字段。 您可以使用百分比符号 （%）和下划线 （ + ） 通配符作为*cExpression*的一部分。 下划线表示字符串中的单个未知字符。  
  
 组 BY*组栏*[，*组列*...  
 根据一个或多个列中的值对查询中的行进行分组。 *组列*可以是以下之一：  
  
-   常规表字段的名称。  
  
-   包含 SQL 字段函数的字段。  
  
-   指示结果表中列位置的数字表达式。 （最左边的列号为 1。  
  
 有*筛选条件*  
 指定组必须满足的筛选器条件才能包含在查询结果中。 在 GROUP BY 中应使用，并且可以根据需要包含尽可能多的筛选器条件，由 AND 或 OR 运算符连接。 您还可以使用 NOT 来反转逻辑表达式的值。  
  
 *筛选器条件*不能包含子查询。  
  
 没有 GROUP BY 子句的"一条"问题子项的行为类似于 WHERE 子句。 您可以在"有"子句中使用本地别名和字段函数。 如果您的"有内容"子句不包含字段函数，请使用 WHERE 子句来提高性能。  
  
 [联合 [所有]*选择命令*|  
 将一个 SELECT 的最终结果与另一个 SELECT 的最终结果相结合。 默认情况下，UNION 会检查组合的结果并消除重复的行。 使用括号组合多个 UNION 子句。  
  
 ALL 可防止 UNION 从组合结果中消除重复行。  
  
 UNION 条款遵循以下规则：  
  
-   不能使用 UNION 组合子查询。  
  
-   两个 SELECT 命令的查询输出中必须具有相同的列数。  
  
-   一个 SELECT 查询结果中的每个列必须具有与其他 SELECT 中的相应列相同的数据类型和宽度。  
  
-   只有最终 SELECT 可以具有 ORDER BY 子句，该子句必须按数字引用输出列。 如果包含 ORDER BY 子句，则会影响完整结果。  
  
 您还可以使用 UNION 子句来模拟外部联接。  
  
 在查询中联接两个表时，输出中仅包含具有匹配值的记录。 如果父表中的记录在子表中没有相应的记录，则父表中的记录不包括在输出中。 外部联接允许您在输出中包括父表中的所有记录以及子表中的匹配记录。 要在 Visual FoxPro 中创建外部联接，必须使用嵌套 SELECT 命令，如以下示例所示：  
  
```  
SELECT customer.company, orders.order_id, orders.emp_id ;  
FROM customer, orders ;  
WHERE customer.cust_id = orders.cust_id ;  
UNION ;  
SELECT customer.company, 0, 0 ;  
FROM customer ;  
WHERE customer.cust_id NOT IN ;  
(SELECT orders.cust_id FROM orders)  
```  
  
> [!NOTE]  
>  请确保包含每个分号之前紧邻的空间。 否则，您将收到错误。  
  
 UNION 子句之前的命令部分从具有匹配值的两个表中选择记录。 不包括没有关联发票的客户公司。 UNION 子句之后的命令部分选择客户表中在订单表中没有匹配记录的记录。  
  
 关于命令的第二部分，请注意以下内容：  
  
-   首先处理括号内的 SELECT 语句。 此语句创建订单表中所有客户编号的选择。  
  
-   WHERE 子句查找客户表中未在订单表中的所有客户编号。 由于命令的第一部分提供了订单表中具有客户编号的所有公司，因此客户表中的所有公司现在都包含在查询结果中。  
  
-   由于 UNION 中包含的表的结构必须相同，因此第二个 SELECT 语句中有两个占位符来表示*订单.order_id*和*订单.emp_id*来自第一个 SELECT 语句。  
  
    > [!NOTE]  
    >  占位符的类型必须与它们表示的字段相同。 如果字段是日期类型，则占位符应为 * / * 。 如果字段是字符字段，则占位符应为空字符串 （""）。  
  
 Order_Item *[ASC* &#124; DESC] *[Order_Item* [ASC &#124; DESC]  
 根据一个或多个列中的数据对查询结果进行排序。 每个*Order_Item*必须对应于查询结果中的列，可以是以下项之一：  
  
-   FROM 表中的字段，也是主 SELECT 子句中的选定项（不在子查询中）。  
  
-   指示结果表中列位置的数字表达式。 （最左边的列是第 1 号。  
  
 ASC 根据订单项或项指定查询结果的提升顺序，是 ORDER BY 的默认值。  
  
 DESC 为查询结果指定降序。  
  
 如果不使用 ORDER BY 指定订单，则查询结果将无序显示。  
  
## <a name="remarks"></a>备注  
 SELECT 是一个 SQL 命令，与任何其他 Visual FoxPro 命令一样内置于 Visual FoxPro 中。 当您使用 SELECT 进行查询时，Visual FoxPro 会解释查询并从表中检索指定的数据。 您可以从命令提示窗口或 Visual FoxPro 程序（与任何其他 Visual FoxPro 命令一样）创建 SELECT 查询。  
  
> [!NOTE]  
>  SELECT 不尊重使用 SET FILTER 指定的当前筛选器条件。  
  
## <a name="driver-remarks"></a>驱动程序备注  
 当您的应用程序将 ODBC SQL 语句 SELECT 发送到数据源时，Visual FoxPro ODBC 驱动程序将该命令转换为 Visual FoxPro SELECT 命令，无需翻译，除非该命令包含 ODBC 转义序列。 ODBC 转义序列中包含的项目将转换为 Visual FoxPro 语法。 有关使用 ODBC 转义序列的详细信息，请参阅[时间和日期函数](../../odbc/microsoft/time-and-date-functions-visual-foxpro-odbc-driver.md)以及 Microsoft *ODBC 程序员的参考*，请参阅[ODBC 中的转义序列](../../odbc/reference/develop-app/escape-sequences-in-odbc.md)。  
  
## <a name="see-also"></a>另请参阅  
 [创建表 - SQL](../../odbc/microsoft/create-table-sql-command.md)   
 [插入 - SQL](../../odbc/microsoft/insert-sql-command.md)   
 [SET ANSI](../../odbc/microsoft/set-ansi-command.md)   
 [设置精确](../../odbc/microsoft/set-exact-command.md)
