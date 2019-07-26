---
title: 重新组织和重新生成索引 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
f1_keywords:
- sql12.swb.indexproperties.fragmentation.f1
- sql12.swb.index.reorg.f1
- sql12.swb.index.rebuild.f1
helpviewer_keywords:
- large object defragmenting
- indexes [SQL Server], reorganizing
- index reorganization [SQL Server]
- reorganizing indexes
- defragmenting large object data types
- index fragmentation [SQL Server]
- index rebuilding [SQL Server]
- rebuilding indexes
- indexes [SQL Server], rebuilding
- defragmenting indexes
- nonclustered indexes [SQL Server], defragmenting
- fragmentation [SQL Server]
- index defragmenting [SQL Server]
- LOB data [SQL Server], defragmenting
- clustered indexes, defragmenting
ms.assetid: a28c684a-c4e9-4b24-a7ae-e248808b31e9
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 2de93079289ffda8ff6287ad09aa4dea150932d7
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/24/2019
ms.locfileid: "68475959"
---
# <a name="reorganize-and-rebuild-indexes"></a>重新组织和重新生成索引
  本主题介绍如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中重新组织或重新生成碎片索引。 无论何时对基础数据执行插入、更新或删除操作， [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 都会自动维护索引。 随着时间的推移，这些修改可能会导致索引中的信息分散在数据库中（含有碎片）。 当索引包含的页中的逻辑排序（基于键值）与数据文件中的物理排序不匹配时，就存在碎片。 碎片非常多的索引可能会降低查询性能，导致应用程序响应缓慢。  
  
 您可以通过重新组织或重新生成索引来修复索引碎片。 对于基于分区方案生成的已分区索引，可以在完整索引或索引的单个分区上使用下列方法之一。 重新生成索引将会删除并重新创建索引。 这将根据指定的或现有的填充因子设置压缩页来删除碎片、回收磁盘空间，然后对连续页中的索引行重新排序。 如果指定 ALL，将删除表中的所有索引，然后在单个事务中重新生成。 使用最少系统资源重新组织索引。 通过对叶级页以物理方式重新排序，使之与叶节点的从左到右的逻辑顺序相匹配，进而对表和视图中的聚集索引和非聚集索引的叶级进行碎片整理。 重新组织还会压缩索引页。 压缩基于现有的填充因子值。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [检测碎片](#Fragmentation)  
  
     [限制和局限](#Restrictions)  
  
     [安全性](#Security)  
  
-   **若要检查索引的碎片，请使用：**  
  
     [SQL Server Management Studio](#SSMSProcedureFrag)  
  
     [Transact-SQL](#TsqlProcedureFrag)  
  
-   **若要重新组织或重新生成索引，请使用：**  
  
     [SQL Server Management Studio](#SSMSProcedureReorg)  
  
     [Transact-SQL](#TsqlProcedureReorg)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Fragmentation"></a> 检测碎片  
 决定使用哪种碎片整理方法的第一步是分析索引以确定碎片程度。 通过使用系统函数 [sys.dm_db_index_physical_stats](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql)，你可以检测特定索引中的碎片、表或索引视图的所有索引、某个数据库中的所有索引或所有数据库中的所有索引。 对于已分区索引， **sys.dm_db_index_physical_stats** 还提供每个分区的碎片信息。  
  
 由 **sys.dm_db_index_physical_stats** 函数返回的结果集包含以下列。  
  
|“列”|描述|  
|------------|-----------------|  
|**avg_fragmentation_in_percent**|逻辑碎片（索引中的无序页）的百分比。|  
|**fragment_count**|索引中的碎片（物理上连续的叶页）数量。|  
|**avg_fragment_size_in_pages**|索引中一个碎片的平均页数。|  
  
 知道碎片程度后，可以使用下表确定修复碎片的最佳方法。  
  
|**avg_fragmentation_in_percent** 值|修复语句|  
|-----------------------------------------------|--------------------------|  
|> 5%, \< = 30%|ALTER INDEX REORGANIZE|  
|> 30%|ALTER INDEX REBUILD WITH (ONLINE = ON) <sup>1</sup>|

<sup>1</sup> 重新生成索引可以联机执行，也可以脱机执行。 重新组织索引始终联机执行。 若要获得与重新组织选项相似的可用性，应联机重新生成索引。  
  
> [!TIP]
> 这些值提供了一个大致指导原则，用于确定应在 `ALTER INDEX REORGANIZE` 和 `ALTER INDEX REBUILD` 之间进行切换的点。 不过，实际值可能会随情况而变化。 必须要通过试验来确定最适合您环境的阈值。 例如, 如果给定索引主要用于扫描操作, 则删除碎片可以提高这些操作的性能。 对于主要用于查找操作的索引, 性能优势不太明显。 同样, 删除堆中的碎片 (不包含聚集索引的表) 对于非聚集索引扫描操作特别有用, 但在查找操作中不起作用。

通常情况下，非常低的碎片级别（小于 5%）不应通过这些命令来解决，因为删除如此少量的碎片所获得的收益始终远低于重新组织或重新生成索引的开销。 

> [!NOTE]
> 重新生成或重新组织小索引不会减少碎片。 小索引的页面有关存储在混合盘区中。 混合区最多可由八个对象共享，因此在重新组织或重新生成小索引之后可能不会减少小索引中的碎片。

### <a name="index-defragmentation-considerations"></a>索引碎片整理注意事项
在某些情况下, 如果非聚集索引记录中包含的物理或逻辑标识符需要更改, 则重新生成聚集索引将自动重新生成引用聚集键的任何非聚集索引。

强制对表自动重新生成所有非聚集索引的方案:

-  对表创建聚集索引
-  删除聚集索引, 从而使表存储为堆
-  更改聚集键以包括或排除列

不需要在表上自动重新生成所有非聚集索引的方案:

-  重新生成唯一聚集索引
-  重新生成非唯一聚集索引
-  更改索引架构, 例如将分区方案应用于聚集索引或将聚集索引移到其他文件组
  
###  <a name="Restrictions"></a> 限制和局限  
  
带有多于 128 个区的索引通过两个单独的阶段重新生成：逻辑阶段和物理阶段。 在逻辑阶段，将把由索引使用的现有分配单元标记为释放，对数据行进行复制并排序，然后将它们移到为存储重新生成的索引而创建的新分配单元。 在物理阶段，先前标记为取消分配的分配单元在发生在后台的短事务中被物理删除，而且不需要很多锁。 有关区的详细信息，请参考[页和区体系结构指南](https://docs.microsoft.com/sql/relational-databases/pages-and-extents-architecture-guide)。

`ALTER INDEX REORGANIZE` 语句要求包含索引的数据文件具有可用的空间，因为该操作仅可在同一文件中分配临时工作，而不能在文件组内的另一个文件中进行分配。 因此，尽管文件组可能有可用的空闲页，用户仍可能会遇到错误 1105：`Could not allocate space for object '###' in database '###' because the '###' filegroup is full. Create disk space by deleting unneeded files, dropping objects in the filegroup, adding additional files to the filegroup, or setting autogrowth on for existing files in the filegroup.`

对超过 1,000 个分区的表创建和重新生成非对齐索引是可能的，但不推荐。 这样做可能会导致性能下降，或在执行这些操作的过程中占用过多内存。

如果索引所在的文件组脱机或设置为只读，则无法重新组织或重新生成索引。 如果指定了关键字 `ALL`，但有一个或多个索引位于脱机文件组或只读文件组中，该语句将失败。
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 要求具有对表或视图的 `ALTER` 权限。 用户必须是 **sysadmin** 固定服务器角色的成员，或者是 **db_ddladmin** 和 **db_owner** 固定数据库角色的成员。  
  
##  <a name="SSMSProcedureFrag"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-check-the-fragmentation-of-an-index"></a>检查索引的碎片  
  
1.  在“对象资源管理器”中，展开其中包含要检查索引碎片的表的数据库。  
  
2.  展开 **“表”** 文件夹。  
  
3.  展开要检查索引碎片的表。  
  
4.  展开 **“索引”** 文件夹。  
  
5.  右键单击要检查碎片的索引，然后选择 **“属性”** 。  
  
6.  在 **“选择页”** 下，选择 **“碎片”** 。  
  
     **“碎片”** 页将提供以下信息：  
  
     **页填充度**  
     指示索引页的平均填充率（以百分比表示）。 100% 表示索引页完全填充。 50% 表示每个索引页平均填充一半。  
  
     **碎片总计**  
     逻辑碎片百分比。 用于指示索引中未按顺序存储的页数。  
  
     **平均行大小**  
     叶级行的平均大小。  
  
     **深度**  
     索引中的级别数（包括叶级别）。  
  
     **前推记录数**  
     堆中具有指向另一个数据位置的转向指针的记录数。 （在更新过程中，如果在原始位置存储新行的空间不足，将会出现此状态。）  
  
     **虚影行数**  
     标记为已删除，但尚未移除的行数。 当服务器不忙时，将通过清除线程移除这些行。 此值不包括由于某个快照隔离事务未完成而保留的行。  
  
     **索引类型**  
     索引的类型。 可能的值包括 **“聚集索引”** 、 **“非聚集索引”** 和 **“主 XML”** 。 表也可以存储为堆（不带索引），但此后将无法打开此“索引属性”页。  
  
     **叶级行数**  
     叶级行的数目。  
  
     **最大行大小**  
     叶级行最大大小。  
  
     **最小行大小**  
     叶级行最小大小。  
  
     **页**  
     数据页总数。  
  
     **Partition ID**  
     包含该索引的 B 树的分区 ID。  
  
     **建立虚影行版本**  
     由于某个快照隔离事务未完成而保留的虚影记录的数目。  
  
##  <a name="TsqlProcedureFrag"></a> 使用 Transact-SQL  
  
#### <a name="to-check-the-fragmentation-of-an-index"></a>检查索引的碎片  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]的实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”** 。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行” 。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Find the average fragmentation percentage of all indexes  
    -- in the HumanResources.Employee table.   
    SELECT a.index_id, name, avg_fragmentation_in_percent  
    FROM sys.dm_db_index_physical_stats (DB_ID(N'AdventureWorks2012'), OBJECT_ID(N'HumanResources.Employee'), NULL, NULL, NULL) AS a  
        JOIN sys.indexes AS b ON a.object_id = b.object_id AND a.index_id = b.index_id;   
    GO  
    ```  
  
     上述语句可能会返回类似于以下内容的结果集。  
  
    ```  
    index_id    name                                                  avg_fragmentation_in_percent  
    ----------- ----------------------------------------------------- ----------------------------  
    1           PK_Employee_BusinessEntityID                          0  
    2           IX_Employee_OrganizationalNode                        0  
    3           IX_Employee_OrganizationalLevel_OrganizationalNode    0  
    5           AK_Employee_LoginID                                   66.6666666666667  
    6           AK_Employee_NationalIDNumber                          50  
    7           AK_Employee_rowguid                                   0  
  
    (6 row(s) affected)  
    ```  
  
 有关详细信息，请参阅 [sys.dm_db_index_physical_stats (Transact-SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql)。  
  
##  <a name="SSMSProcedureReorg"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-reorganize-or-rebuild-an-index"></a>重新组织或重新生成索引  
  
1.  在“对象资源管理器”中，展开包含您要重新组织索引的表的数据库。  
  
2.  展开 **“表”** 文件夹。  
  
3.  展开要为其重新组织索引的表。  
  
4.  展开 **“索引”** 文件夹。  
  
5.  右键单击要重新组织的索引，然后选择 **“重新组织”** 。  
  
6.  在 **“重新组织索引”** 对话框中，确认正确的索引位于 **“要重新组织的索引”** 网格中，然后单击 **“确定”** 。  
  
7.  选中 **“压缩大型对象列数据”** 复选框，以指定也压缩所有包含大型对象 (LOB) 数据的页。  
  
8.  单击“确定” **。**  
  
#### <a name="to-reorganize-all-indexes-in-a-table"></a>重新组织表中的所有索引  
  
1.  在“对象资源管理器”中，展开包含您要重新组织索引的表的数据库。  
  
2.  展开 **“表”** 文件夹。  
  
3.  展开要为其重新组织索引的表。  
  
4.  右键单击 **“索引”** 文件夹，然后选择 **“全部重新组织”** 。  
  
5.  在 **“重新组织索引”** 对话框中，确认正确的索引位于 **“要重新组织的索引”** 中。 若要从 **“要重新组织的索引”** 网格中删除索引，请选择该索引，再按 Delete 键。  
  
6.  选中 **“压缩大型对象列数据”** 复选框，以指定也压缩所有包含大型对象 (LOB) 数据的页。  
  
7.  单击“确定” **。**  
  
#### <a name="to-rebuild-an-index"></a>重新生成索引  
  
1.  在“对象资源管理器”中，展开包含您要重新组织索引的表的数据库。  
  
2.  展开 **“表”** 文件夹。  
  
3.  展开要为其重新组织索引的表。  
  
4.  展开 **“索引”** 文件夹。  
  
5.  右键单击要重新组织的索引，然后选择 **“重新组织”** 。  
  
6.  在 **“重新生成索引”** 对话框中，确认正确的索引位于 **“要重新生成的索引”** 网格中，然后单击 **“确定”** 。  
  
7.  选中 **“压缩大型对象列数据”** 复选框，以指定也压缩所有包含大型对象 (LOB) 数据的页。  
  
8.  单击“确定” **。**  
  
##  <a name="TsqlProcedureReorg"></a> 使用 Transact-SQL  
  
#### <a name="to-reorganize-a-defragmented-index"></a>重新组织碎片索引  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]的实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”** 。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行” 。  
  
    ```  
    USE AdventureWorks2012;   
    GO  
    -- Reorganize the IX_Employee_OrganizationalLevel_OrganizationalNode index on the HumanResources.Employee table.   
  
    ALTER INDEX IX_Employee_OrganizationalLevel_OrganizationalNode ON HumanResources.Employee  
    REORGANIZE ;   
    GO  
    ```  
  
#### <a name="to-reorganize-all-indexes-in-a-table"></a>重新组织表中的所有索引  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]的实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”** 。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行” 。  
  
    ```  
    USE AdventureWorks2012;   
    GO  
    -- Reorganize all indexes on the HumanResources.Employee table.  
    ALTER INDEX ALL ON HumanResources.Employee  
    REORGANIZE ;   
    GO  
    ```  
  
#### <a name="to-rebuild-a-defragmented-index"></a>重新生成碎片索引  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]的实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”** 。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行” 。 该示例在 `Employee` 表中重新生成单个索引。  
  
     [!code-sql[IndexDDL#AlterIndex1](../../snippets/tsql/SQL14/tsql/indexddl/transact-sql/alterindex.sql#alterindex1)]  
  
#### <a name="to-rebuild-all-indexes-in-a-table"></a>重新生成表中的所有索引  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]的实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”** 。  
  
3.  复制以下示例并将其粘贴到查询中，该示例指定了 `ALL`关键字。 这将重新生成与表相关联的所有索引。 其中指定了三个选项。  
  
     [!code-sql[IndexDDL#AlterIndex2](../../snippets/tsql/SQL14/tsql/indexddl/transact-sql/alterindex.sql#alterindex2)]  
  
 有关详细信息，请参阅 [ALTER INDEX (Transact-SQL)](/sql/t-sql/statements/alter-index-transact-sql)。  
  
## <a name="see-also"></a>请参阅  
 [Microsoft SQL Server 2000 索引碎片整理最佳实践](https://technet.microsoft.com/library/cc966523.aspx)  
  
  
