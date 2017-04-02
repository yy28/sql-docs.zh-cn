---
title: "通过逻辑记录对相关行的更改进行分组 | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "合并复制逻辑记录 [SQL Server 复制]"
  - "项目 [SQL Server 复制], 逻辑记录"
  - "逻辑记录 [SQL Server 复制]"
ms.assetid: ad76799c-4486-4b98-9705-005433041321
caps.latest.revision: 55
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 55
---
# 通过逻辑记录对相关行的更改进行分组
    
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
 默认情况下，合并复制逐行处理数据更改。 这适用于许多情况，但对于某些应用程序，需要将相关行作为一个单元进行处理。 合并复制的逻辑记录功能允许在不同表的相关行之间定义一种关系，以便将这些行作为一个单元进行处理。  
  
> [!NOTE]  
>  逻辑记录功能可以单独使用，也可以与联接筛选器一起使用。 有关联接筛选器的详细信息，请参阅 [联接筛选器](../../../relational-databases/replication/merge/join-filters.md)。 若要使用逻辑记录，发布的兼容级别不能低于 90RTM。  
  
 请考虑以下三个相关的表：  
  
 ![三个仅具有列名称的表逻辑记录](../../../relational-databases/replication/merge/media/logical-records-01.gif "三个仅具有列名称的表逻辑记录")  
  
 在此关系中， **Customers** 表是父表，具有主键列 **CustID**。 **Orders** 表具有主键列 **OrderID**和外键约束（ **CustID** 列）。该外键列引用 **Customers** 表中的 **CustID** 列。 同样， **OrderItems** 表具有主键列 **OrderItemID**和外键约束（ **OrderID** 列）。该外键列引用 **Orders** 表中的 **OrderID** 列。  
  
 在此示例中，逻辑记录由 **Orders** 表中与单一 **CustID** 值相关的所有行和 **OrderItems** 表中与 **Orders** 表中的那些行相关的所有行组成。 此关系图显示了 Customer2 的逻辑记录中三个表的所有行：  
  
 ![三个具有值的表逻辑记录](../../../relational-databases/replication/merge/media/logical-records-02.gif "三个具有值的表逻辑记录")  
  
 若要定义项目之间的逻辑记录关系，请参阅 [Define a Logical Record Relationship Between Merge Table Articles](../../../relational-databases/replication/publish/define-a-logical-record-relationship-between-merge-table-articles.md)。  
  
## 逻辑记录的优点  
 逻辑记录功能有两大优点：  
  
-   将数据更改作为一个单元来应用。  
  
-   同时对多个表中的多个行检测和解决冲突。  
  
### 将更改作为一个单元来应用  
 在合并处理中断的情况下（如删除连接），如果使用了逻辑记录，则已完成的部分相关复制更改就会回滚。 例如，考虑这种情况，将订阅服务器上添加新的订单与 **OrderID** = 6 和两个新行中的 **OrderItems** 表与 **OrderItemID** = 10 和 **OrderItemID** = 11 的 **OrderID** = 6。  
  
 ![三个具有值的表逻辑记录](../../../relational-databases/replication/merge/media/logical-records-04.gif "三个具有值的表逻辑记录")  
  
 如果复制过程中断后 **订单** 行 **OrderID** = 6 之前已完成， **OrderItems** 10 和 11 都已完成，并且不使用逻辑记录， **OrderTotal** 值 **OrderID** = 6 将不一致的总和 **OrderAmount** 值 **OrderItems** 行。 如果使用了逻辑记录， **订单** 行 **OrderID** = 6 才会提交相关 **OrderItems** 复制更改。  
  
 在不同的方案中，如果使用了逻辑记录，并且有人在合并进程应用更改时查询表，那么用户在复制更改完成前，看不到已复制的部分更改。 例如，复制进程上载了的 Orders 行 **OrderID** = 6，但用户查询表之前复制进程复制 **OrderItems** 行， **OrderTotal** 值就不会与之和相同 **OrderAmount** 值。 如果使用了逻辑记录，则在 **OrderItems** 完成并且事务作为一个单元提交后，才会显示 **Orders** 行。  
  
### 对多个表应用冲突处理  
 请考虑两台订阅服务器具有上述数据集的情况：  
  
-   在第一台订阅服务器上，用户将 **OrderItemID** 5 的 **OrderAmount** 从 100 改为 150，并将 **OrderID** 3 的 **OrderTotal** 从 200 改为 250。  
  
-   在第二台订阅服务器上，用户将 **OrderItemID** 6 的 **OrderAmount** 从 25 改为 125，并将 **OrderID** 3 的 **OrderTotal** 从 200 改为 300。  
  
 如果不使用逻辑记录复制这些更改， **OrderTotal** 的不同值就会导致冲突，结果只能复制其中一个。 但中的非冲突更改 **OrderItems** 表将被复制，且不发生冲突，致使最终 **OrderTotal** 中相对于不一致状态的值 **OrderItems** 行。 如果在此方案中使用逻辑记录，则与落选的 **Orders** 表更改关联的 **OrderItems** 更改也会回滚，从而使最终的 **OrderTotal** 值成为 **OrderItems** 行的准确汇总。  
  
 有关与冲突检测和解决与逻辑记录相关的选项的详细信息，请参阅 [检测和解决逻辑记录中的冲突](../../../relational-databases/replication/merge/detecting-and-resolving-conflicts-in-logical-records.md)。  
  
## 使用逻辑记录的注意事项  
 使用逻辑记录时，请注意下列事项。  
  
### 一般注意事项  
  
-   建议在逻辑记录中保留尽可能少的表，建议最多为五个表。  
  
-   逻辑记录无法引用具有下列任一数据类型的列：  
  
    -   **varchar （max)** 和 **nvarchar （max)**  
  
    -   **varbinary(max)**  
  
    -   **text** 和 **ntext**  
  
    -   **图像**  
  
    -   **XML**  
  
    -   **UDT**  
  
-   不能使用 CASCADE 选项定义已发布表中的外键关系。 有关详细信息，请参阅 [CREATE TABLE & #40;Transact SQL & #41;](../../../t-sql/statements/create-table-transact-sql.md) 和 [ALTER 表 & #40;Transact SQL & #41;](../../../t-sql/statements/alter-table-transact-sql.md)。  
  
-   不能更新逻辑关系子句中使用的任何列。  
  
-   逻辑记录中包含的项目不支持使用业务逻辑处理程序或自定义冲突解决程序的自定义冲突解决方法。  
  
-   如果在包含参数化筛选器的发布中使用逻辑记录，必须用每台订阅服务器分区的快照初始化相应的订阅服务器。 如果用其他方法初始化订阅服务器，那么合并代理将会失败。 有关详细信息，请参阅 [Snapshots for Merge Publications with Parameterized Filters](../../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md)。  
  
-   包含逻辑记录的冲突不会显示在冲突查看器中。 若要查看有关这些冲突的信息，请使用复制存储过程。 有关详细信息，请参阅 [查看的合并发布 & #40; 的冲突信息复制 TRANSACT-SQL 编程 & #41;](../../../relational-databases/replication/view conflict information for merge publications.md)。  
  
### 发布设置  
  
-   发布的兼容级别必须为 90RTM 或更大。 有关详细信息，请参阅的"发布兼容级别"部分 [复制向后兼容性](../../../relational-databases/replication/replication-backward-compatibility.md)。  
  
-   发布必须使用本机快照模式。 这是默认设置，除非您要复制到不支持逻辑记录的 [!INCLUDE[ssEW](../../../includes/ssew-md.md)]。  
  
-   发布不允许 Web 同步。 有关 Web 同步的详细信息，请参阅 [Web Synchronization for Merge Replication](../../../relational-databases/replication/web-synchronization-for-merge-replication.md)。  
  
-   若要在已筛选的发布上使用逻辑记录：  
  
    -   还必须使用预计算分区。 预计算分区的要求也适用于逻辑记录。 有关详细信息，请参阅 [使用预计算分区优化参数化筛选器性能](../../../relational-databases/replication/merge/optimize-parameterized-filter-performance-with-precomputed-partitions.md)。  
  
    -   不能使用不重叠的参数化筛选器。 有关详细信息，请参阅 [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-row-filters.md)的“设置‘分区选项’”部分。  
  
-   如果发布使用联接筛选器，则必须将逻辑记录关系中所涉及的所有联接筛选器的 **join unique key** 属性设置为 **true** 。 有关详细信息，请参阅 [Join Filters](../../../relational-databases/replication/merge/join-filters.md)。  
  
### 表之间的关系  
  
-   通过逻辑记录相关的表必须具有主键 - 外键关系。  
  
-   不能为外键约束设置 NOT FOR REPLICATION 选项。  
  
-   子表只能有一个父表。  
  
     例如，跟踪班级和学生的数据库的设计可能类似于下面的关系：  
  
     ![具有多个父表的子表](../../../relational-databases/replication/merge/media/logical-records-03.gif "具有多个父表的子表")  
  
     在此关系中，不能使用一个逻辑记录表示三个表，因为 **ClassMembers** 中的行与单一主键行没有关联。 **Classes** 表和 **ClassMembers** 表仍可形成一个逻辑记录， **ClassMembers** 表和 **Students**表也可以，但三个表却不能。  
  
-   发布不能包含循环联接筛选器关系。  
  
     以 **Customers**、 **Orders**和 **OrderItems**这三个表为例，如果 **Orders** 表也有一个引用 **OrderItems** 表的外键约束，就不能使用逻辑记录。  
  
## 逻辑记录对性能的影响  
 逻辑记录功能确实会对性能造成负面影响。 如果不使用逻辑记录，复制代理可以同时处理给定项目的所有更改，并且因为更改是以逐行方式应用的，所以应用这些更改所需的锁定和事务日志要求很小。  
  
 如果使用逻辑记录，则合并代理必须一起处理每个整体逻辑记录的更改。 这会影响合并代理复制行所需的时间。 此外，由于代理要为每个逻辑记录打开一个单独的事务，因此锁定要求就会增加。  
  
## 另请参阅  
 [合并复制的项目选项](../../../relational-databases/replication/merge/article-options-for-merge-replication.md)  
  
  