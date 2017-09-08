---
title: "子字符串函数 (XQuery) |Microsoft 文档"
ms.custom: 
ms.date: 03/09/2017
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
- substring function [XQuery]
- fn:substring function
ms.assetid: 2b3b8651-de51-46dc-af82-c86c45eac871
caps.latest.revision: 42
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2fbe33b349def61c3b093079554db626b56f2f09
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="functions-on-string-values---substring"></a>对字符串值的子字符串函数
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  返回值的一部分*$sourceString*处的值指示的位置开始， *$startingLoc，*并执行的值指示的字符数，持续*$长度*。  
  
## <a name="syntax"></a>语法  
  
```  
  
fn:substring($sourceString as xs:string?,  
                          $startingLoc  as as xs:decimal?) as xs:string?  
  
fn:substring($sourceString as xs:string?,  
                          $startingLoc as xs:decimal?,  
                          $length as xs:decimal?) as xs:string?  
```  
  
## <a name="arguments"></a>参数  
 *$sourceString*  
 资源字符串。  
  
 *$startingLoc*  
 子字符串在资源字符串中的起点。 如果此值为负数或 0，则只返回那些所在位置大于零的字符。 如果该长度超过的长度*$sourceString*，则返回零长度字符串。  
  
 *$length*  
 [可选] 要检索的字符数。 如果未指定，则从中指定的位置返回的所有字符*$startingLoc*直至字符串的末尾。  
  
## <a name="remarks"></a>注释  
 带有三个参数的函数将返回 `$sourceString` 中其位置 `$p` 遵守以下指定的字符串：  
  
 `fn:round($startingLoc) <= $p < fn:round($startingLoc) + fn:round($length)`  
  
 值*$length*可以是中的值的字符数大于*$sourceString*遵循起始位置。 子字符串在此情况下，返回最末尾字符*$sourceString*。  
  
 字符串中第一个字符位于位置 1。  
  
 如果值*$sourceString*空序列，它会被视为零长度字符串。 否则为如果任一*$startingLoc*或*$length*空序列，则返回空序列。  
  
## <a name="supplementary-characters-surrogate-pairs"></a>补充字符（代理项对）  
 XQuery 函数中代理对的行为依赖于数据库兼容级别，并且在某些情况下，还依赖于函数的默认命名空间 URI。 有关详细信息，请参阅主题中的"XQuery 函数是代理项感知"部分[中 SQL Server 2016 数据库引擎功能的重大更改](../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md)。 另请参阅[ALTER DATABASE 兼容级别 &#40;Transact SQL &#41;](../t-sql/statements/alter-database-transact-sql-compatibility-level.md)和[Collation and Unicode Support](../relational-databases/collations/collation-and-unicode-support.md)。  
  
## <a name="implementation-limitations"></a>实现限制  
 SQL Server 要求*$startingLoc*和*$length 参数*为而不是将 xs: double 类型 xs: decimal。  
  
 SQL Server 允许*$startingLoc*和*$length*是空序列，因为空序列是发生动态映射到 （） 的错误的可能值。  
  
## <a name="examples"></a>示例  
 本主题提供对 XML 实例存储在各种 XQuery 示例**xml**类型中的列[!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)]数据库。  
  
### <a name="a-using-the-substring-xquery-function-to-retrieve-partial-summary-product-model-descriptions"></a>A. 使用 substring() XQuery 函数来检索部分概要产品型号说明  
 该查询将检索文档中说明产品型号的文本（<`Summary`> 元素）中的前 50 个字符。  
  
```  
WITH XMLNAMESPACES ('http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd)  
SELECT ProductModelID, CatalogDescription.query('  
    <Prod>{ substring(string((/pd:ProductDescription/pd:Summary)[1]), 1, 50) }</Prod>  
 ') as Result  
FROM Production.ProductModel  
where CatalogDescription.exist('/pd:ProductDescription')  = 1;  
```  
  
 请注意上述查询的以下方面：  
  
-   **String （)**函数返回的字符串值 <`Summary`> 元素。 使用此函数是因为 <`Summary`> 元素既包含文本又包含子元素（html 格式的元素），还因为将跳过这些元素并检索所有文本。  
  
-   **Substring （)**函数从检索到的字符串值中检索前 50 个字符**string （)**。  
  
 下面是部分结果：  
  
```  
ProductModelID Result  
-------------- ----------------------------------------------------  
19      <Prod>Our top-of-the-line competition mountain bike.</Prod>   
23      <Prod>Suitable for any type of riding, on or off-roa</Prod>  
...  
```  
  
## <a name="see-also"></a>另请参阅  
 [针对 xml 数据类型的 XQuery 函数](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
