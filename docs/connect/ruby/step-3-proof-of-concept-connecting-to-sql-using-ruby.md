---
title: "步骤 3： 连接到 SQL 使用 Ruby 的概念证明 |Microsoft 文档"
ms.custom: 
ms.date: 08/08/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ruby
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: cac20b18-0a6d-4243-bbda-a5d1b9476441
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 481061c2d37bd4b6c6cf0c5c131f2c8a24f3025f
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/18/2017
---
# <a name="step-3-proof-of-concept-connecting-to-sql-using-ruby"></a>步骤 3： 连接到 SQL 使用 Ruby 的概念证明

此示例中，应考虑仅概念证明。  示例代码为清楚起见，简化，并不一定表示 Microsoft 推荐的最佳做法。  
  
## <a name="step-1--connect"></a>步骤 1： 连接  
  
[Tinytds:: Client](https://github.com/rails-sqlserver/tiny_tds)函数用于连接到 SQL 数据库。  
  
``` ruby
    require 'tiny_tds'  
    client = TinyTds::Client.new username: 'yourusername@yourserver', password: 'yourpassword',  
    host: 'yourserver.database.windows.net', port: 1433,  
    database: 'AdventureWorks', azure:true  
```  
  
## <a name="step-2--execute-a-query"></a>步骤 2： 执行查询  
  
复制并将以下代码粘贴到空文件中。 Test.rb。 然后，执行它通过从命令提示符下输入以下命令：  
  
    ruby test.rb  
  
在代码示例中， [TinyTds::Result](https://github.com/rails-sqlserver/tiny_tds)函数用于检索针对 SQL 数据库设置从查询结果。 此函数接受查询并返回一个结果集。 使用循环访问结果集[result.each do | 行 |](https://github.com/rails-sqlserver/tiny_tds)。  
  
``` ruby 
    require 'tiny_tds'    
    print 'test'       
    client = TinyTds::Client.new username: 'yourusername@yourserver', password: 'yourpassword',  
    host: 'yourserver.database.windows.net', port: 1433,  
    database: 'AdventureWorks', azure:true  
    results = client.execute("SELECT c.CustomerID, c.CompanyName,COUNT(soh.SalesOrderID) AS OrderCount FROM SalesLT.Customer AS c LEFT OUTER JOIN SalesLT.SalesOrderHeader AS soh ON c.CustomerID = soh.CustomerID GROUP BY c.CustomerID, c.CompanyName ORDER BY OrderCount DESC")  
    results.each do |row|  
    puts row  
    end  
```  
  
## <a name="step-3--insert-a-row"></a>步骤 3： 插入行  
  
在此示例中，你将了解如何执行[插入](../../t-sql/statements/insert-transact-sql.md)语句安全地，传递参数，保护你的应用程序从该[SQL 注入](../../relational-databases/tables/primary-and-foreign-key-constraints.md)值。    
  
若要配合使用 TinyTDS 和 Azure，建议你运行多个`SET`语句来更改当前会话处理特定信息的方式。 建议`SET`中的代码示例提供了语句。 例如，`SET ANSI_NULL_DFLT_ON`将允许创建新列来允许 null 值，即使未显式指定列的为 null 性状态。  
  
为了符合 Microsoft SQL Server [datetime](http://msdn.microsoft.com/library/ms187819.aspx)格式，请使用[strftime](http://ruby-doc.org/core-2.2.0/Time.html#method-i-strftime)函数转换成对应的日期时间格式。  
  
``` ruby
    require 'tiny_tds'  
    client = TinyTds::Client.new username: 'yourusername@yourserver', password: 'yourpassword',  
    host: 'yourserver.database.windows.net', port: 1433,  
    database: 'AdventureWorks', azure:true  
    results = client.execute("SET ANSI_NULLS ON")  
    results = client.execute("SET CURSOR_CLOSE_ON_COMMIT OFF")  
    results = client.execute("SET ANSI_NULL_DFLT_ON ON")  
    results = client.execute("SET IMPLICIT_TRANSACTIONS OFF")  
    results = client.execute("SET ANSI_PADDING ON")  
    results = client.execute("SET QUOTED_IDENTIFIER ON")  
    results = client.execute("SET ANSI_WARNINGS ON")  
    results = client.execute("SET CONCAT_NULL_YIELDS_NULL ON")  
    require 'date'  
    t = Time.now  
    curr_date = t.strftime("%Y-%m-%d %H:%M:%S.%L")  
    results = client.execute("INSERT SalesLT.Product (Name, ProductNumber, StandardCost, ListPrice, SellStartDate)  
    OUTPUT INSERTED.ProductID VALUES ('SQL Server Express New', 'SQLEXPRESS New', 0, 0, '#{curr_date}' )")  
    results.each do |row|  
    puts row  
    end  
```
