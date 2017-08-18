---
title: "创建、更改和删除选择性 XML 索引 | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c398f396-f630-4a2d-a264-f243c5346de1
caps.latest.revision: 8
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: cff16890d58c610a08e7bbe0d5958de2e821b0a5
ms.contentlocale: zh-cn
ms.lasthandoff: 08/18/2017

---
# <a name="create-alter-and-drop-selective-xml-indexes"></a>创建、更改和删除选择性 XML 索引
  说明如何创建新的选择性 XML 索引或者更改或删除现有的选择性 XML 索引。  
  
 有关选择性 XML 索引的详细信息，请参阅 [选择性 XML 索引 (SXI)](../../relational-databases/xml/selective-xml-indexes-sxi.md)。  
  
##  <a name="create"></a> 创建选择性 XML 索引  
  
### <a name="how-to-create-a-selective-xml-index"></a>如何创建选择性 XML 索引  
 **通过使用 Transact-SQL 创建选择性 XML 索引**  
 通过调用 CREATE SELECTIVE XML INDEX 语句创建选择性 XML 索引。 有关详细信息，请参阅 [CREATE SELECTIVE XML INDEX (Transact-SQL)](../../t-sql/statements/create-selective-xml-index-transact-sql.md)。  
  
 **示例**  
  
 下面的示例显示了创建选择性 XML 索引的语法。 它还显示了该语法的若干变化形式，以便描述使用可选的优化提示建立索引的路径。  
  
```tsql  
CREATE SELECTIVE XML INDEX sxi_index  
ON Tbl(xmlcol)  
  
FOR(  
    pathab   = '/a/b' as XQUERY 'node()'  
    pathabc  = '/a/b/c' as XQUERY 'xs:double',   
    pathdtext = '/a/b/d/text()' as XQUERY 'xs:string' MAXLENGTH(200) SINGLETON  
    pathabe = '/a/b/e' as SQL NVARCHAR(100)  
)  
```  
  
  
##  <a name="alter"></a> 更改选择性 XML 索引  
  
### <a name="how-to-alter-a-selective-xml-index"></a>如何更改选择性 XML 索引  
 **通过使用 Transact-SQL 更改选择性 XML 索引**  
 通过调用 ALTER INDEX 语句更改现有的选择性 XML 索引。 有关详细信息，请参阅 [ALTER INDEX（选择性 XML 索引）](../../t-sql/statements/alter-index-selective-xml-indexes.md)。  
  
 **示例**  
  
 下面的示例说明 ALTER INDEX 语句。 该语句将路径 `'/a/b/m'` 添加到索引的 XQuery 部分，并且从在 [CREATE SELECTIVE XML INDEX (Transact-SQL)](../../t-sql/statements/create-selective-xml-index-transact-sql.md) 主题的示例中创建的索引的 SQL 部分删除路径 `'/a/b/e'`。 要删除的路径由在创建时提供给它的名称标识。  
  
```tsql  
ALTER INDEX sxi_index  
ON Tbl  
FOR   
(  
    ADD pathm = '/a/b/m' as XQUERY 'node()' ,  
    REMOVE pathabe  
)  
```  
  
  
##  <a name="drop"></a> 删除选择性 XML 索引  
  
### <a name="how-to-drop-a-selective-xml-index"></a>如何删除选择性 XML 索引  
 **通过使用 Transact-SQL 删除选择性 XML 索引**  
 通过调用 DROP INDEX 语句删除选择性 XML 索引。 有关详细信息，请参阅 [DROP INDEX（选择性 XML 索引）](../../t-sql/statements/drop-index-selective-xml-indexes.md)。  
  
 **示例**  
  
 下面的示例说明 DROP INDEX 语句。  
  
```tsql  
DROP INDEX sxi_index ON tbl  
```  
  
  
  
