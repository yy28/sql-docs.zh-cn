---
title: substring 函数 (XQuery) |Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- substring function [XQuery]
- fn:substring function
ms.assetid: 2b3b8651-de51-46dc-af82-c86c45eac871
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 3185da6f25f0e224240ad0891ad448267b26465c
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/15/2018
ms.locfileid: "51656351"
---
# <a name="functions-on-string-values---substring"></a>基于字符串值的函数 - substring
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  返回的值的一部分 *$sourceString*的值指示的位置处开始 *$startingLoc，* ，并持续所指示的值的字符数 *$长度*。  
  
## <a name="syntax"></a>语法  
  
```  
  
fn:substring($sourceString as xs:string?,  
                          $startingLoc as xs:decimal?) as xs:string?  
  
fn:substring($sourceString as xs:string?,  
                          $startingLoc as xs:decimal?,  
                          $length as xs:decimal?) as xs:string?  
```  
  
## <a name="arguments"></a>参数  
 *$sourceString*  
 资源字符串。  
  
 *$startingLoc*  
 子字符串在资源字符串中的起点。 如果此值为负数或 0，则只返回那些所在位置大于零的字符。 如果大于的长度 *$sourceString*，则返回零长度字符串。  
  
 *$length*  
 [可选] 要检索的字符数。 如果未指定，则从中指定的位置返回的所有字符 *$startingLoc*到字符串的末尾。  
  
## <a name="remarks"></a>备注  
 带有三个参数的函数将返回 `$sourceString` 中其位置 `$p` 遵守以下指定的字符串：  
  
 `fn:round($startingLoc) <= $p < fn:round($startingLoc) + fn:round($length)`  
  
 值 *$length*可能会超出中的值的字符数 *$sourceString*遵循的起始位置。 在这种情况下，子字符串返回的字符最多的最终 *$sourceString*。  
  
 字符串中第一个字符位于位置 1。  
  
 如果的值 *$sourceString*是空序列，它将作为长度为零的字符串进行处理。 否则为如果任一 *$startingLoc*或 *$length*是空序列，则返回空序列。  
  
## <a name="supplementary-characters-surrogate-pairs"></a>补充字符（代理项对）  
 XQuery 函数中代理对的行为依赖于数据库兼容级别，并且在某些情况下，还依赖于函数的默认命名空间 URI。 有关详细信息，请参阅主题中的"XQuery 函数可识别代理"部分[SQL Server 2016 中数据库引擎功能的重大更改](../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md)。 另请参阅[ALTER DATABASE 兼容性级别&#40;TRANSACT-SQL&#41; ](../t-sql/statements/alter-database-transact-sql-compatibility-level.md)并[排序规则和 Unicode 支持](../relational-databases/collations/collation-and-unicode-support.md)。  
  
## <a name="implementation-limitations"></a>实现限制  
 SQL Server 要求 *$startingLoc*并 *$length 参数*的类型 xs: decimal 而不是 xs: double。  
  
 SQL Server 允许 *$startingLoc*并 *$length*为空序列，因为空序列是映射到 （） 的动态错误结果的可能值。  
  
## <a name="examples"></a>示例  
 本主题提供了一些针对 XML 实例存储在各种 XQuery 示例**xml**类型列中的[!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)]数据库。  
  
### <a name="a-using-the-substring-xquery-function-to-retrieve-partial-summary-product-model-descriptions"></a>A. 使用 substring() XQuery 函数来检索部分概要产品型号说明  
 该查询将检索文档中说明产品型号的文本（<`Summary`> 元素）中的前 50 个字符。  
  
```  
WITH XMLNAMESPACES ('https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd)  
SELECT ProductModelID, CatalogDescription.query('  
    <Prod>{ substring(string((/pd:ProductDescription/pd:Summary)[1]), 1, 50) }</Prod>  
 ') as Result  
FROM Production.ProductModel  
where CatalogDescription.exist('/pd:ProductDescription')  = 1;  
```  
  
 请注意上述查询的以下方面：  
  
-   **String （)** 函数返回的字符串值 <`Summary`> 元素。 使用此函数是因为 <`Summary`> 元素既包含文本又包含子元素（html 格式的元素），还因为将跳过这些元素并检索所有文本。  
  
-   **Substring （)** 函数来检索的字符串值中检索前 50 个字符**string （)**。  
  
 这是部分结果：  
  
```  
ProductModelID Result  
-------------- ----------------------------------------------------  
19      <Prod>Our top-of-the-line competition mountain bike.</Prod>   
23      <Prod>Suitable for any type of riding, on or off-roa</Prod>  
...  
```  
  
## <a name="see-also"></a>请参阅  
 [针对 xml 数据类型的 XQuery 函数](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
