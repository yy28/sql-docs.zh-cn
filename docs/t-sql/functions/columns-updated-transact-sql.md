---
title: "COLUMNS_UPDATED (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- COLUMNS_UPDATED_TSQL
- COLUMNS_UPDATED
dev_langs:
- TSQL
helpviewer_keywords:
- COLUMNS_UPDATED function
- testing columns
- column testing [SQL Server]
- updated columns
ms.assetid: 765fde44-1f95-4015-80a4-45388f18a42c
caps.latest.revision: 53
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 8ddb7462ee985ee62efa70455d27c91a51193124
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="columnsupdated-transact-sql"></a>COLUMNS_UPDATED (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

返回**varbinary**指示表或视图中插入或更新了的列的位模式。 COLUMNS_UPDATED 可用于 [!INCLUDE[tsql](../../includes/tsql-md.md)] INSERT 或 UPDATE 触发器主体内部的任意位置，以测试该触发器是否应执行某些操作。
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```sql
COLUMNS_UPDATED ( )   
```  
  
## <a name="return-types"></a>返回类型
**varbinary**
  
## <a name="remarks"></a>注释  
COLUMNS_UPDATED 针对多列执行的 UPDATE 或 INSERT 操作的进行测试。 若要对其进行更新或插入一个列上尝试测试，使用[update （)](../../t-sql/functions/update-trigger-functions-transact-sql.md)。
  
COLUMNS_UPDATED 返回一个或多个从左至右排序的字节，每字节中最不重要的位位于最右侧。 最左侧字节的最右侧位表示表中的第一列；向左的下一位表示第二列，依此类推。 如果创建了触发器的表包含八列以上，则 COLUMNS_UPDATED 返回多个字节，最左侧的为最不重要的字节。 在 INSERT 操作中 COLUMNS_UPDATED 将对所有列返回 TRUE，因为这些列插入了显式值或隐式 (NULL) 值。
  
若要测试针对特定列的更新或插入操作，请遵循使用位运算符和所测试列的整数位掩码的语法。 例如，表**t1**包含列**C1**， **C2**， **C3**， **C4**，和**C5**. 若要验证该列**C2**， **C3**，和**C4**是否所有更新 (与表**t1**具有 UPDATE 触发器)，按照与语法**和 14**。 若要测试是否唯一列**C2**是更新，指定**& 2**。
  
可以在 [!INCLUDE[tsql](../../includes/tsql-md.md)] INSERT 或 UPDATE 触发器内部的任意位置使用 COLUMNS_UPDATED。
  
INFORMATION_SCHEMA.COLUMNS 视图的 ORDINAL_POSITION 列与 COLUMNS_UPDATED 所返回列的位模式不兼容。 若要获取与 COLUMNS_UPDATED 兼容的位模式，请在查询 `ColumnID` 视图时引用 `COLUMNPROPERTY` 系统函数的 `INFORMATION_SCHEMA.COLUMNS` 属性，如以下示例所示。
  
```sql
SELECT TABLE_NAME, COLUMN_NAME,  
    COLUMNPROPERTY(OBJECT_ID(TABLE_SCHEMA + '.' + TABLE_NAME),  
    COLUMN_NAME, 'ColumnID') AS COLUMN_ID  
FROM AdventureWorks2012.INFORMATION_SCHEMA.COLUMNS  
WHERE TABLE_NAME = 'Person';  
```  
  
## <a name="column-sets"></a>列集
对表定义了列集后，COLUMNS_UPDATED 函数的行为如下所述：
-   当显式更新作为列集成员的列后，该列的对应位将设置为 1，列集的对应位也将设置为 1。  
-   显式更新列集后，列集的对应位将设置为 1，该表中的所有稀疏列的对应位也将设置为 1。  
-   对于插入操作，所有位都将设置为 1。  
  
     因为对列集的更改将导致列集中所有列的位设置为 1，所以列集中没有更改的列将显示为已修改。 有关列集的详细信息，请参阅 [使用列集](../../relational-databases/tables/use-column-sets.md)。  
  
## <a name="examples"></a>示例  
  
### <a name="a-using-columnsupdated-to-test-the-first-eight-columns-of-a-table"></a>A. 使用 COLUMNS_UPDATED 测试表的前八列  
下面的示例创建两个表：`employeeData`和`auditEmployeeData`。 人力资源部的成员可以修改 `employeeData` 表，该表包含敏感的雇员薪水信息。 如果更改了雇员的社会保险号码 (SSN)、年薪或银行帐户，则生成审核记录并插入到 `auditEmployeeData` 审核表。
  
通过使用 `COLUMNS_UPDATED()`，可以快速测试对包含敏感雇员信息的列所进行的任何更改。 仅当您尝试检测对表的前八列进行的更改时，以这种方式使用 `COLUMNS_UPDATED()` 才有效。
  
```sql
USE AdventureWorks2012;  
GO  
IF EXISTS(SELECT TABLE_NAME FROM INFORMATION_SCHEMA.TABLES  
   WHERE TABLE_NAME = 'employeeData')  
   DROP TABLE employeeData;  
IF EXISTS(SELECT TABLE_NAME FROM INFORMATION_SCHEMA.TABLES  
   WHERE TABLE_NAME = 'auditEmployeeData')  
   DROP TABLE auditEmployeeData;  
GO  
CREATE TABLE dbo.employeeData (  
   emp_id int NOT NULL PRIMARY KEY,  
   emp_bankAccountNumber char (10) NOT NULL,  
   emp_salary int NOT NULL,  
   emp_SSN char (11) NOT NULL,  
   emp_lname nchar (32) NOT NULL,  
   emp_fname nchar (32) NOT NULL,  
   emp_manager int NOT NULL  
   );  
GO  
CREATE TABLE dbo.auditEmployeeData (  
   audit_log_id uniqueidentifier DEFAULT NEWID() PRIMARY KEY,  
   audit_log_type char (3) NOT NULL,  
   audit_emp_id int NOT NULL,  
   audit_emp_bankAccountNumber char (10) NULL,  
   audit_emp_salary int NULL,  
   audit_emp_SSN char (11) NULL,  
   audit_user sysname DEFAULT SUSER_SNAME(),  
   audit_changed datetime DEFAULT GETDATE()  
   );  
GO  
CREATE TRIGGER dbo.updEmployeeData   
ON dbo.employeeData   
AFTER UPDATE AS  
/*Check whether columns 2, 3 or 4 have been updated. If any or all  
columns 2, 3 or 4 have been changed, create an audit record. The
bitmask is: power(2,(2-1))+power(2,(3-1))+power(2,(4-1)) = 14. To test   
whether all columns 2, 3, and 4 are updated, use = 14 instead of >0  
(below).*/
  
   IF (COLUMNS_UPDATED() & 14) > 0  
/*Use IF (COLUMNS_UPDATED() & 14) = 14 to see whether all columns 2, 3,   
and 4 are updated.*/  
      BEGIN  
-- Audit OLD record.  
      INSERT INTO dbo.auditEmployeeData  
         (audit_log_type,  
         audit_emp_id,  
         audit_emp_bankAccountNumber,  
         audit_emp_salary,  
         audit_emp_SSN)  
         SELECT 'OLD',   
            del.emp_id,  
            del.emp_bankAccountNumber,  
            del.emp_salary,  
            del.emp_SSN  
         FROM deleted del;  
  
-- Audit NEW record.  
      INSERT INTO dbo.auditEmployeeData  
         (audit_log_type,  
         audit_emp_id,  
         audit_emp_bankAccountNumber,  
         audit_emp_salary,  
         audit_emp_SSN)  
         SELECT 'NEW',  
            ins.emp_id,  
            ins.emp_bankAccountNumber,  
            ins.emp_salary,  
            ins.emp_SSN  
         FROM inserted ins;  
   END;  
GO  
  
/*Inserting a new employee does not cause the UPDATE trigger to fire.*/  
INSERT INTO employeeData  
   VALUES ( 101, 'USA-987-01', 23000, 'R-M53550M', N'Mendel', N'Roland', 32);  
GO  
  
/*Updating the employee record for employee number 101 to change the   
salary to 51000 causes the UPDATE trigger to fire and an audit trail to   
be produced.*/  
  
UPDATE dbo.employeeData  
   SET emp_salary = 51000  
   WHERE emp_id = 101;  
GO  
SELECT * FROM auditEmployeeData;  
GO  
  
/*Updating the employee record for employee number 101 to change both   
the bank account number and social security number (SSN) causes the   
UPDATE trigger to fire and an audit trail to be produced.*/  
  
UPDATE dbo.employeeData  
   SET emp_bankAccountNumber = '133146A0', emp_SSN = 'R-M53550M'  
   WHERE emp_id = 101;  
GO  
SELECT * FROM dbo.auditEmployeeData;  
  
GO  
```  
  
### <a name="b-using-columnsupdated-to-test-more-than-eight-columns"></a>B. 使用 COLUMNS_UPDATED 测试八个以上的列  
若要对影响表中前八列以外的列的更新进行测试，请使用 `SUBSTRING` 函数测试 `COLUMNS_UPDATED` 返回的更正位。 下面的示例测试影响的字段的更新`3`， `5`，和`9`中`AdventureWorks2012.Person.Person`表。
  
```sql
USE AdventureWorks2012;  
GO  
IF OBJECT_ID (N'Person.uContact2', N'TR') IS NOT NULL  
    DROP TRIGGER Person.uContact2;  
GO  
CREATE TRIGGER Person.uContact2 ON Person.Person  
AFTER UPDATE AS  
    IF ( (SUBSTRING(COLUMNS_UPDATED(),1,1) & 20 = 20)   
        AND (SUBSTRING(COLUMNS_UPDATED(),2,1) & 1 = 1) )   
    PRINT 'Columns 3, 5 and 9 updated';  
GO  
  
UPDATE Person.Person   
   SET NameStyle = NameStyle,  
      FirstName=FirstName,  
      EmailPromotion=EmailPromotion;  
GO  
```  
  
## <a name="see-also"></a>另请参阅
[按位运算符 &#40;Transact SQL &#41;](../../t-sql/language-elements/bitwise-operators-transact-sql.md)  
[CREATE TRIGGER (Transact-SQL)](../../t-sql/statements/create-trigger-transact-sql.md)  
[更新 &#40; &#41;&#40;Transact SQL &#41;](../../t-sql/functions/update-trigger-functions-transact-sql.md)
  
  

