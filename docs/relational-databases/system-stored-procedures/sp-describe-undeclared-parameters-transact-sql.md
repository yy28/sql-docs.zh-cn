---
title: sp_describe_undeclared_parameters (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/15/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_describe_undeclared_parameters
- sp_describe_undeclared_parameters_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_describe_undeclared_parameters
ms.assetid: 6f016da6-dfee-4228-8b0d-7cd8e7d5a354
caps.latest.revision: 22
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 9b6b17565a12cde0148982f82cf4b84bd1fd8db1
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43099861"
---
# <a name="spdescribeundeclaredparameters-transact-sql"></a>sp_describe_undeclared_parameters (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-asdw-xxx-md.md)]

  返回包含有关中的未声明参数的元数据的结果集[!INCLUDE[tsql](../../includes/tsql-md.md)]批处理。 考虑使用在每个参数 **\@tsql**批处理，但不是声明中 **\@params**。 每个此类参数在返回的结果集中各占一行，并包含推断的参数类型信息。 该过程返回空结果集如果 **\@tsql**输入的批处理仅包含的参数中声明 **\@params**。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```sql
  
sp_describe_undeclared_parameters   
    [ @tsql = ] 'Transact-SQL_batch'   
    [ , [ @params = ] N'parameters' data type ] [, ...n]  
```  
  
## <a name="arguments"></a>参数  
 [  **\@tsql =** ] **'***Transact SQL_batch*****  
 一个或多个 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句。 *Transact SQL_batch*可能**nvarchar (***n***)** 或**nvarchar （max)**。  
  
 [  **\@params =** ] **N'***参数*****  
 \@params 参数提供声明字符串[!INCLUDE[tsql](../../includes/tsql-md.md)]批处理，类似于方式 sp_executesql 工作原理。 *参数*可能**nvarchar (***n***)** 或**nvarchar （max)**。  
  
 是一个字符串，它包含的定义中嵌入的所有参数*Transact SQL_batch*。 字符串必须是 Unicode 常量或 Unicode 变量。 每个参数定义由参数名称和数据类型组成。 n 是表示附加参数定义的占位符。 如果 TRANSACT-SQL 语句中的批处理不包含参数，\@参数不是必需的。 该参数的默认值为 NULL。  
  
 数据类型  
 参数的数据类型。  
  
## <a name="return-code-values"></a>返回代码值  
 **sp_describe_undeclared_parameters**始终返回零返回状态成功。 如果该过程引发错误并且作为 RPC 调用该过程，sys.dm_exec_describe_first_result_set 的 error_type 列中所述的错误的类型由填充返回的状态。 如果该过程是从 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中调用的，则返回值始终为零，甚至在出现错误情况时也不例外。  
  
## <a name="result-sets"></a>结果集  
 **sp_describe_undeclared_parameters**返回以下结果集。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**parameter_ordinal**|**int NOT NULL**|在结果集中包含参数的序号位置。 第一个参数的位置将指定为 1。|  
|**名称**|**sysname NOT NULL**|包含参数的名称。|  
|**suggested_system_type_id**|**int NOT NULL**|包含**system_type_id** sys.types 中指定的参数的数据类型。<br /><br /> 对于 CLR 类型，即使**system_type_name**列将返回 NULL，此列将返回值 240。|  
|**suggested_system_type_name**|**nvarchar (256) NULL**|包含数据类型名称。 包含为参数数据类型指定的参数（例如，length、precision、scale）。 如果数据类型是用户定义的别名类型，则会在此处指定基本系统类型。 如果数据类型是 CLR 用户定义数据类型，则在此列中返回 NULL。 如果无法推断参数类型，则返回 NULL。|  
|**suggested_max_length**|**smallint NOT NULL**|请参阅 sys.columns。 有关**max_length**列的说明。|  
|**suggested_precision**|**tinyint NOT NULL**|请参阅 sys.columns。 了解有关精度列的说明。|  
|**suggested_scale**|**tinyint NOT NULL**|请参阅 sys.columns。 了解有关小数位数列的说明。|  
|**suggested_user_type_id**|**int NULL**|对于 CLR 和别名类型，包含在 sys.types 中指定的列数据类型的 user_type_id。 否则为 NULL。|  
|**suggested_user_type_database**|**sysname NULL**|对于 CLR 和别名类型，包含在其中定义相应类型的数据库的名称。 否则为 NULL。|  
|**suggested_user_type_schema**|**sysname NULL**|对于 CLR 和别名类型，包含在其中定义相应类型的架构的名称。 否则为 NULL。|  
|**suggested_user_type_name**|**sysname NULL**|对于 CLR 和别名类型，包含类型的名称。 否则为 NULL。|  
|**suggested_assembly_qualified_type_name**|**nvarchar (4000) NULL**|对于 CLR 类型，返回的程序集和类定义的类型的名称。 否则为 NULL。|  
|**suggested_xml_collection_id**|**int NULL**|包含 sys.columns 中指定的参数的数据类型的 xml_collection_id。 如果返回的类型与 XML 架构集合不关联，则该列将返回 NULL。|  
|**suggested_xml_collection_database**|**sysname NULL**|包含定义与此类型关联的 XML 架构集合的数据库。 如果返回的类型与 XML 架构集合不关联，则该列将返回 NULL。|  
|**suggested_xml_collection_schema**|**sysname NULL**|包含定义与此类型关联的 XML 架构集合的架构。 如果返回的类型与 XML 架构集合不关联，则该列将返回 NULL。|  
|**suggested_xml_collection_name**|**sysname NULL**|包含与此类型关联的 XML 架构集合的名称。 如果返回的类型与 XML 架构集合不关联，则该列将返回 NULL。|  
|**suggested_is_xml_document**|**位 NOT NULL**|如果要返回的类型为 XML，并且保证该类型是 XML 文档，则返回 1。 否则，返回 0。|  
|**suggested_is_case_sensitive**|**位 NOT NULL**|如果列为区分大小写的字符串类型，则返回 1；否则，返回 0。|  
|**suggested_is_fixed_length_clr_type**|**位 NOT NULL**|如果列为固定长度 CLR 类型，则返回 1；否则，返回 0。|  
|**suggested_is_input**|**位 NOT NULL**|如果在赋值语句左侧以外的任何地方使用参数，则返回 1。 否则，返回 0。|  
|**suggested_is_output**|**位 NOT NULL**|如果在赋值语句左侧使用参数或将参数传递给存储过程的输出参数，则返回 1。 否则，返回 0。|  
|**formal_parameter_name**|**sysname NULL**|如果参数是存储过程或用户定义的函数的参数，则返回相应形参的名称。 否则，返回 NULL。|  
|**suggested_tds_type_id**|**int NOT NULL**|供内部使用。|  
|**suggested_tds_length**|**int NOT NULL**|供内部使用。|  
  
## <a name="remarks"></a>Remarks  
 **sp_describe_undeclared_parameters**始终返回零返回状态。  
  
 最常见的用途是，为应用程序提供的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句可能包含一些参数，并且必须以某种方式处理这些参数。 一个示例是在其中用户提供了使用 ODBC 参数语法的查询的用户界面 （如 ODBCTest 或 RowsetViewer）。 应用程序必须动态查找参数数目，并提示用户输入每个参数。  
  
 另一个例子是，在没有用户输入时，应用程序必须循环访问这些参数，并从某个其他位置（例如，表）获取这些参数的数据。 在这种情况下，应用程序不必同时传递所有参数信息。 相反，应用程序可以从提供程序中获取所有参数信息，并从表中获取数据本身。 使用代码**sp_describe_undeclared_parameters**是更泛型，并不大可能需要进行修改，如果数据结构的更改更高版本。  
  
 **sp_describe_undeclared_parameters**在任何以下情况下返回错误。  
  
-   如果输入\@tsql 不是有效[!INCLUDE[tsql](../../includes/tsql-md.md)]批处理。 通过解析和分析确定有效性[!INCLUDE[tsql](../../includes/tsql-md.md)]批处理。 在查询优化期间或在执行期间由批处理导致的任何错误时确定不会考虑是否[!INCLUDE[tsql](../../includes/tsql-md.md)]批处理是否有效。  
  
-   如果\@params 不为 NULL，并且包含一个字符串，不是语法上有效声明字符串参数，或如果它包含一个字符串，其用于声明任何参数不止一次。  
  
-   如果输入[!INCLUDE[tsql](../../includes/tsql-md.md)]批处理中声明的参数声明具有相同名称的本地变量\@params。  
  
-   如果语句引用临时表。  
  
 如果\@tsql 没有任何参数中, 声明\@参数，该过程返回空结果集。  
  
## <a name="parameter-selection-algorithm"></a>参数选择算法  
 对于具有未声明的参数的查询，将通过三个步骤推断未声明的参数的数据类型。  
  
 **步骤 1**  
  
 要推断具有未声明的参数的查询的数据类型，第一步骤是查找数据类型不依赖于未声明的参数的所有子表达式的数据类型。 可以确定以下表达式的类型：  
  
-   列、常量、变量以及声明的参数。  
  
-   调用用户定义的函数 (UDF) 的结果。  
  
-   数据类型不依赖于所有输入的未声明参数的表达式。  
  
 例如，请考虑 `SELECT dbo.tbl(@p1) + c1 FROM t1 WHERE c2 = @p2 + 2` 查询。 表达式 dbo.tbl (\@p1) + c1 和 c2 具有数据类型和表达式\@p1 和\@p2 + 2 没有。  
  
 在执行此步骤后，如果任何表达式（对 UDF 的调用除外）有两个没有数据类型的参数，类型推断将失败并发生错误。 例如，下面的语句均产生错误：  
  
```sql
SELECT * FROM t1 WHERE @p1 = @p2  
SELECT * FROM t1 WHERE c1 = @p1 + @p2  
SELECT * FROM t1 WHERE @p1 = SUBSTRING(@p2, 2, 3)  
```  
  
 以下示例不产生错误：  
  
```sql
SELECT * FROM t1 WHERE @p1 = dbo.tbl(c1, @p2, @p3)  
```
  
 **步骤 2**  
  
 为给定的未声明参数\@p，类型推断算法查找最内部表达式 E (\@p)，其中包含\@p 是以下值之一：  
  
-   比较或赋值运算符的参数。  
  
-   用户定义的函数（包括表值 UDF）、过程或方法的参数。  
  
-   参数**值**子句**插入**语句。  
  
-   参数**CAST**或**转换**。  
  
 类型推断算法查找目标数据类型 TT (\@p) 为 E (\@p)。 上述示例的目标数据类型如下所示：  
  
-   比较或赋值语句的另一侧的数据类型。  
  
-   将此参数传递到的参数的声明数据类型。  
  
-   将该值插入到的列的数据类型。  
  
-   要将语句转换到的数据类型。  
  
 例如，请考虑 `SELECT * FROM t WHERE @p1 = dbo.tbl(@p2 + c1)` 查询。 然后 E (\@p1) = \@p1，E (\@p2) = \@p2 + c1，TT (\@p1) 是声明的返回数据类型以及 dbo.tbl 和 TT (\@p2) 是 dbo.tbl 的声明的参数数据类型。  
  
 如果\@p 类型推断算法确定第 2 步： 开头列出的任何表达式中不包含该电子 (\@p) 是包含的最大标量表达式\@p 和类型推断算法不计算的目标数据类型 TT (\@p) 为 E (\@p)。 例如，如果查询为 SELECT`@p + 2`然后 E (\@p) = \@p + 2，并且没有 TT (\@p)。  
  
 **步骤 3**  
  
 现在该 E (\@p) 和 TT (\@p) 是标识，类型推断算法将按一种数据类型为\@p 中的以下两种方法之一：  
  
-   简单推断  
  
     如果 E (\@p) = \@p 和 TT (\@p) 存在，即，如果\@p 是直接在步骤 2 开头列出的一个表达式的参数，类型推断算法将推导的数据类型\@p 为 TT （\@p)。 例如：  
  
    ```sql
    SELECT * FROM t WHERE c1 = @p1 AND @p2 = dbo.tbl(@p3)  
    ```  
  
     数据类型为\@p1 \@p2，和\@p3 将 c1，以及 dbo.tbl 返回数据类型的数据类型并且分别键入 dbo.tbl 参数数据。  
  
     作为一种特殊情况，如果\@p 是参数\<，>， \<= 或 > = 运算符，简单推断规则不适用。 类型推断算法使用下一节介绍的一般推断规则。 例如，如果 c1 是 char(30) 数据类型的列，请考虑下面两个查询：  
  
    ```sql
    SELECT * FROM t WHERE c1 = @p  
    SELECT * FROM t WHERE c1 > @p  
    ```  
  
     在第一种情况下，类型推断算法将推导**char （30)** 的数据类型为\@p 根据本主题前面的规则。 在第二种情况下，类型推断算法将推导**varchar(8000)** 根据下一节中的一般推断规则。  
  
-   一般推断  
  
     如果简单推断不适用，则为未声明的参数考虑以下数据类型：  
  
    -   整数数据类型 (**位**， **tinyint**， **smallint**， **int**， **bigint**)  
  
    -   Money 数据类型 (**smallmoney**，**资金**)  
  
    -   浮点数据类型 (**float**，**实际**)  
  
    -   **数值 （38，19）** -不考虑其他 numeric 或 decimal 数据类型。  
  
    -   **varchar(8000)**， **varchar （max)**， **nvarchar(4000)**，并且**nvarchar （max)** -其他字符串数据类型 (如**文本**， **char （8000)**， **nvarchar(30)** 等) 不被视为。  
  
    -   **varbinary(8000)** 并**varbinary （max)** -不考虑其他二进制数据类型 (如**图像**， **binary(8000)**， **varbinary(30)**，等等。)。  
  
    -   **日期**， **time(7)**， **smalldatetime**， **datetime**， **datetime2(7)**， **datetimeoffset(7)** -其他日期和时间类型，如**time(4)**，不考虑。  
  
    -   **sql_variant**  
  
    -   **xml**  
  
    -   CLR 系统定义的类型 (**hierarchyid**， **geometry**， **geography**)  
  
    -   CLR 用户定义的类型  
  
### <a name="selection-criteria"></a>选择条件  
 在候选数据类型中，将拒绝使查询无效的任何数据类型。 在其余候选数据类型中，类型推断算法将根据以下规则选择一种数据类型。  
  
1.  生成最少数量的 E 中隐式转换的数据类型 (\@p) 处于选中状态。 如果特定的数据类型将生成的数据类型 e (\@p) 不同于 TT (\@p)，类型推断算法认为这是从电子的数据类型的额外隐式转换 (\@p) 到 TT (\@p)。  
  
     例如：  
  
    ```sql
    SELECT * FROM t WHERE Col_Int = Col_Int + @p  
    ```  
  
     在此情况下，E (\@p) 为 Col_Int + \@p 和 TT (\@p) 是**int**。**int**为选择\@p 因为它不产生隐式转换。 选择任何其他数据类型都会产生至少一次隐式转换。  
  
2.  如果多种数据类型都产生次数最少的转换，则使用具有较高优先级的数据类型。 例如：  
  
    ```sql
    SELECT * FROM t WHERE Col_Int = Col_smallint + @p  
    ```  
  
     在这种情况下， **int**并**smallint**产生一次转换。 每种其他数据类型产生多次转换。 因为**int**优先于**smallint**， **int**用于\@p。 有关数据类型优先级的详细信息，请参阅[数据类型优先级&#40;TRANSACT-SQL&#41;](../../t-sql/data-types/data-type-precedence-transact-sql.md)。  
  
     只有在每种数据类型之间的隐式转换次数相同（按照规则 1）并且某种数据类型具有最高优先级时，此规则才适用。 如果没有隐式转换，数据类型推断将失败并发生错误。 例如在查询`SELECT @p FROM t`，数据类型推断失败，因为任何数据类型为\@p 是很好。 例如，没有从隐式转换**int**到**xml**。  
  
3.  如果两个类似的数据类型按照规则 1，例如**varchar(8000)** 并**varchar （max)** 较小数据类型 (**varchar(8000)**) 选择。 相同原则也适用于**nvarchar**并**varbinary**数据类型。  
  
4.  就规则 1 而言，类型推断算法倾向于将某些转换视为比其他转换好。 转换从最好到最坏依次为：  
  
    1.  不同长度的相同基本数据类型之间的转换。  
  
    2.  相同的数据类型的固定长度和可变长度版本之间的转换 (例如， **char**到**varchar**)。  
  
    3.  之间的转换**NULL**并**int**。  
  
    4.  任何其他转换。  
  
 例如，对于查询`SELECT * FROM t WHERE [Col_varchar(30)] > @p`， **varchar(8000)** 因为转换 (a) 是最佳选择。 查询`SELECT * FROM t WHERE [Col_char(30)] > @p`， **varchar(8000)** 仍选择，因为它会导致类型 (b) 转换，因为另一个选项 (如**varchar(4000)**) 会导致类型 (d) 转换。  
  
 作为最后一个示例中，给定一个查询`SELECT NULL + @p`， **int**为选择\@p 因为它产生类型 (c) 转换。  
  
## <a name="permissions"></a>Permissions  
 需要具有执行权限\@tsql 自变量。  
  
## <a name="examples"></a>示例  
 以下示例返回一些信息，例如，未声明的 `@id` 和 `@name` 参数的预期数据类型。  
  
```sql
sp_describe_undeclared_parameters @tsql =   
N'SELECT object_id, name, type_desc   
FROM sys.indexes  
WHERE object_id = @id OR name = @name'  
  
```  
  
 如果 `@id` 参数是作为 `@params` 引用提供的，则会在结果集中省略 `@id` 参数，而仅描述 `@name` 参数。  
  
```sql
sp_describe_undeclared_parameters @tsql =   
N'SELECT object_id, name, type_desc   
FROM sys.indexes  
WHERE object_id = @id OR NAME = @name',  
@params = N'@id int'  
  
```  
  
## <a name="see-also"></a>请参阅  
 [sp_describe_first_result_set &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md)   
 [sys.dm_exec_describe_first_result_set &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-transact-sql.md)   
 [sys.dm_exec_describe_first_result_set_for_object &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-for-object-transact-sql.md)
