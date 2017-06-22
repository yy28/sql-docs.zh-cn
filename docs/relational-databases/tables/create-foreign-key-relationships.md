---
title: "创建外键关系 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 05/18/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-tables
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- relationships [SQL Server], creating
ms.assetid: 867a54b8-5be4-46e6-9702-49ae6dabf67c
caps.latest.revision: 21
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: bc2034ac69dee1a72429e94841aec1763703de7c
ms.openlocfilehash: f6d1acfc492d4d2c37bd4e7cfe66a2b95266a80a
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="create-foreign-key-relationships"></a>创建外键关系
[!INCLUDE[tsql-appliesto-ss2016-all_md](../../includes/tsql-appliesto-ss2016-all-md.md)]

 > 有关与以前版本的 SQL Server 相关的内容，请参阅 [Create Foreign Key Relationships](https://msdn.microsoft.com/en-US/library/ms189049(SQL.120).aspx)（创建外键关系）。


  本主题说明如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中创建外键关系。 当希望将一个表的行与另一个表的行相关联时，您可在这两个表之间创建关系。    
     
##  <a name="BeforeYouBegin"></a> 开始之前！ 限制和局限
 
-   外键约束并不仅仅可以与另一表的主键约束相链接，它还可以定义为引用另一个表中 UNIQUE 约束的列。    
    
-   如果在 FOREIGN KEY 约束的列中输入非 NULL 值，则此值必须在被引用列中存在；否则，将返回违反外键约束的错误信息。 若要确保验证了组合外键约束的所有值，请对所有参与列指定 NOT NULL。    
    
-   FOREIGN KEY 约束仅能引用位于同一服务器上的同一数据库中的表。 跨数据库的引用完整性必须通过触发器实现。 有关详细信息，请参阅 [CREATE TRIGGER (Transact-SQL)](../../t-sql/statements/create-trigger-transact-sql.md)。    
    
-   FOREIGN KEY 约束可引用同一表中的其他列。 此行为称为自引用。    
    
-   在列级指定的 FOREIGN KEY 约束只能列出一个引用列。 此列的数据类型必须与定义约束的列的数据类型相同。    
    
-   在表级指定的 FOREIGN KEY 约束所具有的引用列数目必须与约束列列表中的列数相同。 每个引用列的数据类型也必须与列表中相应列的数据类型相同。    
    
-   对于表可包含的引用其他表的 FOREIGN KEY 约束的数目或其他表所拥有的引用特定表的 FOREIGN KEY 约束的数目， [!INCLUDE[ssDE](../../includes/ssde-md.md)] 都没有预定义的限制。 尽管如此，可使用的 FOREIGN KEY 约束的实际数目还是受硬件配置以及数据库和应用程序设计的限制。  表最多可以将 253 个其他表和列作为外键引用（传出引用）。 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 将可在单独的表中引用的其他表和列（传入引用）的数量限制从 253 提高至 10,000。  （兼容性级别至少必须为 130。）数量限制的提高带来了下列约束：    
    
    -   DELETE 和 UPDATE DML 操作支持大于 253 个外键引用。 不支持 MERGE 操作。    
    
    -   对自身进行外键引用的表仍只能进行 253 个外键引用。    
    
    -   列存储索引、内存优化表和 Stretch Database 暂不支持进行超过 253 个外键引用。    
    
-   对于临时表不强制 FOREIGN KEY 约束。    
    
-   如果在 CLR 用户定义类型的列上定义外键，则该类型的实现必须支持二进制排序。 有关详细信息，请参阅 [CLR 用户定义类型](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)。    
    
-   仅当 FOREIGN KEY 约束引用的主键也定义为类型 **varchar(max)** 时，才能在此约束中使用类型为 **varchar(max)**的列。    
    

    
##   <a name="permissions"></a>Permissions    
 使用外键创建新表需要在数据库中具有 CREATE TABLE 权限，并对在其中创建表的架构具有 ALTER 权限。    
    
 在某一现有表中创建外键需要对该表具有 ALTER 权限。    
       
    
## <a name="create-a-foreign-key-relationship-in-table-designer"></a>在表设计器中创建外键关系 
####  <a name="using-sql-server-management-studio"></a>使用 SQL Server Management Studio    
    
1.  在对象资源管理器中，右键单击将位于关系的外键方的表，再单击“设计”。    
    
     此时，将在 **表设计器**中打开该表。    
    
2.  在 **表设计器** 菜单上，单击 **“关系”**。    
    
3.  在“外键关系”对话框中，单击“添加”。    
    
     “选定的关系”列表中将以系统提供的名称显示关系，格式为 FK_\<*tablename*>_\<*tablename*>，其中 *tablename* 是外键表的名称。    
    
4.  在 **“选定的关系”** 列表中单击该关系。    
    
5.  单击右侧网格中的“表和列规范” ，再单击该属性右侧的省略号 (**…**)。    
    
6.  在“表和列”对话框中，从“主键”下拉列表中选择要位于关系主键方的表。    
    
7.  在下方的网格中，选择要分配给表的主键的列。 在每列左侧的相临网格单元格中，选择外键表的相应外键列。    
    
     **表设计器** 将为此关系提供一个建议名称。 若要更改此名称，请编辑 **“关系名”** 文本框的内容。    
    
8.  选择 **“确定”** 以创建该关系。    
       
## <a name="create-a-foreign-key-in-a-new-table"></a>在新表中创建外键  
####  <a name="using-transact-sql"></a>使用 Transact-SQL   
    
1.  在 **“对象资源管理器”**中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的实例。    
    
2.  在标准菜单栏上，单击 **“新建查询”**。    
    
3.  将以下示例复制并粘贴到查询窗口中，然后单击 **“执行”**。 此实例创建一个表并定义针对列 `TempID` 的外键约束，该列引用 `SalesReasonID` 表中的列 `Sales.SalesReason` 。 ON DELETE CASCADE 和 ON UPDATE CASCADE 子句用于确保对 `Sales.SalesReason` 表的更改自动传播到 `Sales.TempSalesReason` 表。    
    
    ```    
    USE AdventureWorks2012;    
    GO    
    CREATE TABLE Sales.TempSalesReason (TempID int NOT NULL, Name nvarchar(50),     
    CONSTRAINT PK_TempSales PRIMARY KEY NONCLUSTERED (TempID),     
    CONSTRAINT FK_TempSales_SalesReason FOREIGN KEY (TempID)     
        REFERENCES Sales.SalesReason (SalesReasonID)     
        ON DELETE CASCADE    
        ON UPDATE CASCADE    
    );GO    
    
    ```    
    
## <a name="create-a-foreign-key-in-an-existing-table"></a>在现有表中创建外键 
#### <a name="using-transasct-sql"></a>使用 Transact-SQL   
    
1.  在 **“对象资源管理器”**中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的实例。    
    
2.  在标准菜单栏上，单击 **“新建查询”**。    
    
3.  将以下示例复制并粘贴到查询窗口中，然后单击 **“执行”**。 此示例针对 `TempID` 列创建外键并引用 `SalesReasonID` 表中的 `Sales.SalesReason` 列。    
    
    ```    
    USE AdventureWorks2012;    
    GO    
    ALTER TABLE Sales.TempSalesReason     
    ADD CONSTRAINT FK_TempSales_SalesReason FOREIGN KEY (TempID)     
        REFERENCES Sales.SalesReason (SalesReasonID)     
        ON DELETE CASCADE    
        ON UPDATE CASCADE    
    ;    
    GO    
    
    ```    
    
     有关详细信息，请参阅 [ALTER TABLE (Transact-SQL)](../../t-sql/statements/alter-table-transact-sql.md)、[CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md) 和 [table_constraint (Transact-SQL)](../../t-sql/statements/alter-table-table-constraint-transact-sql.md)。    
    
  

