---
title: "位 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 07/23/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- bit_TSQL
- bit
dev_langs:
- TSQL
helpviewer_keywords:
- bit data type
ms.assetid: 40adfd08-a31c-49cb-a172-386bcaa6edee
caps.latest.revision: 33
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3817549e5846c68b422fb941907860896b956d9a
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="bit-transact-sql"></a>bit (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  可以取值为 1、0 或 NULL 的 integer 数据类型。  
  
## <a name="remarks"></a>注释  
[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]优化存储**位**列。 如果有 8 或更小**位**列在表中，列存储为 1 个字节。 如果来自最多支持 16 9**位**列，列存储为 2 个字节，依次类推。
  
TRUE 和 FALSE 的字符串值可以转换为**位**值： TRUE 转换为 1，FALSE 转换为 0。
  
转换为 bit 会将任何非零值升为 1。
  
## <a name="see-also"></a>另请参阅
[ALTER TABLE (Transact-SQL)](../../t-sql/statements/alter-table-transact-sql.md)  
[CAST 和 CONVERT (Transact-SQL)](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md)  
[数据类型转换 &#40; 数据库引擎 &#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)  
[数据类型 (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)  
[DECLARE @local_variable (Transact-SQL)](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
[SET @local_variable (Transact-SQL)](../../t-sql/language-elements/set-local-variable-transact-sql.md)  
[sys.types &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)
  
  

