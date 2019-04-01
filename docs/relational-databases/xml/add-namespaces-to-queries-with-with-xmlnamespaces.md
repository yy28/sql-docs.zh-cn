---
title: 使用 WITH XMLNAMESPACES 将命名空间添加到查询 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- ELEMENTS XSINIL directive
- adding namespaces
- XSINIL directive
- default namespaces
- queries [XML in SQL Server], WITH XMLNAMESPACES clause
- predefined namespaces [XML in SQL Server]
- FOR XML clause, WITH XMLNAMESPACES clause
- namespaces [XML in SQL Server]
- xml data type [SQL Server], WITH XMLNAMESPACES clause
- WITH XMLNAMESPACES clause
ms.assetid: 2189cb5e-4460-46c5-a254-20c833ebbfec
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1905daf01b919e3e661b4c93302418c418cf7b69
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "58511474"
---
# <a name="add-namespaces-to-queries-with-with-xmlnamespaces"></a>使用 WITH XMLNAMESPACES 将命名空间添加到查询
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  [WITH XMLNAMESPACES (Transact-SQL)](../../t-sql/xml/with-xmlnamespaces.md) 按以下方式提供对命名空间 URI 支持：  
  
-   在 [使用 FOR XML 查询构造 XML](../../relational-databases/xml/for-xml-sql-server.md) 时，它可以使命名空间前缀到 URI 的映射可用。  
  
-   它使命名空间到 URI 的映射对 [xml 数据类型方法](../../t-sql/xml/xml-data-type-methods.md)的静态命名空间上下文可用。  
  
## <a name="using-with-xmlnamespaces-in-the-for-xml-queries"></a>在 FOR XML 查询中使用 WITH XMLNAMESPACES  
 WITH XMLNAMESPACES 允许您在 FOR XML 查询中包含 XML 命名空间。 例如，考虑下列 FOR XML 查询：  
  
```  
SELECT ProductID, Name, Color  
FROM   Production.Product  
WHERE  ProductID=316 or ProductID=317  
FOR XML RAW  
```  
  
 结果如下：  
  
```  
<row ProductID="316" Name="Blade" />  
<row ProductID="317" Name="LL Crankarm" Color="Black" />  
  
```  
  
 若要向 FOR XML 查询构造的 XML 添加命名空间，请先使用 WITH NAMESPACES 子句指定命名空间前缀到 URI 的映射。 然后，使用命名空间前缀在查询中指定名称，如下列修改的查询所示。 请注意，WITH XMLNAMESPACES 子句指定命名空间前缀 (`ns1`) 到 URI (`uri`) 的映射。 然后 `ns1` 前缀用来指定 FOR XML 查询要构造的元素名称和属性名称。  
  
```  
WITH XMLNAMESPACES ('uri' as ns1)  
SELECT ProductID as 'ns1:ProductID',  
       Name      as 'ns1:Name',   
       Color     as 'ns1:Color'  
FROM Production.Product  
WHERE ProductID=316 or ProductID=317  
FOR XML RAW ('ns1:Prod'), ELEMENTS  
  
```  
  
 XML 结果包含命名空间前缀：  
  
```  
<ns1:Prod xmlns:ns1="uri">  
  <ns1:ProductID>316</ns1:ProductID>  
  <ns1:Name>Blade</ns1:Name>  
</ns1:Prod>  
<ns1:Prod xmlns:ns1="uri">  
  <ns1:ProductID>317</ns1:ProductID>  
  <ns1:Name>LL Crankarm</ns1:Name>  
  <ns1:Color>Black</ns1:Color>  
</ns1:Prod>  
  
```  
  
 下列内容适用于 WITH XMLNAME 子句：  
  
-   只有在 FOR XML 查询的 RAW、AUTO 和 PATH 模式中才支持该子句。 EXPLICIT 模式不支持该子句。  
  
-   该子句仅影响 FOR XML 查询的命名空间前缀和 **xml** 数据类型方法，而不影响 XML 分析器。 例如，下列查询将返回一个错误，因为 XML 文档没有为 myNS 前缀声明命名空间。  
  
-   使用 WITH XMLNAMESPACES 子句时，不能使用 FOR XML 指令 XMLSCHEMA 和 XMLDATA。  
  
    ```  
    CREATE TABLE T (x xml)  
    go  
    WITH XMLNAMESPACES ('https://abc' as myNS )  
    INSERT INTO T VALUES('<myNS:root/>')  
    ```  
  
## <a name="using-the-xsinil-directive"></a>使用 XSINIL 指令  
 如果使用的是 ELEMENTS XSINI 指令，则无法在 WITH XMLNAMESPACES 子句中定义 xsi 前缀。 但是，在使用 ELEMENTS XSINIL 时会自动添加该前缀。 下列查询使用了生成以元素为中心的 XML 的 ELEMENTS XSINIL 指令，在此 XML 中 Null 值映射到将 **xsi:nil** 属性设置为 True 的元素。  
  
```  
WITH XMLNAMESPACES ('uri' as ns1)  
SELECT ProductID as 'ns1:ProductID',  
       Name      as 'ns1:Name',   
       Color     as 'ns1:Color'  
FROM Production.Product  
WHERE ProductID=316   
FOR XML RAW, ELEMENTS XSINIL  
```  
  
 结果如下：  
  
```  
<row xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:ns1="uri">  
  <ns1:ProductID>316</ns1:ProductID>  
  <ns1:Name>Blade</ns1:Name>  
  <ns1:Color xsi:nil="true" />  
</row>  
```  
  
## <a name="specifying-default-namespaces"></a>指定默认的命名空间  
 可以使用 DEFAULT 关键字声明默认的命名空间来代替声明命名空间前缀。 在 FOR XML 查询中，这会将默认的命名空间绑定到所得到的 XML 中的 XML 节点。 在下列示例中，WITH XMLNAMESPA 定义了两个和默认的命名空间一起定义的命名空间前缀。  
  
```  
WITH XMLNAMESPACES ('uri1' as ns1,   
                    'uri2' as ns2,  
                    DEFAULT 'uri2')  
SELECT ProductID,   
      Name,  
      Color  
FROM Production.Product   
WHERE ProductID=316 or ProductID=317  
FOR XML RAW ('ns1:Product'), ROOT('ns2:root'), ELEMENTS  
```  
  
 FOR XML 查询生成以元素为中心的 XML。 请注意，此查询使用两个命名空间前缀来命名节点。 在 SELECT 子句中，ProductID、Name 和 Color 不指定带有任何前缀的名称。 因此，所得到的 XML 中的相应元素属于默认的命名空间。  
  
```  
<ns2:root xmlns="uri2" xmlns:ns2="uri2" xmlns:ns1="uri1">  
  <ns1:Product>  
    <ProductID>316</ProductID>  
    <Name>Blade</Name>  
  </ns1:Product>  
  <ns1:Product>  
    <ProductID>317</ProductID>  
    <Name>LL Crankarm</Name>  
    <Color>Black</Color>  
  </ns1:Product>  
</ns2:root>  
```  
  
 下列查询与前一个查询类似，只是指定了 FOR XML AUTO 模式。  
  
```  
WITH XMLNAMESPACES ('uri1' as ns1,  'uri2' as ns2,DEFAULT 'uri2')  
SELECT ProductID,   
      Name,  
      Color  
FROM Production.Product as "ns1:Product"  
WHERE ProductID=316 or ProductID=317  
FOR XML AUTO, ROOT('ns2:root'), ELEMENTS  
```  
  
## <a name="using-predefined-namespaces"></a>使用预定义的命名空间  
 当使用预定义命名空间时（若 ELEMENTS XSINIL 时，则不包括 xml 命名空间和 xsi 命名空间），必须使用 WITH XMLNAMESPAC 显式指定命名空间绑定。 下列查询为预定义命名空间 (`urn:schemas-microsoft-com:xml-sql`) 显式定义了命名空间前缀到 URI 的绑定。  
  
```  
WITH XMLNAMESPACES ('urn:schemas-microsoft-com:xml-sql' as sql)  
SELECT 'SELECT * FROM Customers FOR XML AUTO, ROOT("a")' AS "sql:query"  
FOR XML PATH('sql:root')  
```  
  
 结果如下： SQLXML 用户熟悉此 XML 模板。 有关详细信息，请参阅 [SQLXML 4.0 编程概念](../../relational-databases/sqlxml/sqlxml-4-0-programming-concepts.md)。  
  
```  
<sql:root xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <sql:query>SELECT * FROM Customers FOR XML AUTO, ROOT("a")</sql:query>  
</sql:root>  
```  
  
 只有 xml 命名空间无须在 WITH XMLNAMESPAC 中显式定义即可使用，如下列 PATH 模式查询所示。 此外，如果声明了前缀，则前缀必须绑定到命名空间 http://www.w3.org/XML/1998/namespace。 在 SELECT 子句中指定的名称将引用未使用 WITH XMLNAMESPACES 进行显式定义的 xml 命名空间前缀。  
  
```  
SELECT 'en'    as "English/@xml:lang",  
       'food'  as "English",  
       'ger'   as "German/@xml:lang",  
       'Essen' as "German"  
FOR XML PATH ('Translation')  
go  
```  
  
 @xml:lang 属性使用预定义的 xml 命名空间。 由于 1.0 版的 XML 不需要显式声明 xml 命名空间绑定，因此结果中将不包命名空间绑定的显式声明。  
  
 结果如下：  
  
```  
<Translation>  
  <English xml:lang="en">food</English>  
  <German xml:lang="ger">Essen</German>  
</Translation>  
```  
  
## <a name="using-with-xmlnamespaces-with-the-xml-data-type-methods"></a>将 WITH XMLNAMESPACES 与 xml 数据类型方法结合使用  
 所有在 SELECT 查询中或在 UPDATE 中（当使用 [modify()](../../t-sql/xml/xml-data-type-methods.md) 方法时）指定的 **xml 数据类型方法** 都必须在它们的 prolog 中重复命名空间的声明。 这可能要花很长时间。 例如，下列查询将检索目录说明中确实包含规范的产品型号 ID。 即存在 <`Specifications`> 元素。  
  
```  
SELECT ProductModelID, CatalogDescription.query('  
declare namespace pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
    <Product   
        ProductModelID= "{ sql:column("ProductModelID") }"   
        />  
') AS Result  
FROM Production.ProductModel  
WHERE CatalogDescription.exist('  
    declare namespace  pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     /pd:ProductDescription[(pd:Specifications)]'  
    ) = 1  
```  
  
 在前一个查询中，**query()** 和 **exist()** 方法在它们的 prolog 中声明了相同的命名空间。 例如：  
  
```  
declare namespace pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
```  
  
 此外，您也可以先声明 WITH XMLNAMESPACE，然后在查询中使用命名空间前缀。 这样， **query()** 和 **exist()** 方法便不必在它们的 prolog 中包含命名空间声明。  
  
```  
WITH XMLNAMESPACES ('https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' as pd)  
SELECT ProductModelID, CatalogDescription.query('  
    <Product   
        ProductModelID= "{ sql:column("ProductModelID") }"   
        />  
') AS Result  
FROM Production.ProductModel  
WHERE CatalogDescription.exist('  
     /pd:ProductDescription[(pd:Specifications)]'  
    ) = 1  
Go  
```  
  
 请注意，XQuery prolog 中的显式声明可覆盖在 WITH 子句中定义的命名空间前缀和默认的元素命名空间。  
  
## <a name="see-also"></a>另请参阅  
 [xml 数据类型方法](../../t-sql/xml/xml-data-type-methods.md)   
 [XQuery 语言参考 (SQL Server)](../../xquery/xquery-language-reference-sql-server.md)   
 [WITH XMLNAMESPACES (Transact-SQL)](../../t-sql/xml/with-xmlnamespaces.md)   
 [FOR XML (SQL Server)](../../relational-databases/xml/for-xml-sql-server.md)  
  
  
