---
title: 查看边缘约束属性 | Microsoft Docs
ms.custom: ''
ms.date: 09/18/2018
ms.prod: sql
ms.prod_service: table-view-index, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- edge constraints [SQL Server], attributes
- displaying edge constraint attributes
- viewing edge constraint attributes
ms.assetid: b0e57cb7-9b26-4b96-b76a-1f59f5f498c5
author: shkale-msft
ms.author: shkale
manager: craigg
monikerRange: '>=sql-server-2017||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 129d61ddf42a159dbeba74a168d10dac72094b3a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47790675"
---
# <a name="view-edge-constraint-properties"></a>查看边缘约束属性
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx.md](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

  可以通过使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查看边缘约束属性 [!INCLUDE[noversion](../../includes/ssnoversion-md.md)]。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [Security](#Security)  
  
-   **查看特定表的外键属性，使用：**  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-view-the-foreign-key-attributes-of-a-relationship-in-a-specific-table"></a>查看特定表中关系的外键属性  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行” 。 此实例返回 tempdb 数据库中的边缘表 `bought` 的所有边缘约束及其属性。  
    
    ```sql
    USE TEMPDB
    GO
    -- CREATE node and edge tables
    CREATE TABLE Customer
      (
        ID INTEGER PRIMARY KEY, 
        CustomerName VARCHAR(100)
      )
    AS NODE
    GO

    CREATE TABLE Supplier
      (
        ID INTEGER PRIMARY KEY, 
        SupplierName VARCHAR(100)
      )
    AS NODE
    GO

    CREATE TABLE Product 
      (
        ID INTEGER PRIMARY KEY, 
        ProductName VARCHAR(100)
      ) 
    AS NODE
    GO
    -- CREATE edge table with edge constraints.
    CREATE TABLE bought
      (
        PurchaseCount INT,
        CONSTRAINT EC_BOUGHT CONNECTION (Customer TO Product, Supplier TO Product)
      )
    AS EDGE
    GO
    
    -- Query sys.edge_constraints and sys.edge_constraint_clauses to view 
    -- edge constraint properties. 
    SELECT
        EC.name AS edge_constraint_name
        , OBJECT_NAME(EC.parent_object_id) AS edge_table_name
        , OBJECT_NAME(ECC.from_object_id) AS from_node_table_name
        , OBJECT_NAME(ECC.to_object_id) AS to_node_table_name
        , is_disabled
        , is_not_trusted
    FROM sys.edge_constraints EC
    INNER JOIN sys.edge_constraint_clauses ECC
        ON EC.object_id = ECC.object_id
    WHERE EC.parent_object_id = object_id('bought')
    ```  
  
 有关详细信息，请参阅 [sys.edge_constraints &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-edge-constraints-transact-sql.md) 和 [sys.edge_constraint_clauses &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-edge-constraint-clauses-transact-sql.md)。  
  
###  <a name="TsqlExample"></a>  
