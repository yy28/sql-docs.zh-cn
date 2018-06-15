---
title: DATALENGTH (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DATALENGTH_TSQL
- DATALENGTH
dev_langs:
- TSQL
helpviewer_keywords:
- number of bytes representing expression
- data types [SQL Server], length
- DATALENGTH function
- expressions [SQL Server], length
- lengths [SQL Server], data
ms.assetid: 00f377f1-cc3e-4eac-be47-b3e3f80267c9
caps.latest.revision: 31
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: e1d3b1e73a1e353fb87dcb7cd5782f551e9508a2
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
ms.locfileid: "34047028"
---
# <a name="datalength-transact-sql"></a>DATALENGTH (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

此函数返回用于表示任何表达式的字节数。
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```sql
DATALENGTH ( expression )   
```  
  
## <a name="arguments"></a>参数  
*expression*  
任何数据类型的[表达式](../../t-sql/language-elements/expressions-transact-sql.md)。
  
## <a name="return-types"></a>返回类型
如果 expression 具有一个 nvarchar(max)、varbinary(max) 或 varchar(max) 数据类型，则为 bigint；否则为 int。
  
## <a name="remarks"></a>Remarks  
`DATALENGTH` 与数据类型配合使用时

- **图像**
- **ntext**
- **nvarchar**
- **text**
- **varbinary**

和

- **varchar**

尤其有用，因为这些数据类型可以存储可变长度数据。
  
对于 NULL 值，`DATALENGTH` 返回 NULL。
  
> [!NOTE]  
>  兼容级别可能影响返回值。 有关兼容性级别的详细信息，请参阅 [ALTER DATABASE 兼容性级别 (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)。  
  
## <a name="examples"></a>示例  
此示例查找 `Product` 表中的 `Name` 列的长度：
  
```sql
-- Uses AdventureWorks  
  
SELECT length = DATALENGTH(EnglishProductName), EnglishProductName  
FROM dbo.DimProduct  
ORDER BY EnglishProductName;  
GO  
```  
  
## <a name="see-also"></a>另请参阅
[LEN (Transact-SQL)](../../t-sql/functions/len-transact-sql.md)  
[CAST 和 CONVERT (Transact-SQL)](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[数据类型 (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)  
[系统函数 (Transact-SQL)](../../relational-databases/system-functions/system-functions-for-transact-sql.md)
  
  

