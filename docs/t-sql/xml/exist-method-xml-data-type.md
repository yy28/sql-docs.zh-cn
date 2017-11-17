---
title: "exist （) 方法 (xml 数据类型) |Microsoft 文档"
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|xml
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- exist() method
- exist method
ms.assetid: a55b75e0-0a17-4787-a525-9b095410f7af
caps.latest.revision: 35
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0e152abc34c459d82f451c5ded02d30f5fb76b23
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="exist-method-xml-data-type"></a>exist() 方法（xml 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  返回**位**表示以下条件之一：  
  
-   1，表示 True（如果查询中的 XQuery 表达式返回一个非空结果）。 即，它至少返回一个 XML 节点。  
  
-   0，表示 False（如果它返回一个空结果）。  
  
-   如果**xml**执行查询时所依据的数据类型实例包含空值。  
  
## <a name="syntax"></a>语法  
  
```  
  
exist (XQuery)   
```  
  
## <a name="arguments"></a>参数  
 XQuery  
 是一个 XQuery 表达式，字符串文字。  
  
## <a name="remarks"></a>注释  
  
> [!NOTE]  
>  **Exist （)**方法返回 1 返回非空的结果的 XQuery 表达式。 如果指定**true()**或**false （)**函数内**exist （)**方法， **exist （)**方法将返回 1，因为函数**true()**和**false （)**分别返回布尔值 True 和 False。 也就是说，它们将返回非空结果。 因此， **exist （)**将返回 1 (True)，如下面的示例中所示：  
  
```  
declare @x xml;  
set @x='';  
select @x.exist('true()');   
```  
  
## <a name="examples"></a>示例  
 下面的示例演示如何指定**exist （)**方法。  
  
### <a name="example-specifying-the-exist-method-against-an-xml-type-variable"></a>示例：对 xml 类型变量指定 exist() 方法  
 在下面的示例中，@x 是 **xml** 类型变量 (非类型化 xml) 和 @f 是一个整数类型变量，将存储返回的值 **exist （)** 方法。 **Exist （)**方法返回 True (1)，如果 XML 实例中存储的日期值是`2002-01-01`。  
  
```  
declare @x xml;  
declare @f bit;  
set @x = '<root Somedate = "2002-01-01Z"/>';  
set @f = @x.exist('/root[(@Somedate cast as xs:date?) eq xs:date("2002-01-01Z")]');  
select @f;  
```  
  
 在比较中的日期**exist （)**方法，请注意以下事项：  
  
-   代码`cast as xs:date?`用于将值强制转换**xs: date**的用途的比较类型。  
  
-   值 **@Somedate** 属性是非类型化。 在将此值进行比较，它被隐式强制转换为比较的右侧类型**xs: date**类型。  
  
-   而不是**强制转换为 xs:date()**，你可以使用**xs:date()**构造函数。 有关详细信息，请参阅[构造函数 &#40;XQuery &#41;](../../xquery/constructor-functions-xquery.md).  
  
 下面的示例与上一示例类似，不同之处在于它具有 <`Somedate`> 元素。  
  
```  
DECLARE @x xml;  
DECLARE @f bit;  
SET @x = '<Somedate>2002-01-01Z</Somedate>';  
SET @f = @x.exist('/Somedate[(text()[1] cast as xs:date ?) = xs:date("2002-01-01Z") ]')  
SELECT @f;  
```  
  
 请注意上述查询的以下方面：  
  
-   **Text （)**方法返回一个包含非类型化的值的文本节点`2002-01-01`。 (XQuery 类型是**xdt:untypedAtomic**。)必须显式强制转换此类型化的值从**x**到**xsd:date**，因为在这种情况下不支持隐式强制转换。  
  
### <a name="example-specifying-the-exist-method-against-a-typed-xml-variable"></a>示例：对类型化 xml 变量指定 exist() 方法  
 下面的示例演示如何使用**exist （)**方法依据**xml**类型变量。 它是类型化的 XML 变量，因为它指定了架构命名空间集合名称 `ManuInstructionsSchemaCollection`。  
  
 在示例中，文档首先分配给此变量生产说明，然后**exist （)**使用方法来查找该文档是否包含 <`Location`> 元素其**LocationID**属性值为 50。  
  
 **Exist （)**方法对指定@x变量返回 1 (True)，如果文档包含的生产说明 <`Location`> 元素，该元素`LocationID=50`。 否则，该方法返回 0 (False)。  
  
```  
DECLARE @x xml (Production.ManuInstructionsSchemaCollection);  
SELECT @x=Instructions  
FROM Production.ProductModel  
WHERE ProductModelID=67;  
--SELECT @x  
DECLARE @f int;  
SET @f = @x.exist(' declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
    /AWMI:root/AWMI:Location[@LocationID=50]  
');  
SELECT @f;  
```  
  
### <a name="example-specifying-the-exist-method-against-an-xml-type-column"></a>示例：对 xml 类型列指定 exist() 方法  
 下面的查询检索的是目录说明中不包括规范（<`Specifications`> 元素）的产品型号 ID：  
  
```  
SELECT ProductModelID, CatalogDescription.query('  
declare namespace pd="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
    <Product   
        ProductModelID= "{ sql:column("ProductModelID") }"   
        />  
') AS Result  
FROM Production.ProductModel  
WHERE CatalogDescription.exist('  
    declare namespace  pd="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     /pd:ProductDescription[not(pd:Specifications)]'  
    ) = 1;  
```  
  
 请注意上述查询的以下方面：  
  
-   WHERE 子句选择仅从这些行**ProductDescription**满足针对指定的条件的表**CatalogDescription xml**类型列。  
  
-   **Exist （)**方法中的 WHERE 子句将返回 1 (True)，如果 XML 中不包括任何 <`Specifications`> 元素。 请注意，使用[not() 函数 (XQuery)](../../xquery/functions-on-boolean-values-not-function.md)。  
  
-   [Sql:column() 函数 (XQuery)](../../xquery/xquery-extension-functions-sql-column.md)函数用于从非 XML 列中值引入。  
  
-   此查询返回一个空的行集。  
  
 该查询指定**query （)**和**exist （)** xml 数据类型方法，这两种方法声明相同的命名空间在查询 prolog 中。 在本例中，可能需要使用 WITH XMLNAMESPACES 来声明前缀并在查询中使用它。  
  
```  
WITH XMLNAMESPACES ('http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd)  
SELECT ProductModelID, CatalogDescription.query('  
    <Product   
        ProductModelID= "{ sql:column("ProductModelID") }"   
        />  
') AS Result  
FROM Production.ProductModel  
WHERE CatalogDescription.exist('  
     /pd:ProductDescription[not(pd:Specifications)]'  
    ) = 1;  
```  
  
## <a name="see-also"></a>另请参阅  
 [使用 WITH XMLNAMESPACES 将命名空间添加到查询](../../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)   
 [类型化的 XML 与非类型化的 XML 的比较](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [创建 XML 数据的实例](../../relational-databases/xml/create-instances-of-xml-data.md)   
 [xml 数据类型方法](../../t-sql/xml/xml-data-type-methods.md)   
 [XML 数据修改语言 &#40;XML DML &#41;](../../t-sql/xml/xml-data-modification-language-xml-dml.md)  
  
  

