---
title: "JSON_VALUE (TRANSACT-SQL) |Microsoft 文档"
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
- JSON_VALUE
- JSON_VALUE_TSQL
helpviewer_keywords:
- JSON_VALUE function
- JSON, extracting
- JSON, querying
ms.assetid: cd016e14-11eb-4eaf-bf05-c7cfcc820a10
caps.latest.revision: "18"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: 5762af5115dd65b819bc74c3585cfc8275a516b1
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="jsonvalue-transact-sql"></a>JSON_VALUE (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  从 JSON 字符串中提取标量值。  
  
 若要从 JSON 字符串而不是标量值中提取对象或数组，请参阅[JSON_QUERY &#40;Transact SQL &#41;](../../t-sql/functions/json-query-transact-sql.md). 有关之间的差异信息**JSON_VALUE**和**JSON_QUERY**，请参阅[比较 JSON_VALUE 和 JSON_QUERY](../../relational-databases/json/validate-query-and-change-json-data-with-built-in-functions-sql-server.md#JSONCompare)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```sql  
JSON_VALUE ( expression , path )  
```  
  
## <a name="arguments"></a>参数  
 *expression*  
 一个表达式。 通常的变量或包含 JSON 文本的列的名称。  
 
 如果**JSON_VALUE**查找不在有效的 JSON*表达式*找到由标识的值之前*路径*，函数将返回错误。 如果 **JSON_VALUE*找不到由标识的值*路径*，它在扫描整个文本，并且会返回一个错误如果它找到 JSON，中的任意位置无效*表达式*。
  
 *路径*  
 指定要提取的属性的 JSON 路径。 有关详细信息，请参阅[JSON 路径表达式 &#40;SQL server&#41;](../../relational-databases/json/json-path-expressions-sql-server.md).  
 
在[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]并在[!INCLUDE[ssSDSfull_md](../../includes/sssdsfull-md.md)]，可以提供变量的值作为*路径*。
  
 如果格式*路径*无效， **JSON_VALUE**返回错误。  
  
## <a name="return-value"></a>返回值  
 返回类型 nvarchar （4000） 的单个文本值。 返回值的排序规则操作输入表达式的排序规则相同。  
  
 如果值大于 4000 个字符：  
  
-   在不严格模式下， **JSON_VALUE** ，则返回 null。  
  
-   在严格模式下， **JSON_VALUE**返回错误。  
  
 如果必须返回标量值大于 4000 个字符，请使用**OPENJSON**而不是**JSON_VALUE**。 有关详细信息，请参阅 [OPENJSON (Transact-SQL)](../../t-sql/functions/openjson-transact-sql.md)。  
  
## <a name="remarks"></a>注释

### <a name="lax-mode-and-strict-mode"></a>宽松模式和严格模式

 请考虑以下 JSON 文本：  
  
```json  
DECLARE @jsonInfo NVARCHAR(MAX)

SET @jsonInfo=N'{  
     "info":{    
       "type":1,  
       "address":{    
         "town":"Bristol",  
         "county":"Avon",  
         "country":"England"  
       },  
       "tags":["Sport", "Water polo"]  
    },  
    "type":"Basic"  
 }'  
```  
  
 下表比较的行为**JSON_VALUE**在不严格模式下和在严格模式下。 可选的路径模式规范 （lax 或 strict） 有关的详细信息，请参阅[JSON 路径表达式 &#40;SQL server&#41;](../../relational-databases/json/json-path-expressions-sql-server.md).  
  
|路径|在不严格模式下的返回值|在严格模式下的返回值|详细信息|  
|----------|------------------------------|---------------------------------|---------------|  
|$|NULL|错误|不是标量值。<br /><br /> 使用**JSON_QUERY**相反。|  
|$。 info.type|N '1'|N '1'|N/A|  
|$。 info.address.town|N'Bristol|N'Bristol|N/A|  
|$.info。"地址"|NULL|错误|不是标量值。<br /><br /> 使用**JSON_QUERY**相反。|  
|$。 info.tags|NULL|错误|不是标量值。<br /><br /> 使用**JSON_QUERY**相反。|  
|$。 info.type[0]|NULL|错误|不是数组。|  
|$。 info.none|NULL|错误|属性不存在。|  
  
## <a name="examples"></a>示例  
  
### <a name="example-1"></a>示例 1  
 下面的示例使用的 JSON 属性的值`town`和`state`在查询结果中。 由于**JSON_VALUE**保留了源，结果的排序顺序的排序规则取决于的排序规则`jsonInfo`列。  
  
```sql  
SELECT FirstName,LastName,
 JSON_VALUE(jsonInfo,'$.info.address[0].town') AS Town
FROM Person.Person
WHERE JSON_VALUE(jsonInfo,'$.info.address[0].state') LIKE 'US%'
ORDER BY JSON_VALUE(jsonInfo,'$.info.address[0].town')
```  
  
### <a name="example-2"></a>示例 2  
 下面的示例将 JSON 属性的值提取`town`到本地变量。  
  
```sql  
DECLARE @jsonInfo NVARCHAR(MAX)
DECLARE @town NVARCHAR(32)

SET @jsonInfo=N'<array of address info>'

SET @town=JSON_VALUE(@jsonInfo,'$.info.address.town')
```  
  
### <a name="example-3"></a>示例 3  
 下面的示例创建计算的列基于 JSON 属性的值。  
  
```sql  
CREATE TABLE dbo.Store
 (
  StoreID INT IDENTITY(1,1) NOT NULL,
  Address VARCHAR(500),
  jsonContent NVARCHAR(8000),
  Longitude AS JSON_VALUE(jsonContent, '$.address[0].longitude'),
  Latitude AS JSON_VALUE(jsonContent, '$.address[0].latitude')
 )
```  
  
## <a name="see-also"></a>另请参阅  
 [JSON 路径表达式 &#40;SQL server&#41;](../../relational-databases/json/json-path-expressions-sql-server.md)   
 [JSON 数据 &#40;SQL server&#41;](../../relational-databases/json/json-data-sql-server.md)  
  
  
