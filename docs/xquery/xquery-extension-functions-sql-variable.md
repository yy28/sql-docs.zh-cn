---
title: sql：可变（） 函数 （XQuery） |微软文档
description: 了解如何使用 XQuery 扩展函数 sql：variable（） 公开包含 XQuery 表达式中的 SQL 关系值的变量。
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- sql:variable() function
- sql:variable function
ms.assetid: 6e2e5063-c1cf-4b5a-b642-234921e3f4f7
author: rothja
ms.author: jroth
ms.openlocfilehash: 8241e15643eb4aa25912451ddfed94699954797f
ms.sourcegitcommit: a3f5c3742d85d21f6bde7c6ae133060dcf1ddd44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/15/2020
ms.locfileid: "81388607"
---
# <a name="xquery-extension-functions---sqlvariable"></a>XQuery 扩展函数 - sql:variable()
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  显示在 XQuery 表达式中包含 SQL 关系值的变量。  
  
## <a name="syntax"></a>语法  
  
```  
  
sql:variable("variableName") as xdt:anyAtomicType?  
```  
  
## <a name="remarks"></a>备注  
 如在主题[绑定关系数据在XML中](../t-sql/xml/binding-relational-data-inside-xml-data.md)所述，当使用[XML数据类型方法](../t-sql/xml/xml-data-type-methods.md)在XQuery中公开关系值时，可以使用此功能。  
  
 例如[，query（） 方法](../t-sql/xml/query-method-xml-data-type.md)用于指定针对存储在**xml**数据类型变量或列中的 XML 实例的查询。 有时，您可能还希望查询使用 [!INCLUDE[tsql](../includes/tsql-md.md)] 变量或参数中的值同时引入关系数据和 XML 数据。 为此，请使用**sql：变量**函数。  
  
 SQL 值将映射到相应的 XQuery 值，其类型将是等效于相应 SQL 类型的 XQuery 基类型。  
  
 只能在 XML-DML 插入语句的源表达式上下文中引用**xml**实例;否则，您不能引用类型**为 xml**或通用语言运行时 （CLR） 用户定义的类型的值。  
  
## <a name="examples"></a>示例  
  
### <a name="a-using-the-sqlvariable-function-to-bring-a-transact-sql-variable-value-into-xml"></a>A. 使用 sql:variable() 函数将 Transact-SQL 变量值放到 XML 中  
 以下示例构造由下列值组成的 XML 实例：  
  
-   非 XML 列中的值 (`ProductID`)。 [sql：列（）函数](../xquery/xquery-extension-functions-sql-column.md)用于在 XML 中绑定此值。  
  
-   另一个表中非 XML 列中的值 (`ListPrice`)。 同样，`sql:column()` 用于在 XML 中绑定此值。  
  
-   [!INCLUDE[tsql](../includes/tsql-md.md)] 变量中的值 (`DiscountPrice`)。 `sql:variable()` 方法用于将此值绑定到 XML。  
  
-   xml 类型`ProductModelName`列中的值**xml**（ ）， 以使查询更有趣。  
  
 以下是查询语句：  
  
```sql
DECLARE @price money  
  
SET @price=2500.00  
SELECT ProductID, Production.ProductModel.ProductModelID,CatalogDescription.query('  
declare namespace pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
  
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
  
-   该`namespace`关键字用于在[XQuery Prolog](../xquery/modules-and-prologs-xquery-prolog.md)中定义命名空间前缀。 执行此操作的原因为 `ProductModelName` 属性值是从 `CatalogDescription xml` 类型列（具有与其关联的架构）中检索的。  
  
 结果如下：  
  
```xml
<Product ProductID="771" ProductModelID="19"   
         ProductModelName="Mountain 100"   
         ListPrice="3399.99" DiscountPrice="2500" />  
```  
  
## <a name="see-also"></a>另请参阅  
 [SQL 服务器 XQuery 扩展函数](https://msdn.microsoft.com/library/4bc5d499-5fec-4c3f-b11e-5ab5ef9d8f97)   
 [将键入的 XML 与未键入的 XML 进行比较](../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [XML 数据&#40;SQL 服务器&#41;](../relational-databases/xml/xml-data-sql-server.md)   
 [创建 XML 数据的实例](../relational-databases/xml/create-instances-of-xml-data.md)   
 [xml 数据类型方法](../t-sql/xml/xml-data-type-methods.md)   
 [XML 数据修改语言 (XML DML)](../t-sql/xml/xml-data-modification-language-xml-dml.md)  
  
  
