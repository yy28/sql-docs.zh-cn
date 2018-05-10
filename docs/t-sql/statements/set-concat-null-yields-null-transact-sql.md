---
title: SET CONCAT_NULL_YIELDS_NULL (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: cc4261d54d86300783499871f50b5ec7d7d152fd
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="set-concatnullyieldsnull-transact-sql"></a>SET CONCAT_NULL_YIELDS_NULL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  控制是将串联结果视为 Null 还是空字符串值。  
  
> [!IMPORTANT]  
>  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的未来版本中，CONCAT_NULL_YIELDS_NULL 将始终为 ON，而且将该选项显式设置为 OFF 的任何应用程序都将生成一个错误。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。  
  
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
  
## <a name="remarks"></a>Remarks  
 当 SET CONCAT_NULL_YIELDS_NULL 为 ON 时，串联空值与字符串将产生 NULL 结果。 例如，`SELECT 'abc' + NULL` 将生成 `NULL`。 当 SET CONCAT_NULL_YIELDS_NULL 为 OFF 时，串联空值与字符串将产生字符串本身（空值作为空字符串处理）。 例如，`SELECT 'abc' + NULL` 将生成 `abc`。  
  
 如果未指定 SET CONCAT_NULL_YIELDS_NULL，则应用 **CONCAT_NULL_YIELDS_NULL** 数据库选项的设置。  
  
> [!NOTE]  
>  SET CONCAT_NULL_YIELDS_NULL 与 ALTER DATABASE 的 CONCAT_NULL_YIELDS_NULL 设置相同。  
  
 SET CONCAT_NULL_YIELDS_NULL 的设置是在执行或运行时设置的，而不是在分析时设置的。  
  
 当对计算列或索引视图创建或更改索引时，SET CONCAT_NULL_YIELDS_NULL 必须为 ON。 如果 SET CONCAT_NULL_YIELDS_NULL 为 OFF，则以计算列或索引视图创建索引的表中的任何 CREATE、UPDATE、INSERT 和 DELETE 语句都将失败。 有关计算列的索引视图和索引需要的 SET 选项设置的详细信息，请参阅 [SET Statements (Transact-SQL)](../../t-sql/statements/set-statements-transact-sql.md) 中的“使用 SET 语句时的注意事项”。  
  
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
 [SESSIONPROPERTY (Transact-SQL)](../../t-sql/functions/sessionproperty-transact-sql.md)  
  
  
