---
title: "DBCC SHOWCONTIG (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 07/17/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|database-console-commands
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DBCC_SHOWCONTIG_TSQL
- DBCC SHOWCONTIG
- SHOWCONTIG
- SHOWCONTIG_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- displaying defragmentation information
- DBCC SHOWCONTIG statement
- defragmenting indexes
- leaf level defragmenting
- fragmentation [SQL Server]
- index defragmenting [SQL Server]
ms.assetid: 1df2123a-1197-4fff-91a3-25e3d8848aaa
caps.latest.revision: 78
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: aecf422ca2289b2a417147eb402921bb8530d969
ms.openlocfilehash: 901067b9bd9c85887b66ea8d32999cf439873952
ms.contentlocale: zh-cn
ms.lasthandoff: 10/24/2017

---
# <a name="dbcc-showcontig-transact-sql"></a>DBCC SHOWCONTIG (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

显示指定的表或视图的数据和索引的碎片信息。
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]使用[sys.dm_db_index_physical_stats](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)相反。  
  
**适用于**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]通过[当前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658))
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```sql
DBCC SHOWCONTIG   
[ (   
    { table_name | table_id | view_name | view_id }   
    [ , index_name | index_id ]   
) ]   
    [ WITH   
        {   
         [ , [ ALL_INDEXES ] ]   
         [ , [ TABLERESULTS ] ]   
         [ , [ FAST ] ]  
         [ , [ ALL_LEVELS ] ]   
         [ NO_INFOMSGS ]  
         }  
    ]  
```  
  
## <a name="arguments"></a>参数  
 *table_name* | *针对 table_id 所* | *view_name* | *view_id*  
 要检查碎片信息的表或视图。 如果未指定，则检查当前数据库中的所有表和索引视图。 若要获取表或查看 ID，使用[OBJECT_ID](../../t-sql/functions/object-id-transact-sql.md)函数。  
  
 *index_name* | *index_id*  
 要检查碎片信息的索引。 如果未指定，则该语句将处理指定表或视图的基本索引。 若要获取的索引 ID，请使用[sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)目录视图。  
  
 替换为  
 指定有关 DBCC 语句返回的信息类型的选项。  
  
 FAST  
 指定是否要对索引执行快速扫描和输出最少信息。 快速扫描不读取索引的叶级或数据级页。  
  
 ALL_INDEXES  
 显示指定表和视图的所有索引的结果，即使指定了特定索引也是如此。  
  
 TABLERESULTS  
 将结果显示为含附加信息的行集。  
  
 ALL_LEVELS  
 维护该列只是为了向后兼容。 即使指定了 ALL_LEVELS，也只对索引叶级或表数据级进行处理。  
  
 NO_INFOMSGS  
 取消严重级别从 0 到 10 的所有信息性消息。  
  
## <a name="result-sets"></a>结果集  
下表对结果集中的信息进行了说明。
  
|统计信息|Description|  
|---|---|
|**扫描的页**|表或索引中的页数。|  
|**范围扫描**|表或索引中的区数。|  
|**扩展盘区开关**|遍历表或索引的页时，DBCC 语句从一个区移动到另一个区的次数。|  
|**页的每个区的页**|页链中每个区的页数。|  
|**扫描密度 [最佳计数： 实际计数]**|百分比。 它是比率**最佳计数**到**实际计数**。 如果所有内容都是连续的，则该值为 100；如果该值小于 100，则存在一些碎片。<br /><br /> **最佳计数**的所有内容连续链接时理想的区更改数。 **实际计数**是实际区更改数。|  
|**逻辑扫描碎片**|扫描索引的叶级页时返回的出错页的百分比。 此数与堆无关。 无序页是为其分配给索引下一步物理页不是指向下一步页的页的页*e*当前叶级页中的指针。|  
|**扩展盘区扫描碎片**|扫描索引的叶级页时出错区所占的百分比。 此数与堆无关。 对于出错区，包含当前索引页的区在物理上不是包含上一个索引页的区的下一个区。<br /><br /> 注意： 当索引跨多个文件时，此数字是无意义。|  
|**页的每页可用字节数**|扫描的页上平均可用字节数。 此数字越大，则页的填充程度越低。 如果索引不会有很多随机插入，则数字越小越好。 此数字还受行大小影响：行越大，此数字就越大。|  
|**页的页密度 （完整）**|页的平均密度，以百分比表示。 该值会考虑行大小。 因此，该值可以更准确地指示页的填充程度。 百分比越大越好。|  
  
当*针对 table_id 所*和快速指定，DBCC SHOWCONTIG 返回具有下面的列的结果集。
-   **扫描的页**  
-   **扩展盘区开关**  
-   **扫描密度 [最佳计数： 实际计数]**  
-   **扩展盘区扫描碎片**  
-   **逻辑扫描碎片**  
  
如果指定了 TABLERESULTS，则 DBCC SHOWCONTIG 将返回以下列以及上一个表中说明的九个列。
  
|统计信息|Description|  
|---|---|
|**Object Name**|处理的表或视图的名称。|  
|**ObjectId**|对象名的 ID。|  
|**IndexName**|处理的索引的名称。 堆的 IndexName 为 NULL。|  
|**IndexId**|索引的 ID。 堆的 IndexId 为 0。|  
|**Level**|索引的级别。 级别 0 是索引的叶（或数据）级。<br /><br /> 堆的级别为 0。|  
|**页**|组成某个索引级别或整个堆的页数。|  
|**行**|某个索引级别上的数据或索引记录数。 对于堆，此值是整个堆中的数据记录数。<br /><br /> 对于堆，此函数返回的记录数可能与通过对堆运行 SELECT COUNT(*) 返回的行数不匹配。 这是因为一行可能包含多个记录。 例如，在某些更新情况下，单个堆行可能由于更新操作而包含一条前推记录和一条被前推记录。 此外，多数大型 LOB 行在 LOB_DATA 存储中拆分为多个记录。|  
|**MinimumRecordSize**|某个索引级别或整个堆中的最小记录大小。|  
|**MaximumRecordSize**|某个索引级别或整个堆中的最大记录大小。|  
|**AverageRecordSize**|某个索引级别或整个堆中的平均记录大小。|  
|**ForwardedRecords**|该索引级别或整个堆中的被前推记录数。|  
|**扩展盘区**|某个索引级别或整个堆中的区数。|  
|**ExtentSwitches**|遍历表或索引的页时，DBCC 语句从一个区移动到另一个区的次数。|  
|**AverageFreeBytes**|扫描的页上平均可用字节数。 此数字越大，则页的填充程度越低。 如果索引不会有很多随机插入，则数字越小越好。 此数字还受行大小影响：行越大，此数字就越大。|  
|**AveragePageDensity**|页的平均密度，以百分比表示。 该值会考虑行大小。 因此，该值可以更准确地指示页的填充程度。 百分比越大越好。|  
|**ScanDensity**|百分比。 它是比率**BestCount**到**ActualCount**。 如果所有内容都是连续的，则该值为 100；如果该值小于 100，则存在一些碎片。|  
|**BestCount**|所有内容连续链接时的区更改理想数量。|  
|**ActualCount**|区更改实际数量。|  
|**LogicalFragmentation**|扫描索引的叶级页时返回的出错页的百分比。 此数与堆无关。 无序页是为其分配给索引下一步物理页不是指向下一步页的页的页*e*当前叶级页中的指针。|  
|**ExtentFragmentation**|扫描索引的叶级页时出错区所占的百分比。 此数与堆无关。 对于出错区，包含当前索引页的区在物理上不是包含上一个索引页的区的下一个区。<br /><br /> 注意： 当索引跨多个文件时，此数字是无意义。|  
  
如果指定了 WITH TABLERESULTS 和 FAST，则结果集将与指定 WITH TABLERESULTS 时一样，但以下列的值将为 null：

| 行| Extents |
|---|---|
|**MinimumRecordSize**|**AverageFreeBytes**|  
|**MaximumRecordSize**|**AveragePageDensity**|  
|**AverageRecordSize**|**ExtentFragmentation**|  
|**ForwardedRecords**||  
  
## <a name="remarks"></a>注释  
DBCC SHOWCONTIG 语句遍历指定的叶级别的页链索引*index_id*指定。 如果仅*针对 table_id 所*指定或如果*index_id*为 0，扫描指定的表的数据页。 此操作只需要一个意向共享 (IS) 表锁。 通过这种方式，除了需要排他 (X) 表锁的更新和插入以外，可执行所有更新和插入。 这就可以根据返回的统计信息数量，实现执行速度与不减少并发之间进行权衡。 但是，如果使用此命令只是为了测量碎片，则建议您使用 WITH FAST 选项以优化性能。 快速扫描不读取索引的叶级或数据级页。 WITH FAST 选项不适用于堆。
  
## <a name="restrictions"></a>限制  
DBCC SHOWCONTIG 不显示与数据**ntext**，**文本**，和**映像**数据类型。 这是因为不再有存储文本和图像数据的文本索引。
  
此外，DBCC SHOWCONTIG 也不支持某些新功能。 例如：
-   如果指定的表或索引已分区，则 DBCC SHOWCONTIG 只显示指定表或索引的第一个分区。  
-   DBCC SHOWCONTIG 不显示行溢出存储信息和其他新的行外数据类型，如**nvarchar (max)**， **varchar （max)**， **varbinary （max)**，和**xml**。  
-   DBCC SHOWCONTIG 不支持空间索引。  
  
完全支持所有的新功能[sys.dm_db_index_physical_stats &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)动态管理视图。
  
## <a name="table-fragmentation"></a>表碎片  
DBCC SHOWCONTIG 可确定表是否高度碎片化。 在对表进行数据修改（INSERT、UPDATE 和 DELETE 语句）的过程中会出现表碎片现象。 由于这些修改通常并不在表的行中平均分布，所以每页的填满状态会随时间而改变。 对于扫描部分或全部表的查询，这样的表碎片会导致读取额外的页。 这会妨碍数据的并行扫描。
  
如果索引的碎片非常多，可选择以下方法来减少碎片：
-   删除然后重新创建聚集索引。  
     重新创建聚集索引将重新组织数据，从而使数据页填满。 填充度可以使用 CREATE INDEX 中的 FILLFACTOR 选项进行配置。 这种方法的缺点是索引在删除/重新创建周期内为脱机状态，并且该操作是一个整体，不可中断。 如果中断索引创建，则不能重新创建索引。  
-   对索引的叶级页按逻辑顺序重新排序。  
     使用 INDEX…REORGANIZE，对索引的页级页按逻辑顺序重新排序。 由于此操作是联机操作，因此语句运行时索引可用。 此外，中断该操作不会丢失已完成的工作。 这种方法的缺点是在重新组织数据方面没有聚集索引的删除/重新创建操作有效。  
-   重新生成索引。  
     使用 REBUILD 和 ALTER INDEX 重新生成索引。 有关详细信息，请参阅 [ALTER INDEX (Transact-SQL)](../../t-sql/statements/alter-index-transact-sql.md)。  
  
“页中**每页可用字节数**和**avg.页上密度 （完整）**结果集中的统计信息指示索引页的填充度。 “页中**每页可用字节数**数目应为低和**avg.页上密度 （完整）**数目应为高对于不具有很多随机插入的索引。 使用指定的 FILLFACTOR 选项删除并重建索引可改善统计信息。 另外，REORGANIZE 和 ALTER INDEX 可根据其 FILLFACTOR 选项压缩索引，从而改善统计信息。
  
> [!NOTE]  
>  如果索引有很多随机插入和很满的页，则其页拆分数将增加。 这将导致更多的碎片。  
  
索引的碎片级别可通过以下方式确定：
-   通过比较的值**扩展盘区开关**和**扫描扩展盘区**。  
     值**扩展盘区开关**应尽可能接近于其中**扫描扩展盘区**。 此比率的计算方式为**扫描密度**值。 此值应尽可能的大，可通过减少索引碎片得到改善。  
  
    > [!NOTE]  
    >  如果索引涉及多个文件，则此方法无效。  
  
-   通过了解**逻辑扫描碎片**和**扩展盘区扫描碎片**值。  
     **扫描的逻辑碎片**和较小的范围内，**扩展盘区扫描碎片**的值为一个表的碎片级别的最佳指示器。 这两个值应尽可能接近零，但 0% 到 10% 之间的值都是可接受的。  
  
    > [!NOTE]  
    >  **扩展盘区扫描碎片**值会很高，如果索引跨越多个文件。 若要减小这些值，必须减少索引碎片。  
  
## <a name="permissions"></a>Permissions  
用户必须拥有某个表，或者是的成员**sysadmin**固定服务器角色、 **db_owner**固定数据库角色或**db_ddladmin**固定的数据库角色。
  
## <a name="examples"></a>示例  
### <a name="a-displaying-fragmentation-information-for-a-table"></a>A. 显示表的碎片信息  
下面的示例将显示 `Employee` 表的碎片信息。
  
```sql  
USE AdventureWorks2012;  
GO  
DBCC SHOWCONTIG ('HumanResources.Employee');  
GO  
```  
  
### <a name="b-using-objectid-to-obtain-the-table-id-and-sysindexes-to-obtain-the-index-id"></a>B. 使用 OBJECT_ID 获得表 ID，使用 sys.indexes 获得索引 ID  
下面的示例使用`OBJECT_ID`和`sys.indexes`目录视图以获取表 ID 和索引的 ID`AK_Product_Name`索引`Production.Product`表中[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]数据库。
  
```sql  
USE AdventureWorks2012;  
GO  
DECLARE @id int, @indid int  
SET @id = OBJECT_ID('Production.Product')  
SELECT @indid = index_id   
FROM sys.indexes  
WHERE object_id = @id   
   AND name = 'AK_Product_Name'  
DBCC SHOWCONTIG (@id, @indid);  
GO  
```  
  
### <a name="c-displaying-an-abbreviated-result-set-for-a-table"></a>C. 显示表的简略结果集  
下面的示例返回缩写的结果集`Product`表中[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]数据库。
  
```sql  
USE AdventureWorks2012;  
GO  
DBCC SHOWCONTIG ('Production.Product', 1) WITH FAST;  
GO  
```  
  
### <a name="d-displaying-the-full-result-set-for-every-index-on-every-table-in-a-database"></a>D. 显示数据库中每个表的每个索引的完整结果集  
下面的示例将返回 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库中每个表的每个索引的完整表结果集。
  
```sql  
USE AdventureWorks2012;  
GO  
DBCC SHOWCONTIG WITH TABLERESULTS, ALL_INDEXES;  
GO  
```  
  
### <a name="e-using-dbcc-showcontig-and-dbcc-indexdefrag-to-defragment-the-indexes-in-a-database"></a>E. 使用 DBCC SHOWCONTIG 和 DBCC INDEXDEFRAG 对数据库中的索引进行碎片整理  
以下示例将展示一种简单的方法，对数据库中碎片数量在声明的阈值之上的所有索引进行碎片整理。
  
```sql
/*Perform a 'USE <database name>' to select the database in which to run the script.*/  
-- Declare variables  
SET NOCOUNT ON;  
DECLARE @tablename varchar(255);  
DECLARE @execstr   varchar(400);  
DECLARE @objectid  int;  
DECLARE @indexid   int;  
DECLARE @frag      decimal;  
DECLARE @maxfrag   decimal;  
  
-- Decide on the maximum fragmentation to allow for.  
SELECT @maxfrag = 30.0;  
  
-- Declare a cursor.  
DECLARE tables CURSOR FOR  
   SELECT TABLE_SCHEMA + '.' + TABLE_NAME  
   FROM INFORMATION_SCHEMA.TABLES  
   WHERE TABLE_TYPE = 'BASE TABLE';  
  
-- Create the table.  
CREATE TABLE #fraglist (  
   ObjectName char(255),  
   ObjectId int,  
   IndexName char(255),  
   IndexId int,  
   Lvl int,  
   CountPages int,  
   CountRows int,  
   MinRecSize int,  
   MaxRecSize int,  
   AvgRecSize int,  
   ForRecCount int,  
   Extents int,  
   ExtentSwitches int,  
   AvgFreeBytes int,  
   AvgPageDensity int,  
   ScanDensity decimal,  
   BestCount int,  
   ActualCount int,  
   LogicalFrag decimal,  
   ExtentFrag decimal);  
  
-- Open the cursor.  
OPEN tables;  
  
-- Loop through all the tables in the database.  
FETCH NEXT  
   FROM tables  
   INTO @tablename;  
  
WHILE @@FETCH_STATUS = 0  
BEGIN  
-- Do the showcontig of all indexes of the table  
   INSERT INTO #fraglist   
   EXEC ('DBCC SHOWCONTIG (''' + @tablename + ''')   
      WITH FAST, TABLERESULTS, ALL_INDEXES, NO_INFOMSGS');  
   FETCH NEXT  
      FROM tables  
      INTO @tablename;  
END;  
  
-- Close and deallocate the cursor.  
CLOSE tables;  
DEALLOCATE tables;  
  
-- Declare the cursor for the list of indexes to be defragged.  
DECLARE indexes CURSOR FOR  
   SELECT ObjectName, ObjectId, IndexId, LogicalFrag  
   FROM #fraglist  
   WHERE LogicalFrag >= @maxfrag  
      AND INDEXPROPERTY (ObjectId, IndexName, 'IndexDepth') > 0;  
  
-- Open the cursor.  
OPEN indexes;  
  
-- Loop through the indexes.  
FETCH NEXT  
   FROM indexes  
   INTO @tablename, @objectid, @indexid, @frag;  
  
WHILE @@FETCH_STATUS = 0  
BEGIN  
   PRINT 'Executing DBCC INDEXDEFRAG (0, ' + RTRIM(@tablename) + ',  
      ' + RTRIM(@indexid) + ') - fragmentation currently '  
       + RTRIM(CONVERT(varchar(15),@frag)) + '%';  
   SELECT @execstr = 'DBCC INDEXDEFRAG (0, ' + RTRIM(@objectid) + ',  
       ' + RTRIM(@indexid) + ')';  
   EXEC (@execstr);  
  
   FETCH NEXT  
      FROM indexes  
      INTO @tablename, @objectid, @indexid, @frag;  
END;  
  
-- Close and deallocate the cursor.  
CLOSE indexes;  
DEALLOCATE indexes;  
  
-- Delete the temporary table.  
DROP TABLE #fraglist;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
[ALTER INDEX (Transact-SQL)](../../t-sql/statements/alter-index-transact-sql.md)  
[CREATE INDEX (Transact-SQL)](../../t-sql/statements/create-index-transact-sql.md)  
[DBCC (Transact-SQL)](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[DROP INDEX (Transact-SQL)](../../t-sql/statements/drop-index-transact-sql.md)  
[sys.dm_db_index_physical_stats (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)  
[OBJECT_ID (Transact-SQL)](../../t-sql/functions/object-id-transact-sql.md)  
[sys.indexes (Transact-SQL)](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)
  
  


