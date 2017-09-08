---
title: "标识 （函数） (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
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
- IDENTITY function
- SELECT statement [SQL Server], IDENTITY function
- inserting identity columns
- columns [SQL Server], creating
- identity columns [SQL Server], IDENTITY function
ms.assetid: ebec77eb-fc02-4feb-b6c5-f0098d43ccb6
caps.latest.revision: 23
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 43d42425842def7572cf7961a89cae355e6b78ae
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="identity-function-transact-sql"></a>IDENTITY（函数）(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  仅在带有 INTO 的 SELECT 语句中使用*表*子句将标识列插入新表。 尽管类似，但是 IDENTITY 函数不是与 CREATE TABLE 和 ALTER TABLE 一起使用的 IDENTITY 属性。  
  
> [!NOTE]  
>  要创建一个可在多个表中使用的自动递增数字或者可以从应用程序中调用而不引用任何表的自动递增数字，请参阅[序列号](../../relational-databases/sequence-numbers/sequence-numbers.md)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
IDENTITY (data_type [ , seed , increment ] ) AS column_name  
```  
  
## <a name="arguments"></a>参数  
 *data_type*  
 标识列的数据类型。 有效的数据类型对于标识列的整数数据类型类别中，任何数据类型除外**位**数据类型，或**十进制**数据类型。  
  
 *种子*  
 要分配给表中第一行的整数值。 每个后续行分配的下一步的标识值，其值等于最后一个标识值加上*递增*值。 如果既没有*种子*也不*递增*指定，均默认为 1。  
  
 *增量*  
 是的整数值将添加到*种子*表中的连续行的值。  
  
 *column_name*  
 将插入到新表中的列的名称。  
  
## <a name="return-types"></a>返回类型  
 返回与相同*data_type*。  
  
## <a name="remarks"></a>注释  
 因为该函数在表中创建一个列，所以必须用下列方式中的一种在选择列表中指定该列的名称：  
  
```  
--(1)  
SELECT IDENTITY(int, 1,1) AS ID_Num  
INTO NewTable  
FROM OldTable;  
  
--(2)  
SELECT ID_Num = IDENTITY(int, 1, 1)  
INTO NewTable  
FROM OldTable;  
  
```  
  
## <a name="examples"></a>示例  
 下面的示例将来自 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 数据库的 `Contact` 表的所有行都插入到名为 `NewContact` 的新表。 使用 IDENTITY 函数在 `NewContact` 表中从 100 而不是 1 开始编标识号。  
  
```  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID (N'Person.NewContact', N'U') IS NOT NULL  
    DROP TABLE Person.NewContact;  
GO  
ALTER DATABASE AdventureWorks2012 SET RECOVERY BULK_LOGGED;  
GO  
SELECT  IDENTITY(smallint, 100, 1) AS ContactNum,  
        FirstName AS First,  
        LastName AS Last  
INTO Person.NewContact  
FROM Person.Person;  
GO  
ALTER DATABASE AdventureWorks2012 SET RECOVERY FULL;  
GO  
SELECT ContactNum, First, Last FROM Person.NewContact;  
GO  
  
```  
  
## <a name="see-also"></a>另请参阅  
 [CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md)   
 [@@IDENTITY (Transact-SQL)](../../t-sql/functions/identity-transact-sql.md)   
 [IDENTITY（属性）&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql-identity-property.md)   
 [选择@local_variable&#40;Transact SQL &#41;](../../t-sql/language-elements/select-local-variable-transact-sql.md)   
 [DBCC CHECKIDENT &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkident-transact-sql.md)   
 [sys.identity_columns &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-identity-columns-transact-sql.md)  
  
  
