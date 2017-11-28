---
title: "ISJSON (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 07/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-json
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ISJSON
- ISJSON_TSQL
helpviewer_keywords:
- ISJSON function
- JSON, validating
ms.assetid: c836f3d3-3e17-44ae-92bf-f341918896c3
caps.latest.revision: "12"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 0ecbcc4ced2b9503ec9161f7aa93a1a5266960ef
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="isjson-transact-sql"></a>ISJSON (TRANSACT-SQL)
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
 返回该字符串包含有效 JSON; 如果为 1否则，返回 0。 返回 null 如果*表达式*为 null。  
  
 不返回错误。  
  
## <a name="remarks"></a>注释  
 **ISJSON**不会检查在同一级别的键的唯一性。  
  
## <a name="examples"></a>示例  
  
### <a name="example-1"></a>示例 1  
下面的示例运行语句块有条件地如果参数值`@param`包含有效 JSON。  
  
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
 [JSON 数据 &#40;SQL server&#41;](../../relational-databases/json/json-data-sql-server.md)  
  
  
