---
title: 联接 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 02/18/2018
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: performance
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- HASH join
- NESTED LOOPS join
- MERGE join
- joins [SQL Server], about joins
- join hints [SQL Server]
ms.assetid: bfc97632-c14c-4768-9dc5-a9c512f4b2bd
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 3f346ab353e7e9e2565198b4a350870cbb224e4c
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37222307"
---
# <a name="joins-sql-server"></a>联接 (SQL Server)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用内存中的排序和哈希联接技术执行排序、交集、并集、差分等操作。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 利用这种类型的查询计划支持垂直表分区（有时称为分列存储）。   

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用三种类型的联接操作：    
-   嵌套循环联接     
-   合并联接   
-   哈希联接   

## <a name="fundamentals"></a> 联接基础知识
通过联接，可以从两个或多个表中根据各个表之间的逻辑关系来检索数据。 联接指明了 Microsoft SQL Server 应如何使用一个表中的数据来选择另一个表中的行。    

联接条件可通过以下方式定义两个表在查询中的关联方式：    
-   指定每个表中要用于联接的列。 典型的联接条件在一个表中指定一个外键，而在另一个表中指定与其关联的键。    
-   指定用于比较各列的值的逻辑运算符（例如 = 或 <>）。    

可以在 `FROM` 或 `WHERE` 子句中指定内部联接。 只能在 `FROM` 子句中指定外部联接。 联接条件与 `WHERE` 和 `HAVING` 搜索条件相结合，用于控制从 `FROM` 子句所引用的基表中选定的行。    

在 `FROM` 子句中指定联接条件有助于将这些联接条件与 `WHERE` 子句中可能指定的其他任何搜索条件分开，建议用这种方法来指定联接。 简化的 ISO FROM 子句联接语法如下：

```
FROM first_table join_type second_table [ON (join_condition)]
```

join_type 指定执行的联接类型：内部、外部或交叉联接。 join_condition 定义用于对每一对联接行进行求值的谓词。 下面是 FROM 子句联接规范示例：

```sql
FROM Purchasing.ProductVendor JOIN Purchasing.Vendor
     ON (ProductVendor.BusinessEntityID = Vendor.BusinessEntityID)
```

下面是使用此联接的一个简单 SELECT 语句：

```sql
SELECT ProductID, Purchasing.Vendor.BusinessEntityID, Name
FROM Purchasing.ProductVendor JOIN Purchasing.Vendor
    ON (Purchasing.ProductVendor.BusinessEntityID = Purchasing.Vendor.BusinessEntityID)
WHERE StandardPrice > $10
  AND Name LIKE N'F%'
GO
```

此选择会返回某个公司所提供的一组产品以及供应商信息，该公司名以字母 F 开头，并且产品价格在 10 美元以上。   

当在单个查询中引用多个表时，所有列引用都必须是明确的。 在上面的示例中，ProductVendor 和 Vendor 表都具有一个名为 BusinessEntityID 的列。 在查询所引用的两个或多个表中，任何重复的列名都必须用表名加以限定。 此示例中对 Vendor 列的所有引用均已限定。   

如果某个列名在查询用到的两个或多个表中不重复，则对该列的引用就必用表名加以限定。 如上例所示。 由于没有指明提供每个列的表，因此这样的 SELECT 语句有时会难以理解。 如果所有的列都用它们的表名加以限定，将会提高查询的可读性。 如果使用了表的别名，将会进一步提高可读性，尤其是当表名自身必须用数据库名和所有者名加以限定时。 下例与上例相同，只不过分配了表的别名并且用表的别名对列加以限定，从而提高了可读性：

```sql
SELECT pv.ProductID, v.BusinessEntityID, v.Name
FROM Purchasing.ProductVendor AS pv 
JOIN Purchasing.Vendor AS v
    ON (pv.BusinessEntityID = v.BusinessEntityID)
WHERE StandardPrice > $10
    AND Name LIKE N'F%';
```

上例是在 FROM 子句中指定联接条件的，这是首选的方法。 下列查询包含相同的联接条件，该联接条件在 WHERE 子句中指定：

```sql
SELECT pv.ProductID, v.BusinessEntityID, v.Name
FROM Purchasing.ProductVendor AS pv, Purchasing.Vendor AS v
WHERE pv.BusinessEntityID=v.BusinessEntityID
    AND StandardPrice > $10
    AND Name LIKE N'F%';
```

联接选择列表可以引用联接表中的所有列或任意一部分列。 选择列表不必包含联接中每个表的列。 例如，在三表联接中，只能用一个表作为中间表来联接另外两个表，而选择列表不必引用该中间表的任何列。   

虽然联接条件通常使用相等比较 (=)，但也可以像指定其他谓词一样指定其他比较运算符或关系运算符。 有关详细信息，请参阅[比较运算符 (Transact-SQL)](../../t-sql/language-elements/comparison-operators-transact-sql.md) 和 [WHERE (Transact-SQL)](../../t-sql/queries/where-transact-sql.md)。  

当 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 处理联接时，查询引擎会从多种可行的方法中选择最有效的方法来处理联接。 由于各种联接的实际执行过程会采用多种不同的优化，因此无法可靠地预测。   

联接条件中用到的列不必具有相同的名称或相同的数据类型。 但如果数据类型不相同，则必须兼容，或者是可由 SQL Server 进行隐式转换的类型。 如果数据类型不能进行隐式转换，则联接条件必须使用 `CAST` 函数显式转换数据类型。 有关隐式和显式转换的详细信息，请参阅[数据类型转换（数据库引擎）](../../t-sql/data-types/data-type-conversion-database-engine.md)。    

大多数使用联接的查询可以用子查询（嵌套在其他查询中的查询）重写，并且大多数子查询可以重写为联接。 有关子查询的详细信息，请参阅[子查询](../../relational-databases/performance/subqueries.md)。   

> [!NOTE]
> 不能在 ntext、text 或 image 列上直接联接表。 但可以使用 `SUBSTRING` 在 ntext、text 或 image 列上间接联接表。    
> 例如，`SELECT * FROM t1 JOIN t2 ON SUBSTRING(t1.textcolumn, 1, 20) = SUBSTRING(t2.textcolumn, 1, 20)` 可对表 t1 和 t2 中每个文本列的前 20 个字符进行两表内部联接。   
> 此外，另一种可以采用的比较两个表中 ntext 或 text 列的方法是用 `WHERE` 子句比较这些列的长度，例如：`WHERE DATALENGTH(p1.pr_info) = DATALENGTH(p2.pr_info)`

## <a name="nested_loops"></a> 了解嵌套循环联接
如果一个联接输入很小（不到 10 行），而另一个联接输入很大而且已在其联接列上创建了索引，则索引 Nested Loops 连接是最快的联接操作，因为它们需要的 I/O 和比较都最少。 

嵌套循环联接也称为嵌套迭代，它将一个联接输入用作外部输入表（显示为图形执行计划中的顶端输入），将另一个联接输入用作内部（底端）输入表。 外部循环逐行处理外部输入表。 内部循环会针对每个外部行执行，在内部输入表中搜索匹配行。   

最简单的情况是，搜索时扫描整个表或索引；这称为单纯嵌套循环联接。 如果搜索时使用索引，则称为索引嵌套循环联接。 如果将索引生成为查询计划的一部分（并在查询完成后立即将索引破坏），则称为临时索引嵌套循环联接。 查询优化器考虑了所有这些不同情况。   

如果外部输入较小而内部输入较大且预先创建了索引，则嵌套循环联接尤其有效。 在许多小事务中（如那些只影响较小的一组行的事务），索引嵌套循环联接优于合并联接和哈希联接。 但在大型查询中，嵌套循环联接通常不是最佳选择。    

## <a name="merge"></a> 了解合并联接
如果两个联接输入并不小但已在二者联接列上排序（例如，如果它们是通过扫描已排序的索引获得的），则合并联接是最快的联接操作。 如果两个联接输入都很大，而且这两个输入的大小差不多，则预先排序的合并联接提供的性能与哈希联接相近。 但是，如果这两个输入的大小相差很大，则哈希联接操作通常快得多。       

合并联接要求两个输入都在合并列上排序，而合并列由联接谓词的等效 (ON) 子句定义。 通常，查询优化器扫描索引（如果在适当的一组列上存在索引），或在合并联接的下面放一个排序运算符。 在极少数情况下，虽然可能有多个等效子句，但只用其中一些可用的等效子句获得合并列。    

由于每个输入都已排序，因此 Merge Join 运算符将从每个输入获取一行并将其进行比较。 例如，对于内联接操作，如果行相等则返回。 如果行不相等，则废弃值较小的行并从该输入获得另一行。 这一过程将重复进行，直到处理完所有的行为止。    

合并联接操作可以是常规操作，也可以是多对多操作。 多对多合并联接使用临时表存储行。 如果每个输入中有重复值，则在处理其中一个输入中的每个重复项时，另一个输入必须重绕到重复项的开始位置。    

如果存在驻留谓词，则所有满足合并谓词的行都将对该驻留谓词取值，而只返回那些满足该驻留谓词的行。   

合并联接本身的速度很快，但如果需要排序操作，选择合并联接就会非常费时。 然而，如果数据量很大且能够从现有 B 树索引中获得预排序的所需数据，则合并联接通常是最快的可用联接算法。    

## <a name="hash"></a> 了解哈希联接
哈希联接可以有效处理未排序的大型非索引输入。 它们对复杂查询的中间结果很有用，因为：
-   中间结果未经索引（除非已经显式保存到磁盘上然后创建索引），而且通常不为查询计划中的下一个操作进行适当的排序。
-   查询优化器只估计中间结果的大小。 由于对于复杂查询，估计可能有很大的误差，因此如果中间结果比预期的大得多，则处理中间结果的算法不仅必须有效而且必须适度弱化。   

哈希联接可以减少使用非规范化。 非规范化一般通过减少联接操作获得更好的性能，尽管这样做有冗余之险（如不一致的更新）。 哈希联接则减少使用非规范化的需要。 哈希联接使垂直分区（用单独的文件或索引代表单个表中的几组列）得以成为物理数据库设计的可行选项。     

哈希联接有两种输入：**生成**输入和**探测**输入。 查询优化器指派这些角色，使两个输入中较小的那个作为生成输入。    

哈希联接用于多种设置匹配操作：内部联接；左外部联接、右外部联接和完全外部联接；左半联接和右半联接；交集；并集和差异。 此外，哈希联接的某种变形可以进行重复删除和分组，例如 `SUM(salary) GROUP BY department`。 这些修改对生成和探测角色只使用一个输入。   

以下几节介绍了不同类型的哈希联接：内存中的哈希联接、Grace 哈希联接和递归哈希联接。    

### <a name="inmem_hash"></a> 内存中的哈希联接

哈希联接先扫描或计算整个生成输入，然后在内存中生成哈希表。 根据计算得出的哈希键的哈希值，将每行插入哈希存储桶。 如果整个生成输入小于可用内存，则可以将所有行都插入哈希表中。 生成阶段之后是探测阶段。 一次一行地对整个探测输入进行扫描或计算，并为每个探测行计算哈希键的值，扫描相应的哈希存储桶并生成匹配项。    

### <a name="grace_hash"></a> Grace 哈希联接

如果生成输入大于内存，哈希联接将分为几步进行。 这称为“Grace 哈希联接”。 每一步都分为生成阶段和探测阶段。 首先，消耗整个生成和探测输入并将其分区（使用哈希键上的哈希函数）为多个文件。 对哈希键使用哈希函数可以保证任意两个联接记录一定位于相同的文件对中。 因此，联接两个大输入的任务简化为相同任务的多个较小的实例。 然后将哈希联接应用于每对分区文件。    

### <a name="recursive_hash"></a> 递归哈希联接

如果生成输入非常大，以至于标准外部合并的输入需要多个合并级别，则需要多个分区步骤和多个分区级别。 如果只有某些分区较大，则只需对那些分区使用附加的分区步骤。 为了使所有分区步骤尽可能快，将使用大的异步 I/O 操作以便单个线程就能使多个磁盘驱动器繁忙工作。    

> [!NOTE]
> 如果生成输入仅稍大于可用内存，则内存中的哈希联接和 Grace 哈希联接的元素将结合在一个步骤中，生成混合哈希联接。   

在优化过程中不能始终确定使用哪种哈希联接。 因此，SQL Server 开始时使用内存中的哈希联接，然后根据生成输入的大小逐渐转换到 Grace 哈希联接和递归哈希联接。    

如果查询优化器错误地预计两个输入中哪个较小并由此确定哪个作为生成输入，生成角色和探测角色将动态反转。 哈希联接确保使用较小的溢出文件作为生成输入。 这一技术称为角色反转。 至少一个文件溢出到磁盘后，哈希联接中才会发生角色反转。     

> [!NOTE]
> 角色反转的发生独立于任何查询提示或结构。 角色反转不会显示在查询计划中；角色反转对于用户是透明的。

### <a name="hash_bailout"></a> 哈希援助

术语“哈希援助”有时用于描述 Grace 哈希联接或递归哈希联接。    

> [!NOTE]
> 递归哈希联接或哈希援助会导致服务器性能降低。 如果跟踪中显示许多哈希警告事件，请更新正在联接的列上的统计信息。    

有关哈希援助的详细信息，请参阅 [Hash Warning 事件类](../../relational-databases/event-classes/hash-warning-event-class.md)。    
  
## <a name="nulls_joins"></a> NULL 值和联接
联接表的列中的 null 值（如果有）互相不匹配。 如果其中一个联接表的列中出现空值，只能通过外部联接返回这些空值（除非 `WHERE` 子句不包括空值）。     

下面的两个表中，每个表中要参与联接的列中均包含 NULL 值：     

```
table1                          table2
a           b                   c            d
-------     ------              -------      ------
      1        one                 NULL         two
   NULL      three                    4        four
      4      join4
```    

将列 a 中的值与列 c 中的值进行比较的联接在包含 NULL 值的列上不会获得匹配项：

```sql
SELECT *
FROM table1 t1 JOIN table2 t2
   ON t1.a = t2.c
ORDER BY t1.a;
GO
```  

而是只返回列 a 和 c 中具有 4 的一行：

```
a           b      c           d      
----------- ------ ----------- ------ 
4           join4  4           four   

(1 row(s) affected)
```   

另外，从基表返回的空值与从外部联接返回的空值很难区分开。 例如，下面的 `SELECT` 语句对这两个表执行左向外部联接：   

```sql
SELECT *
FROM table1 t1 LEFT OUTER JOIN table2 t2
   ON t1.a = t2.c
ORDER BY t1.a;
GO
```   

[!INCLUDE[ssResult](../../includes/ssresult-md.md)]   

```
a           b      c           d      
----------- ------ ----------- ------ 
NULL        three  NULL        NULL 
1           one    NULL        NULL 
4           join4  4           four   

(3 row(s) affected)
```   

从结果中很难区分数据中的 NULL 值和表示联接失败的 NULL 值。 如果联接的数据有空值，最好用常规联接从结果中删除这些空值。    

## <a name="see-also"></a>另请参阅  
[Showplan 逻辑运算符和物理运算符参考](../../relational-databases/showplan-logical-and-physical-operators-reference.md)     
[比较运算符 (Transact-SQL)](../../t-sql/language-elements/comparison-operators-transact-sql.md)    
[数据类型转换（数据库引擎）](../../t-sql/data-types/data-type-conversion-database-engine.md)   
[子查询](../../relational-databases/performance/subqueries.md)      
[自适应联接](../../relational-databases/performance/adaptive-query-processing.md#batch-mode-adaptive-joins)    


  
  
