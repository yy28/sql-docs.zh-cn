---
title: "配置并行索引操作 | Microsoft Docs"
ms.custom: 
ms.date: 02/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-indexes
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- index parallel operations [SQL Server]
- processors [SQL Server], parallel index operations
- max degree of parallelism option
- MAXDOP index option, parallel index operations
- parallel index operations [SQL Server]
ms.assetid: 8ec8c71e-5fc1-443a-92da-136ee3fc7f88
caps.latest.revision: 43
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 3e68d3b1d6d08153e24ec3afdb5102e5c1ae6c46
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="configure-parallel-index-operations"></a>配置并行索引操作
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  本主题通过使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中定义最大并行度 (max degree of parallelism) 并说明如何修改此设置。 在运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise 或更高版本的多处理器计算机上，索引语句可能会像其他查询那样，使用多个处理器来执行与索引语句关联的扫描、排序和索引操作。 用于运行单个索引语句的处理器数由 [最大并行度](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md) 配置选项、当前工作负荷以及索引统计信息决定。 max degree of parallelism 选项决定了执行并行计划时使用的最大处理器数。 如果 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 检测到系统忙，索引操作的并行度将自动降低，然后再开始执行语句。 如果非分区索引的第一个键列包含有限数量的非重复值，或者每个非重复值的出现频率变化较大， [!INCLUDE[ssDE](../../includes/ssde-md.md)] 也可能会降低并行度。  
  
> [!NOTE]  
>  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的各版本中均不提供并行索引操作。 有关详细信息，请参阅“SQL Server 2016 各个版本支持的功能”  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [限制和局限](#Restrictions)  
  
     [安全性](#Security)  
  
-   **若要设置最大并行度，请使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Restrictions"></a> 限制和局限  
  
-   查询优化器使用的处理器数量通常能够提供最佳的性能。 但是，有些操作（如创建、重新生成或删除很大的索引）占用大量资源，在索引操作期间会造成没有足够的资源供其他应用程序和数据库操作使用。 出现此问题时，您可以通过限制用于索引操作的处理器数，手动配置用于运行索引语句的最大处理器数。  
  
-   MAXDOP 索引选项只为指定此选项的查询覆盖 max degree of parallelism 配置选项。 下表列出了可为 max degree of parallelism 配置选项和 MAXDOP 索引选项指定的有效整数值。  
  
    |值|说明|  
    |-----------|-----------------|  
    |0|指定服务器根据当前系统工作负荷确定所使用的 CPU 数目。 这是默认值，还是推荐设置。|  
    |1|取消生成并行计划。 操作将以串行方式执行。|  
    |2-64|将处理器的数量限制为指定的值。 根据当前工作负荷，可能使用较少的处理器。 如果指定的值大于可用的 CPU 数量，将使用实际可用的 CPU 数量。|  
  
-   并行索引执行和 MAXDOP 索引选项适用于下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句：  
  
    -   CREATE INDEX  
  
    -   ALTER INDEX REBUILD  
  
    -   DROP INDEX（只适用于聚集索引。）  
  
    -   ALTER TABLE ADD (索引) CONSTRAINT  
  
    -   ALTER TABLE DROP (聚集索引) CONSTRAINT  
  
-   不能在 ALTER INDEX REORGANIZE 语句中指定 MAXDOP 索引选项。  
  
-   如果查询优化器将并行度应用于生成操作，则需要排序的已分区索引操作的内存需求可能会很大。 并行度越高，内存需求就越大。 有关详细信息，请参阅 [Partitioned Tables and Indexes](../../relational-databases/partitions/partitioned-tables-and-indexes.md)。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 权限  
 要求对表或视图具有 ALTER 权限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-set-max-degree-of-parallelism-on-an-index"></a>设置索引的最大并行度  
  
1.  在对象资源管理器中，单击加号以展开所需的数据库，其中包含您要设置索引最大并行度的表。  
  
2.  展开 **“表”** 文件夹。  
  
3.  单击加号以展开您要设置索引的最大并行度的表。  
  
4.  展开 **“索引”** 文件夹。  
  
5.  右键单击要为其设置最大并行度的索引，然后选择“属性”。  
  
6.  在 **“选择页”**下，选择 **“选项”**。  
  
7.  选择 **“最大并行度”**，然后输入 1 和 64 之间的某个值。  
  
8.  单击 **“确定”**。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-set-max-degree-of-parallelism-on-an-existing-index"></a>设置现有索引的最大并行度  
  
1.  在 **“对象资源管理器”**中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击 **“执行”**。  
  
    ```  
    USE AdventureWorks2012;   
    GO  
    /*Alters the IX_ProductVendor_VendorID index on the Purchasing.ProductVendor table so that, if the server has eight or more processors, the Database Engine will limit the execution of the index operation to eight or fewer processors.  
    */  
    ALTER INDEX IX_ProductVendor_VendorID ON Purchasing.ProductVendor  
    REBUILD WITH (MAXDOP=8);   
    GO  
    ```  
  
 有关详细信息，请参阅 [ALTER INDEX (Transact-SQL)](../../t-sql/statements/alter-index-transact-sql.md)。  
  
#### <a name="set-max-degree-of-parallelism-on-a-new-index"></a>设置新建索引的最大并行度  
  
1.  在 **“对象资源管理器”**中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击 **“执行”**。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    CREATE INDEX IX_ProductVendor_NewVendorID   
    ON Purchasing.ProductVendor (BusinessEntityID)  
    WITH (MAXDOP=8);  
    GO  
    ```  
  
 有关详细信息，请参阅 [CREATE INDEX (Transact-SQL)](../../t-sql/statements/create-index-transact-sql.md)。  
  
  

