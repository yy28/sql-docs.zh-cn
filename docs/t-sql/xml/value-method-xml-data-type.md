---
title: "value （) 方法 (xml 数据类型) |Microsoft 文档"
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- value method
- value() method
ms.assetid: 298a7361-dc9a-4902-9b1e-49a093cd831d
caps.latest.revision: 38
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3b2cd81e4b96ce5c38a816c50728d794390bb383
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="value-method-xml-data-type"></a>value() 方法（xml 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  对 XML 执行 XQuery，并返回 SQL 类型的值。 此方法将返回标量值。  
  
 通常使用此方法来从存储在 XML 实例中提取值**xml**类型列、 参数或变量。 这样，您就可以指定将 XML 数据与非 XML 列中的数据进行合并或比较的 SELECT 查询。  
  
## <a name="syntax"></a>语法  
  
```  
  
value (XQuery, SQLType)  
```  
  
## <a name="arguments"></a>参数  
 *XQuery*  
 是*XQuery*表达式、 文本，检索 XML 实例内的数据的字符串。 XQuery 必须最多返回一个值。 否则，将返回错误。  
  
 *SQLType*  
 要返回的首选 SQL 类型（一种字符串文字）。 此方法的返回类型匹配*SQLType*参数。 *SQLType*不能为**xml**数据类型、 公共语言运行时 (CLR) 用户定义类型，**映像**，**文本**， **ntext**，或**sql_variant**数据类型。 *SQLType*可以是 SQL 用户定义数据类型。  
  
 **Value （)**方法使用[!INCLUDE[tsql](../../includes/tsql-md.md)]将隐式转换运算符，并尝试将结果的 XQuery 表达式，序列化的字符串表示形式，转换从 XSD 类型设置为由指定的相应SQL类型[!INCLUDE[tsql](../../includes/tsql-md.md)]转换。 转换类型强制转换规则的详细信息，请参阅[CAST 和 CONVERT &#40;Transact SQL &#41;](../../t-sql/functions/cast-and-convert-transact-sql.md).  
  
> [!NOTE]  
>  出于性能原因，而不是使用**value （)**中一个谓词，用于比较的关系的值，请使用方法**exist （)**与**sql:column()**。 如下面的示例 D 所示。  
  
## <a name="examples"></a>示例  
  
### <a name="a-using-the-value-method-against-an-xml-type-variable"></a>A. 对 xml 类型的变量使用 value() 方法  
 在下面的示例中，XML 实例存储在 `xml` 类型的变量中。 `value()` 方法从 XML 中检索 `ProductID` 属性值。 然后将该值分配给 `int` 变量。  
  
```  
DECLARE @myDoc xml  
DECLARE @ProdID int  
SET @myDoc = '<Root>  
<ProductDescription ProductID="1" ProductName="Road Bike">  
<Features>  
  <Warranty>1 year parts and labor</Warranty>  
  <Maintenance>3 year parts and labor extended maintenance is available</Maintenance>  
</Features>  
</ProductDescription>  
</Root>'  
  
SET @ProdID =  @myDoc.value('(/Root/ProductDescription/@ProductID)[1]', 'int' )  
SELECT @ProdID  
```  
  
 返回值 1 作为结果。  
  
 即使 XML 实例中仅有一个 `ProductID` 属性，静态类型化规则也会要求显式指定路径表达式返回 1。 因此，在路径表达式结尾处指定了另一个 `[1]`。 有关静态类型的详细信息，请参阅[的 XQuery 和静态类型](../../xquery/xquery-and-static-typing.md)。  
  
### <a name="b-using-the-value-method-to-retrieve-a-value-from-an-xml-type-column"></a>B. 使用 value() 方法从 xml 类型的列中检索值  
 下面的查询指定针对**xml**类型列 (`CatalogDescription`) 中`AdventureWorks`数据库。 查询从列中存储的每个 XML 实例中检索 `ProductModelID` 属性值。  
  
```  
SELECT CatalogDescription.value('             
    declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";             
       (/PD:ProductDescription/@ProductModelID)[1]', 'int') AS Result             
FROM Production.ProductModel             
WHERE CatalogDescription IS NOT NULL             
ORDER BY Result desc             
```  
  
 请注意上述查询的以下方面：  
  
-   `namespace` 关键字用于定义命名空间前缀。  
  
-   对于每个静态类型化要求，都在 `[1]` 方法的路径表达式结尾处添加 `value()` 以显式指示路径表达式返回 1。  
  
 下面是部分结果：  
  
```  
-----------  
35           
34           
...  
```  
  
### <a name="c-using-the-value-and-exist-methods-to-retrieve-values-from-an-xml-type-column"></a>C. 使用 value() 和 exist() 方法从 xml 类型的列中检索值  
 下面的示例演示使用`value()`方法和[exist （） 方法](../../t-sql/xml/exist-method-xml-data-type.md)的**xml**数据类型。 `value()` 方法用于从 XML 中检索 `ProductModelID` 属性值。 `exist()` 子句中的 `WHERE` 方法用于从表中筛选行。  
  
 此查询将从把保修信息（<`Warranty`> 元素）作为功能之一的 XML 实例中检索产品型号 ID。 `WHERE` 子句中的条件使用 `exist()` 方法仅检索满足该条件的行。  
  
```  
SELECT CatalogDescription.value('  
     declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
           (/PD:ProductDescription/@ProductModelID)[1] ', 'int') as Result  
FROM  Production.ProductModel  
WHERE CatalogDescription.exist('  
     declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     declare namespace wm="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain";  
  
     /PD:ProductDescription/PD:Features/wm:Warranty ') = 1  
```  
  
 请注意上述查询的以下方面：  
  
-   `CatalogDescription` 列是类型化的 XML 列。 这意味着它具有与其相关的架构集合。 在[XQuery Prolog](../../xquery/modules-and-prologs-xquery-prolog.md)，命名空间声明用于定义的前缀，使用更高版本中查询正文。  
  
-   如果 `exist()` 方法返回 `1` (True)，则指示 XML 实例包括 <`Warranty`> 子元素作为功能之一。  
  
-   然后，`value()` 子句中的 `SELECT` 方法将 `ProductModelID` 属性值作为整数进行检索。  
  
 下面是部分结果：  
  
```  
Result       
-----------  
19           
23           
...  
```  
  
### <a name="d-using-the-exist-method-instead-of-the-value-method"></a>D. 使用 exist() 方法而不使用 value() 方法  
 由于性能原因，不在谓词中使用 `value()` 方法与关系值进行比较，而改用具有 `exist()` 的 `sql:column()`。 例如：  
  
```  
CREATE TABLE T (c1 int, c2 varchar(10), c3 xml)  
GO  
  
SELECT c1, c2, c3   
FROM T  
WHERE c3.value( '/root[1]/@a', 'integer') = c1  
GO  
```  
  
 可以写入以下语句：  
  
```  
SELECT c1, c2, c3   
FROM T  
WHERE c3.exist( '/root[@a=sql:column("c1")]') = 1  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [使用 WITH XMLNAMESPACES 将命名空间添加到查询](../../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)   
 [类型化的 XML 与非类型化的 XML 的比较](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [创建 XML 数据的实例](../../relational-databases/xml/create-instances-of-xml-data.md)   
 [xml 数据类型方法](../../t-sql/xml/xml-data-type-methods.md)   
 [XML 数据修改语言 &#40;XML DML &#41;](../../t-sql/xml/xml-data-modification-language-xml-dml.md)  
  
  

