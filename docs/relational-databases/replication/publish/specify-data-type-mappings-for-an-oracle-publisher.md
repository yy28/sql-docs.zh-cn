---
title: "指定 Oracle 发布服务器的数据类型映射 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Oracle 发布 [SQL Server 复制], 数据类型映射"
  - "数据类型 [SQL Server 复制], Oracle 发布"
  - "映射数据类型 [SQL Server 复制]"
ms.assetid: f172d631-3b8c-4912-bd0f-568366cd9870
caps.latest.revision: 37
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 37
---
# 指定 Oracle 发布服务器的数据类型映射
  本主题说明如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中指定 Oracle 发布服务器的数据类型映射。 虽然已经为 Oracle 发布服务器提供了一组默认数据类型映射，但可能仍有必要为给定发布指定不同的映射。  
  
 **本主题内容**  
  
-   **指定 Oracle 发布服务器的数据类型映射，使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 在指定数据类型映射 **数据映射** 的选项卡上 **项目属性-\< 项目>** 对话框。 这是可从 **文章** 新建发布向导的页面和 **发布属性-\< 发布>** 对话框。 有关使用向导和访问对话框中的详细信息，请参阅 [从 Oracle 数据库创建发布](../../../relational-databases/replication/publish/create-a-publication-from-an-oracle-database.md) 和 [查看和修改发布属性](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)。  
  
#### 指定数据类型映射  
  
1.  在 **文章** 新建发布向导的页面或 **发布属性-\< 发布>** 对话框中，选择一个表，然后单击 **项目属性**。  
  
2.  单击 **“设置突出显示的表项目的属性”**。  
  
3.  在 **数据映射** 的选项卡上 **项目属性-\< 项目>** 对话框中，选择映射与从 **订阅服务器数据类型** 列︰  
  
    -   对于某些数据类型，只能有一种可能的映射，在这种情况下，属性网格中的相应列是只读的。  
  
    -   对于某些数据类型，有多种可供选择的映射类型。 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 建议使用默认映射。 有关详细信息，请参阅 [Data Type Mapping for Oracle Publishers](../../../relational-databases/replication/non-sql/data-type-mapping-for-oracle-publishers.md)。  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 可以使用复制存储过程，以编程方式指定自定义数据类型映射。 您还可以设置间映射数据类型时，将使用的默认映射 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 和非[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据库管理系统 (DBMS)。 有关详细信息，请参阅 [Data Type Mapping for Oracle Publishers](../../../relational-databases/replication/non-sql/data-type-mapping-for-oracle-publishers.md)。  
  
#### 在创建属于 Oracle 发布的项目时定义自定义数据类型映射  
  
1.  如果尚不存在 Oracle 发布，请创建一个。  
  
2.  在分发服务器上，执行 [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)。 将值指定为 **0** 为 **@use_default_datatypes**。 有关详细信息，请参阅 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)。  
  
3.  在分发服务器上，执行 [sp_helparticlecolumns](../../../relational-databases/system-stored-procedures/sp-helparticlecolumns-transact-sql.md) 若要查看已发布的文章中的某一列的现有映射。  
  
4.  在分发服务器上，执行 [sp_changearticlecolumndatatype](../../../relational-databases/system-stored-procedures/sp-changearticlecolumndatatype-transact-sql.md)。 为 **@publisher**指定 Oracle 发布服务器的名称，并指定 **@publication**、 **@article**和 **@column** 以定义已发布的列。 为 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] @type **指定要映射到的**数据类型的名称，并在必要时指定 **@length**、 **@precision**和 **@scale**。  
  
5.  在分发服务器上，执行 [sp_articleview](../../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)。 这将创建用于从 Oracle 发布生成快照的视图。  
  
#### 将映射指定为数据类型的默认映射  
  
1.  （可选）在任何数据库上分发服务器上，执行 [sp_getdefaultdatatypemapping](../../../relational-databases/system-stored-procedures/sp-getdefaultdatatypemapping-transact-sql.md)。 指定 **@source_dbms**, ，**@source_type**, ，**@destination_dbms**, ，**@destination_version**, ，以及标识源 DBMS 所需的任何其他参数。 将使用输出参数返回有关目标 DBMS 中当前映射的数据类型的信息。  
  
2.  （可选）在任何数据库上分发服务器上，执行 [sp_helpdatatypemap](../../../relational-databases/system-stored-procedures/sp-helpdatatypemap-transact-sql.md)。 指定 **@source_dbms** 和筛选结果集所需的任何其他参数。 记下的值 **mapping_id** 对于结果中所需的映射设置。  
  
3.  在任何数据库上分发服务器上，执行 [sp_setdefaultdatatypemapping](../../../relational-databases/system-stored-procedures/sp-setdefaultdatatypemapping-transact-sql.md)。  
  
    -   如果您知道所需的值的 **mapping_id** 获得在步骤 2 中，指定它为 **@mapping_id**。  
  
    -   如果不知道 **mapping_id**, ，指定的参数 **@source_dbms**, ，**@source_type**, ，**@destination_dbms**, ，**@destination_type**, ，以及标识现有映射所需的任何其他参数。  
  
#### 查找针对给定的 Oracle 数据类型的有效数据类型  
  
1.  在任何数据库上分发服务器上，执行 [sp_helpdatatypemap](../../../relational-databases/system-stored-procedures/sp-helpdatatypemap-transact-sql.md)。 将值指定为 **ORACLE** 为 **@source_dbms** 和筛选结果集所需的任何其他参数。  
  
###  <a name="TsqlExample"></a> 示例 (Transact-SQL)  
 此示例将更改具有类型为 Oracle 数据类型 NUMBER 的列映射到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据类型 **数值**(38，38) 而不是默认数据类型 **float**。  
  
 [!code-sql[HowTo#sp_changecolumndatatype](../../../relational-databases/replication/codesnippet/tsql/specify-data-type-mappin_1.sql)]  
  
 此示例查询将返回 Oracle 9 数据类型 **CHAR**的默认映射及替代映射。  
  
 [!code-sql[HowTo#sp_helpcolumndatatype_char](../../../relational-databases/replication/codesnippet/tsql/specify-data-type-mappin_2.sql)]  
  
 此示例查询在未对 Oracle 9 数据类型 **NUMBER** 指定小数位数或精度时，返回该数据类型的默认映射。  
  
 [!code-sql[HowTo#sp_helpcolumndatatype_number](../../../relational-databases/replication/codesnippet/tsql/specify-data-type-mappin_3.sql)]  
  
## 另请参阅  
 [Oracle 发布服务器的数据类型映射](../../../relational-databases/replication/non-sql/data-type-mapping-for-oracle-publishers.md)   
 [异类数据库复制](../../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [复制系统存储过程概念](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [配置 Oracle 发布服务器](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)  
  
  