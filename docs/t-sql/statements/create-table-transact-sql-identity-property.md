---
title: "IDENTITY （属性） (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- IDENTITY_TSQL
- IDENTITY
dev_langs:
- TSQL
helpviewer_keywords:
- IDENTITY property
- columns [SQL Server], creating
- identity columns [SQL Server], IDENTITY property
- autonumbers, identity numbers
ms.assetid: 8429134f-c821-4033-a07c-f782a48d501c
caps.latest.revision: 27
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1eb7f960210ec89a66f1307d8476e6d47494861f
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="create-table-transact-sql-identity-property"></a>创建表 (Transact SQL) IDENTITY （属性）
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-xxx-md.md](../../includes/tsql-appliesto-ss2008-asdb-asdw-xxx-md.md)]

  在表中创建一个标识列。 此属性与 CREATE TABLE 和 ALTER TABLE [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句一起使用。  
  
> [!NOTE]  
>  标识属性是不同于 SQL-DMO**标识**公开某一列的行标识属性的属性。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
IDENTITY [ (seed , increment) ]  
```  
  
## <a name="arguments"></a>参数  
 *种子*  
 加载到表中的第一个行所使用的值。  
  
 *增量*  
 与前一个加载的行的标识值相加的增量值。  
  
 必须同时指定种子和增量，或者二者都不指定。 如果二者都未指定，则取默认值 (1,1)。  
  
## <a name="remarks"></a>注释  
 标识列可用于生成键值。 列上的标识属性确保：  
  
-   每个新值都基于当前种子和增量而生成。  
  
-   特定事务的每个新值不同于表上的其他并发事务的新值。  
  
 列上的标识属性不确保：  
  
-   **值的唯一性**– 必须使用强制唯一性**主键**或**UNIQUE**约束或**UNIQUE**索引。  
  
-   **在事务中的连续值**– 不能保证事务插入多行获得行的连续值，因为其他并发插入可能发生在表上。 如果值必须是连续，则事务应该对表使用的排他锁，或使用**SERIALIZABLE**隔离级别。  
  
-   **之后重新启动服务器或其他故障导致的连续值**–[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]可能缓存标识值，出于性能原因，并可能在数据库故障或服务器重新启动期间丢失某些分配的值。 这可能导致在插入时标识值之间有间隔。 如果不允许有间隔，应用程序应使用自己的机制来生成键值。 使用与序列生成器**NOCACHE**选项可以限制事务永远不会提交的缺口。  
  
-   **重用值**-具有特定种子/递增，标识值不会重新使用引擎的给定的标识属性。 如果特定 insert 语句失败或回滚该 insert 语句，则使用的标识值会丢失，且不会重新生成。 这可能导致在生成后续标识值时引入间隔。  
  
 这些限制是为了提升性能而在设计中加入的，而且在大多数情形下是可接受的。 如果您因为这些限制而不能使用标识值，则可以创建一个包含当前值的独立表，并使用您的应用程序管理对该表的访问和数字分配。  
  
 如果发布了包含标识列的表以进行复制，则必须使用与所用复制类型对应的方式来管理标识列。 有关详细信息，请参阅[复制标识列](../../relational-databases/replication/publish/replicate-identity-columns.md)。  
  
 每个表只能创建一个标识列。  
  
 在内存优化表中，种子和增量必须分别设置为 1、1。 设置种子或增量为 1 会导致以下错误以外的值： 使用种子和增量值其他不是内存优化表不支持 1。  
  
## <a name="examples"></a>示例  
  
### <a name="a-using-the-identity-property-with-create-table"></a>A. 将 IDENTITY 属性与 CREATE TABLE 一起使用  
 以下示例将创建一个新表，该表使用 `IDENTITY` 属性来生成自动递增的标识号。  
  
```  
USE AdventureWorks2012;  
  
IF OBJECT_ID ('dbo.new_employees', 'U') IS NOT NULL  
   DROP TABLE new_employees;  
GO  
CREATE TABLE new_employees  
(  
 id_num int IDENTITY(1,1),  
 fname varchar (20),  
 minit char(1),  
 lname varchar(30)  
);  
  
INSERT new_employees  
   (fname, minit, lname)  
VALUES  
   ('Karin', 'F', 'Josephs');  
  
INSERT new_employees  
   (fname, minit, lname)  
VALUES  
   ('Pirkko', 'O', 'Koskitalo');  
```  
  
### <a name="b-using-generic-syntax-for-finding-gaps-in-identity-values"></a>B. 使用常规语法查找标识值之间的间隔  
 以下示例显示了删除了数据时，用于在标识值中查找间隔的常规语法。  
  
> [!NOTE]  
>  以下 [!INCLUDE[tsql](../../includes/tsql-md.md)] 脚本的第一部分仅供阐释之用。 您可以运行以下面的注释开头的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 脚本：`-- Create the img table`  
  
```  
-- Here is the generic syntax for finding identity value gaps in data.  
-- The illustrative example starts here.  
SET IDENTITY_INSERT tablename ON;  
DECLARE @minidentval column_type;  
DECLARE @maxidentval column_type;  
DECLARE @nextidentval column_type;  
SELECT @minidentval = MIN($IDENTITY), @maxidentval = MAX($IDENTITY)  
    FROM tablename  
IF @minidentval = IDENT_SEED('tablename')  
   SELECT @nextidentval = MIN($IDENTITY) + IDENT_INCR('tablename')  
   FROM tablename t1  
   WHERE $IDENTITY BETWEEN IDENT_SEED('tablename') AND   
      @maxidentval AND  
      NOT EXISTS (SELECT * FROM tablename t2  
         WHERE t2.$IDENTITY = t1.$IDENTITY +   
            IDENT_INCR('tablename'))  
ELSE  
   SELECT @nextidentval = IDENT_SEED('tablename');  
SET IDENTITY_INSERT tablename OFF;  
-- Here is an example to find gaps in the actual data.  
-- The table is called img and has two columns: the first column   
-- called id_num, which is an increasing identification number, and the   
-- second column called company_name.  
-- This is the end of the illustration example.  
  
-- Create the img table.  
-- If the img table already exists, drop it.  
-- Create the img table.  
IF OBJECT_ID ('dbo.img', 'U') IS NOT NULL  
   DROP TABLE img;  
GO  
CREATE TABLE img (id_num int IDENTITY(1,1), company_name sysname);  
INSERT img(company_name) VALUES ('New Moon Books');  
INSERT img(company_name) VALUES ('Lucerne Publishing');  
-- SET IDENTITY_INSERT ON and use in img table.  
SET IDENTITY_INSERT img ON;  
  
DECLARE @minidentval smallint;  
DECLARE @nextidentval smallint;  
SELECT @minidentval = MIN($IDENTITY) FROM img  
 IF @minidentval = IDENT_SEED('img')  
    SELECT @nextidentval = MIN($IDENTITY) + IDENT_INCR('img')  
    FROM img t1  
    WHERE $IDENTITY BETWEEN IDENT_SEED('img') AND 32766 AND  
      NOT    EXISTS (SELECT * FROM img t2  
          WHERE t2.$IDENTITY = t1.$IDENTITY + IDENT_INCR('img'))  
 ELSE  
    SELECT @nextidentval = IDENT_SEED('img');  
SET IDENTITY_INSERT img OFF;  
```  
  
## <a name="see-also"></a>另请参阅  
 [ALTER TABLE (Transact-SQL)](../../t-sql/statements/alter-table-transact-sql.md)   
 [CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md)   
 [DBCC CHECKIDENT &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkident-transact-sql.md)   
 [Ident_incr 和 &#40;Transact SQL &#41;](../../t-sql/functions/ident-incr-transact-sql.md)   
 [@@IDENTITY (Transact-SQL)](../../t-sql/functions/identity-transact-sql.md)   
 [标识 &#40;函数 &#41;&#40;Transact SQL &#41;](../../t-sql/functions/identity-function-transact-sql.md)   
 [IDENT_SEED &#40;Transact SQL &#41;](../../t-sql/functions/ident-seed-transact-sql.md)   
 [SELECT (Transact-SQL)](../../t-sql/queries/select-transact-sql.md)   
 [设置 IDENTITY_INSERT &#40;Transact SQL &#41;](../../t-sql/statements/set-identity-insert-transact-sql.md)   
 [复制标识列](../../relational-databases/replication/publish/replicate-identity-columns.md)  
  
  
