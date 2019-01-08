---
title: SELECT-SQL 命令 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0c2d991afa179fdfbb536853e302b33de8bf12e1
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2018
ms.locfileid: "52540243"
---
# <a name="select---sql-command"></a>SELECT - SQL 命令
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
...]  
   [AND | OR FilterCondition [AND | OR FilterCondition ...]]]  
[GROUP BY GroupColumn [, GroupColumn ...]]  
[HAVING FilterCondition]  
[UNION [ALL] SELECTCommand]  
[ORDER BY Order_Item [ASC | DESC] [, Order_Item [ASC | DESC] ...]]  
```  
  
## <a name="arguments"></a>参数  
  
> [!NOTE]  
>  一个*子查询*、 中以下自变量引用、 select 语句中 SELECT 和必须括在括号中。 可以在同一级别上具有最多两个的子查询 （不嵌套） 在 WHERE 子句中。 （请参阅参数的该部分。）子查询可以包含多个联接条件。  
  
 [所有&#124;DISTINCT]  [*别名*。]*Select_Item* [AS *Column_Name*] [，[*别名*。]*Select_Item* [AS *Column_Name*]...]  
 SELECT 子句指定字段、 常量和查询结果中显示的表达式。  
  
 默认情况下，所有查询结果中显示的所有行。  
  
 DISTINCT 查询结果中排除重复项的任何行。  
  
> [!NOTE]  
>  每个 SELECT 子句，可以使用 DISTINCT 一次。  
  
 *别名*。 符合条件匹配的项名称。 使用指定的每个项*Select_Item*生成查询结果的一列。 如果两个或多个项具有相同的名称，包括表别名和项名称，以防止列重复出现前的一段。  
  
 *Select_Item*指定要在查询结果中包含的项。 项可以是以下值之一：  
  
-   FROM 子句中的表中的字段的名称。  
  
-   一个常数，指定相同的常量值将出现在查询结果中的每一行中。  
  
-   一个表达式，可以是用户定义函数的名称。  
  
 **选择与用户定义函数**  
  
 尽管在 SELECT 子句中使用用户定义的函数具有明显的优势，还应考虑以下限制：  
  
-   执行的此类用户定义的函数的速度可能会受限于执行选择操作的速度。 使用 API 和 C 或程序集语言中编写用户定义的函数可能会更好地实现涉及多个用户定义的函数的大容量操作。  
  
-   若要将值传递给调用从选择的用户定义函数的唯一可靠方法是通过在调用时传递给函数的参数列表。  
  
-   即使您试验并发现据推测禁止的操作 FoxPro 的某些版本中正常运行，则它将继续在更高版本中无法保证。  
  
 除了这些限制，用户定义函数是在 SELECT 子句中可接受的。 但请记住，使用 SELECT 可能会降低性能。  
  
 以下字段函数是可供使用的字段或涉及字段的表达式的选择项的使用：  
  
-   AVG (*Select_Item*)-计算平均值的数值数据列。  
  
-   计数 (*Select_Item*) 的计算列中选择项的数目。 COUNT(*) 对在查询输出中的行数进行计数。  
  
-   最小值 (*Select_Item*)-确定的最小值*Select_Item*列中。  
  
-   最大值 (*Select_Item*)-确定的最大值*Select_Item*列中。  
  
-   SUM (*Select_Item*)-所有总计值的数值数据列。  
  
 不能嵌套字段函数。  
  
 AS *Column_Name*  
 在查询输出中指定的列标题。 时，此操作很有用*Select_Item*是一个表达式或包含一个字段函数，并且想要为该列提供有意义的名称。 *Column_Name*可以是表达式，但不能包含表的字段名称中不允许的字符 （例如，空格）。  
  
 从 [*DatabaseName*！]*表*[*Local_Alias*] [，[*DatabaseName*！]*表*[*Local_Alias*]...]  
 列出包含该查询将检索的数据的表。 如果没有表处于打开状态，将显示 Visual FoxPro**打开**对话框中，以便您可以指定文件位置。 已打开后，表查询完成后保持打开状态。  
  
 *DatabaseName*！ 指定与数据源指定的数据库的名称。 必须包含与数据源未指定的数据库包含的表的数据库的名称。 包含感叹号 （！） 分隔符之后的数据库名称和表名称之前。  
  
 *Local_Alias*指定的表中命名的临时名称*表*。 如果指定本地别名，则必须使用本地的别名，而不是整个 SELECT 语句的表名称。 本地别名不会影响 Visual FoxPro 环境。  
  
 其中*JoinCondition* [AND *JoinCondition* ...]   [AND&#124;或者*FilterCondition* [AND&#124;或者*FilterCondition* ...]]  
 告知 Visual FoxPro 查询结果中包含的特定记录。 在需要从多个表中检索数据。  
  
 *JoinCondition*指定链接在 FROM 子句中的表的字段。 如果您在查询中包含多个表，则应后第一个指定每个表的联接条件。  
  
> [!IMPORTANT]  
>  创建联接条件时，请考虑以下信息：  
  
-   如果在查询中包括两个表，并且未指定联接条件，第一个表中的每个记录已联接到第二个表中的每个记录，只要满足筛选器条件。 此类查询可以生成很长的结果。  
  
-   联接表使用空字段，因为 Visual FoxPro 与空字段相匹配时要格外小心。 例如，如果客户上联接。ZIP 和发票。压缩并将查询输出客户包含 100 空邮政编码和发票包含 400 空邮政编码，如果包含 40,000 额外记录而产生的空字段。 使用**空 （)** 函数来消除从查询输出的空记录。  
  
-   您必须使用 AND 运算符连接多个联接条件。 每个联接条件具有以下形式：  
  
     *比较 FieldName1 FieldName2*  
  
     *FieldName1*是一个表中的字段的名称*FieldName2*是另一个表中的字段的名称和*比较*是下表中描述的运算符之一。  
  
|运算符|比较|  
|--------------|----------------|  
|=|等于|  
|==|全等|  
|LIKE|类似于 SQL 的|  
|<>, !=, #|不等于|  
|>|多个|  
|>=|大于或等于|  
|<|小于|  
|<=|小于或等于|  
  
 当你使用 = 运算符使用字符串，其作用方式不同，具体取决于设置 ANSI 设置。 当设置 ANSI 设置为 OFF 时，Visual FoxPro 将以 Xbase 用户熟悉的方式处理字符串比较。 当设置 ANSI 设置为 ON 时，Visual FoxPro 遵循 ANSI 标准的字符串比较。 请参阅[设置 ANSI](../../odbc/microsoft/set-ansi-command.md)并[确切设置](../../odbc/microsoft/set-exact-command.md)有关 Visual FoxPro 执行字符串比较方式的详细信息。  
  
 *FilterCondition*指定记录包含在查询结果而必须满足的条件。 可以包含任意数量的筛选条件的查询中根据需要，将它们连接用 AND 或 OR 运算符。 此外可以使用 NOT 运算符来反转逻辑表达式的值也可以使用**空 （)** 若要检查的空字段。 *FilterCondition*可以采用任何窗体在下面的示例中：  
  
 **示例 1** *FieldName1 FieldName2 比较*  
  
 `customer.cust_id = orders.cust_id`  
  
 **示例 2** *FieldName 比较表达式*  
  
 `payments.amount >= 1000`  
  
 **示例 3** *FieldName 比较*所有 (*子查询*)  
  
 `company < ALL ;`  
  
 `(SELECT company FROM customer WHERE country = "USA")`  
  
 当筛选器条件包括所有时，该字段必须满足查询结果中包括的记录之前，先由子查询生成的所有值的比较条件。  
  
 **示例 4** *FieldName 比较*ANY &#124; SOME (*子查询*)  
  
 `company < ANY ;`  
  
 `(SELECT company FROM customer WHERE country = "USA")`  
  
 当筛选条件包含所有或部分时，该字段必须满足至少一个子查询生成的值的比较条件。  
  
 以下示例检查以查看字段中的值是否在指定的值范围内：  
  
 **示例 5** *FieldName* [NOT] 之间*Start_Range* AND *End_Range*  
  
 `customer.postalcode BETWEEN 90000 AND 99999`  
  
 以下示例检查以查看是否至少有一行符合子查询中的条件。 当筛选条件包含 EXISTS 时，筛选器条件的计算结果为 True (。T。） 除非子查询的计算结果为空集。  
  
 **示例 6** [NOT] 存在 (*子查询*)  
  
 `EXISTS ;`  
  
 `(SELECT * FROM orders WHERE customer.postalcode =`  
  
 `orders.postalcode)`  
  
 **示例 7** *FieldName* [NOT] IN *Value_Set*  
  
 `customer.postalcode NOT IN ("98052","98072","98034")`  
  
 当筛选条件包含 IN 时，字段必须包含一个值的查询结果中包括的记录之前，先。  
  
 **示例 8** *FieldName* [NOT] IN (*子查询*)  
  
 `customer.cust_id IN ;`  
  
 `(SELECT orders.cust_id FROM orders WHERE orders.city="Seattle")`  
  
 此处的字段必须包含一个查询结果中包括的记录之前，先子查询返回的值。  
  
 **示例 9** *FieldName* [NOT] LIKE *cExpression*  
  
 `customer.country NOT LIKE "USA"`  
  
 此筛选条件搜索匹配的每个字段*cExpression*。 作为的一部分，可以使用百分号 （%） 和下划线 (_) 通配符*cExpression*。 下划线表示一个未知的字符在字符串中。  
  
 GROUP BY *GroupColumn* [， *GroupColumn* ...]  
 基于一个或多个列中的值在查询中的行进行分组。 *GroupColumn*可以是以下之一：  
  
-   常规表字段的名称。  
  
-   一个字段，包括 SQL 字段函数。  
  
-   数值表达式，指示结果表中的列的位置。 （最左侧的列数为 1。）  
  
 具有*FilterCondition*  
 指定必须满足组的查询结果中包含的筛选器条件。 HAVING 应与 GROUP BY 和可以包含任意数量的筛选条件所需连接 and 或 OR 运算符。 您还可用于不反转逻辑表达式的值。  
  
 *FilterCondition*不能包含子查询。  
  
 不带 GROUP BY 子句的 HAVING 子句的行为类似于 WHERE 子句。 可以在 HAVING 子句中使用本地别名和字段函数。 WHERE 子句用于更快的性能，如果 HAVING 子句中包含没有字段函数。  
  
 [[ALL] UNION *SELECTCommand*]  
 将组选择的最终结果与另一个选择的最终结果结合起来。 默认情况下，UNION 检查组合的结果，并消除重复行。 使用括号来组合多个 UNION 子句。  
  
 所有可防止联合消除重复行的组合结果中。  
  
 UNION 子句遵循以下规则：  
  
-   不能使用 UNION 组合的子查询。  
  
-   这两个选择的命令必须在其查询输出中具有相同的列数。  
  
-   一个选择查询结果中的每一列必须与在其他选择对应的列具有相同的数据类型和宽度。  
  
-   仅最后一个选择可以具有一个 ORDER BY 子句，必须引用输出列的数目。 如果包含 ORDER BY 子句，则它会影响完整的结果。  
  
 在 UNION 子句还可用于模拟外部联接。  
  
 当在查询中联接两个表时，输出中包含仅具有联接字段中的匹配值的记录。 如果父表中的记录的子表中没有相应的记录，输出中不包含父表中的记录。 外部联接可以包括在输出中，以及在子表中的匹配记录的父表中的所有记录。 若要在 Visual FoxPro 中创建外部联接，必须使用嵌套的 SELECT 命令，如以下示例所示：  
  
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
>  请确保包含每个分号后面紧跟的空间。 否则，将收到错误。  
  
 具有匹配的值之前的 UNION 子句选择两个表中记录的命令的一部分。 不具有关联的发票客户公司不包括在内。 命令在 UNION 子句之后的部分不具有匹配的订单表中的记录在 customer 表中选择记录。  
  
 有关命令的第二个部分，请注意以下事项：  
  
-   首先处理 SELECT 语句的括号中。 此语句创建订单表中选择的所有客户编号。  
  
-   WHERE 子句查找不在订单表中的 customer 表中所有的客户编号。 由于该命令的第一个部分提供了客户编号订单表中的所有公司，customer 表中的所有公司现在都包含查询结果中。  
  
-   在第二个 SELECT 语句来表示联合中包含的表的结构必须完全相同，因为有两个占位符*orders.order_id*并*orders.emp_id*从第一个选择语句。  
  
    > [!NOTE]  
    >  占位符必须与它们所表示的字段相同的类型。 如果此字段为日期类型，应为占位符 {/ /}。 如果该字段是字符字段，占位符应为空字符串 ("")。  
  
 排序依据*Order_Item* [ASC &#124; DESC] [， *Order_Item* [ASC &#124; DESC]...]  
 排序查询结果基于一个或多个列中的数据。 每个*Order_Item*必须对应于查询结果中的列和可以是以下之一：  
  
-   也是主要的 SELECT 子句 （不在子查询） 中选择项的从表中的字段。  
  
-   数值表达式，指示结果表中的列的位置。 (最左侧的列是数字 1。)  
  
 ASC 指定升序顺序的查询结果中，根据订单项或项，并且默认值为 ORDER BY。  
  
 DESC 指定查询结果的降序顺序。  
  
 如果未指定顺序使用 ORDER BY 查询结果将显示未排序。  
  
## <a name="remarks"></a>备注  
 选择是像任何其他 Visual FoxPro 命令内置于 Visual FoxPro 的 SQL 命令。 当你使用时选择此选项可以带来查询、 Visual FoxPro 解释查询，并从表中检索指定的数据。 （与任何其他 Visual FoxPro 命令），可以创建从命令提示符窗口或 Visual FoxPro 程序内的 SELECT 查询。  
  
> [!NOTE]  
>  选择不遵从设置筛选器与指定的当前筛选器条件。  
  
## <a name="driver-remarks"></a>驱动程序备注  
 当你的应用程序将发送到数据源的 ODBC SQL 语句选择时，Visual FoxPro ODBC 驱动程序将无需转换的 Visual FoxPro 选择命令转换为命令除非该命令包含 ODBC 转义序列。 ODBC 转义序列中的项将转换为 Visual FoxPro 语法。 有关使用 ODBC 转义序列，请参阅[时间和日期函数](../../odbc/microsoft/time-and-date-functions-visual-foxpro-odbc-driver.md)并在*Microsoft ODBC 程序员参考*，请参阅[ODBC 中的转义序列](../../odbc/reference/develop-app/escape-sequences-in-odbc.md).  
  
## <a name="see-also"></a>请参阅  
 [创建表的 SQL](../../odbc/microsoft/create-table-sql-command.md)   
 [INSERT-SQL](../../odbc/microsoft/insert-sql-command.md)   
 [SET ANSI](../../odbc/microsoft/set-ansi-command.md)   
 [设置完全](../../odbc/microsoft/set-exact-command.md)
