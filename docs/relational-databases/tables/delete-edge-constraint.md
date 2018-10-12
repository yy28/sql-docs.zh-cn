---
title: 删除边缘约束 | Microsoft Docs
ms.custom: ''
ms.date: 09/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- removing edge constraint
- deleting edge constraint, deleting connection constraint
- SQL Graph
- graph edge constraints
ms.assetid: ''
author: shkale-msft
ms.author: shkale
manager: craigg
monikerRange: '>=sql-server-2017||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3761d9e8507eb7051fe7a6cc39b83abfa091566d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47774675"
---
# <a name="delete-edge-constraints"></a>删除边缘约束
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx.md](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

  可以使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 删除 [!INCLUDE[ssNoversion](../../includes/ssnoversion-md.md)] 中的边缘约束。 
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [Security](#Security)  
  
-   **使用以下工具删除主键：**  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 需要对表的 ALTER 权限。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-delete-an-edge-constraint"></a>删除边缘约束
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行” 。 该示例首先标识边缘约束的名称，然后删除该约束。  
  
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

    CREATE TABLE Product 
    (
        ID INTEGER PRIMARY KEY, 
        ProductName VARCHAR(100)
    ) AS NODE
    GO

    CREATE TABLE bought
    (
        PurchaseCount INT,
        CONSTRAINT EC_BOUGHT CONNECTION (Customer TO Product)
    )
    AS EDGE
    GO
    
    -- Return the name of edge constraint.
    SELECT name  
    FROM sys.edge_constraints  
    WHERE type = 'EC' AND parent_object_id = OBJECT_ID('bought');  
    GO  

    -- Delete the primary key constraint.  
    ALTER TABLE bought
    DROP CONSTRAINT EC_BOUGHT
    GO
    ```  
  
 有关详细信息，请参阅 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)、[sys.edge_constraints &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-edge-constraints-transact-sql.md) 和 [ssys.edge_constraint_clauses &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-edge-constraint-clauses-transact-sql.md)
  
###  <a name="TsqlExample"></a>  
