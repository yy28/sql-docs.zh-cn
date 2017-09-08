---
title: "sql: variable 函数 (XQuery) |Microsoft 文档"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
dev_langs:
- XML
helpviewer_keywords:
- sql:variable() function
- sql:variable function
ms.assetid: 6e2e5063-c1cf-4b5a-b642-234921e3f4f7
caps.latest.revision: 36
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ffacec1b08bd0fa4fed107a1149273034057e405
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="xquery-extension-functions---sqlvariable"></a>XQuery 扩展函数-sql: variable
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  显示在 XQuery 表达式中包含 SQL 关系值的变量。  
  
## <a name="syntax"></a>语法  
  
```  
  
sql:variable("variableName") as xdt:anyAtomicType?  
```  
  
## <a name="remarks"></a>注释  
 本主题中所述[绑定关系的数据在 XML](../t-sql/xml/binding-relational-data-inside-xml-data.md)，当你使用时，可以使用此函数[XML 数据类型方法](../t-sql/xml/xml-data-type-methods.md)公开内 XQuery 关系的值。  
  
 例如， [query （） 方法](../t-sql/xml/query-method-xml-data-type.md)用于指定对 XML 实例中存储查询**xml**数据类型变量或列。 有时，您可能还希望查询使用 [!INCLUDE[tsql](../includes/tsql-md.md)] 变量或参数中的值同时引入关系数据和 XML 数据。 若要执行此操作，请使用**sql: variable**函数。  
  
 SQL 值将映射到相应的 XQuery 值，其类型将是 XQuery 基类型，它等效于相应的 SQL 类型。  
  
 你只能引用**xml**实例的上下文中的 XML DML 的源表达式 insert 语句; 否则不能引用类型的值中**xml**或公共语言运行时 (CLR)用户定义的类型。  
  
## <a name="examples"></a>示例  
  
### <a name="a-using-the-sqlvariable-function-to-bring-a-transact-sql-variable-value-into-xml"></a>A. 使用 sql:variable() 函数将 Transact-SQL 变量值放到 XML 中  
 以下示例构造由下列值组成的 XML 实例：  
  
-   非 XML 列中的值 (`ProductID`)。 [Sql:column() 函数](../xquery/xquery-extension-functions-sql-column.md)用于 XML 中将此值。  
  
-   另一个表中非 XML 列中的值 (`ListPrice`)。 同样，`sql:column()` 用于在 XML 中绑定此值。  
  
-   [!INCLUDE[tsql](../includes/tsql-md.md)] 变量中的值 (`DiscountPrice`)。 `sql:variable()` 方法用于将此值绑定到 XML。  
  
-   一个值 (`ProductModelName`) 从**xml**类型列中，为使查询能够更加有趣。  
  
 以下是查询语句：  
  
```  
DECLARE @price money  
  
SET @price=2500.00  
SELECT ProductID, Production.ProductModel.ProductModelID,CatalogDescription.query('  
declare namespace pd="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
  
       <Product   
           ProductID="{ sql:column("Production.Product.ProductID") }"  
           ProductModelID= "{ sql:column("Production.Product.ProductModelID") }"  
           ProductModelName="{/pd:ProductDescription[1]/@ProductModelName }"  
           ListPrice="{ sql:column("Production.Product.ListPrice") }"  
           DiscountPrice="{ sql:variable("@price") }"  
        />')   
FROM Production.Product   
JOIN Production.ProductModel  
ON Production.Product.ProductModelID = Production.ProductModel.ProductModelID  
WHERE ProductID=771  
```  
  
 请注意上述查询的以下方面：  
  
-   `query()` 方法中的 XQuery 构造 XML。  
  
-   `namespace`关键字用于定义命名空间前缀的[XQuery Prolog](../xquery/modules-and-prologs-xquery-prolog.md)。 执行此操作的原因为 `ProductModelName` 属性值是从 `CatalogDescription xml` 类型列（具有与其关联的架构）中检索的。  
  
 结果如下：  
  
```  
<Product ProductID="771" ProductModelID="19"   
         ProductModelName="Mountain 100"   
         ListPrice="3399.99" DiscountPrice="2500" />  
```  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server XQuery 扩展函数](http://msdn.microsoft.com/library/4bc5d499-5fec-4c3f-b11e-5ab5ef9d8f97)   
 [类型化的 XML 与非类型化的 XML 的比较](../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [XML 数据 (SQL Server)](../relational-databases/xml/xml-data-sql-server.md)   
 [创建 XML 数据的实例](../relational-databases/xml/create-instances-of-xml-data.md)   
 [xml 数据类型方法](../t-sql/xml/xml-data-type-methods.md)   
 [XML 数据修改语言 &#40;XML DML &#41;](../t-sql/xml/xml-data-modification-language-xml-dml.md)  
  
  
