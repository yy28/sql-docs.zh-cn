---
title: "对 XML 列创建视图 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-xml"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "视图 [SQL Server 中的 XML]"
ms.assetid: eb5f0439-1f69-49c2-8759-e59bda1633b7
caps.latest.revision: 14
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 14
---
# 对 XML 列创建视图
  可以使用 **xml** 类型列创建视图。 下面的示例创建了一个视图，在该视图中，使用 **xml** 数据类型的 **value()** 方法检索 `xml` 类型列中的值。  
  
```  
-- Create the table.  
CREATE TABLE T (  
    ProductID          int primary key,   
    CatalogDescription xml)  
GO  
-- Insert sample data.  
INSERT INTO T values(1,'<ProductDescription ProductID="1" ProductName="SomeName" />')  
GO  
-- Create view (note the value() method used to retrieve ProductName   
-- attribute value from the XML).  
CREATE VIEW MyView AS   
  SELECT ProductID,  
         CatalogDescription.value('(/ProductDescription/@ProductName)[1]', 'varchar(40)') AS PName  
  FROM T  
GO   
```  
  
 对此视图执行下面的查询：  
  
```  
SELECT *   
FROM   MyView  
```  
  
 结果如下：  
  
```  
ProductID   PName        
----------- ------------  
1           SomeName   
```  
  
 关于使用 **xml** 数据类型创建视图，请注意以下几点：  
  
-   可以在具体化视图中创建 xml 数据类型。 具体化视图不能基于 xml 数据类型方法。 但是，它可以转换为不同于基表中的 xml 类型列的 XML 架构集合。  
  
-   不能将 **xml** 数据类型用于分布式分区视图。  
  
-   不会将对视图运行的 SQL 谓词推送到相应视图定义的 XQuery 中。  
  
-   视图中的 XML 数据类型方法不可更新。  
  
  