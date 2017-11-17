---
title: "解压缩 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 11/30/2015
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DECOMPRESS
- DECOMPRESS_TSQL
helpviewer_keywords:
- DECOMPRESS function
ms.assetid: 738d56be-3870-4774-b112-3dce27becc11
caps.latest.revision: 8
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7918a9bce5afcd7ce59551a60fc7e3f2f318f492
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="decompress-transact-sql"></a>解压缩 (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  解压缩使用 GZIP 算法的输入的表达式。 压缩的结果是字节数组 （varbinary （max） 类型）。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
DECOMPRESS ( expression )  
```  
  
## <a name="arguments"></a>参数  
 *expression*  
 是**varbinary (***n***)**， **varbinary （max)**，或**二进制 (** *n***)**. 有关详细信息，请参阅[表达式 (Transact-SQL)](../../t-sql/language-elements/expressions-transact-sql.md)。  
  
## <a name="return-types"></a>返回类型  
 返回的数据类型**varbinary （max)**类型。 输入自变量被解压缩使用 ZIP 算法。 如果需要用户应显式强制转换为目标类型的结果。  
  
## <a name="remarks"></a>注释  
  
## <a name="examples"></a>示例  
  
### <a name="a-decompress-data-at-query-time"></a>A. 在查询时解压缩的数据  
 下面的示例演示如何显示从表的压缩数据：  
  
```  
SELECT _id, name, surname, datemodified,  
             CAST(DECOMPRESS(info) AS NVARCHAR(MAX)) AS info  
FROM player;  
```  
  
### <a name="b-display-compressed-data-using-computed-column"></a>B. 显示使用计算的列的压缩的数据  
 下面的示例演示如何创建用于存储解压缩的数据的表：  
  
```  
CREATE TABLE (  
    _id int primary key identity,  
    name nvarchar(max),  
    surname nvarchar(max),  
    info varbinary(max),  
    info_json as CAST(decompress(info) as nvarchar(max))  
);  
```  
  
## <a name="see-also"></a>另请参阅  
 [字符串函数 &#40;Transact SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)   
 [COMPRESS &#40;Transact SQL &#41;](../../t-sql/functions/compress-transact-sql.md)  
  
  

