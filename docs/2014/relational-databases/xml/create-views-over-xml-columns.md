---
title: 基于 XML 列创建视图 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- views [XML in SQL Server]
ms.assetid: eb5f0439-1f69-49c2-8759-e59bda1633b7
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 767844d7b195ece286b8f19cc34855bf50185a0c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48049827"
---
# <a name="create-views-over-xml-columns"></a>对 XML 列创建视图
  可以使用`xml`类型列创建视图。 以下示例在其中创建一个视图中的值`xml`类型列使用检索`value()`方法的`xml`数据类型。  
  
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
  
 请注意以下几点有关使用`xml`数据类型创建视图：  
  
-   可以在具体化视图中创建 xml 数据类型。 具体化视图不能基于 xml 数据类型方法。 但是，它可以转换为不同于基表中的 xml 类型列的 XML 架构集合。  
  
-   `xml`数据类型不能使用分布式分区视图。  
  
-   不会将对视图运行的 SQL 谓词推送到相应视图定义的 XQuery 中。  
  
-   视图中的 XML 数据类型方法不可更新。  
  
  
