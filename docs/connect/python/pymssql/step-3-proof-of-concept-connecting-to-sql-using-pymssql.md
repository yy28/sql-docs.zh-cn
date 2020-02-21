---
title: 步骤 3：使用 pymssql 连接到 SQL 的概念证明 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 2246ddeb-7c2f-46f3-8a91-cdd718d39b40
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c1dfce515eeadbdbaf1fd96e6dcf1a08cd536ab5
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "74200460"
---
# <a name="step-3-proof-of-concept-connecting-to-sql-using-pymssql"></a>步骤 3：使用 pymssql 连接到 SQL 的概念证明
[!INCLUDE[Driver_Python_Download](../../../includes/driver_python_download.md)]

此示例应只视为概念证明。  为清楚起见，示例代码已简化，不一定代表 Microsoft 建议的最佳做法。  
  
## <a name="step-1--connect"></a>步骤 1：连接  
  
[Pymssql.connect](https://pypi.org/project/pymssql/) 函数用于连接到 SQL 数据库。  
  
```python
    import pymssql  
    conn = pymssql.connect(server='yourserver.database.windows.net', user='yourusername@yourserver', password='yourpassword', database='AdventureWorks')  
```  
  
  
## <a name="step-2--execute-query"></a>步骤 2：执行查询  
  
[Cursor.execute](https://pypi.org/project/pymssql/) 函数可用于针对 SQL 数据库从查询中检索结果集。 此函数实际上可接受任何查询，并返回可使用 [cursor.fetchone()](https://pypi.org/project/pymssql/) 循环访问的结果集。  
  
  
```python
    import pymssql  
    conn = pymssql.connect(server='yourserver.database.windows.net', user='yourusername@yourserver', password='yourpassword', database='AdventureWorks')  
    cursor = conn.cursor()  
    cursor.execute('SELECT c.CustomerID, c.CompanyName,COUNT(soh.SalesOrderID) AS OrderCount FROM SalesLT.Customer AS c LEFT OUTER JOIN SalesLT.SalesOrderHeader AS soh ON c.CustomerID = soh.CustomerID GROUP BY c.CustomerID, c.CompanyName ORDER BY OrderCount DESC;')  
    row = cursor.fetchone()  
    while row:  
        print str(row[0]) + " " + str(row[1]) + " " + str(row[2])     
        row = cursor.fetchone()  
```  
  
## <a name="step-3--insert-a-row"></a>步骤 3：插入行  
  
此示例展示了如何安全执行 [INSERT](../../../t-sql/statements/insert-transact-sql.md) 语句，并传递用于保护应用程序免遭 [SQL 注入](../../../relational-databases/tables/primary-and-foreign-key-constraints.md)值影响的参数。    
  
  
```python
    import pymssql  
    conn = pymssql.connect(server='yourserver.database.windows.net', user='yourusername@yourserver', password='yourpassword', database='AdventureWorks')  
    cursor = conn.cursor()  
    cursor.execute("INSERT SalesLT.Product (Name, ProductNumber, StandardCost, ListPrice, SellStartDate) OUTPUT INSERTED.ProductID VALUES ('SQL Server Express', 'SQLEXPRESS', 0, 0, CURRENT_TIMESTAMP)")  
    row = cursor.fetchone()  
    while row:  
        print "Inserted Product ID : " +str(row[0])  
        row = cursor.fetchone()  
    conn.commit()
    conn.close()
```  
  
## <a name="step-4--rollback-a-transaction"></a>步骤 4：回滚事务  
  
此代码示例演示了可以在其中执行以下操作的事务的用法：  
  
* 开始一个事务  
* 插入一行数据  
* 回滚事务以撤消插入  
  
```python
    import pymssql  
    conn = pymssql.connect(server='yourserver.database.windows.net', user='yourusername@yourserver', password='yourpassword', database='AdventureWorks')  
    cursor = conn.cursor()  
    cursor.execute("BEGIN TRANSACTION")  
    cursor.execute("INSERT SalesLT.Product (Name, ProductNumber, StandardCost, ListPrice, SellStartDate) OUTPUT INSERTED.ProductID VALUES ('SQL Server Express New', 'SQLEXPRESS New', 0, 0, CURRENT_TIMESTAMP)")  
    conn.rollback()  
    conn.close()
```  
    
  ## <a name="next-steps"></a>后续步骤  
  
有关详细信息，请参阅 [Python 开发人员中心](https://azure.microsoft.com/develop/python/)。
