---
title: ISJSON (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: genemi
ms.technology: t-sql
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
monikerRange: = azuresqldb-current||= azure-sqldw-latest||>= sql-server-2016||>= sql-server-linux-2017||= sqlallproducts-allversions
ms.openlocfilehash: 9b98e7250f6cea54401ba533c769ab2be0bc82cf
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "65577573"
---
# <a name="isjson-transact-sql"></a>ISJSON (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

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
 如果字符串包含有效 JSON，则返回 1；否则，返回 0。 如果 expression  为 NULL，则返回 NULL。  
  
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
  
  
