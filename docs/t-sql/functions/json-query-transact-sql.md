---
title: "JSON_QUERY (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 06/02/2016
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
- JSON_QUERY
- JSON_QUERY_TSQL
helpviewer_keywords:
- JSON, extracting
- JSON, querying
- JSON_QUERY function
ms.assetid: 1ab0d90f-19b6-4988-ab4f-22fdf28b7c79
caps.latest.revision: "19"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 310d85e26226cd54eff5d1c99e94b235348a90f7
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="jsonquery-transact-sql"></a>JSON_QUERY (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

 从 JSON 字符串中提取对象或数组。  
  
 若要从 JSON 字符串而不是对象或数组中提取标量值，请参阅[JSON_VALUE &#40;Transact SQL &#41;](../../t-sql/functions/json-value-transact-sql.md). 有关之间的差异信息**JSON_VALUE**和**JSON_QUERY**，请参阅[比较 JSON_VALUE 和 JSON_QUERY](../../relational-databases/json/validate-query-and-change-json-data-with-built-in-functions-sql-server.md#JSONCompare)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```sql  
JSON_QUERY ( expression [ , path ] )  
```  
  
## <a name="arguments"></a>参数  
 *expression*  
 一个表达式。 通常的变量或包含 JSON 文本的列的名称。  
  
 如果**JSON_QUERY**查找不在有效的 JSON*表达式*找到由标识的值之前*路径*，函数将返回错误。 如果**JSON_QUERY**找不到由标识的值*路径*，它在扫描整个文本，并且会返回一个错误如果它找到 JSON，中的任意位置无效*表达式*。  
  
 *路径*  
 指定对象或要提取的数组的 JSON 路径。

在[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]并在[!INCLUDE[ssSDSfull_md](../../includes/sssdsfull-md.md)]，可以提供变量的值作为*路径*。

JSON 路径可以指定用于分析的 lax 或 strict 模式。 如果未指定的分析模式，宽松的模式是默认值。 有关详细信息，请参阅[JSON 路径表达式 &#40;SQL server&#41;](../../relational-databases/json/json-path-expressions-sql-server.md).  

默认值为*路径*是 '$'。 因此，如果你未提供的值*路径*， **JSON_QUERY**返回输入*表达式*。

如果格式*路径*无效， **JSON_QUERY**返回错误。  
  
## <a name="return-value"></a>返回值  
 返回 JSON 片段的 nvarchar (max) 类型。 返回值的排序规则操作输入表达式的排序规则相同。  
  
 如果值不是对象或数组：  
  
-   在不严格模式下， **JSON_QUERY** ，则返回 null。  
  
-   在严格模式下， **JSON_QUERY**返回错误。  
  
## <a name="remarks"></a>注释  

### <a name="lax-mode-and-strict-mode"></a>宽松模式和严格模式

 请考虑以下 JSON 文本：  
  
```json  
{
    "info": {
        "type": 1,
        "address": {
            "town": "Bristol",
            "county": "Avon",
            "country": "England"
        },
        "tags": ["Sport", "Water polo"]
    },
    "type": "Basic"
} 
```  
  
 下表比较的行为**JSON_QUERY**在不严格模式下和在严格模式下。 可选的路径模式规范 （lax 或 strict） 有关的详细信息，请参阅[JSON 路径表达式 &#40;SQL server&#41;](../../relational-databases/json/json-path-expressions-sql-server.md).  
  
|路径|在不严格模式下的返回值|在严格模式下的返回值|详细信息|  
|----------|------------------------------|---------------------------------|---------------|  
|$|返回整个 JSON 文本。|返回整个 JSON 文本。|N/A|  
|$。 info.type|NULL|错误|不一个对象或数组。<br /><br /> 使用**JSON_VALUE**相反。|  
|$。 info.address.town|NULL|错误|不一个对象或数组。<br /><br /> 使用**JSON_VALUE**相反。|  
|$.info。"地址"|N {"镇":"卡纸"，"县":"Avon"，"国家/地区":"英格兰"}|N {"镇":"卡纸"，"县":"Avon"，"国家/地区":"英格兰"}|N/A|  
|$。 info.tags|N '["端口"，"水位马"]|N '["端口"，"水位马"]|N/A|  
|$。 info.type[0]|NULL|错误|不是数组。|  
|$。 info.none|NULL|错误|属性不存在。|  

### <a name="using-jsonquery-with-for-json"></a>借助 FOR JSON 中使用 JSON_QUERY

**JSON_QUERY**返回有效的 JSON 片段。 因此， **FOR JSON**不能摆脱中的特殊字符**JSON_QUERY**返回值。

如果你正在使用 FOR JSON，返回的结果，并且您要包含已在 JSON 格式 （列中或作为表达式的结果） 的数据，使用的 JSON 数据换行**JSON_QUERY**而无需*路径*参数。

## <a name="examples"></a>示例  
  
### <a name="example-1"></a>示例 1  
 下面的示例演示如何返回 JSON 片段从`CustomFields`在查询结果中的列。  
  
```sql  
SELECT PersonID,FullName,
 JSON_QUERY(CustomFields,'$.OtherLanguages') AS Languages
FROM Application.People
```  
  
### <a name="example-2"></a>示例 2  
下面的示例演示如何在 FOR JSON 子句的输出中包含 JSON 片段。  
  
```sql  
SELECT StockItemID, StockItemName,
         JSON_QUERY(Tags) as Tags,
         JSON_QUERY(CONCAT('["',ValidFrom,'","',ValidTo,'"]')) ValidityPeriod
FROM Warehouse.StockItems
FOR JSON PATH
```  
  
## <a name="see-also"></a>另请参阅  
 [JSON 路径表达式 &#40;SQL server&#41;](../../relational-databases/json/json-path-expressions-sql-server.md)   
 [JSON 数据 &#40;SQL server&#41;](../../relational-databases/json/json-data-sql-server.md)  
