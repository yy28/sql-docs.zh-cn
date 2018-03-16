---
title: COMPRESS (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: reference
f1_keywords:
- COMPRESS
- COMPRESS_TSQL
helpviewer_keywords:
- COMPRESS function
ms.assetid: c2bfe9b8-57a4-48b4-b028-e1a3ed5ece88
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 01500cd6560fd60dda2cb9060c2968d7c010d8e2
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="compress-transact-sql"></a>COMPRESS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

使用 GZIP 算法压缩输入表达式。 压缩的结果是 varbinary(max) 类型的字节数组。
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```sql
COMPRESS ( expression )  
```  
  
## <a name="arguments"></a>参数  
*expression*  
nvarchar(n)、nvarchar(max)、varchar(n)、varchar(max)、varbinary(n)、varbinary(max)、char(n)、nchar(n) 或 binary(n) 表达式。 有关详细信息，请参阅[表达式 (Transact-SQL)](../../t-sql/language-elements/expressions-transact-sql.md)。
  
## <a name="return-types"></a>返回类型
返回表示输入压缩内容的 varbinary(max) 数据类型。
  
## <a name="remarks"></a>Remarks  
压缩数据无法编入索引。
  
COMPRESS 函数压缩将提供的数据压缩为输入表达式。对于每个要压缩的数据部分，必须调用该函数。 有关在存储过程中以行或页级别进行自动压缩的信息，请参阅[数据压缩](../../relational-databases/data-compression/data-compression.md)。
  
## <a name="examples"></a>示例  
  
### <a name="a-compress-data-during-the-table-insert"></a>A. 在插入表格期间压缩数据  
以下示例演示如何压缩插入到表格中的数据：
  
```sql
INSERT INTO player (name, surname, info )  
VALUES (N'Ovidiu', N'Cracium',   
        COMPRESS(N'{"sport":"Tennis","age": 28,"rank":1,"points":15258, turn":17}'));  
  
INSERT INTO player (name, surname, info )  
VALUES (N'Michael', N'Raheem', compress(@info));  
```  
  
### <a name="b-archive-compressed-version-of-deleted-rows"></a>B. 将已删除行的压缩版本进行存档  
以下语句从 `player` 表删除旧播放器记录，并将记录以压缩格式存储在 `inactivePlayer` 表中，从而节省空间。
  
```sql
DELETE player  
WHERE datemodified < @startOfYear  
OUTPUT id, name, surname datemodifier, COMPRESS(info)   
INTO dbo.inactivePlayers ;  
```  
  
## <a name="see-also"></a>另请参阅
[字符串函数 (Transact-SQL)](../../t-sql/functions/string-functions-transact-sql.md)  
[DECOMPRESS (Transact-SQL)](../../t-sql/functions/decompress-transact-sql.md)
  
  
