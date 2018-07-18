---
title: concat 函数 (XQuery) |Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: sql
ms.component: xquery
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
dev_langs:
- XML
helpviewer_keywords:
- fn:concat function
- concat function [XQuery]
ms.assetid: d50afd20-a297-445e-be9e-13b48017e7ca
caps.latest.revision: 32
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 8be65777bb65ad54735ad6bdf43ea88608355c5b
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "37981929"
---
# <a name="functions-on-string-values---concat"></a>基于字符串值-concat 函数
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  接受零或更多个字符串作为参数，并返回通过连接其中的每个参数值而创建的字符串。  
  
## <a name="syntax"></a>语法  
  
```  
  
fn:concat ($string as xs:string?  
           ,$string as xs:string?  
           [, ...]) as xs:string  
```  
  
## <a name="arguments"></a>参数  
 *$string*  
 可选择进行连接的字符串。  
  
## <a name="remarks"></a>Remarks  
 此函数必须至少包含两个参数。 如果一个参数为空序列，则将被作为零长度字符串处理。  
  
## <a name="supplementary-characters-surrogate-pairs"></a>补充字符（代理项对）  
 XQuery 函数中代理对的行为依赖于数据库兼容级别，并且在某些情况下，还依赖于函数的默认命名空间 URI。 有关详细信息，请参阅主题中的"XQuery 函数可识别代理"部分[SQL Server 2016 中数据库引擎功能的重大更改](../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md)。 另请参阅[ALTER DATABASE 兼容性级别&#40;TRANSACT-SQL&#41; ](../t-sql/statements/alter-database-transact-sql-compatibility-level.md)并[排序规则和 Unicode 支持](../relational-databases/collations/collation-and-unicode-support.md)。  
  
## <a name="examples"></a>示例  
 本主题提供了一些针对 XML 实例存储在各种中的 XQuery 示例**xml**类型列中的 AdventureWorks 示例数据库。  
  
### <a name="a-using-the-concat-xquery-function-to-concatenate-strings"></a>A. 使用 concat() XQuery 函数连接字符串  
 对于特定产品型号，此查询将返回通过连接保修期和保修说明而创建的字符串。 在目录说明文档中，<`Warranty`> 元素由 <`WarrantyPeriod`> 和 <`Description`> 子元素组成。  
  
```  
WITH XMLNAMESPACES (  
'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd,  
'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain' AS wm)  
SELECT CatalogDescription.query('  
    <Product   
        ProductModelID= "{ (/pd:ProductDescription/@ProductModelID)[1] }"  
        ProductModelName = "{ sql:column("PD.Name") }" >  
        {   
          concat( string((/pd:ProductDescription/pd:Features/wm:Warranty/wm:WarrantyPeriod)[1]), "-",  
                  string((/pd:ProductDescription/pd:Features/wm:Warranty/wm:Description)[1]))   
         }   
     </Product>  
 ') as Result  
FROM Production.ProductModel PD  
WHERE  PD.ProductModelID=28  
  
```  
  
 请注意上述查询的以下方面：  
  
-   在 SELECT 子句中，CatalogDescription 是**xml**类型列。 因此， [query （） 方法 （XML 数据类型）](../t-sql/xml/query-method-xml-data-type.md)，instructions.query。 XQuery 语句指定为该查询方法的参数。  
  
-   对其执行查询的文档将使用命名空间。 因此，**命名空间**关键字用于定义命名空间的前缀。 有关详细信息，请参阅[XQuery Prolog](../xquery/modules-and-prologs-xquery-prolog.md)。  
  
 结果如下：  
  
```  
<Product ProductModelID="28" ProductModelName="Road-450">1 year-parts and labor</Product>  
```  
  
 上一个查询检索了有关特定产品的信息。 以下查询将针对为其存储了 XML 目录说明的所有产品检索同样的信息。 **Exist （)** 方法**xml**数据类型中的 WHERE 子句将返回 True，如果行中的 XML 文档具有 <`ProductDescription`> 元素。  
  
```  
WITH XMLNAMESPACES (  
'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd,  
'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain' AS wm)  
  
SELECT CatalogDescription.query('  
    <Product   
        ProductModelID= "{ (/pd:ProductDescription/@ProductModelID)[1] }"   
        ProductName = "{ sql:column("PD.Name") }" >  
        {   
          concat( string((/pd:ProductDescription/pd:Features/wm:Warranty/wm:WarrantyPeriod)[1]), "-",  
                  string((/pd:ProductDescription/pd:Features/wm:Warranty/wm:Description)[1]))   
         }   
     </Product>  
 ') as Result  
FROM Production.ProductModel PD  
WHERE CatalogDescription.exist('//pd:ProductDescription ') = 1  
  
```  
  
 请注意，返回的布尔值**exist （)** 方法**xml**类型与 1 进行比较。  
  
### <a name="implementation-limitations"></a>实现限制  
 限制如下：  
  
-   **Concat （)** SQL Server 中的函数仅接受类型 xs: string 的值。 其他值必须显式转换为 xs:string 或 xdt:untypedAtomic 类型。  
  
## <a name="see-also"></a>请参阅  
 [针对 xml 数据类型的 XQuery 函数](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
