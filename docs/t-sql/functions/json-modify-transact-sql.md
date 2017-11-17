---
title: "JSON_MODIFY (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 06/02/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 96bc8255-a037-4907-aec4-1a9c30814651
caps.latest.revision: 16
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 70f2c1456da6469c39389fada6a74ccf46383582
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="jsonmodify-transact-sql"></a>JSON_MODIFY (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  更新的 JSON 字符串中属性的值并返回更新的 JSON 字符串。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```sql  
JSON_MODIFY ( expression , path , newValue )  
```  
  
## <a name="arguments"></a>参数  
 *expression*  
 一个表达式。 通常的变量或包含 JSON 文本的列的名称。  
  
 **JSON_MODIFY**如果返回错误*表达式*不包含有效 JSON。  
  
 *路径*  
 JSON 路径表达式，指定要更新的属性。

 *路径*具有以下语法：  
  
 `[append] [ lax | strict ] $.<json path>`  
  
-   *追加*  
    指定应将新值追加到所引用的数组的可选修饰符 *\<json 路径 >*。  
  
-   *宽松*  
    指定该属性引用的 *\<json 路径 >*不必存在。 如果该属性不存在，JSON_MODIFY 尝试插入指定路径上的新值。 如果属性不能插入路径上，插入可能会失败。 如果没有指定*宽松*或*严格*，*宽松*是默认模式。  
  
-   *严格*  
    指定该属性引用的 *\<json 路径 >*必须在 JSON 表达式中。 如果该属性不存在，则 JSON_MODIFY 返回错误。  
  
-   *\<json 路径 >*  
    指定要更新的属性的路径。 有关详细信息，请参阅[JSON 路径表达式 &#40;SQL server&#41;](../../relational-databases/json/json-path-expressions-sql-server.md).  
  
在[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]并在[!INCLUDE[ssSDSfull_md](../../includes/sssdsfull-md.md)]，可以提供变量的值作为*路径*。

**JSON_MODIFY**如果返回错误的格式*路径*无效。  
  
 *newValue*  
 指定的属性的新值*路径*。  
  
 在不严格模式下，JSON_MODIFY 删除指定的密钥，如果新值为 NULL。  
  
JSON_MODIFY 如果值的类型是 NVARCHAR 或 VARCHAR 的新值中的所有特殊字符进行转义。 如果正确未转义的文本值的格式由 FOR JSON、 JSON_QUERY 或 JSON_MODIFY 的 JSON。  
  
## <a name="return-value"></a>返回值  
 返回的更新的值*表达式*为正确格式的 JSON 文本。  
  
## <a name="remarks"></a>注释  
 JSON_MODIFY 函数可以更新现有属性的值、 插入新的键： 值对，或删除某一项基于模式的组合，提供的值。  
  
 下表比较的行为**JSON_MODIFY**在不严格模式下和在严格模式下。 可选的路径模式规范 （lax 或 strict） 有关的详细信息，请参阅[JSON 路径表达式 &#40;SQL server&#41;](../../relational-databases/json/json-path-expressions-sql-server.md).  
  
|现有的值|路径存在|宽松模式|严格模式|  
|--------------------|-----------------|--------------|-----------------|  
|不为 NULL|是|更新现有值。|更新现有值。|  
|不为 NULL|是|尝试在指定路径上创建新的键： 值对。<br /><br /> 这可能会失败。 例如，如果你指定的路径`$.user.setting.theme`，JSON_MODIFY 不会插入密钥`theme`如果`$.user`或`$.user.settings`对象不存在，或者如果设置为一个数组或标量值。|错误 – INVALID_PROPERTY|  
|NULL|是|删除现有的属性。|将现有值设置为 null。|  
|NULL|是|执行任何操作。 作为结果返回的第一个参数。|错误 – INVALID_PROPERTY|  
  
 在不严格模式下，JSON_MODIFY 尝试创建新的键： 值对，但在某些情况下可能会失败。  
  
## <a name="examples"></a>示例  
  
### <a name="example---basic-operations"></a>示例-基本操作  
 下面的示例演示可通过 JSON 文本的基本操作。  
  
 **Query**  
  
```sql  

DECLARE @info NVARCHAR(100)='{"name":"John","skills":["C#","SQL"]}'

PRINT @info

-- Update name  

SET @info=JSON_MODIFY(@info,'$.name','Mike')

PRINT @info

-- Insert surname  

SET @info=JSON_MODIFY(@info,'$.surname','Smith')

PRINT @info

-- Delete name  

SET @info=JSON_MODIFY(@info,'$.name',NULL)

PRINT @info

-- Add skill  

SET @info=JSON_MODIFY(@info,'append $.skills','Azure')

PRINT @info
```  
  
 **结果**  
  
```json  
{
    "name": "John",
    "skills": ["C#", "SQL"]
} {
    "name": "Mike",
    "skills": ["C#", "SQL"]
} {
    "name": "Mike",
    "skills": ["C#", "SQL"],
    "surname": "Smith"
} {
    "skills": ["C#", "SQL"],
    "surname": "Smith"
} {
    "skills": ["C#", "SQL", "Azure"],
    "surname": "Smith"
}
```  
  
### <a name="example---multiple-updates"></a>示例-多个更新  
 使用 JSON_MODIFY 可以更新仅一个属性。 如果你必须执行多个更新，你可以使用多个 JSON_MODIFY 调用。  
  
 **Query**  
  
```sql  
DECLARE @info NVARCHAR(100)='{"name":"John","skills":["C#","SQL"]}'

PRINT @info

-- Multiple updates  

SET @info=JSON_MODIFY(JSON_MODIFY(JSON_MODIFY(@info,'$.name','Mike'),'$.surname','Smith'),'append $.skills','Azure')

PRINT @info
```  
  
 **结果**  
  
```json  
{
    "name": "John",
    "skills": ["C#", "SQL"]
} {
    "name": "Mike",
    "skills": ["C#", "SQL", "Azure"],
    "surname": "Smith"
}
```  
  
### <a name="example---rename-a-key"></a>示例-重命名某个键  
 下面的示例演示如何重命名使用 JSON_MODIFY 函数的 JSON 文本中的属性。 首先，你可以获取现有属性的值，并将其作为新的键： 值对插入。 然后，你可以通过将旧的属性的值设置为 NULL 来删除旧密钥。  
  
 **Query**  
  
```sql  
DECLARE @product NVARCHAR(100)='{"price":49.99}'

PRINT @product

-- Rename property  

SET @product=
 JSON_MODIFY(
  JSON_MODIFY(@product,'$.Price',CAST(JSON_VALUE(@product,'$.price') AS NUMERIC(4,2))),
  '$.price',
  NULL
 )

PRINT @product
```  
  
 **结果**  
  
```json  
{
    "price": 49.99
} {
    "Price": 49.99
}
```  
  
 如果不强制转换为数值类型的新值，JSON_MODIFY 会将其视为文本，并在它用双引号。  
  
### <a name="example---increment-a-value"></a>示例-递增一个值  
 下面的示例演示如何使用 JSON_MODIFY 函数的 JSON 文本中的属性的值递增。 首先，你可以获取现有属性的值，并将其作为新的键： 值对插入。 然后，你可以通过将旧的属性的值设置为 NULL 来删除旧密钥。  
  
 **Query**  
  
```sql  
DECLARE @stats NVARCHAR(100)='{"click_count": 173}'

PRINT @stats

-- Increment value  

SET @stats=JSON_MODIFY(@stats,'$.click_count',
 CAST(JSON_VALUE(@stats,'$.click_count') AS INT)+1)

PRINT @stats
```  
  
 **结果**  
  
```json  
{
    "click_count": 173
} {
    "click_count": 174
}
```  
  
### <a name="example---modify-a-json-object"></a>示例-修改 JSON 对象  
 JSON_MODIFY 将*newValue*自变量作为即使它包含正确的纯文本格式的 JSON 文本。 因此，用双引号括的 JSON 输出的函数和的所有特殊字符进行转义，如下面的示例中所示。  
  
 **Query**  
  
```sql  
DECLARE @info NVARCHAR(100)='{"name":"John","skills":["C#","SQL"]}'

PRINT @info

-- Update skills array

SET @info=JSON_MODIFY(@info,'$.skills','["C#","T-SQL","Azure"]')

PRINT @info
```  
  
 **结果**  
  
```json  
{
    "name": "John",
    "skills": ["C#", "SQL"]
} {
    "name": "John",
    "skills": "["C#","T-SQL","Azure"]"
}
```  
  
 若要避免自动转义，提供*newValue*通过使用 JSON_QUERY 函数。 JSON_MODIFY 知道 JSON_MODIFY 返回的值是正确格式设置 JSON，因此它不能摆脱值。  
  
 **Query**  
  
```sql  
DECLARE @info NVARCHAR(100)='{"name":"John","skills":["C#","SQL"]}'

PRINT @info

-- Update skills array  

SET @info=JSON_MODIFY(@info,'$.skills',JSON_QUERY('["C#","T-SQL","Azure"]'))

PRINT @info
```  
  
 **结果**  
  
```json  
{
    "name": "John",
    "skills": ["C#", "SQL"]
} {
    "name": "John",
    "skills": ["C#", "T-SQL", "Azure"]
}
```  
  
### <a name="example---update-a-json-column"></a>示例-更新 JSON 列  
 下面的示例更新包含 JSON 的表列中属性的值。  
  
```sql  
UPDATE Employee
SET jsonCol=JSON_MODIFY(jsonCol,"$.info.address.town",'London')
WHERE EmployeeID=17
 
```  
  
## <a name="see-also"></a>另请参阅  
 [JSON 路径表达式 &#40;SQL server&#41;](../../relational-databases/json/json-path-expressions-sql-server.md)   
 [JSON 数据 &#40;SQL server&#41;](../../relational-databases/json/json-data-sql-server.md)  
  
  

