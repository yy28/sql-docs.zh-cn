---
title: "压缩 (Transact SQL) |Microsoft 文档"
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
caps.latest.revision: 9
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c30cb5f351d9a84beec608483380edb94b8c7844
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="compress-transact-sql"></a>压缩 (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

压缩使用 GZIP 算法的输入的表达式。 压缩的结果是字节数组的类型**varbinary （max)**。
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```sql
COMPRESS ( expression )  
```  
  
## <a name="arguments"></a>参数  
*expression*  
是**nvarchar (***n***)**， **nvarchar (max)**， **varchar (** *n*  **)**， **varchar （max)**， **varbinary (**  *n*  **)**， **varbinary （max)**， **char (***n***)**， **nchar (**  *n*  **)**，或**二进制 (***n***)**表达式。 有关详细信息，请参阅[表达式 (Transact-SQL)](../../t-sql/language-elements/expressions-transact-sql.md)。
  
## <a name="return-types"></a>返回类型
返回的数据类型**varbinary （max)**表示输入的压缩的内容。
  
## <a name="remarks"></a>注释  
无法为压缩的数据创建索引。
  
COMPRESS 函数压缩数据用作输入的表达式，必须调用每个部分的数据进行压缩。 在存储过程在行或页级别的自动压缩，请参阅[数据压缩](../../relational-databases/data-compression/data-compression.md)。
  
## <a name="examples"></a>示例  
  
### <a name="a-compress-data-during-the-table-insert"></a>A. 表插入期间压缩数据  
下面的示例演示如何压缩数据插入到表：
  
```sql
INSERT INTO player (name, surname, info )  
VALUES (N'Ovidiu', N'Cracium',   
        COMPRESS(N'{"sport":"Tennis","age": 28,"rank":1,"points":15258, turn":17}'));  
  
INSERT INTO player (name, surname, info )  
VALUES (N'Michael', N'Raheem', compress(@info));  
```  
  
### <a name="b-archive-compressed-version-of-deleted-rows"></a>B. 存档压缩已删除的行版本  
下面的语句删除从旧播放器记录`player`表并将存储中的记录`inactivePlayer`以节省空间以压缩格式的表。
  
```sql
DELETE player  
WHERE datemodified < @startOfYear  
OUTPUT id, name, surname datemodifier, COMPRESS(info)   
INTO dbo.inactivePlayers ;  
```  
  
## <a name="see-also"></a>另请参阅
[字符串函数 &#40;Transact SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)  
[解压缩 &#40;Transact SQL &#41;](../../t-sql/functions/decompress-transact-sql.md)
  
  

