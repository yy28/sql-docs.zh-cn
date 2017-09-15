---
title: "步骤 3： 连接到 SQL 使用 pymssql 的概念证明 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 2246ddeb-7c2f-46f3-8a91-cdd718d39b40
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 732e6fd574d80d58aef81a149acc54376231e6cc
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="step-3-proof-of-concept-connecting-to-sql-using-pymssql"></a>步骤 3： 连接到 SQL 使用 pymssql 的概念证明
[!INCLUDE[Driver_Python_Download](../../../includes/driver_python_download.md)]

此示例中，应考虑仅概念证明。  示例代码为清楚起见，简化，并不一定表示 Microsoft 推荐的最佳做法。  
  
## <a name="step-1--connect"></a>步骤 1： 连接  
  
[Pymssql.connect](http://pymssql.org/en/latest/ref/pymssql.html)函数用于连接到 SQL 数据库。  
  
```python
    import pymssql  
    conn = pymssql.connect(server='yourserver.database.windows.net', user='yourusername@yourserver', password='yourpassword', database='AdventureWorks')  
```  
  
  
## <a name="step-2--execute-query"></a>步骤 2： 执行查询  
  
[Cursor.execute](http://pymssql.org/en/latest/ref/pymssql.html#pymssql.Cursor.execute)函数可以用于检索针对 SQL 数据库设置从查询结果。 此函数实际上可接受任何查询，并返回可循环访问与使用的结果集[cursor.fetchone （)](http://pymssql.org/en/latest/ref/pymssql.html#pymssql.Cursor.fetchone)。  
  
  
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
  
在此示例中，你将了解如何执行[插入](https://msdn.microsoft.com/library/ms174335.aspx)语句安全地，传递参数，保护你的应用程序从该[SQL 注入](https://technet.microsoft.com/library/ms161953(v=sql.105).aspx)漏洞，并检索自动生成[主键](https://msdn.microsoft.com/library/ms179610.aspx)值。    
  
  
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
  
## <a name="step-4--rollback-a-transaction"></a>步骤 4： 事务回滚  
  
此代码示例演示使用事务在其中你：  
  
* 开始执行事务  
* 插入数据行  
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
  
有关详细信息，请参阅[Python 开发人员中心](https://azure.microsoft.com/en-us/develop/python/)。
