---
title: "正斜杠星型 （块注释） (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 07/27/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- /*...*/_TSQL
- Comment
- /*...*/
dev_langs: TSQL
helpviewer_keywords:
- nonexecuting text strings [SQL Server]
- /*...*/ (comment)
- remarks [SQL Server]
- comments [SQL Server]
ms.assetid: 4d9ab1b2-4bbb-4c16-beb1-cafc1af7417c
caps.latest.revision: "30"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: b82dd750c41038c6e526b4f3c3db2583198a0091
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/19/2018
---
# <a name="slash-star-block-comment-transact-sql"></a>正斜杠星型 （块注释） (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]


  表示用户提供的文本。 之间的文本 / * 和\*/ 服务器不计。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
/*  
text_of_comment  
*/  
```  
  
## <a name="arguments"></a>参数  
 *text_of_comment*  
 是注释的文本。 它是一个或多个字符串。  
  
## <a name="remarks"></a>注释  
 注释可以插入单独行中，也可以插入 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句中。 必须由指示多行注释 / * 和\*/。 多行的注释，通常使用的样式规则是开始使用的第一行 /\*，因为在后续行用\* \*，且以结尾\*/。  
  
 注释没有最大长度限制。  
  
 支持嵌套注释。 如果 / * 在现有的注释中的任何位置发生字符模式，它将被视为嵌套注释的开始和，因此，需要右\*/ 注释标记。 如果没有注释的结尾标记，便会生成错误。  
  
 例如，以下代码生成一个错误。  
  
```  
DECLARE @comment AS varchar(20);  
GO  
/*  
SELECT @comment = '/*';  
*/   
SELECT @@VERSION;  
GO   
```  
  
 若要解决该错误，请执行以下更改。  
  
```  
DECLARE @comment AS varchar(20);  
GO  
/*  
SELECT @comment = '/*';  
*/ */  
SELECT @@VERSION;  
GO  
  
```  
  
## <a name="examples"></a>示例  
 以下示例使用注释解释将要执行哪个代码段。  
  
```  
USE AdventureWorks2012;  
GO  
/*  
This section of the code joins the Person table with the Address table,   
by using the Employee and BusinessEntityAddress tables in the middle to   
get a list of all the employees in the AdventureWorks2012 database   
and their contact information.  
*/  
SELECT p.FirstName, p.LastName, a.AddressLine1, a.AddressLine2, a.City, a.PostalCode  
FROM Person.Person AS p  
JOIN HumanResources.Employee AS e ON p.BusinessEntityID = e.BusinessEntityID   
JOIN Person.BusinessEntityAddress AS ea ON e.BusinessEntityID = ea.BusinessEntityID  
JOIN Person.Address AS a ON ea.AddressID = a.AddressID;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [-- &#40;Comment&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/comment-transact-sql.md)   
 [控制流语言 &#40;Transact SQL &#41;](~/t-sql/language-elements/control-of-flow.md)  
  
  

