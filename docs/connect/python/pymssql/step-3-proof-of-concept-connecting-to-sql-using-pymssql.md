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
manager: jroth
ms.openlocfilehash: 48ae75c5eee03cba273e65297b3652c1a2da99ec
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2019
ms.locfileid: "66800858"
---
# <a name="step-3-proof-of-concept-connecting-to-sql-using-pymssql"></a>步骤 3：使用 pymssql 连接到 SQL 的概念验证
[!INCLUDE[Driver_Python_Download](../../../includes/driver_python_download.md)]

此示例中，应考虑仅概念证明。  示例代码简化为清楚起见，而不一定表示 Microsoft 推荐的最佳做法。  
  
## <a name="step-1--connect"></a>步骤 1： 连接  
  
[Pymssql.connect](https://pymssql.org/en/latest/ref/pymssql.html)函数用于连接到 SQL 数据库。  
  
```python
    import pymssql  
    conn = pymssql.connect(server='yourserver.database.windows.net', user='yourusername@yourserver', password='yourpassword', database='AdventureWorks')  
```  
  
  
## <a name="step-2--execute-query"></a>步骤 2： 执行查询  
  
[Cursor.execute](https://pymssql.org/en/latest/ref/pymssql.html#pymssql.Cursor.execute)函数可用于检索针对 SQL 数据库的查询集的结果。 此函数实际上可接受任何查询并返回一个结果集，可以循环访问与使用[cursor.fetchone （)](https://pymssql.org/en/latest/ref/pymssql.html#pymssql.Cursor.fetchone)。  
  
  
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
  
## <a name="step-3--insert-a-row"></a>步骤 3： 插入行  
  
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
  
## <a name="step-4--rollback-a-transaction"></a>步骤 4： 回滚事务  
  
此代码示例演示如何使用事务在其中你：  
  
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
  
有关详细信息，请参阅[Python 开发人员中心](https://azure.microsoft.com/develop/python/)。
