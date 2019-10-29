---
title: 步骤 3：使用 pyodbc 连接到 SQL 的概念证明 | Microsoft Docs
ms.custom: ''
ms.date: 10/09/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4bfd6e52-817d-4f0a-a33d-11466e3f0484
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0e241d84ebc60acceafe09b1a9240711a72d2067
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/23/2019
ms.locfileid: "72798315"
---
# <a name="step-3-proof-of-concept-connecting-to-sql-using-pyodbc"></a>步骤 3：使用 pyodbc 连接到 SQL 的概念验证

此示例只应视为概念证明。  为清楚起见，示例代码已简化，不一定表示 Microsoft 推荐的最佳做法。  

**运行下面的示例脚本** 创建一个名为 test.py 的文件，并根据需要添加每个代码片段。 

```
> python test.py
```
  
## <a name="step-1--connect"></a>步骤1：连接  
  
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
  
  
## <a name="step-2--execute-query"></a>步骤2：执行查询  
  
cursor.execute 函数可用于从针对 SQL 数据库的查询中检索结果集。 此函数实际上可接受任何查询，并返回可使用 cursor.fetchone() 循环访问的结果集
  
  
```python
#Sample select query
cursor.execute("SELECT @@version;") 
row = cursor.fetchone() 
while row: 
    print(row[0])
    row = cursor.fetchone()

```  
  
## <a name="step-3--insert-a-row"></a>步骤3：插入行  
  
此示例展示了如何安全执行 [INSERT](../../../t-sql/statements/insert-transact-sql.md) 语句，并传递用于保护应用程序免遭 [SQL 注入](../../../relational-databases/tables/primary-and-foreign-key-constraints.md)值影响的参数。    
  
  
```python

#Sample insert query
cursor.execute("INSERT SalesLT.Product (Name, ProductNumber, StandardCost, ListPrice, SellStartDate) OUTPUT INSERTED.ProductID VALUES ('SQL Server Express New 20', 'SQLEXPRESS New 20', 0, 0, CURRENT_TIMESTAMP )") 
cnxn.commit()
row = cursor.fetchone()

while row: 
    print 'Inserted Product key is ' + str(row[0]) 
    row = cursor.fetchone()
```  

## <a name="azure-active-directory-aad-and-the-connection-string"></a>Azure Active Directory （AAD）和连接字符串

pyODBC 使用 Microsoft ODBC Driver for SQL Server。
如果 ODBC 驱动程序的版本是17.1 或更高版本，则可以通过 pyODBC 使用 ODBC 驱动程序的 AAD 交互模式。
如果 Python 和 pyODBC 允许 ODBC 驱动程序弹出对话框，则此 AAD interactive 选项有效。
此选项仅在 Windows 操作系统上可用。

### <a name="example-connection-string-for-aad-interactive-authentication"></a>AAD 交互身份验证的连接字符串示例

下面是一个指定 AAD 交互身份验证的示例 ODBC 连接字符串：

- `server=Server;database=Database;UID=UserName;Authentication=ActiveDirectoryInteractive;`

有关 ODBC 驱动程序的 AAD 身份验证选项的详细信息，请参阅以下文章：

- [结合使用 Azure Active Directory 和 ODBC 驱动程序](../../odbc/using-azure-active-directory.md#new-andor-modified-dsn-and-connection-string-keywords)

## <a name="next-steps"></a>后续步骤
  
有关详细信息，请参阅 [Python 开发人员中心](https://azure.microsoft.com/develop/python/)。
