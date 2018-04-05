---
title: 选择的 SQL 命令 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- select [ODBC]
ms.assetid: 2149c3ca-3a71-446d-8d53-3d056e2f301a
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3e7295a800b3cc84f6eb64f5dfa762573fe80b6b
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="select---sql-command"></a>选择的 SQL 命令
从一个或多个表中检索数据。  
  
 Visual FoxPro ODBC 驱动程序支持本机 Visual FoxPro 语言语法，此命令。 特定于驱动程序的信息，请参阅**驱动程序备注**。  
  
## <a name="syntax"></a>语法  
  
```  
  
SELECT [ALL | DISTINCT]  
   [Alias.] Select_Item [AS Column_Name]  
   [, [Alias.] Select_Item [AS Column_Name] ...]   
FROM [DatabaseName!]Table [Local_Alias]  
   [, [DatabaseName!]Table [Local_Alias] ...]   
[WHERE JoinCondition [AND JoinCondition  
…]  
   [AND | OR FilterCondition [AND | OR FilterCondition ...]]]  
[GROUP BY GroupColumn [, GroupColumn ...]]  
[HAVING FilterCondition]  
[UNION [ALL] SELECTCommand]  
[ORDER BY Order_Item [ASC | DESC] [, Order_Item [ASC | DESC] ...]]  
```  
  
## <a name="arguments"></a>参数  
  
> [!NOTE]  
>  A*子查询*、 在以下自变量中称为、 SELECT 中 select 和必须括在括号中。 你可以在同一级别中具有最多两个子查询 （不嵌套） WHERE 子句中。 （请参阅自变量的那一节。）子查询可以包含多个联接条件。  
  
 [所有 &#124;非重复] [*别名*。]*Select_Item* [AS *Column_Name*] [，[*别名*。]*Select_Item* [AS *Column_Name*]...]  
 SELECT 子句指定字段、 常量和查询结果中显示的表达式。  
  
 默认情况下，所有查询结果中显示的所有行。  
  
 DISTINCT 查询结果中排除任何行重复的项。  
  
> [!NOTE]  
>  还可以使用一次 DISTINCT 根据 SELECT 子句。  
  
 *别名*。 限定匹配项的名称。 使用指定的每一项*Select_Item*都会生成的查询结果的一列。 如果两个或多个项具有相同的名称，包括表别名和项名称，以防止列重复前的一段。  
  
 *Select_Item*指定要在查询结果中包含的项。 项可以是以下项之一：  
  
-   在 FROM 子句中表的字段的名称。  
  
-   一个常数，它指定相同的常量值显示在查询结果的每一行。  
  
-   一个表达式，可以是用户定义函数的名称。  
  
 **与选择的用户定义函数**  
  
 尽管在 SELECT 子句中使用用户定义函数有明显的好处，还应考虑以下限制：  
  
-   带有 SELECT 执行的操作的速度可能会受到从该处执行此类用户定义函数的速度。 使用 API 和用 C 或程序集语言编写的用户定义的函数可能更好地完成涉及多个用户定义函数的大容量操作。  
  
-   将值传递给调用从选择的用户定义函数的唯一可靠方法是通过传递给函数，当调用它的自变量列表。  
  
-   即使您进行试验，并发现应该禁止的操作的正常 FoxPro 的某些版本中，则它将继续工作更高版本中不保证。  
  
 除了这些限制后，用户定义函数是在 SELECT 子句中可接受。 但请记住，使用选择可能会降低性能。  
  
 以下字段函数是可与的字段或涉及字段的表达式的选择项一起使用：  
  
-   AVG (*Select_Item*)-计算平均值的数值数据列。  
  
-   计数 (*Select_Item*)-对列中选择项的数目进行计数。 COUNT(*) 对查询输出中的行数进行计数。  
  
-   最小值 (*Select_Item*)-确定的最小值*Select_Item*列中。  
  
-   最大 (*Select_Item*)-确定的最大值*Select_Item*列中。  
  
-   SUM (*Select_Item*)-总计数值数据的列。  
  
 你无法嵌套字段函数。  
  
 AS *Column_Name*  
 在查询输出中指定某一列标题。 这非常有用*Select_Item*是一个表达式，或包含一个字段函数，并且想要为列提供一个有意义的名称。 *Column_Name*可以是表达式，但不能包含表字段名称中不允许使用的字符 （例如，空格）。  
  
 从 [*DatabaseName*！]*表*[*Local_Alias*] [，[*DatabaseName*！]*表*[*Local_Alias*]...]  
 列出包含该查询将检索的数据的表。 如果没有表处于打开状态，将显示 Visual FoxPro**打开**对话框中，以便你能够指定文件位置。 已打开后，表保持打开状态，查询完成后。  
  
 *DatabaseName*！ 指定与数据源指定以外的数据库的名称。 必须包括包含的表，如果数据库未指定与数据源数据库的名称。 之后的数据库名称和表名称之前，请包括感叹号 （！） 分隔符。  
  
 *Local_Alias*指定中名为的表的临时名称*表*。 如果你指定的本地别名，则必须使用本地的别名，而不是整个 SELECT 语句的表名称。 本地别名并不影响 Visual FoxPro 环境。  
  
 其中*JoinCondition* [AND *JoinCondition* ...]   [和 &#124;或者*FilterCondition* [AND &#124;或者*FilterCondition* ...]]  
 告知 Visual FoxPro 将只有某些记录包括在查询结果。 如果需要从多个表检索数据。  
  
 *JoinCondition*指定链接的 FROM 子句中表的字段。 如果您在查询中包含多个表，则应后第一个指定每个表的联接条件。  
  
> [!IMPORTANT]  
>  创建联接条件时，请考虑下列信息：  
  
-   如果你在查询中包括两个表，并且未指定联接条件，只要满足筛选器条件第二个表中的每个记录中加入第一个表中的每个记录。 此类查询可以生成很长的结果。  
  
-   联接表具有空字段，因为 Visual FoxPro 与空字段相匹配时要格外小心。 例如，如果在客户加入。ZIP 和发票。压缩并将查询输出如果客户包含 100 空邮政编码和发票包含 400 空邮政编码，包含生成的从空的字段的 40000 额外记录。 使用**空 （)**函数来消除在查询输出中的空记录。  
  
-   你必须使用 AND 运算符连接多个联接条件。 每个联接条件具有以下形式：  
  
     *FieldName1 比较 FieldName2*  
  
     *FieldName1*是从一个表的字段的名称*FieldName2*是另一个表中的字段的名称和*比较*是下表中描述的运算符之一。  
  
|运算符|比较|  
|--------------|----------------|  
|=|等于|  
|==|全等|  
|LIKE|类似的 SQL|  
|<>, !=, #|不等于|  
|>|多个|  
|>=|大于或等于|  
|<|小于|  
|<=|小于或等于|  
  
 当你使用 = 运算符对于字符串，它可以充当有所不同，具体取决于设置 ANSI 的设置。 当设置 ANSI 设置为 OFF 时，Visual FoxPro 以为 Xbase 用户所熟悉的方式处理字符串比较。 当设置 ANSI 设置为 ON 时，则 Visual FoxPro 遵循 ANSI 标准的字符串比较。 请参阅[设置 ANSI](../../odbc/microsoft/set-ansi-command.md)和[确切设置](../../odbc/microsoft/set-exact-command.md)有关 Visual FoxPro 如何执行字符串比较的详细信息。  
  
 *FilterCondition*指定记录包含在查询结果中必须满足的条件。 可以包含任意数量的筛选条件在查询中的根据需要，将它们连接使用 AND 或 OR 运算符。 你还可以使用 NOT 运算符颠倒的逻辑表达式时，值或可以使用**空 （)**检查空字段。 *FilterCondition*可以接受任何窗体在下面的示例：  
  
 **示例 1** *FieldName1 比较 FieldName2*  
  
 `customer.cust_id = orders.cust_id`  
  
 **示例 2** *FieldName 比较表达式*  
  
 `payments.amount >= 1000`  
  
 **示例 3** *FieldName 比较*所有 (*子查询*)  
  
 `company < ALL ;`  
  
 `(SELECT company FROM customer WHERE country = "USA")`  
  
 当筛选条件包含所有时，该字段必须满足在查询结果中包含的记录之前生成的子查询的所有值的比较条件。  
  
 **示例 4** *FieldName 比较*任何 &#124;一些 (*子查询*)  
  
 `company < ANY ;`  
  
 `(SELECT company FROM customer WHERE country = "USA")`  
  
 当筛选条件包含任何或部分时，该字段必须满足至少一个子查询生成的值的比较条件。  
  
 下面的示例检查以查看字段中的值是否在指定的值范围内：  
  
 **示例 5** *FieldName* [NOT] 之间*Start_Range* AND *End_Range*  
  
 `customer.postalcode BETWEEN 90000 AND 99999`  
  
 下面的示例检查以查看是否至少有一行是否符合子查询中的条件。 当筛选条件包含 EXISTS 时，筛选器条件的计算结果为 True (。T。） 除非子查询的计算结果为空集。  
  
 **示例 6** [NOT] 存在 (*子查询*)  
  
 `EXISTS ;`  
  
 `(SELECT * FROM orders WHERE customer.postalcode =`  
  
 `orders.postalcode)`  
  
 **示例 7** *FieldName* [NOT] IN *Value_Set*  
  
 `customer.postalcode NOT IN ("98052","98072","98034")`  
  
 当筛选条件包含 IN 时，字段必须包含的值之一之前在查询结果中包含的记录。  
  
 **示例 8** *FieldName* [NOT] IN (*子查询*)  
  
 `customer.cust_id IN ;`  
  
 `(SELECT orders.cust_id FROM orders WHERE orders.city="Seattle")`  
  
 此处字段必须包含在查询结果中包括的记录之前，先由子查询返回的值之一。  
  
 **示例 9** *FieldName* [NOT] LIKE *cExpression*  
  
 `customer.country NOT LIKE "USA"`  
  
 此筛选条件搜索匹配每个字段*cExpression*。 你可以使用百分号 （%） 和下划线 (_) 通配符作为的一部分*cExpression*。 下划线表示字符串中的单个未知的字符。  
  
 GROUP BY *GroupColumn* [， *GroupColumn* ...]  
 一个或多个列中的值为基础的查询中的组行。 *GroupColumn*可以是以下之一：  
  
-   常规表字段的名称。  
  
-   包含 SQL 字段函数的字段。  
  
-   数值表达式，该值指示结果表中的列的位置。 （最左边的列数为 1。）  
  
 具有*FilterCondition*  
 指定必须满足组以包含在查询结果的筛选器条件。 HAVING 应与 GROUP BY 和可以包含任意数量的筛选条件所需连接通过 AND 或 OR 运算符。 你还可用于不反向逻辑表达式的值。  
  
 *FilterCondition*不能包含子查询。  
  
 没有 GROUP BY 子句的 HAVING 子句与 WHERE 子句的行为。 HAVING 子句中，可以使用本地别名和字段函数。 如果你 HAVING 子句不包含任何字段函数将 WHERE 子句用于更快的性能。  
  
 [联合 [ALL] *SELECTCommand*]  
 将选择的最终结果合并使用另一个选择的最终结果。 默认情况下，联合检查合并的结果，并消除重复的行。 使用括号来组合多个 UNION 子句。  
  
 所有可防止联合消除从合并的结果的重复行。  
  
 UNION 子句遵循以下规则：  
  
-   联合不能用于合并子查询。  
  
-   这两个选择的命令必须在其查询输出中具有相同的列数。  
  
-   一个选择的查询结果中每一列必须在其他选择相应的列具有相同的数据类型和宽度。  
  
-   仅最终选择可以具有的 ORDER BY 子句，必须引用按编号的输出列。 如果包括 ORDER BY 子句，则它会影响完整结果。  
  
 UNION 子句还可用于模拟外部联接。  
  
 当在查询中联接两个表时，输出中包含仅具有联接字段中的匹配值的记录。 如果父表中的记录的子表中没有相应的记录，输出中不包含父表中的记录。 外部联接，您可以在输出中，子表中的匹配记录以及父表中包含的所有记录。 若要在 Visual FoxPro 中创建外部联接，必须使用嵌套的 SELECT 命令，如以下示例所示：  
  
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
>  请确保你保留紧接在之前的每个分号的空格。 否则，你将收到错误。  
  
 具有匹配值命令之前的 UNION 子句选择两个表中记录的部分。 不具有关联的发票的客户公司不包括在内。 UNION 子句之后命令的部分中没有匹配记录 orders 表中的客户表选择记录。  
  
 有关命令的第二个部分，请注意以下事项：  
  
-   首先处理在括号内的 SELECT 语句。 此语句在订单表中创建选定的所有客户编号。  
  
-   WHERE 子句不 orders 表中的客户表中查找所有客户编号。 由于该命令的第一个部分提供在订单表中已有客户编号的所有公司，在 customer 表中的所有公司现在都包括在查询结果中。  
  
-   在第二个 SELECT 语句来表示包含联合中的表的结构必须相同，因为有两个占位符*orders.order_id*和*orders.emp_id*从第一个选择语句。  
  
    > [!NOTE]  
    >  占位符必须与它们所表示的字段相同的类型。 如果此字段为日期类型，将占位符应为 {/ /}。 如果该字段是字符字段，将占位符应为空字符串 ("")。  
  
 ORDER BY *Order_Item* [ASC &#124;DESC] [， *Order_Item* [ASC &#124;DESC]...]  
 排序查询结果基于一个或多个列中的数据。 每个*Order_Item*必须对应于查询结果中的列，可以是以下之一：  
  
-   也是主要的 SELECT 子句 （不在子查询） 中选择项的从表中的字段。  
  
-   数值表达式，该值指示结果表中的列的位置。 (最左边的列是数字 1。)  
  
 ASC 指定一个按升序为查询结果，请根据订单项或项，并且的默认值为 ORDER BY。  
  
 DESC 指定查询结果的降序顺序。  
  
 如果你没有使用 ORDER BY 指定订单，查询结果将显示未排序。  
  
## <a name="remarks"></a>Remarks  
 选择是像任何其他 Visual FoxPro 命令内置于 Visual FoxPro 一个 SQL 命令。 当你使用选择引起查询、 Visual FoxPro 解释查询和检索表中指定的数据。 你可以创建 SELECT 查询从命令提示符窗口或 Visual FoxPro 程序中的 （与任何其他 Visual FoxPro 命令）。  
  
> [!NOTE]  
>  选择不遵从设置筛选器与指定的当前筛选器条件。  
  
## <a name="driver-remarks"></a>驱动程序备注  
 当你的应用程序将 ODBC SQL 语句选择发送到数据源时，Visual FoxPro ODBC 驱动程序将不转换 Visual FoxPro SELECT 命令转换为命令除非该命令包含 ODBC 转义序列。 括在 ODBC 转义序列中的项转换为 Visual FoxPro 语法。 有关使用 ODBC 转义序列，请参阅[时间和日期函数](../../odbc/microsoft/time-and-date-functions-visual-foxpro-odbc-driver.md)并在*Microsoft ODBC 程序员参考*，请参阅[ODBC 中的转义序列](../../odbc/reference/develop-app/escape-sequences-in-odbc.md).  
  
## <a name="see-also"></a>另请参阅  
 [创建表的 SQL](../../odbc/microsoft/create-table-sql-command.md)   
 [插入-SQL](../../odbc/microsoft/insert-sql-command.md)   
 [集 ANSI](../../odbc/microsoft/set-ansi-command.md)   
 [设置完全](../../odbc/microsoft/set-exact-command.md)
