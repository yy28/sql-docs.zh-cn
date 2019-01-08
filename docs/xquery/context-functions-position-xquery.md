---
title: position 函数 (XQuery) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- position function
- fn:position function
ms.assetid: f1bab9e4-1715-4c06-9cb0-06c7e0c9c97f
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: c7ec642a516d4ad2ac5a0f8d894351fc6670c117
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2018
ms.locfileid: "52540622"
---
# <a name="context-functions---position-xquery"></a>上下文函数 - position (XQuery)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回一个整数值，指示上下文项在当前处理的项序列中的位置。  
  
## <a name="syntax"></a>语法  
  
```  
  
fn:position() as xs:integer  
```  
  
## <a name="remarks"></a>备注  
 在中[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]， **fn:position()** 仅可以使用上下文相关的谓词的上下文中。 确切地说，仅可用在方括号 ([ ]) 内。与此函数比较不会在静态类型推导过程中减少基数。  
  
## <a name="examples"></a>示例  
 本主题提供了一些针对 XML 实例存储在各种中的 XQuery 示例**xml**类型列中的[!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)]数据库。  
  
### <a name="a-using-the-position-xquery-function-to-retrieve-the-first-two-product-features"></a>A. 使用 position() XQuery 函数检索前两个产品功能  
 以下查询从产品型号目录说明检索前两个功能，即 <`Features`> 元素的前两个子元素。 如果有更多功能，将向结果添加 <`there-is-more/`> 元素。  
  
```  
SELECT CatalogDescription.query('  
     declare namespace pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
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
  
-   **命名空间**中的关键字[XQuery Prolog](../xquery/modules-and-prologs-xquery-prolog.md)定义查询主体中使用的命名空间前缀。  
  
-   查询主体构造的 XML\<产品 > 具有元素**ProductModelID**并**ProductModelName**属性和作为子元素返回的产品功能。  
  
-   **Position （)** 函数用于在谓词中确定的位置\<功能 > 上下文中的子元素。 如果是第一个或第二个功能，将返回该子元素。  
  
-   IF 语句将添加\<此处是更 / > 如果产品目录中有两个以上的功能的结果的元素。  
  
-   由于不是所有产品型号都将其目录说明存储在表中，因此使用 WHERE 子句来放弃 CatalogDescriptions 为 NULL 的行。  
  
 这是部分结果：  
  
```  
<Product ProductModelID="19" ProductModelName="Mountain 100">  
  <p1:Warranty xmlns:p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
    <p1:WarrantyPeriod>3 year</p1:WarrantyPeriod>  
    <p1:Description>parts and labor</p1:Description>  
  </p1:Warranty>  
  <p2:Maintenance xmlns:p2="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
    <p2:NoOfYears>10</p2:NoOfYears>  
    <p2:Description>maintenance contact available through your dealer or  
                    any AdventureWorks retail store.</p2:Description>  
  </p2:Maintenance>  
  <there-is-more/>  
</Product>   
...  
```  
  
## <a name="see-also"></a>请参阅  
 [针对 xml 数据类型的 XQuery 函数](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
