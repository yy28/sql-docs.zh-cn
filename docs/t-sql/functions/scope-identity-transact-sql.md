---
title: "SCOPE_IDENTITY (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 07/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SCOPE_IDENTITY
- SCOPE_IDENTITY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- identity columns [SQL Server], SCOPE_IDENTITY function
- SCOPE_IDENTITY function
- last-inserted identity values
- identity values [SQL Server], last-inserted
ms.assetid: eef24670-059b-4f10-91d4-a67bc1ed12ab
caps.latest.revision: 36
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1950d65a35d6fab52025d069e0338493ee7c639d
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="scopeidentity-transact-sql"></a>SCOPE_IDENTITY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  返回插入到同一作用域中的标识列内的最后一个标识值。 一个范围是一个模块：存储过程、触发器、函数或批处理。 因此，如果两个语句在相同的存储的过程、 函数或批处理中，它们就同一作用域中。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
SCOPE_IDENTITY()  
```  
  
## <a name="return-types"></a>返回类型  
 **numeric(38,0)**  
  
## <a name="remarks"></a>注释  
 SCOPE_IDENTITY，IDENT_CURRENT，和 @@IDENTITY是类似的函数，因为它们返回插入到标识列的值。  
  
 IDENT_CURRENT 不受作用域和会话的限制，而受限于指定的表。 IDENT_CURRENT 返回为任何会话和作用域中的特定表所生成的值。 有关详细信息，请参阅[IDENT_CURRENT &#40;Transact SQL &#41;](../../t-sql/functions/ident-current-transact-sql.md).  
  
 SCOPE_IDENTITY 和 @@IDENTITY返回在当前会话中生成任何表中的最后一个标识值。 但是，SCOPE_IDENTITY 返回仅在当前作用域; 中插入值@@IDENTITY并不局限于特定的作用域。  
  
 例如，有两个表 T1 和 T2，并且在 T1 上定义了 INSERT 触发器。 当将某行插入 T1 时，触发器被激发，并在 T2 中插入一行。 该方案演示了两个作用域：在 T1 上的插入，以及在 T2 通过触发器的插入。  
  
 假定 T1 和 T2 具有标识列，@IDENTITY和 SCOPE_IDENTITY 在 T1 上都返回不同的值，在 INSERT 语句的末尾。 @@IDENTITY返回在任何范围之间插入当前会话中的最后一个标识列值。 这是在 T2 中插入的值。 Scope_identity （） 返回在 T1 中插入的标识值。 这是在同一个作用域内发生的最后的插入。 如果到标识列的任何 INSERT 语句的作用域中发生之前调用此函数，scope_identity （） 函数将返回 null 值。  
  
 如果语句和事务失败，它们会更改表的当前标识，从而使标识列中的值出现不连贯现象。 即使未提交试图向表中插入值的事务，也永远无法回滚标识值。 例如，如果因 IGNORE_DUP_KEY 冲突而导致 INSERT 语句失败，表的当前标识值仍然会增加。  
  
## <a name="examples"></a>示例  
  
### <a name="a-using-identity-and-scopeidentity-with-triggers"></a>A. 使用@IDENTITY和 SCOPE_IDENTITY 具有触发器  
 下面的示例创建两个表，`TZ` 和 `TY`，并对 `TZ` 创建一个 INSERT 触发器。 当将某行插入表 `TZ` 中时，触发器 (`Ztrig`) 将激发并在 `TY` 中插入一行。  
  
```sql  
USE tempdb;  
GO  
CREATE TABLE TZ (  
   Z_id  int IDENTITY(1,1)PRIMARY KEY,  
   Z_name varchar(20) NOT NULL);  
  
INSERT TZ  
   VALUES ('Lisa'),('Mike'),('Carla');  
  
SELECT * FROM TZ;  
```     
结果集： 这是表 TZ 外观。  
  
```  
Z_id   Z_name  
-------------  
1      Lisa  
2      Mike  
3      Carla  
```  
```sql 
CREATE TABLE TY (  
   Y_id  int IDENTITY(100,5)PRIMARY KEY,  
   Y_name varchar(20) NULL);  
  
INSERT TY (Y_name)  
   VALUES ('boathouse'), ('rocks'), ('elevator');  
  
SELECT * FROM TY;  
```   
结果集： 这是 TY 外观：  
```  
Y_id  Y_name  
---------------  
100   boathouse  
105   rocks  
110   elevator  
```  

创建用于将行插入表 TY，TZ 表中插入行时的触发器。  
```sql  
CREATE TRIGGER Ztrig  
ON TZ  
FOR INSERT AS   
   BEGIN  
   INSERT TY VALUES ('')  
   END;  
```  
激发触发器，并确定哪些标识值与获取 @@IDENTITY和 SCOPE_IDENTITY 函数。   
```sql
INSERT TZ VALUES ('Rosalie');  
  
SELECT SCOPE_IDENTITY() AS [SCOPE_IDENTITY];  
GO  
SELECT @@IDENTITY AS [@@IDENTITY];  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
```
/*SCOPE_IDENTITY returns the last identity value in the same scope. This was the insert on table TZ.*/`  
SCOPE_IDENTITY  
4  

/*@@IDENTITY returns the last identity value inserted to TY by the trigger. 
  This fired because of an earlier insert on TZ.*/
@@IDENTITY  
115  
```  
  
### <a name="b-using-identity-and-scopeidentity-with-replication"></a>B. 使用@IDENTITY和 scope_identity （） 进行复制  
 下面的示例说明如何针对为合并复制发布的数据库中的插入内容使用 `@@IDENTITY` 和 `SCOPE_IDENTITY()`。 示例中的两个表都在 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 示例数据库中，其中 `Person.ContactType` 未发布，`Sales.Customer` 已发布。 合并复制将把触发器添加到已发布的表中。 因此，`@@IDENTITY` 可以从复制系统表中的插入内容而非用户表中的插入内容返回值。  
  
 `Person.ContactType`表具有最大标识值 20。 如果在该表中插入一行，`@@IDENTITY` 和 `SCOPE_IDENTITY()` 将返回相同的值。  
  
```sql  
USE AdventureWorks2012;  
GO  
INSERT INTO Person.ContactType ([Name]) VALUES ('Assistant to the Manager');  
GO  
SELECT SCOPE_IDENTITY() AS [SCOPE_IDENTITY];  
GO  
SELECT @@IDENTITY AS [@@IDENTITY];  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
```  
SCOPE_IDENTITY  
21  
@@IDENTITY  
21
```  
  
 `Sales.Customer` 表的最大标识值为 29483。 如果在该表中插入一行，`@@IDENTITY` 和 `SCOPE_IDENTITY()` 将返回不同的值。 `SCOPE_IDENTITY()` 从用户表的插入内容返回值，而 `@@IDENTITY` 从复制系统表中的插入内容返回值。 请对需要访问插入的标识值的应用程序使用 `SCOPE_IDENTITY()`。  
  
```sql  
INSERT INTO Sales.Customer ([TerritoryID],[PersonID]) VALUES (8,NULL);  
GO  
SELECT SCOPE_IDENTITY() AS [SCOPE_IDENTITY];  
GO  
SELECT @@IDENTITY AS [@@IDENTITY];  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
 ```
 SCOPE_IDENTITY  
 29484  
 @@IDENTITY  
 89
 ```  
  
## <a name="see-also"></a>另请参阅  
 [@@IDENTITY (Transact-SQL)](../../t-sql/functions/identity-transact-sql.md)  
  
  

