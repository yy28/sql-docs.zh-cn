---
title: ISJSON (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: douglasl
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- ISJSON
- ISJSON_TSQL
helpviewer_keywords:
- ISJSON function
- JSON, validating
ms.assetid: c836f3d3-3e17-44ae-92bf-f341918896c3
author: jovanpop-msft
ms.author: jovanpop
manager: craigg
ms.openlocfilehash: b9abfcd7fe78420f1a67b96fdedfd50e8a6f058a
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "38055135"
---
# <a name="isjson-transact-sql"></a>ISJSON (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  测试字符串是否包含有效 JSON。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```sql  
ISJSON ( expression )  
```  
  
## <a name="arguments"></a>参数  
 *expression*  
 要测试的字符串。  
  
## <a name="return-value"></a>返回值  
 如果字符串包含有效 JSON，则返回 1；否则，返回 0。 如果 expression 为 NULL，则返回 NULL。  
  
 不返回错误。  
  
## <a name="remarks"></a>Remarks  
 **ISJSON** 不检查在相同级别的键的唯一性。  
  
## <a name="examples"></a>示例  
  
### <a name="example-1"></a>示例 1  
如果参数值 `@param` 包含有效 JSON，则下面的示例有条件地运行语句块。  
  
```sql  
DECLARE @param <data type>
SET @param = <value>

IF (ISJSON(@param) > 0)  
BEGIN  
     -- Do something with the valid JSON value of @param.  
END
 
```  
  
### <a name="example-2"></a>示例 2  
下面的示例将返回其列 `json_col` 包含有效 JSON 的行。  
  
```sql  
SELECT id, json_col
FROM tab1
WHERE ISJSON(json_col) > 0 
```  
  
## <a name="see-also"></a>另请参阅  
 [JSON 数据 (SQL Server)](../../relational-databases/json/json-data-sql-server.md)  
  
  
