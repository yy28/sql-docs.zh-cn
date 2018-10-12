---
title: 创建边缘约束 | Microsoft Docs
ms.custom: ''
ms.date: 09/11/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- edge constraints [SQL Server]
- CONNECTION constraints
- edge constraints [Azure SQL Database]
- graph edge constraints
- SQL Graph
ms.assetid: ''
author: shkale-msft
ms.author: shkale
manager: craigg
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 160de04e9b8fbe83e8a771f5622f4f6103a8c7bb
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47845591"
---
# <a name="create-edge-constraints"></a>创建边缘约束
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx.md](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

   可以使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 定义 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的边缘约束。 
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Restrictions"></a> 限制和局限  
  
-   边缘约束只能在图形边缘表上进行定义。 
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  

### <a name="to-create-an-edge-constraint-on-a-new-edge-table"></a>在新边缘表上创建边缘约束
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行” 。 该示例在购买边缘表上创建边缘约束。  
  
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
 ```  

### <a name="to-add-edge-constraint-to-an-existing-edge-table"></a>将边缘约束添加到现有边缘表。 
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行” 。 该示例使用 ALTER TABLE 将边缘约束添加到购买边缘表。
  
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
        PurchaseCount INT
    )
 AS EDGE
 GO

 ALTER TABLE bought ADD CONSTRAINT EC_BOUGHT1 CONNECTION (Customer TO Product)
 GO
 ```  

### <a name="creating-a-new-edge-constraint-on-existing-edge-table-with-additional-edge-constraint-clauses"></a>在现有边缘表上创建新边缘约束，其中包含其他边缘约束子句。
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行” 。 该示例使用 ALTER TABLE 在购买边缘表上添加含有其他边缘约束子句的新边缘约束。
  
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
  ) AS NODE
 GO

 CREATE TABLE bought
    (
        PurchaseCount INT,
        CONSTRAINT EC_BOUGHT CONNECTION (Customer TO Product)
    )
 AS EDGE
 GO

 -- Drop the existing edge constraint first and then create a new one.
 ALTER TABLE bought DROP CONSTRAINT EC_BOUGHT
 GO

 -- User ALTER TABLE to create a new edge constraint.
 ALTER TABLE bought ADD CONSTRAINT EC_BOUGHT1 CONNECTION (Customer TO Product, Supplier TO Product)
 GO
 ```  
 请注意，在 EC_BOUGHT1 约束中有两个边缘约束子句，一个子句将客户连接到产品，另一个子句将供应商连接到产品。 这两个子句都可应用于析取。 即，给定的边缘必须满足这两个子句之一，才能在边缘表中使用。 



### <a name="creating-a-new-edge-constraint-on-existing-edge-table-with-new-edge-constraint-clause"></a>在现有边缘表上创建新边缘约束，其中包含新的边缘约束子句。
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行” 。 该示例使用 ALTER TABLE 在购买边缘表上添加含有新边缘约束子句的新边缘约束。
  
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
  ) AS NODE
 GO

 CREATE TABLE bought
    (
        PurchaseCount INT,
        CONSTRAINT EC_BOUGHT CONNECTION (Customer TO Product)
    )
 AS EDGE
 GO

 ALTER TABLE bought ADD CONSTRAINT EC_BOUGHT1 CONNECTION (Supplier TO Product)
 GO
 ```  

 在此示例中，我们在购买边缘表中创建了两个单独的边缘约束：EC_BOUGHT 和 EC_BOUGHT1。 这两个边缘约束都具有不同的边缘约束子句。 如果一个边缘表在其上具有多个边缘约束，则给定的边缘表必须满足所有边缘约束，才能在边缘表中使用它。 因为此处没有能够同时满足 EC_BOUGHT 和 EC_BOUGHT1 的任何边缘，所以购买边缘表必须保持为空。 

 为了在此边缘表中成功实现插入操作，必须删除其中的一个边缘约束，或必须将这两个边缘约束全部删除，且应创建一个新的边缘约束，该约束中包含这两个边缘约束子句。 

 ```sql
 USE TEMPDB
 GO
 -- Drop the existing edge constraint first and then create a new one.
 ALTER TABLE bought DROP CONSTRAINT EC_BOUGHT
 GO
 
 ALTER TABLE bought DROP CONSTRAINT EC_BOUGHT1
 GO
 
 ALTER TABLE bought ADD CONSTRAINT EC_BOUGHT_NEW CONNECTION (Customer TO Product, Supplier TO Product)
 GO
 ```  

 为了能够在购买边缘中使用给定的边缘，它必须满足 EC_BOUGHT_NEW 约束中的边缘约束子句之一。 因此，将允许使用尝试将有效的客户连接到产品或将供应商连接到产品节点的任何边缘。 
