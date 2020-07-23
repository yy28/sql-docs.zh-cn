---
title: StructureColumn （DMX） |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: cb07dd463ddbbc15942ca6f62c4ccb708a8c5efd
ms.sourcegitcommit: 205de8fa4845c491914902432791bddf11002945
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/23/2020
ms.locfileid: "86970289"
---
# <a name="structurecolumn-dmx"></a>StructureColumn (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  返回对应于指定事例的结构列的值，或者返回指定事例中的嵌套表的表值。  
  
## <a name="syntax"></a>语法  
  
```  
  
StructureColumn('structure column name')  
```  
  
## <a name="arguments"></a>参数  
 结构列名称。  
 事例或嵌套表挖掘结构列的名称。  
  
## <a name="result-type"></a>结果类型  
 返回的类型取决于参数中引用的列的类型 \<structure column name> 。 例如，如果引用的挖掘结构列包含标量值，函数将返回标量值。  
  
 如果引用的挖掘结构列是嵌套表，函数将返回表值。 返回的表值可用于 sub-SELECT 语句的 FROM 子句中。  
  
## <a name="remarks"></a>备注  
 此函数是多态函数，可在允许有表达式（包括 SELECT 表达式列表、WHERE 条件表达式和 ORDER BY 表达式）的语句中的任意位置使用。  
  
 挖掘结构中的列的名称是字符串值，因此必须用单引号引起来：例如， `StructureColumn('` **列 1** `')` 。 如果多个列具有相同的名称，则该名称在包含 SELECT 语句的上下文中解析。  
  
 使用**StructureColumn**函数从查询返回的结果受模型上的任何筛选器的存在的影响。 也就是说，模型筛选器控制包含在挖掘模型中的事例。 因此，结构列查询可以只返回挖掘模型中使用的那些事例。 有关说明挖掘模型筛选器对事例表和嵌套表的影响的代码示例，请参阅本主题的“示例”部分。  
  
 有关如何在 DMX SELECT 语句中使用此函数的详细信息，请参阅[SELECT FROM &#60;model&#62;。&#40;DMX&#41;](../dmx/select-from-model-cases-dmx.md)或[从 &#60;结构&#62; 中选择事例。事例](../dmx/select-from-structure-cases.md)。  
  
## <a name="error-messages"></a>错误消息  
 如果用户没有父挖掘结构的钻取权限，则会引发以下安全错误：  
  
 用户 "% {user/}" 无权钻取到挖掘模型 "% {model/}" 的父挖掘结构。  
  
 如果指定了无效的结构列名称，则会引发以下错误消息：  
  
 当前上下文（第% {line/} 行，第% {column/} 列）的 "% {structure/}" 父挖掘结构中找不到 "% {structure-列名/}" 挖掘结构列。  
  
## <a name="examples"></a>示例  
 我们将在这些示例中使用以下挖掘结构。 请注意，该挖掘结构包含两个嵌套表列 `Products` 和 `Hobbies`。 `Hobbies` 列中的嵌套表有一个列用作该嵌套表的键。 `Products` 列中的嵌套表是复杂的嵌套表，其中一个列用作键列，其他列用作输入列。 以下示例说明如何将数据挖掘结构设计为包含许多不同的列，尽管不是所有的列在模型中都能用到。 其中的某些列可能在模型级别对于通用化模式没有用，但可能对于钻取非常有用。  
  
```  
CREATE MINING STRUCTURE [MyStructure]   
(  
CustomerName TEXT KEY,  
Occupation TEXT DISCRETE,  
Age LONG CONTINUOUS,  
MaritalStatus TEXT DISCRETE,  
Income LONG CONTINUOUS,  
Products  TABLE  
 (  
    ProductNameTEXT KEY,  
    Quantity LONG CONTINUOUS,  
    OnSale BOOLEAN  DISCRETE  
)  
 Hobbies  TABLE  
 (  
    Hobby KEY  
 ))  
```  
  
 接下来，使用以下示例代码基于您刚刚创建的结构创建挖掘模型：  
  
```  
ALTER MINING STRUCTURE [MyStructure] ADD MINING MODEL [MyModel] (  
CustomerName,  
Age,  
MaritalStatus,  
Income PREDICT,  
Products   
(  
ProductName  
) WITH FILTER(NOT OnSale)  
) USING Microsoft_Decision_Trees   
WITH FILTER(EXISTS (Products))  
```  
  
### <a name="sample-query-1-returning-a-column-from-the-mining-structure"></a>示例查询 1：从挖掘结构返回列  
 以下示例查询返回作为挖掘模型一部分定义的 `CustomerName` 列和 `Age` 列。 但是，该查询还返回 `Age` 列，该列是结构的一部分，但不是挖掘模型的一部分。  
  
```  
SELECT CustomerName, Age, StructureColumn('Occupation') FROM MyModel.CASES   
WHERE Age > 30  
```  
  
 请注意，对将事例限制为 30 岁以上客户的行的筛选发生在模型级别。 因此，此表达式不会返回包含在结构数据中但模型不使用的事例。 由于用于创建模型的筛选条件 (`EXISTS (Products)`) 仅将事例限制为购买产品的那些客户，因此结构中还可能存在该查询没有返回的事例。  
  
### <a name="sample-query-2-applying-a-filter-to-the-structure-column"></a>示例查询 2：对结构列应用筛选器  
 以下示例查询不仅返回模型列 `CustomerName` 和 `Age` 以及嵌套表 `Products`，而且返回嵌套表中不是模型一部分的 `Quantity` 列的值。  
  
```  
SELECT CustomerName, Age,  
(SELECT ProductName, StructureColumn('Quantity') FROM Products) FROM MA.CASES   
WHERE StructureColumn('Occupation') = 'Architect'  
```  
  
 请注意，在此示例中，筛选器将应用于结构列，以将事例限制为其职业为 "架构师" （）的客户 `WHERE StructureColumn('Occupation') = 'Architect'` 。 由于创建模型时模型筛选条件始终应用于事例，因此只有在 `Products` 表中至少包含一个合格行的事例才包含在模型事例中。 因此，将应用针对嵌套表 `Products` 的筛选器和针对事例 `('Occupation')` 的筛选器。  
  
### <a name="sample-query-3-selecting-columns-from-a-nested-table"></a>示例查询 3：选择嵌套表中的列  
 以下示例查询从模型中返回用作培训事例的客户的姓名。 对于每个客户，查询还返回包含购买详细信息的嵌套表。 尽管模型包含 `ProductName` 列，但模型不使用列的值 `ProductName` 。 该模型仅检查产品是否是按常规（ `NOT``OnSale` ）价格购买的。 此查询不仅返回产品名称，而且返回未包含在模型中的购买的数量。  
  
```  
SELECT CustomerName,    
(SELECT ProductName, StructureColumn('Quantity')FROM Products)   
FROM MyModel.CASES  
```  
  
 请注意，不能返回 `ProductName` 列或 `Quantity` 列，除非对挖掘模型启用钻取。  
  
### <a name="sample-query-4-filtering-on-and-returning-nested-table-columns"></a>示例查询 4：筛选和返回嵌套表列  
 以下示例查询返回包含在挖掘结构中但不包含在模型中的事例和嵌套表列。 该模型已经针对是否为 `OnSale` 产品进行了筛选，但此查询将针对挖掘结构列 `Quantity` 添加筛选器：  
  
```  
SELECT CustomerName, Age, StructureColumn('Occupation'),   
(SELECT ProductName, StructureColumn('Quantity') FROM Products)   
FROM MyModel.CASES   
WHERE EXISTS (SELECT * FROM Products WHERE StructureColumn('Quantity')>1)  
```  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘扩展插件 &#40;DMX&#41; 函数参考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [函数 &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [&#40;DMX&#41;的常规预测函数](../dmx/general-prediction-functions-dmx.md)  
  
  
