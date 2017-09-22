---
title: "步骤 3： 连接到 SQL 使用 pyodbc 的概念证明 |Microsoft 文档"
ms.custom: 
ms.date: 08/08/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4bfd6e52-817d-4f0a-a33d-11466e3f0484
caps.latest.revision: 2
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: a6aeda8e785fcaabef253a8256b5f6f7a842a324
ms.openlocfilehash: a93a7d4c341cd035faba52e5626608ef362359cd
ms.contentlocale: zh-cn
ms.lasthandoff: 09/21/2017

---
# <a name="step-3-proof-of-concept-connecting-to-sql-using-pyodbc"></a>步骤 3： 连接到 SQL 使用 pyodbc 的概念证明

此示例中，应考虑仅概念证明。  示例代码为清楚起见，简化，并不一定表示 Microsoft 推荐的最佳做法。  

**运行下面的示例脚本**创建名为 test.py，并根据自己的意愿添加每个代码段。 

```
> python test.py
```
  
## <a name="step-1--connect"></a>步骤 1： 连接  
  
```python

import pyodbc 
server = 'tcp:myserver.database.windows.net' 
database = 'mydb' 
username = 'myusername' 
password = 'mypassword' 
cnxn = pyodbc.connect('DRIVER={ODBC Driver 13 for SQL Server};SERVER='+server+';DATABASE='+database+';UID='+username+';PWD='+ password)
cursor = cnxn.cursor()

```  
  
  
## <a name="step-2--execute-query"></a>步骤 2： 执行查询  
  
Cursor.executefunction 可以用于检索针对 SQL 数据库设置从查询结果。 此函数实际上可接受任何查询，并返回可循环访问 cursor.fetchone （） 使用的结果集
  
  
```python
#Sample select query
cursor.execute("SELECT @@version;") 
row = cursor.fetchone() 
while row: 
    print row[0] 
    row = cursor.fetchone()

```  
  
## <a name="step-3--insert-a-row"></a>步骤 3： 插入行  
  
在此示例中，你将了解如何执行[插入](/sql-docs/docs/t-sql/statements/insert-transact-sql)语句安全地，传递参数，保护你的应用程序从该[SQL 注入](/sql-docs/docs/relational-databases/tables/primary-and-foreign-key-constraints)值。    
  
  
```python

#Sample insert query
cursor.execute("INSERT SalesLT.Product (Name, ProductNumber, StandardCost, ListPrice, SellStartDate) OUTPUT INSERTED.ProductID VALUES ('SQL Server Express New 20', 'SQLEXPRESS New 20', 0, 0, CURRENT_TIMESTAMP )") 
row = cursor.fetchone()

while row: 
    print 'Inserted Product key is ' + str(row[0]) 
    row = cursor.fetchone()
```  
  `      
  ## <a name="next-steps"></a>后续步骤  
  
有关详细信息，请参阅[Python 开发人员中心](https://azure.microsoft.com/en-us/develop/python/)。
