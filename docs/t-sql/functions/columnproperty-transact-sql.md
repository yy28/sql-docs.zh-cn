---
title: "COLUMNPROPERTY (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- COLUMNPROPERTY
- COLUMNPROPERTY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- column properties [SQL Server]
- parameters [SQL Server], properties
- COLUMNPROPERTY function
ms.assetid: 2408c264-6eca-4120-bb71-df043c7c2792
caps.latest.revision: 44
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 80c1228faeaaa4012afc0fd27992a2f5cf389f6e
ms.openlocfilehash: c6c2af8d231f03c40ee87d3468977c3b66cbeeb4
ms.contentlocale: zh-cn
ms.lasthandoff: 10/05/2017

---
# <a name="columnproperty-transact-sql"></a>COLUMNPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

返回有关列或参数的信息。
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```sql
COLUMNPROPERTY ( id , column , property )   
```  
  
## <a name="arguments"></a>参数  
*id*  
是[表达式](../../t-sql/language-elements/expressions-transact-sql.md)，其中包含的表或过程的标识符 (ID)。
  
*列*  
一个表达式，其中包含列或参数的名称。
  
*属性*  
是一个包含要为返回的信息的表达式*id*，并且可以是以下值之一。
  
|值|Description|返回的值|  
|---|---|---|
|**AllowsNull**|允许空值。|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 输入无效。|  
|**ColumnId**|列 ID 值对应于**sys.columns.column_id**。|列 ID<br /><br /> **注意：**顺序的列 ID 值可能会出现在查询多个列，间距。|  
|**FullTextTypeColumn**|包含文档类型信息的表中的类型列*列*。|列的全文 TYPE COLUMN 的 ID，作为此属性的第二个参数传递。|  
|**IsComputed**|列是计算列。|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 输入无效。|  
|**IsCursorType**|过程参数类型为 CURSOR。|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 输入无效。|  
|**IsDeterministic**|列是确定性列。 此属性只适用于计算列和视图列。|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 输入无效。 非计算列或视图列。|  
|**IsFulltextIndexed**|列已经注册为全文索引。|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 输入无效。|  
|**IsIdentity**|列使用 IDENTITY 属性。|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 输入无效。|  
|**IsIdNotForRepl**|列检查 IDENTITY_INSERT 设置。|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 输入无效。|  
|**IsIndexable**|可以对列进行索引。|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 输入无效。|  
|**IsOutParam**|过程参数是输出参数。|1 = TRUE<br /><br /> 0 = FALSE NULL = 输入无效。|  
|**IsPrecise**|列是精确列。 此属性只适用于确定性列。|1 = TRUE<br /><br /> 0 = FALSE NULL = 输入无效。 不是确定性列|  
|**IsRowGuidCol**|列具有**uniqueidentifier**数据类型和具有 ROWGUIDCOL 属性定义。|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 输入无效。|  
|**IsSystemVerified**|列的确定性和精度属性可以使用[!INCLUDE[ssDE](../../includes/ssde-md.md)]验证。 此属性只应用于计算列和视图中的列。|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 输入无效。|  
|**IsXmlIndexable**|可以在 XML 索引中使用 XML 列。|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 输入无效。|  
|**精度**|列或参数的数据类型的长度。|指定的列数据类型的长度<br /><br /> 为-1 = **xml**或较大的值类型<br /><br /> NULL = 输入无效。|  
|**小数位数**|列或参数的数据类型的小数位数。|小数位数<br /><br /> NULL = 输入无效。|  
|**StatisticalSemantics**|支持对列进行语义索引。|1 = TRUE<br /><br /> 0 = FALSE|  
|**将 SystemDataAccess**|列是由访问 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的系统目录或虚拟系统表中数据的函数派生的。 此属性只应用于计算列和视图中的列。|1 = TRUE（指示只读访问。）<br /><br /> 0 = FALSE<br /><br /> NULL = 输入无效。|  
|**UserDataAccess**|列是由访问储存于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 本地实例的用户表中数据的函数派生的。 此属性只应用于计算列和视图中的列。|1 = TRUE（指示只读访问。）<br /><br /> 0 = FALSE<br /><br /> NULL = 输入无效。|  
|**UsesAnsiTrim**|第一次创建表时，ANSI_PADDING 设置为 ON。 此属性仅适用于列或参数的类型**char**或**varchar**。|1= TRUE<br /><br /> 0= FALSE<br /><br /> NULL = 输入无效。|  
|**IsSparse**|列为稀疏列。 有关详细信息，请参阅 [使用稀疏列](../../relational-databases/tables/use-sparse-columns.md)。|1= TRUE<br /><br /> 0= FALSE<br /><br /> NULL = 输入无效。|  
|**IsColumnSet**|列为列集。 有关详细信息，请参阅 [使用列集](../../relational-databases/tables/use-column-sets.md)。|1= TRUE<br /><br /> 0= FALSE<br /><br /> NULL = 输入无效。|  
|**GeneratedAlwaysType**|是由系统生成的列的值。 对应于**sys.columns.generated_always_type**|**适用范围**： [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 0 = 不生成始终<br /><br /> 1 = Generated always 作为行开始<br /><br /> 2 – generated always 作为行结束|  
|**IsHidden**|是由系统生成的列的值。 对应于**sys.columns.is_hidden**|**适用范围**： [!INCLUDE[ssCurrentLong](../../includes/sscurrentlong-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 0 = 不隐藏<br /><br /> 1 = Hidden|  
  
## <a name="return-types"></a>返回类型
 **int**  
  
## <a name="exceptions"></a>异常  
出现错误时或调用方没有查看对象的权限时，将返回 NULL。
  
用户只能查看符合如下条件的安全对象的元数据：该安全对象为该用户所有，或已授予该用户对该安全对象的权限。 这意味着，如果用户对对象没有任何权限，则元数据生成的内置函数（如 COLUMNPROPERTY）可能返回 NULL。 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。
  
## <a name="remarks"></a>注释  
检查列的确定性属性时，首先测试该列是否为计算列。 **IsDeterministic**未计算列，则返回 NULL。 可以将计算列指定为索引列。
  
## <a name="examples"></a>示例  
以下示例将返回 `LastName` 列的长度。
  
```sql
USE AdventureWorks2012;  
GO  
SELECT COLUMNPROPERTY( OBJECT_ID('Person.Person'),'LastName','PRECISION')AS 'Column Length';  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
Column Length
-------------
50
```  
  
## <a name="see-also"></a>另请参阅
[元数据函数 &#40;Transact SQL &#41;](../../t-sql/functions/metadata-functions-transact-sql.md)  
[TYPEPROPERTY &#40;Transact SQL &#41;](../../t-sql/functions/typeproperty-transact-sql.md)
  
  

