---
title: "定位函数 (XQuery) |Microsoft 文档"
ms.custom: 
ms.date: 08/09/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- position function
- fn:position function
ms.assetid: f1bab9e4-1715-4c06-9cb0-06c7e0c9c97f
caps.latest.revision: 29
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a5f89e98a0c441d153899b03f0dc0b1a809b89af
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="context-functions---position-xquery"></a>上下文函数的位置 (XQuery)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回一个整数值，指示上下文项在当前处理的项序列中的位置。  
  
## <a name="syntax"></a>语法  
  
```  
  
fn:position() as xs:integer  
```  
  
## <a name="remarks"></a>注释  
 在[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]， **fn:position()**只能依赖于上下文的谓词的上下文中。 确切地说，仅可用在方括号 ([ ]) 内。与此函数比较不会在静态类型推导过程中减少基数。  
  
## <a name="examples"></a>示例  
 本主题提供对存储在各种的 XML 实例的 XQuery 示例**xml**类型中的列[!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)]数据库。  
  
### <a name="a-using-the-position-xquery-function-to-retrieve-the-first-two-product-features"></a>A. 使用 position() XQuery 函数检索前两个产品功能  
 以下查询从产品型号目录说明检索前两个功能，即 <`Features`> 元素的前两个子元素。 如果有更多功能，将向结果添加 <`there-is-more/`> 元素。  
  
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
') as x  
FROM Production.ProductModel  
WHERE CatalogDescription is not null  
```  
  
 请注意上述查询的以下方面：  
  
-   **命名空间**中的关键字[XQuery Prolog](../xquery/modules-and-prologs-xquery-prolog.md)定义查询正文中使用命名空间前缀。  
  
-   查询正文构造的 XML\<产品 > 具有元素**ProductModelID**和**ProductModelName**属性，并具有作为子元素返回的产品功能。  
  
-   **Position()**函数用于谓词中确定的位置\<功能 > 上下文中的子元素。 如果是第一个或第二个功能，将返回该子元素。  
  
-   IF 语句将添加\<这里是更 / > 如果产品目录中有两个以上的功能的结果的元素。  
  
-   由于不是所有产品型号都将其目录说明存储在表中，因此使用 WHERE 子句来放弃 CatalogDescriptions 为 NULL 的行。  
  
 下面是部分结果：  
  
```  
<Product ProductModelID="19" ProductModelName="Mountain 100">  
  <p1:Warranty xmlns:p1="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
    <p1:WarrantyPeriod>3 year</p1:WarrantyPeriod>  
    <p1:Description>parts and labor</p1:Description>  
  </p1:Warranty>  
  <p2:Maintenance xmlns:p2="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
    <p2:NoOfYears>10</p2:NoOfYears>  
    <p2:Description>maintenance contact available through your dealer or  
                    any AdventureWorks retail store.</p2:Description>  
  </p2:Maintenance>  
  <there-is-more/>  
</Product>   
…  
```  
  
## <a name="see-also"></a>另请参阅  
 [针对 xml 数据类型的 XQuery 函数](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  

