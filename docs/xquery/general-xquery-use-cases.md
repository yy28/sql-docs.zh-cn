---
title: "常规 XQuery 用例就 |Microsoft 文档"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
dev_langs: XML
helpviewer_keywords: XQuery, general usage cases
ms.assetid: 5187c97b-6866-474d-8bdb-a082634039cc
caps.latest.revision: "34"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4bef0c77a25ac81adb5a758ecb96e1d02a1177ea
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="general-xquery-use-cases"></a>XQuery 常规使用情况
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  本主题提供 XQuery 常规使用情况示例。  
  
## <a name="examples"></a>示例  
  
### <a name="a-query-catalog-descriptions-to-find-products-and-weights"></a>A. 查询目录说明以查找产品和权重  
 下面的查询将从产品目录说明中返回产品型号 ID 和权重（如果它们存在的话）。 该查询将构造如下形式的 XML 内容：  
  
```  
<Product ProductModelID="…">  
  <Weight>…</Weight>  
</Product>  
```  
  
 以下是查询语句：  
  
```  
SELECT CatalogDescription.query('  
declare namespace p1="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
  <Product  ProductModelID="{ (/p1:ProductDescription/@ProductModelID)[1] }">  
     {   
       /p1:ProductDescription/p1:Specifications/Weight   
     }   
  </Product>  
') as Result  
FROM Production.ProductModel  
WHERE CatalogDescription is not null  
```  
  
 请注意上述查询的以下方面：  
  
-   **命名空间**关键字在 XQuery prolog 中的定义查询正文中使用的命名空间前缀。  
  
-   查询主体用于构造所需的 XML。  
  
-   在 WHERE 子句中， **exist （)**方法用于查找包含产品目录说明的行。 即，包含 <`ProductDescription`> 元素的 XML。  
  
 结果如下：  
  
```  
<Product ProductModelID="19"/>  
<Product ProductModelID="23"/>   
<Product ProductModelID="25"/>   
<Product ProductModelID="28"><Weight>Varies with size.</Weight></Product>  
<Product ProductModelID="34"/>  
<Product ProductModelID="35"/>  
```  
  
 下面的查询将检索相同的信息，但是仅限于其目录说明在规范（<`Specifications`> 元素）中包含权重（<`Weight`> 元素）的那些产品型号。 此示例使用 WITH XMLNAMESPACES 来声明 pd 前缀与其命名空间的绑定。 在这种方式，绑定不描述在**query （)**方法并在**exist （)**方法。  
  
```  
WITH XMLNAMESPACES ('http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd)  
SELECT CatalogDescription.query('  
          <Product  ProductModelID="{ (/pd:ProductDescription/@ProductModelID)[1] }">  
                 {   
                      /pd:ProductDescription/pd:Specifications/Weight   
                 }   
          </Product>  
') as x  
FROM Production.ProductModel  
WHERE CatalogDescription.exist('/pd:ProductDescription/pd:Specifications//Weight ') = 1  
```  
  
 在前面的查询， **exist （)**方法**xml**数据类型中的 WHERE 子句进行检查，以查看是否存在 <`Weight`> 中的元素 <`Specifications`> 元素。  
  
### <a name="b-find-product-model-ids-for-product-models-whose-catalog-descriptions-include-front-angle-and-small-size-pictures"></a>B. 为其目录说明包含前角和小幅图片的产品型号查找产品型号 ID  
 XML 产品目录说明包含产品图片（<`Picture`> 元素）。 每个图片都具有若干属性。 这些属性包括图片角度（<`Angle`> 元素）和大小（<`Size`> 元素）。  
  
 对于其目录说明包含前角和小幅图片的产品型号，查询将构造具有以下形式的 XML：  
  
```  
< Product ProductModelID="…">  
  <Picture>  
    <Angle>front</Angle>  
    <Size>small</Size>  
  </Picture>  
</Product>  
WITH XMLNAMESPACES ('http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd)  
SELECT CatalogDescription.query('  
   <pd:Product  ProductModelID="{ (/pd:ProductDescription/@ProductModelID)[1] }">  
      <Picture>  
         {  /pd:ProductDescription/pd:Picture/pd:Angle }   
         {  /pd:ProductDescription/pd:Picture/pd:Size }   
      </Picture>  
   </pd:Product>  
') as Result  
FROM  Production.ProductModel  
WHERE CatalogDescription.exist('/pd:ProductDescription/pd:Picture') = 1  
AND   CatalogDescription.value('(/pd:ProductDescription/pd:Picture/pd:Angle)[1]', 'varchar(20)')  = 'front'  
AND   CatalogDescription.value('(/pd:ProductDescription/pd:Picture/pd:Size)[1]', 'varchar(20)')  = 'small'  
```  
  
 请注意上述查询的以下方面：  
  
-   在 WHERE 子句中， **exist （)**方法用于检索具有与产品目录说明的行 <`Picture`> 元素。  
  
-   WHERE 子句使用**value （)**方法两次来比较的值 <`Size`> 和 <`Angle`> 元素。  
  
 下面是部分结果：  
  
```  
<p1:Product   
  xmlns:p1="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription"   
  ProductModelID="19">  
  <Picture>  
    <p1:Angle>front</p1:Angle>  
    <p1:Size>small</p1:Size>  
  </Picture>  
</p1:Product>  
...  
```  
  
### <a name="c-create-a-flat-list-of-the-product-model-name-and-feature-pairs-with-each-pair-enclosed-in-the-features-element"></a>C. 创建产品的简单列表括在每个对模型名称和功能对\<功能 > 元素  
 在产品型号目录说明中，XML 包含若干种产品功能。 所有这些功能都包含在 <`Features`> 元素中。 该查询使用[XML 构造 (XQuery)](../xquery/xml-construction-xquery.md)构造必需的 XML。 大括号中的表达式将替换为结果。  
  
```  
SELECT CatalogDescription.query('  
declare namespace p1="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
  for $pd in /p1:ProductDescription,  
   $f in $pd/p1:Features/*  
  return  
   <Feature>  
     <ProductModelName> { data($pd/@ProductModelName) } </ProductModelName>  
     { $f }  
  </Feature>          
') as x  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 请注意上述查询的以下方面：  
  
-   $pd/p1:Features/* 只返回 <`Features`> 的元素节点子级，但 $pd/p1:Features/node() 将返回所有节点。 其中包括元素节点、文本节点、处理指令和注释。  
  
-   两个 FOR 循环将生成笛卡儿积，将从该积返回产品名称和单个功能。  
  
-   **ProductName**是一个属性。 此查询中的 XML 构造将其作为一个元素返回。  
  
 下面是部分结果：  
  
```  
<Feature>  
 <ProductModelName>Mountain 100</ProductModelName>  
 <ProductModelID>19</ProductModelID>  
 <p1:Warranty   
   xmlns:p1="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
    <p1:WarrantyPeriod>3 year</p1:WarrantyPeriod>  
    <p1:Description>parts and labor</p1:Description>  
 </p1:Warranty>  
</Feature>  
<Feature>  
 <ProductModelName>Mountain 100</ProductModelName>  
 <ProductModelID>19</ProductModelID>  
 <p2:Maintenance xmlns:p2="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
    <p2:NoOfYears>10</p2:NoOfYears>  
    <p2:Description>maintenance contact available through your dealer   
           or any AdventureWorks retail store.</p2:Description>  
    </p2:Maintenance>  
</Feature>  
...  
...      
```  
  
### <a name="d-from-the-catalog-description-of-a-product-model-list-the-product-model-name-model-id-and-features-grouped-inside-a-product-element"></a>D. 产品型号的目录说明，从列表产品模型名称、 模型 ID，并将功能分组内\<产品 > 元素  
 使用存储在产品型号的目录说明中的信息，以下查询将列出产品型号的模型 ID 和功能组合到\<产品 > 元素。  
  
```  
SELECT ProductModelID, CatalogDescription.query('  
     declare namespace pd="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     <Product>  
         <ProductModelName>   
           { data(/pd:ProductDescription/@ProductModelName) }   
         </ProductModelName>  
         <ProductModelID>   
           { data(/pd:ProductDescription/@ProductModelID) }   
         </ProductModelID>  
         { /pd:ProductDescription/pd:Features/* }  
     </Product>          
') as x  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 下面是部分结果：  
  
```  
<Product>  
  <ProductModelName>Mountain 100</ProductModelName>  
  <ProductModelID>19</ProductModelID>  
  <p1:Warranty>... </p1:Warranty>  
  <p2:Maintenance>...  </p2:Maintenance>  
  <p3:wheel xmlns:p3="http://www.adventure-works.com/schemas/OtherFeatures">High performance wheels.</p3:wheel>  
  <p4:saddle xmlns:p4="http://www.adventure-works.com/schemas/OtherFeatures">  
    <p5:i xmlns:p5="http://www.w3.org/1999/xhtml">Anatomic design</p5:i> and made from durable leather for a full-day of riding in comfort.</p4:saddle>  
  <p6:pedal xmlns:p6="http://www.adventure-works.com/schemas/OtherFeatures">  
    <p7:b xmlns:p7="http://www.w3.org/1999/xhtml">Top-of-the-line</p7:b> clipless pedals with adjustable tension.</p6:pedal>  
   ...  
```  
  
### <a name="e-retrieve-product-model-feature-descriptions"></a>E. 检索产品型号功能说明  
 以下查询构造 XML 包含 <`Product`> 元素，该元素**ProducModelID**， **ProductModelName**属性和第一个的两个产品功能。 前两个产品功能特指 <`Features`> 元素的前两个子元素。 如果有更多的功能，此查询将返回空的 <`There-is-more/`> 元素。  
  
```  
SELECT CatalogDescription.query('  
declare namespace pd="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     <Product>   
          { /pd:ProductDescription/@ProductModelID }  
          { /pd:ProductDescription/@ProductModelName }   
          {  
            for $f in /pd:ProductDescription/pd:Features/*[position()<=2]  
            return  
            $f   
          }  
          {  
            if (count(/pd:ProductDescription/pd:Features/*) > 2)  
            then <there-is-more/>  
            else ()  
          }   
     </Product>          
') as Result  
FROM Production.ProductModel  
WHERE CatalogDescription is not NULL  
```  
  
 请注意上述查询的以下方面：  
  
-   FOR ...RETURN 循环结构用于检索前两个产品功能。 **Position()**函数用于查找在该序列的元素的位置。  
  
### <a name="f-find-element-names-from-the-product-catalog-description-that-end-with-ons"></a>F. 从产品目录说明中查找以“ons”结尾的元素名称  
 下面的查询将搜索目录说明并返回 <`ProductDescription`> 元素中其名称以“ons”结尾的所有元素。  
  
```  
SELECT ProductModelID, CatalogDescription.query('  
     declare namespace p1="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
      for $pd in /p1:ProductDescription/*[substring(local-name(.),string-length(local-name(.))-2,3)="ons"]  
      return   
          <Root>  
             { $pd }  
          </Root>  
') as Result  
FROM Production.ProductModel  
WHERE CatalogDescription is not NULL  
```  
  
 下面是部分结果：  
  
```  
ProductModelID   Result  
-----------------------------------------  
         19        <Root>         
                     <p1:Specifications xmlns:p1="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">          
                          ...         
                     </p1:Specifications>         
                   </Root>          
```  
  
### <a name="g-find-summary-descriptions-that-contain-the-word-aerodynamic"></a>G. 查找包含单词“Aerodynamic”的概要说明  
 下面的查询将检索其目录说明在概要说明中包含单词“Aerodynamic”的产品型号：  
  
```  
WITH XMLNAMESPACES ('http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd)  
SELECT ProductModelID, CatalogDescription.query('  
          <Prod >  
             { /pd:ProductDescription/@ProductModelID }  
             { /pd:ProductDescription/pd:Summary }  
          </Prod>  
 ') as Result  
FROM Production.ProductModel  
WHERE CatalogDescription.value('  
     contains( string( (/pd:ProductDescription/pd:Summary)[1] ),"Aerodynamic")','bit') = 1  
```  
  
 请注意，SELECT 查询指定**query （)**和**value （)**方法**xml**数据类型。 因此，该查询中使用了前缀 pd，并且只使用 WITH XMLNAMESPACES 定义了一次该前缀 pd，而不是在两个不同的查询 prolog 中两次重复声明命名空间。  
  
 请注意上述查询的以下方面：  
  
-   WHERE 子句用于只检索其目录说明在 <`Summary`> 元素中包含单词“Aerodynamic”的行。  
  
-   **Contains （)**函数用于查看是否在文本中包括单词。  
  
-   **Value （)**方法**xml**数据类型将返回的值进行比较**contains （)**为 1。  
  
 结果如下：  
  
```  
ProductModelID Result        
-------------- ------------------------------------------  
28     <Prod ProductModelID="28">  
        <pd:Summary xmlns:pd="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">  
       <p1:p xmlns:p1="http://www.w3.org/1999/xhtml">  
         A TRUE multi-sport bike that offers streamlined riding and a  
         revolutionary design. Aerodynamic design lets you ride with the   
         pros, and the gearing will conquer hilly roads.</p1:p>  
       </pd:Summary>  
      </Prod>    
```  
  
### <a name="h-find-product-models-whose-catalog-descriptions-do-not-include-product-model-pictures"></a>H. 查找其目录说明不包含产品型号图片的产品型号  
 下面的查询将检索其目录说明不包含 <`Picture`> 元素的产品型号的 ProductModelID。  
  
```  
SELECT  ProductModelID  
FROM    Production.ProductModel  
WHERE   CatalogDescription is not NULL  
AND     CatalogDescription.exist('declare namespace p1="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     /p1:ProductDescription/p1:Picture  
') = 0  
```  
  
 请注意上述查询的以下方面：  
  
-   如果**exist （)**方法中的 WHERE 子句，则返回 False (0)，返回产品型号 ID。 否则，将不返回。  
  
-   由于所有产品说明都包含 <`Picture`> 元素，因此在这种情况下结果集为空。  
  
## <a name="see-also"></a>另请参阅  
 [XQueries 涉及层次结构](../xquery/xqueries-involving-hierarchy.md)   
 [XQueries 涉及顺序](../xquery/xqueries-involving-order.md)   
 [XQueries 处理关系数据](../xquery/xqueries-handling-relational-data.md)   
 [在 XQuery 中的字符串搜索](../xquery/string-search-in-xquery.md)   
 [处理在 XQuery 中的命名空间](../xquery/handling-namespaces-in-xquery.md)   
 [使用 WITH XMLNAMESPACES 将命名空间添加到查询](../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)   
 [XML 数据 (SQL Server)](../relational-databases/xml/xml-data-sql-server.md)   
 [XQuery 语言参考 (SQL Server)](../xquery/xquery-language-reference-sql-server.md)  
  
  
