---
title: "query （) 方法 (xml 数据类型) |Microsoft 文档"
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
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
- query method
- query() method
ms.assetid: f48f6f7b-219f-463a-bf36-bc10f21afaeb
caps.latest.revision: 28
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: db0f9b1ffc4c6ca13084942144e13d64765d7019
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="query-method-xml-data-type"></a>query() 方法（xml 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  指定实例的 XQuery **xml**数据类型。 结果为**xml**类型。 该方法返回非类型化的 XML 实例。  
  
## <a name="syntax"></a>语法  
  
```  
  
query ('XQuery')  
```  
  
## <a name="arguments"></a>参数  
 XQuery  
 字符串，查询 XML 实例中的 XML 节点（如元素、属性）的 XQuery 表达式。  
  
## <a name="examples"></a>示例  
 本部分提供使用 query （） 方法的示例**xml**数据类型。  
  
### <a name="a-using-the-query-method-against-an-xml-type-variable"></a>A. 对 xml 类型的变量使用 query() 方法  
 下面的示例声明一个变量 **@myDoc** 的**xml**键入，然后将 XML 实例分配给它。 **Query （)**方法然后用于对文档指定 XQuery。  
  
 该查询检索 <`ProductDescription`> 元素的 <`Features`> 子元素：  
  
```  
declare @myDoc xml  
set @myDoc = '<Root>  
<ProductDescription ProductID="1" ProductName="Road Bike">  
<Features>  
  <Warranty>1 year parts and labor</Warranty>  
  <Maintenance>3 year parts and labor extended maintenance is available</Maintenance>  
</Features>  
</ProductDescription>  
</Root>'  
SELECT @myDoc.query('/Root/ProductDescription/Features')  
```  
  
 结果如下：  
  
```  
<Features>  
  <Warranty>1 year parts and labor</Warranty>  
  <Maintenance>3 year parts and labor extended maintenance is available</Maintenance>  
</Features>        
```  
  
### <a name="b-using-the-query-method-against-an-xml-type-column"></a>B. 对 XML 类型列使用 query() 方法  
 在下面的示例中， **query （)**方法用于对指定 XQuery **CatalogDescription**列**xml**键入**AdventureWorks**数据库：  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
<Product ProductModelID="{ /PD:ProductDescription[1]/@ProductModelID }" />  
') as Result  
FROM Production.ProductModel  
where CatalogDescription.exist('  
declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
declare namespace wm="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain";  
     /PD:ProductDescription/PD:Features/wm:Warranty ') = 1  
```  
  
 请注意上述查询的以下方面：  
  
-   CatalogDescription 列是类型化**xml**列。 这表示它包含一个与之相关联的架构集合。 在[XQuery Prolog](../../xquery/modules-and-prologs-xquery-prolog.md)、**命名空间**关键字用于查询正文中定义的前缀，在以后使用。  
  
-   **Query （)**方法构造 XML，<`Product`> 元素，该元素**ProductModelID**属性，在其中**ProductModelID**属性值是从数据库中检索。 有关 XML 构造的详细信息，请参阅[XML 构造 &#40;XQuery &#41;](../../xquery/xml-construction-xquery.md).  
  
-   [Exist （） 方法 （XML 数据类型）](../../t-sql/xml/exist-method-xml-data-type.md)在 WHERE 子句用于查找包含的行 <`Warranty`> 的 XML 中的元素。 同样，**命名空间**关键字用于定义两个命名空间前缀。  
  
 下面是部分结果：  
  
```  
<Product ProductModelID="19"/>   
<Product ProductModelID="23"/>   
...  
```  
  
 请注意，query() 方法和 exist() 方法都声明 PD 前缀。 在这些情况下，可以使用 WITH XMLNAMESPACES 首先定义前缀，然后在查询中使用它。  
  
```  
WITH XMLNAMESPACES (  
   'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS PD,  
   'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain' AS wm)  
SELECT CatalogDescription.query('  
<Product ProductModelID="{ /PD:ProductDescription[1]/@ProductModelID }" />  
') as Result  
FROM Production.ProductModel  
where CatalogDescription.exist('  
     /PD:ProductDescription/PD:Features/wm:Warranty ') = 1  
```  
  
## <a name="see-also"></a>另请参阅  
 [使用 WITH XMLNAMESPACES 将命名空间添加到查询](../../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)   
 [类型化的 XML 与非类型化的 XML 的比较](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [创建 XML 数据的实例](../../relational-databases/xml/create-instances-of-xml-data.md)   
 [xml 数据类型方法](../../t-sql/xml/xml-data-type-methods.md)   
 [XML 数据修改语言 &#40;XML DML &#41;](../../t-sql/xml/xml-data-modification-language-xml-dml.md)  
  
  

