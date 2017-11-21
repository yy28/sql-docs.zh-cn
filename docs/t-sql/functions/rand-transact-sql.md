---
title: "RAND (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- RAND
- RAND_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- RAND function
- values [SQL Server], random float
- random float value
ms.assetid: 363c84d6-b9fa-49ba-9a75-e44f27535ff6
caps.latest.revision: 22
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b1d358122487d3568167021ac3a296e1eb2d1974
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="rand-transact-sql"></a>RAND (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-xxx-md.md)]

  返回伪随机**float**介于 0 和 1，独占的值。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
RAND ( [ seed ] )  
```  
  
## <a name="arguments"></a>参数  
 *种子*  
 是一个整数[表达式](../../t-sql/language-elements/expressions-transact-sql.md)(**tinyint**， **smallint**，或**int**)，它将授予的种子值。 如果*种子*未指定，[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]将随机分配种子值。 对于指定的种子值，返回的结果始终相同。  
  
## <a name="return-types"></a>返回类型  
 **float**  
  
## <a name="remarks"></a>注释  
 使用同一个种子值重复调用 RAND() 会返回相同的结果。  
  
 对于一个连接，如果使用指定的种子值调用 RAND()，则 RAND() 的所有后续调用将基于使用该指定种子值的 RAND() 调用生成结果。 例如，以下查询将始终返回相同的数字序列。  
  
```  
SELECT RAND(100), RAND(), RAND()   
```  
  
## <a name="examples"></a>示例  
 以下示例将产生由 RAND 函数生成的四个不同的随机数。  
  
```  
DECLARE @counter smallint;  
SET @counter = 1;  
WHILE @counter < 5  
   BEGIN  
      SELECT RAND() Random_Number  
      SET @counter = @counter + 1  
   END;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [数学函数 &#40;Transact SQL &#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)  
  
  

