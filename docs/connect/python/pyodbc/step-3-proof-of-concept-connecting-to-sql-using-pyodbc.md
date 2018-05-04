---
title: 步骤 3： 连接到 SQL 使用 pyodbc 的概念证明 |Microsoft 文档
ms.custom: ''
ms.date: 08/08/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: python
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 4bfd6e52-817d-4f0a-a33d-11466e3f0484
caps.latest.revision: 2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5200aff9d34bd45074e8e2c8e6b61c979e1aed56
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
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
# Some other example server values are
# server = 'localhost\sqlexpress' # for a named instance
# server = 'myserver,port' # to specify an alternate port
server = 'tcp:myserver.database.windows.net' 
database = 'mydb' 
username = 'myusername' 
password = 'mypassword' 
cnxn = pyodbc.connect('DRIVER={ODBC Driver 17 for SQL Server};SERVER='+server+';DATABASE='+database+';UID='+username+';PWD='+ password)
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
  
在此示例中，你将了解如何执行[插入](../../../t-sql/statements/insert-transact-sql.md)语句安全地，传递参数，保护你的应用程序从该[SQL 注入](../../../relational-databases/tables/primary-and-foreign-key-constraints.md)值。    
  
  
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
