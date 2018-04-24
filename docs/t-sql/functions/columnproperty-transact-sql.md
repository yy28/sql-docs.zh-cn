---
title: COLUMNPROPERTY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 5c26df937a654289c6a5313631a612bfbd386cc6
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="columnproperty-transact-sql"></a>COLUMNPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

返回有关列或参数的信息。
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```sql
COLUMNPROPERTY ( id , column , property )   
```  
  
## <a name="arguments"></a>参数  
*id*  
一个[表达式](../../t-sql/language-elements/expressions-transact-sql.md)，其中包含表或过程的标识符 (ID)。
  
*column*  
一个表达式，其中包含列或参数的名称。
  
property  
一个表达式，其中包含要为 id 返回的信息，可以为下列值之一。
  
|ReplTest1|Description|返回的值|  
|---|---|---|
|**AllowsNull**|允许空值。|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 输入无效。|  
|**ColumnId**|对应于 sys.columns.column_id 的列 ID 值。|列 ID<br /><br /> 请注意：查询多列时，列 ID 值的序列中可能出现间隔。|  
|**FullTextTypeColumn**|表中的 TYPE COLUMN，其中包含列的文档类型信息。|列的全文 TYPE COLUMN 的 ID，作为此属性的第二个参数传递。|  
|**IsComputed**|列是计算列。|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 输入无效。|  
|**IsCursorType**|过程参数类型为 CURSOR。|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 输入无效。|  
|**IsDeterministic**|列是确定性列。 此属性只适用于计算列和视图列。|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 输入无效。 非计算列或视图列。|  
|**IsFulltextIndexed**|列已经注册为全文索引。|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 输入无效。|  
|IsIdentity|列使用 IDENTITY 属性。|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 输入无效。|  
|IsIdNotForRepl|列检查 IDENTITY_INSERT 设置。|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 输入无效。|  
|**IsIndexable**|可以对列进行索引。|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 输入无效。|  
|**IsOutParam**|过程参数是输出参数。|1 = TRUE<br /><br /> 0 = FALSE NULL = 输入无效。|  
|**IsPrecise**|列是精确列。 此属性只适用于确定性列。|1 = TRUE<br /><br /> 0 = FALSE NULL = 输入无效。 不是确定性列|  
|**IsRowGuidCol**|列具有 uniqueidentifier 数据类型，并且使用 ROWGUIDCOL 属性定义。|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 输入无效。|  
|**IsSystemVerified**|列的确定性和精度属性可以使用[!INCLUDE[ssDE](../../includes/ssde-md.md)]验证。 此属性只应用于计算列和视图中的列。|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 输入无效。|  
|**IsXmlIndexable**|可以在 XML 索引中使用 XML 列。|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 输入无效。|  
|**精度**|列或参数的数据类型的长度。|指定的列数据类型的长度<br /><br /> -1 = xml 或大值类型<br /><br /> NULL = 输入无效。|  
|**小数位数**|列或参数的数据类型的小数位数。|比例<br /><br /> NULL = 输入无效。|  
|**StatisticalSemantics**|支持对列进行语义索引。|1 = TRUE<br /><br /> 0 = FALSE|  
|**SystemDataAccess**|列是由访问 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的系统目录或虚拟系统表中数据的函数派生的。 此属性只应用于计算列和视图中的列。|1 = TRUE（指示只读访问。）<br /><br /> 0 = FALSE<br /><br /> NULL = 输入无效。|  
|**UserDataAccess**|列是由访问储存于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 本地实例的用户表中数据的函数派生的。 此属性只应用于计算列和视图中的列。|1 = TRUE（指示只读访问。）<br /><br /> 0 = FALSE<br /><br /> NULL = 输入无效。|  
|**UsesAnsiTrim**|第一次创建表时，ANSI_PADDING 设置为 ON。 此属性仅适用于 char 或 varchar 类型的列或参数。|1= TRUE<br /><br /> 0= FALSE<br /><br /> NULL = 输入无效。|  
|**IsSparse**|列为稀疏列。 有关详细信息，请参阅 [使用稀疏列](../../relational-databases/tables/use-sparse-columns.md)。|1= TRUE<br /><br /> 0= FALSE<br /><br /> NULL = 输入无效。|  
|**IsColumnSet**|列为列集。 有关详细信息，请参阅 [使用列集](../../relational-databases/tables/use-column-sets.md)。|1= TRUE<br /><br /> 0= FALSE<br /><br /> NULL = 输入无效。|  
|**GeneratedAlwaysType**|由系统生成的列值。 对应于 sys.columns.generated_always_type|**适用范围**： [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 0 = 有时生成<br /><br /> 1 = 始终在行开始时生成<br /><br /> 2 = 始终在行结束时生成|  
|**IsHidden**|由系统生成的列值。 对应于 sys.columns.is_hidden|**适用范围**： [!INCLUDE[ssCurrentLong](../../includes/sscurrentlong-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 0 = 未隐藏<br /><br /> 1 = 隐藏|  
  
## <a name="return-types"></a>返回类型
 **int**  
  
## <a name="exceptions"></a>异常  
出现错误时或调用方没有查看对象的权限时，将返回 NULL。
  
用户只能查看符合如下条件的安全对象的元数据：该安全对象为该用户所有，或已授予该用户对该安全对象的权限。 这意味着，如果用户对对象没有任何权限，则元数据生成的内置函数（如 COLUMNPROPERTY）可能返回 NULL。 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。
  
## <a name="remarks"></a>Remarks  
检查列的确定性属性时，首先测试该列是否为计算列。 IsDeterministic 为非计算列返回 NULL。 可以将计算列指定为索引列。
  
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
[元数据函数 (Transact-SQL)](../../t-sql/functions/metadata-functions-transact-sql.md)  
[TYPEPROPERTY (Transact-SQL)](../../t-sql/functions/typeproperty-transact-sql.md)
  
  
