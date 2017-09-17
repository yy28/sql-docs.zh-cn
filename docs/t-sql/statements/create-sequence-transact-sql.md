---
title: "创建序列 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 04/11/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SEQUENCE
- CREATE SEQUENCE
- SEQUENCE_TSQL
- CREATE_SEQUENCE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE SEQUENCE statement
- sequence number object, creating
- sequence object
- number, sequence
ms.assetid: 419f907b-8a72-4d6c-80cb-301df44c24c1
caps.latest.revision: 40
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 89a96d101c17f528b9ff14ca523e5dc41ada2f4c
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="create-sequence-transact-sql"></a>CREATE SEQUENCE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  创建一个序列对象并指定其属性。 序列是用户定义的绑定到架构的对象，该对象可根据创建序列所依据的规范来生成数值序列。 这组数值以定义的间隔按升序或降序生成，并且可配置为用尽时重新启动（循环）。 序列不与特定表相关联，这一点与标识列不同。 应用程序将引用某一序列对象以便检索其下一个值。 序列与表之间的关系由应用程序控制。 用户应用程序可以引用一个序列对象，并跨多个行和表协调值。  
  
 与不同的是标识列插入行时生成的值，应用程序可以获得下一个序列号而不必通过调用插入行[NEXT VALUE FOR 函数](../../t-sql/functions/next-value-for-transact-sql.md)。 使用 [sp_sequence_get_range](../../relational-databases/system-stored-procedures/sp-sequence-get-range-transact-sql.md) 同时获取多个序列号。  
  
 有关同时使用 **CREATE SEQUENCE** 和 **NEXT VALUE FOR** 函数的信息，请参阅 [序列号](../../relational-databases/sequence-numbers/sequence-numbers.md)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
CREATE SEQUENCE [schema_name . ] sequence_name  
    [ AS [ built_in_integer_type | user-defined_integer_type ] ]  
    [ START WITH <constant> ]  
    [ INCREMENT BY <constant> ]  
    [ { MINVALUE [ <constant> ] } | { NO MINVALUE } ]  
    [ { MAXVALUE [ <constant> ] } | { NO MAXVALUE } ]  
    [ CYCLE | { NO CYCLE } ]  
    [ { CACHE [ <constant> ] } | { NO CACHE } ]  
    [ ; ]  
```  
  
## <a name="arguments"></a>参数  
 *sequence_name*  
 指定数据库中标识序列的唯一名称。 类型是**sysname**。  
  
 [ built_in_integer_type | user-defined_integer_type  
 序列可定义为任何整数类型。 允许使用下面的类型。  
  
-   **tinyint** -0 到 255 范围  
  
-   **smallint** -范围-32,768 到 32,767  
  
-   **int** -范围-2,147,483,648 到 2,147,483,647  
  
-   **bigint** -范围-9223372036854775808 到 9223372036854775807  
  
-   **十进制**和**数值**小数位数为 0。  
  
-   基于这些允许类型之一的任何用户定义数据类型（别名类型）。  
  
 如果未不提供任何数据类型， **bigint**数据类型用作默认值。  
  
 开始\<常量 >  
 序列对象返回的第一个值。 **启动**值必须是值小于或等于最大值并大于或等于序列对象的最小值。 新序列对象的默认起始值是升序序列对象的最小值和降序序列对象的最大值。  
  
 递增通过\<常量 >  
 值，该值用于递增 （或递减如果负） 每次调用序列对象的值**NEXT VALUE FOR**函数。 如果增量是负值，则序列对象为降序，否则为升序。 增量不能为 0。 新序列对象的默认增量为 1。  
  
 [MINVALUE\<常量 > |**没有 MINVALUE** ]  
 指定序列对象的边界。 一个新序列对象的默认最小值是该序列对象的数据类型的最小值。 对于 **tinyint** 数据类型，此值为零，对于所有其他数据类型则为负数。  
  
 [MAXVALUE\<常量 > |**没有 MAXVALUE**  
 指定序列对象的边界。 一个新序列对象的默认最大值是该序列对象的数据类型的最大值。  
  
 [周期 |**NO 周期**]  
 此属性指定当超过序列对象的最小值或最大值时，序列对象是应从最小值（对于降序序列对象，则为最大值）重新开始，还是应引发异常。 新序列对象的默认循环选项是 NO CYCLE。  
  
 请注意，循环不从起始值重新开始，而是从最小值或最大值重新开始。  
  
 [**缓存**[\<常量 >] |无缓存]  
 通过最大限度地减少生成序列编号所需的磁盘 IO 数，可以提高使用序列对象的应用程序的性能。 默认值为 CACHE。  
  
 例如，如果选择的缓存大小为 50，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]不会保留缓存的 50 单个值。 它只是缓存当前值和缓存中保留的值数。 这意味着，存储缓存所需的内存量始终为序列对象的数据类型的两个实例。  
  
> [!NOTE]  
>  如果启用缓存选项而不指定缓存大小，数据库引擎将选择一个大小。 但是，所选的大小并不是一成不变。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 可能会更改计算缓存大小的方法而不另行通知。  
  
 当使用创建时**缓存**选项，意外的关机 （如电源故障） 可能会导致在缓存中剩余的序列号丢失。  
  
## <a name="general-remarks"></a>一般备注  
 序列号在当前事务的作用域之外生成。 无论提交还是回滚使用序列号的事务，都会占用序列号。  
  
### <a name="cache-management"></a>缓存管理  
 若要提高性能，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]预先分配的由指定的序列号数**缓存**自变量。  
  
 例如，用起始值 1 和缓存大小 15 创建一个新序列。 在需要第一个值时，便可从内存中使用值 1 到 15。 最后缓存的值 (15) 将写入磁盘上的系统表中。 使用完所有的 15 个数字后，下一个请求（数字 16）将导致重新分配缓存。 新的最后缓存值 (30) 将写入系统表中。  
  
 如果在使用了 22 个数字后[!INCLUDE[ssDE](../../includes/ssde-md.md)]停止，则会将内存中的下一个预期序列号 (23) 写入系统表，替换以前存储的数字。  
  
 在 SQL Server 重新启动并且需要一个序列号之后，将从系统表中读取起始编号 (23)。 会为内存分配 15 个数字 (23-38) 的缓存量，并将下一个非缓存编号 (39) 写入到系统表。  
  
 如果[!INCLUDE[ssDE](../../includes/ssde-md.md)]带从系统表 (39) 数字读异常为如电源故障事件停止，该序列重启。 任何序列分配给内存 （但永远不会由用户或应用程序请求） 的数字将会丢失。 此功能可能留有间隔，但相同的值将永远不会颁发两次为单个序列对象除非它被定义为保证**周期**或手动重新启动。  
  
 将通过跟踪当前值（发出的最后一个值）和缓存中留下的值数量来在内存中保留缓存。 因此，缓存所使用的内存量始终为序列对象的数据类型的两个实例。  
  
 将缓存参数设置为**无缓存**将写入系统表的每次使用一个序列的当前序列值。 这样会增加磁盘访问，从而降低性能，但可以减少出现意外间隙的机会。 数字方式请求使用时，仍会发生缺口**NEXT VALUE FOR**或**sp_sequence_get_range**函数，但随后数字或者不使用或在未提交的事务中使用。  
  
 当某一序列对象使用**缓存**选项，如果在重新启动序列对象，或更改**递增**，**周期**， **MINVALUE**，**MAXVALUE**，或缓存大小属性，它将导致缓存要写入的系统表之前发生更改。 然后，从当前值（即没有跳过任何数字）开始重新加载缓存。 更改缓存大小将立即生效。  
  
 **缓存的值不可用时，缓存选项**  
  
 使用下列过程每次进行一个序列对象请求生成的下一步值**缓存**选项如果有可用的未使用的值在序列对象的内存中缓存中。  
  
1.  计算序列对象的下一个值。  
  
2.  在内存中更新该序列对象的新当前值。  
  
3.  将计算的值返回给调用语句。  
  
 **在用完缓存的缓存选项**  
  
 每次请求序列对象生成的下一个值，以下进程时发生**缓存**如果已耗尽缓存选项：  
  
1.  计算序列对象的下一个值。  
  
2.  计算新缓存的最后一个值。  
  
3.  锁定序列对象的系统表行，将在步骤 2 中计算的值（最后一个值）写入系统 表。 触发缓存已用完的 xevent，向用户通知新的持久值。  
  
 **无缓存选项**  
  
 使用下列过程每次进行一个序列对象请求生成的下一步值**无缓存**选项：  
  
1.  计算序列对象的下一个值。  
  
2.  将序列对象的新当前值写入系统表。  
  
3.  将计算的值返回给调用语句。  
  
## <a name="metadata"></a>元数据  
 有关序列的信息，请查询 [sys.sequences](../../relational-databases/system-catalog-views/sys-sequences-transact-sql.md)。  
  
## <a name="security"></a>安全性  
  
### <a name="permissions"></a>Permissions  
 要求对 SCHEMA 拥有 **CREATE SEQUENCE**、 **ALTER**或 **CONTROL** 权限。  
  
-   Db_owner 和 db_ddladmin 固定数据库角色的成员可以创建、 更改和删除序列对象。  
  
-   Db_owner 和 db_datawriter 固定数据库角色的成员可以通过从而导致它们来生成随机数更新序列对象。  
  
 下面的示例授予用户在测试架构中创建序列 AdventureWorks\Larry 权限。  
  
```  
GRANT CREATE SEQUENCE ON SCHEMA::Test TO [AdventureWorks\Larry]  
```  
  
 可以使用传输序列对象的所有权**ALTER AUTHORIZATION**语句。  
  
 如果序列使用用户定义的数据类型，则序列的创建者必须对该类型拥有 REFERENCES 权限。  
  
### <a name="audit"></a>审核  
 审核**创建序列**，监视器**SCHEMA_OBJECT_CHANGE_GROUP**。  
  
## <a name="examples"></a>示例  
 创建序列和使用的示例**NEXT VALUE FOR**函数来生成序列号，请参阅[序列号](../../relational-databases/sequence-numbers/sequence-numbers.md)。  
  
 大部分下面的示例在名为 Test 的架构中创建序列对象。  
  
 若要创建测试架构，请执行以下语句。  
  
```  
CREATE SCHEMA Test ;  
GO  
```  
  
### <a name="a-creating-a-sequence-that-increases-by-1"></a>A. 创建按 1 递增的序列  
 在下面的示例中，Thierry 创建一个名为 CountBy1 会增加，每次使用它时的序列。  
  
```  
CREATE SEQUENCE Test.CountBy1  
    START WITH 1  
    INCREMENT BY 1 ;  
GO  
```  
  
### <a name="b-creating-a-sequence-that-decreases-by-1"></a>B. 创建按 1 递减的序列  
 以下示例从 0 开始，每次使用时递减 1。  
  
```  
CREATE SEQUENCE Test.CountByNeg1  
    START WITH 0  
    INCREMENT BY -1 ;  
GO  
```  
  
### <a name="c-creating-a-sequence-that-increases-by-5"></a>C. 创建按 5 递增的序列  
 以下示例创建一个每次使用时增加 5 的序列。  
  
```  
CREATE SEQUENCE Test.CountBy1  
    START WITH 5  
    INCREMENT BY 5 ;  
GO  
```  
  
### <a name="d-creating-a-sequence-that-starts-with-a-designated-number"></a>D. 创建以指定数字开始的序列  
 在导入表后，Thierry 注意到所使用的最高 ID 号是 24,328。 Thierry 需要将生成从 24,329 开始的数字的序列。 下面的代码将创建一个从 24,329 开始、增量为 1 的序列。  
  
```  
CREATE SEQUENCE Test.ID_Seq  
    START WITH 24329  
    INCREMENT BY 1 ;  
GO  
```  
  
### <a name="e-creating-a-sequence-using-default-values"></a>E. 使用默认值创建序列  
 以下示例将使用默认值创建一个序列。  
  
```  
CREATE SEQUENCE Test.TestSequence ;  
```  
  
 执行以下语句可查看序列的属性。  
  
```  
SELECT * FROM sys.sequences WHERE name = 'TestSequence' ;  
```  
  
 输出的部分列表演示了默认值。  
  
|||  
|-|-|  
|`start_value`|`-9223372036854775808`|  
|`increment`|`1`|  
|`mimimum_value`|`-9223372036854775808`|  
|`maximum_value`|`9223372036854775807`|  
|`is_cycling`|`0`|  
|`is_cached`|`1`|  
|`current_value`|`-9223372036854775808`|  
  
### <a name="f-creating-a-sequence-with-a-specific-data-type"></a>F. 创建具有特定数据类型的序列  
 下面的示例创建序列使用**smallint**数据类型，从-32,768 到 32,767 的范围。  
  
```  
CREATE SEQUENCE SmallSeq  
    AS smallint ;  
```  
  
### <a name="g-creating-a-sequence-using-all-arguments"></a>G. 使用所有参数创建序列  
 下面的示例创建名为 DecSeq 使用一个序列**十进制**具有介于 0 到 255 之间的数据类型。 序列以 125 开始，每次生成数字时递增 25。 因为该序列配置为可循环，所以，当值超过最大值 200 时，序列将从最小值 100 重新开始。  
  
```  
CREATE SEQUENCE Test.DecSeq  
    AS decimal(3,0)   
    START WITH 125  
    INCREMENT BY 25  
    MINVALUE 100  
    MAXVALUE 200  
    CYCLE  
    CACHE 3  
;  
```  
  
 执行以下语句可查看第一个值；`START WITH` 选项为 125。  
  
```  
SELECT NEXT VALUE FOR Test.DecSeq;  
```  
  
 将该语句再执行三次，以返回 150、175 和 200。  
  
 再次执行该语句，以查看起始值如何循环回到 `MINVALUE` 选项值 100。  
  
 执行以下代码，以确认缓存大小并查看当前值。  
  
```  
SELECT cache_size, current_value   
FROM sys.sequences  
WHERE name = 'DecSeq' ;  
```  
  
## <a name="see-also"></a>另请参阅  
 [ALTER 序列 &#40;Transact SQL &#41;](../../t-sql/statements/alter-sequence-transact-sql.md)   
 [拖放序列 &#40;Transact SQL &#41;](../../t-sql/statements/drop-sequence-transact-sql.md)   
 [下一个值 &#40;Transact SQL &#41;](../../t-sql/functions/next-value-for-transact-sql.md)   
 [序列号](../../relational-databases/sequence-numbers/sequence-numbers.md)  
  
  

