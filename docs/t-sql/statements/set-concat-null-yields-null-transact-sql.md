---
title: "集 CONCAT_NULL_YIELDS_NULL (TRANSACT-SQL) |Microsoft 文档"
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
- CONCAT_NULL_YIELDS_NULL_TSQL
- SET CONCAT_NULL_YIELDS_NULL
- CONCAT_NULL_YIELDS_NULL
- SET_CONCAT_NULL_YIELDS_NULL_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CONCAT_NULL_YIELDS_NULL option
- null values [SQL Server], concatenation results
- concatenation [SQL Server]
- SET CONCAT_NULL_YIELDS_NULL statement
ms.assetid: 3091b71c-6518-4eb4-88ab-acae49102bc5
caps.latest.revision: 34
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 60281ff903bf7eb04165a65e8f2b75a80f589780
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="set-concatnullyieldsnull-transact-sql"></a>SET CONCAT_NULL_YIELDS_NULL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw_md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  控制是将串联结果视为 Null 还是空字符串值。  
  
> [!IMPORTANT]  
>  未来版本中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]CONCAT_NULL_YIELDS_NULL 将始终为 ON 和任何应用程序显式将选项设置为 OFF 将生成错误。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
-- Syntax for SQL Server  
    
SET CONCAT_NULL_YIELDS_NULL { ON | OFF }   
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
SET CONCAT_NULL_YIELDS_NULL ON    
```  
  
## <a name="remarks"></a>注释  
 当 SET CONCAT_NULL_YIELDS_NULL 为 ON 时，串联空值与字符串将产生 NULL 结果。 例如，`SELECT 'abc' + NULL` 将生成 `NULL`。 当 SET CONCAT_NULL_YIELDS_NULL 为 OFF 时，串联空值与字符串将产生字符串本身（空值作为空字符串处理）。 例如，`SELECT 'abc' + NULL` 将生成 `abc`。  
  
 如果未指定 SET CONCAT_NULL_YIELDS_NULL 的设置**CONCAT_NULL_YIELDS_NULL**数据库选项适用。  
  
> [!NOTE]  
>  SET CONCAT_NULL_YIELDS_NULL 与 ALTER DATABASE 的 CONCAT_NULL_YIELDS_NULL 设置相同。  
  
 SET CONCAT_NULL_YIELDS_NULL 的设置是在执行或运行时设置的，而不是在分析时设置的。  
  
 当对计算列或索引视图创建或更改索引时，SET CONCAT_NULL_YIELDS_NULL 必须为 ON。 如果 SET CONCAT_NULL_YIELDS_NULL 为 OFF，则以计算列或索引视图创建索引的表中的任何 CREATE、UPDATE、INSERT 和 DELETE 语句都将失败。 对计算列所需的 SET 选项设置的索引的视图和索引的详细信息，请参阅"当你使用 SET 语句的注意事项"中[SET 语句 &#40;Transact SQL &#41;](../../t-sql/statements/set-statements-transact-sql.md).  
  
 如果将 CONCAT_NULL_YIELDS_NULL 设置为 OFF，则不能出现跨服务器边界的字符串串联。  
  
 要查看此设置的当前设置，请运行以下查询。  
  
```  
DECLARE @CONCAT_NULL_YIELDS_NULL VARCHAR(3) = 'OFF';  
IF ( (4096 & @@OPTIONS) = 4096 ) SET @CONCAT_NULL_YIELDS_NULL = 'ON';  
SELECT @CONCAT_NULL_YIELDS_NULL AS CONCAT_NULL_YIELDS_NULL;  
  
```  
  
## <a name="examples"></a>示例  
 以下示例显示如何同时使用两个 `SET CONCAT_NULL_YIELDS_NULL` 设置。  
  
```  
PRINT 'Setting CONCAT_NULL_YIELDS_NULL ON';  
GO  
-- SET CONCAT_NULL_YIELDS_NULL ON and testing.  
SET CONCAT_NULL_YIELDS_NULL ON;  
GO  
SELECT 'abc' + NULL ;  
GO  
  
-- SET CONCAT_NULL_YIELDS_NULL OFF and testing.  
SET CONCAT_NULL_YIELDS_NULL OFF;  
GO  
SELECT 'abc' + NULL;   
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [SET 语句 (Transact-SQL)](../../t-sql/statements/set-statements-transact-sql.md)   
 [SESSIONPROPERTY &#40;Transact SQL &#41;](../../t-sql/functions/sessionproperty-transact-sql.md)  
  
  

