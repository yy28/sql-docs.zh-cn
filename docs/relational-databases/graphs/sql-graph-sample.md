---
title: SQL 图形数据库示例 |Microsoft Docs
description: 一个快速示例，将帮助你开始使用 SQL 图形数据库中引入的新语法。
ms.date: 04/19/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.custom: ''
ms.technology: ''
ms.topic: language-reference
helpviewer_keywords:
- SQL graph
- SQL graph, tsql reference
ms.assetid: ''
author: shkale-msft
ms.author: shkale
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 1737ae8427df8d6d9bd6dbb9dea359da09f0c657
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68035876"
---
# <a name="create-a-graph-database-and-run-some-pattern-matching-queries-using-t-sql"></a>创建图形数据库并运行一些模式匹配使用 T-SQL 查询

[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

此示例提供了[!INCLUDE[tsql-md](../../includes/tsql-md.md)]脚本使用的节点和边缘创建图形数据库，然后使用新的 MATCH 子句匹配的一些模式，并遍历关系图。 此示例脚本将用于这两个 Azure SQL 数据库和 [!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)]  

## <a name="sample-schema"></a>示例架构

此示例创建关系图架构，正如图 1 中所演示的假设的社交网络的人员、 餐馆和市/县的节点。 这些节点连接到使用朋友、 点赞、 LivesIn 和 LocatedIn 边缘。

![人员城市餐馆表](../../relational-databases/graphs/media/person-cities-restaurants-tables.png "Sql 图形数据库示例")  
图 1:示例架构包含餐馆、 城市、 人员节点和 LivesIn，LocatedIn，点赞边缘。

## <a name="sample-script"></a>示例脚本

```
-- Create a graph demo database
CREATE DATABASE graphdemo;
go

USE  graphdemo;
go

-- Create NODE tables
CREATE TABLE Person (
  ID INTEGER PRIMARY KEY,
  name VARCHAR(100)
) AS NODE;

CREATE TABLE Restaurant (
  ID INTEGER NOT NULL,
  name VARCHAR(100),
  city VARCHAR(100)
) AS NODE;

CREATE TABLE City (
  ID INTEGER PRIMARY KEY,
  name VARCHAR(100),
  stateName VARCHAR(100)
) AS NODE;

-- Create EDGE tables. 
CREATE TABLE likes (rating INTEGER) AS EDGE;
CREATE TABLE friendOf AS EDGE;
CREATE TABLE livesIn AS EDGE;
CREATE TABLE locatedIn AS EDGE;

-- Insert data into node tables. Inserting into a node table is same as inserting into a regular table
INSERT INTO Person VALUES (1,'John');
INSERT INTO Person VALUES (2,'Mary');
INSERT INTO Person VALUES (3,'Alice');
INSERT INTO Person VALUES (4,'Jacob');
INSERT INTO Person VALUES (5,'Julie');

INSERT INTO Restaurant VALUES (1,'Taco Dell','Bellevue');
INSERT INTO Restaurant VALUES (2,'Ginger and Spice','Seattle');
INSERT INTO Restaurant VALUES (3,'Noodle Land', 'Redmond');

INSERT INTO City VALUES (1,'Bellevue','wa');
INSERT INTO City VALUES (2,'Seattle','wa');
INSERT INTO City VALUES (3,'Redmond','wa');

-- Insert into edge table. While inserting into an edge table,
-- you need to provide the $node_id from $from_id and $to_id columns.
INSERT INTO likes VALUES ((SELECT $node_id FROM Person WHERE ID = 1), 
       (SELECT $node_id FROM Restaurant WHERE ID = 1),9);
INSERT INTO likes VALUES ((SELECT $node_id FROM Person WHERE ID = 2), 
      (SELECT $node_id FROM Restaurant WHERE ID = 2),9);
INSERT INTO likes VALUES ((SELECT $node_id FROM Person WHERE ID = 3), 
      (SELECT $node_id FROM Restaurant WHERE ID = 3),9);
INSERT INTO likes VALUES ((SELECT $node_id FROM Person WHERE ID = 4), 
      (SELECT $node_id FROM Restaurant WHERE ID = 3),9);
INSERT INTO likes VALUES ((SELECT $node_id FROM Person WHERE ID = 5), 
      (SELECT $node_id FROM Restaurant WHERE ID = 3),9);

INSERT INTO livesIn VALUES ((SELECT $node_id FROM Person WHERE ID = 1),
      (SELECT $node_id FROM City WHERE ID = 1));
INSERT INTO livesIn VALUES ((SELECT $node_id FROM Person WHERE ID = 2),
      (SELECT $node_id FROM City WHERE ID = 2));
INSERT INTO livesIn VALUES ((SELECT $node_id FROM Person WHERE ID = 3),
      (SELECT $node_id FROM City WHERE ID = 3));
INSERT INTO livesIn VALUES ((SELECT $node_id FROM Person WHERE ID = 4),
      (SELECT $node_id FROM City WHERE ID = 3));
INSERT INTO livesIn VALUES ((SELECT $node_id FROM Person WHERE ID = 5),
      (SELECT $node_id FROM City WHERE ID = 1));

INSERT INTO locatedIn VALUES ((SELECT $node_id FROM Restaurant WHERE ID = 1),
      (SELECT $node_id FROM City WHERE ID =1));
INSERT INTO locatedIn VALUES ((SELECT $node_id FROM Restaurant WHERE ID = 2),
      (SELECT $node_id FROM City WHERE ID =2));
INSERT INTO locatedIn VALUES ((SELECT $node_id FROM Restaurant WHERE ID = 3),
      (SELECT $node_id FROM City WHERE ID =3));

-- Insert data into the friendOf edge.
INSERT INTO friendOf VALUES ((SELECT $NODE_ID FROM Person WHERE ID = 1), (SELECT $NODE_ID FROM Person WHERE ID = 2));
INSERT INTO friendOf VALUES ((SELECT $NODE_ID FROM Person WHERE ID = 2), (SELECT $NODE_ID FROM Person WHERE ID = 3));
INSERT INTO friendOf VALUES ((SELECT $NODE_ID FROM Person WHERE ID = 3), (SELECT $NODE_ID FROM Person WHERE ID = 1));
INSERT INTO friendOf VALUES ((SELECT $NODE_ID FROM Person WHERE ID = 4), (SELECT $NODE_ID FROM Person WHERE ID = 2));
INSERT INTO friendOf VALUES ((SELECT $NODE_ID FROM Person WHERE ID = 5), (SELECT $NODE_ID FROM Person WHERE ID = 4));


-- Find Restaurants that John likes
SELECT Restaurant.name
FROM Person, likes, Restaurant
WHERE MATCH (Person-(likes)->Restaurant)
AND Person.name = 'John';

-- Find Restaurants that John's friends like
SELECT Restaurant.name 
FROM Person person1, Person person2, likes, friendOf, Restaurant
WHERE MATCH(person1-(friendOf)->person2-(likes)->Restaurant)
AND person1.name='John';

-- Find people who like a restaurant in the same city they live in
SELECT Person.name
FROM Person, likes, Restaurant, livesIn, City, locatedIn
WHERE MATCH (Person-(likes)->Restaurant-(locatedIn)->City AND Person-(livesIn)->City);
```

## <a name="clean-up"></a>清理  
清理的架构和创建示例数据库。

```
USE graphdemo;
go

DROP TABLE IF EXISTS likes;
DROP TABLE IF EXISTS Person;
DROP TABLE IF EXISTS Restaurant;
DROP TABLE IF EXISTS City;
DROP TABLE IF EXISTS friendOf;
DROP TABLE IF EXISTS livesIn;
DROP TABLE IF EXISTS locatedIn;

USE master;
go
DROP DATABASE graphdemo;
go
```

## <a name="script-explanation"></a>脚本说明  
此脚本使用新的 T-SQL 语法创建节点和边界表。 演示如何将数据插入到使用的节点和边缘表`INSERT`语句，并还演示如何使用`MATCH`子句用于模式匹配和导航。

|Command    |说明
|---  |---  |
|[CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-sql-graph.md)  |创建图形节点或边界表  |
|[INSERT (Transact-SQL)](../../t-sql/statements/insert-sql-graph.md)  |插入节点或边界表  |
|[MATCH &#40;Transact-SQL&#41;](../../t-sql/queries/match-sql-graph.md)  |使用匹配来匹配模式或遍历关系图  |
