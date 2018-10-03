---
title: 步骤 3：使用 pyodbc 连接到 SQL 的概念证明 | Microsoft Docs
ms.custom: ''
ms.date: 08/08/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4bfd6e52-817d-4f0a-a33d-11466e3f0484
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cd861c50523e218bc1cf0ed6e538e66eeb3671f3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47756309"
---
# <a name="step-3-proof-of-concept-connecting-to-sql-using-pyodbc"></a>步骤 3：使用 pyodbc 连接到 SQL 的概念验证

此示例中，应考虑仅概念证明。  示例代码简化为清楚起见，而不一定表示 Microsoft 推荐的最佳做法。  

**运行下面的示例脚本**创建一个名为 test.py，文件并将每个代码段添加意愿。 

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
  
Cursor.executefunction 可以用于检索针对 SQL 数据库的查询集的结果。 此函数实际上可接受任何查询并返回一个结果集，可以循环访问与使用 cursor.fetchone （）
  
  
```python
#Sample select query
cursor.execute("SELECT @@version;") 
row = cursor.fetchone() 
while row: 
    print row[0] 
    row = cursor.fetchone()

```  
  
## <a name="step-3--insert-a-row"></a>步骤 3： 插入行  
  
在此示例中您将了解如何执行[插入](../../../t-sql/statements/insert-transact-sql.md)语句，传递参数以保护应用程序免遭[SQL 注入](../../../relational-databases/tables/primary-and-foreign-key-constraints.md)值。    
  
  
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
  
有关详细信息，请参阅[Python 开发人员中心](https://azure.microsoft.com/develop/python/)。
