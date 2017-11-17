---
title: "OPENQUERY (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- OPENQUERY_TSQL
- OPENQUERY
dev_langs:
- TSQL
helpviewer_keywords:
- DELETE statement [SQL Server], OPENQUERY function
- OPENQUERY function
- FROM clause, OPENQUERY function
- UPDATE statement [SQL Server], OPENQUERY function
- pass-through queries [SQL Server]
- INSERT statement [SQL Server], OPENQUERY function
ms.assetid: b805e976-f025-4be1-bcb0-3a57b0c57717
caps.latest.revision: 42
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 834bba08c90262fd72881ab2890abaaf7b8f7678
ms.openlocfilehash: 2a3ad57f9cd898d4c059df725b380be28622035e
ms.contentlocale: zh-cn
ms.lasthandoff: 10/02/2017

---
# <a name="openquery-transact-sql"></a>OPENQUERY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  在指定的链接服务器上执行指定的传递查询。 该服务器是 OLE DB 数据源。 OPENQUERY 可以在查询的 FROM 子句中引用，就好象它是一个表名。 OPENQUERY 也可以作为 INSERT、UPDATE 或 DELETE 语句的目标表进行引用。 但这要取决于 OLE DB 访问接口的功能。 尽管查询可能返回多个结果集，但是 OPENQUERY 只返回第一个。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
OPENQUERY ( linked_server ,'query' )  
```  
  
## <a name="arguments"></a>参数  
 *linked_server*  
 表示链接服务器名称的标识符。  
  
  *查询*   
 在链接服务器中执行的查询字符串。 该字符串的最大长度为 8 KB。  
  
## <a name="remarks"></a>注释  
 OPENQUERY 不接受其参数的变量。  
  
 OPENQUERY 不能用于对链接服务器执行扩展存储过程。 但是，通过使用四部分名称，可以在链接服务器上执行扩展存储过程。 例如：  
  
```t-sql  
EXEC SeattleSales.master.dbo.xp_msver  
```  
  
 FROM 子句中对 OPENDATASOURCE、OPENQUERY 或 OPENROWSET 的任何调用与对用作更新目标的这些函数的任何调用都是分开独立计算的，即使为两个调用提供的参数相同也是如此。 具体而言，应用到上述任一调用的结果的筛选器或联接条件不会影响其他调用的结果。  
  
## <a name="permissions"></a>Permissions  
 任何用户都可以执行 OPENQUERY。 用于连接到远程服务器的权限是从为链接服务器定义的设置中获取的。  
  
## <a name="examples"></a>示例  
  
### <a name="a-executing-an-update-pass-through-query"></a>A. 执行 UPDATE 传递查询  
 以下示例针对示例 A 中创建的链接服务器使用 `UPDATE` 传递查询。  
  
```t-sql  
UPDATE OPENQUERY (OracleSvr, 'SELECT name FROM joe.titles WHERE id = 101')   
SET name = 'ADifferentName';  
```  
  
### <a name="b-executing-an-insert-pass-through-query"></a>B. 执行 INSERT 传递查询  
 以下示例针对示例 A 中创建的链接服务器使用 `INSERT` 传递查询。  
  
```t-sql  
INSERT OPENQUERY (OracleSvr, 'SELECT name FROM joe.titles')  
VALUES ('NewTitle');  
```  
  
### <a name="c-executing-a-delete-pass-through-query"></a>C. 执行 DELETE 传递查询  
 以下示例使用 `DELETE` 传递查询删除示例 C 中插入的行。  
  
```t-sql  
DELETE OPENQUERY (OracleSvr, 'SELECT name FROM joe.titles WHERE name = ''NewTitle''');  
```  
  
### <a name="d-executing-a-select-pass-through-query"></a>D. 执行 SELECT 传递查询  
 下面的示例使用传递`SELECT`查询，以便选择示例 C.中插入的行  
  
```t-sql  
SELECT * FROM OPENQUERY (OracleSvr, 'SELECT name FROM joe.titles WHERE name = ''NewTitle''');  
```  
    
## <a name="see-also"></a>另请参阅  
 [DELETE (Transact-SQL)](../../t-sql/statements/delete-transact-sql.md)   
 [FROM (Transact-SQL)](../../t-sql/queries/from-transact-sql.md)   
 [INSERT (Transact-SQL)](../../t-sql/statements/insert-transact-sql.md)   
 [OPENDATASOURCE (Transact-SQL)](../../t-sql/functions/opendatasource-transact-sql.md)   
 [OPENROWSET (Transact-SQL)](../../t-sql/functions/openrowset-transact-sql.md)   
 [行集函数 &#40;Transact SQL &#41;](../../t-sql/functions/rowset-functions-transact-sql.md)   
 [SELECT (Transact-SQL)](../../t-sql/queries/select-transact-sql.md)   
 [sp_addlinkedserver (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)   
 [sp_serveroption &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-serveroption-transact-sql.md)   
 [UPDATE (Transact-SQL)](../../t-sql/queries/update-transact-sql.md)   
 [其中 &#40;Transact SQL &#41;](../../t-sql/queries/where-transact-sql.md)  
  
  

