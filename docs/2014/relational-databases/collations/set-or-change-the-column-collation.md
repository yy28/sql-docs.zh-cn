---
title: 设置或更改列排序规则 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- tempdb database [SQL Server], collations
- collations [SQL Server], column
ms.assetid: d7a9638b-717c-4680-9b98-8849081e08be
caps.latest.revision: 29
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 3de84f26e894f00760a45d5e65769c0db8d4b009
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36014793"
---
# <a name="set-or-change-the-column-collation"></a>设置或更改列排序规则
  您可以重写的数据库排序规则`char`， `varchar`， `text`， `nchar`， `nvarchar`，和`ntext`数据通过指定表的特定列不同的排序规则并使用以下项之一：  
  
-   [CREATE TABLE](/sql/t-sql/statements/create-table-transact-sql) 和 [ALTER TABLE](/sql/t-sql/statements/alter-table-transact-sql)的 COLLATE 子句。 例如：  
  
    ```  
    CREATE TABLE dbo.MyTable  
      (PrimaryKey   int PRIMARY KEY,  
       CharCol      varchar(10) COLLATE French_CI_AS NOT NULL  
      );  
    GO  
    ALTER TABLE dbo.MyTable ALTER COLUMN CharCol  
                varchar(10)COLLATE Latin1_General_CI_AS NOT NULL;  
    GO  
    ```  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]的 COLLATE 子句。 有关详细信息，请参阅 [Collation and Unicode Support](collation-and-unicode-support.md)。  
  
-   使用`Column.Collation`中的属性[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]管理对象 (SMO)。  
  
 如果下列其中之一当前正在引用一个列，则无法更改该列的排序规则。  
  
-   计算列  
  
-   索引  
  
-   自动生成或由 CREATE STATISTICS 语句生成的分发统计信息  
  
-   CHECK 约束  
  
-   FOREIGN KEY 约束  
  
 使用 **tempdb**时， [COLLATE](/sql/t-sql/statements/collations) 子句包括了 *database_default* 选项，以此来指定对于该连接，临时表中的列使用当前用户数据库的默认排序规则而非 **tempdb**的排序规则。  
  
## <a name="collations-and-text-columns"></a>排序规则和文本列  
 您可以插入或更新中的值`text`列的排序规则是不同于数据库的默认排序规则代码页。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 会隐式地将这些值转换为该列的排序规则。  
  
## <a name="collations-and-tempdb"></a>排序规则和 tempdb  
 每次启动 **时，都会创建** tempdb [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库。该数据库与 **model** 数据库具有相同的默认排序规则。 这通常与实例的默认排序规则相同。 如果为创建的用户数据库指定的默认排序规则与 **model**的排序规则不同，则该用户数据库与 **tempdb**的默认排序规则也不同。 所有临时存储过程或临时表都创建和存储在 **tempdb**中。 这意味着临时表中的所有隐式列以及临时存储过程中的所有强制默认常量、变量和参数都具有与可比较对象（在永久表和存储过程中创建）不同的排序规则。  
  
 这将导致用户定义的数据库和系统数据库对象之间的排序规则出现互相不匹配的问题。 例如， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例使用 Latin1_General_CS_AS 排序规则，而您执行以下语句：  
  
```  
CREATE DATABASE TestDB COLLATE Estonian_CS_AS;  
USE TestDB;  
CREATE TABLE TestPermTab (PrimaryKey int PRIMARY KEY, Col1 nchar );  
```  
  
 在此系统中， **tempdb** 数据库使用代码页 1252 的 Latin1_General_CS_AS 排序规则， `TestDB` 和 `TestPermTab.Col1` 使用代码页 1257 的 `Estonian_CS_AS` 排序规则。 例如：  
  
```  
USE TestDB;  
GO  
-- Create a temporary table with the same column declarations  
-- as TestPermTab  
CREATE TABLE #TestTempTab (PrimaryKey int PRIMARY KEY, Col1 nchar );  
INSERT INTO #TestTempTab  
         SELECT * FROM TestPermTab;  
GO  
```  
  
 在上述示例中， **tempdb** 数据库使用 Latin1_General_CS_AS 排序规则， `TestDB` 和 `TestTab.Col1` 使用 `Estonian_CS_AS` 排序规则。 例如：  
  
```  
SELECT * FROM TestPermTab AS a INNER JOIN #TestTempTab on a.Col1 = #TestTempTab.Col1;  
```  
  
 由于 **tempdb** 使用默认的服务器排序规则，而 `TestPermTab.Col1` 使用其他排序规则，因此 SQL Server 会返回如下错误：“无法解决等于运算中 'Latin1_General_CI_AS_KS_WS' 与 'Estonian_CS_AS' 之间的排序规则冲突。”  
  
 为防止出现此错误，可以使用下列方法之一：  
  
-   指定临时表列使用用户数据库（而不是 **tempdb**）的默认排序规则。 如果系统需要，这可以使临时表在多个数据库中使用具有类似格式的表。  
  
    ```  
    CREATE TABLE #TestTempTab  
       (PrimaryKey int PRIMARY KEY,  
        Col1 nchar COLLATE database_default  
       );  
    ```  
  
-   为 `#TestTempTab` 列指定正确的排序规则：  
  
    ```  
    CREATE TABLE #TestTempTab  
       (PrimaryKey int PRIMARY KEY,  
        Col1 nchar COLLATE Estonian_CS_AS  
       );  
    ```  
  
## <a name="see-also"></a>请参阅  
 [设置或更改服务器排序规则](set-or-change-the-server-collation.md)   
 [设置或更改数据库排序规则](set-or-change-the-database-collation.md)   
 [Collation and Unicode Support](collation-and-unicode-support.md)  
  
  
