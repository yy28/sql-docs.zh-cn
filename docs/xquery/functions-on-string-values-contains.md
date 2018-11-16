---
title: 包含函数 (XQuery) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- contains function (XQuery)
- fn:contains function
ms.assetid: 2c88c015-04fc-429b-84b2-835596a28b65
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: f611fead43166972860436e7c3bc378ee8e44f38
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/15/2018
ms.locfileid: "51670256"
---
# <a name="functions-on-string-values---contains"></a>基于字符串值的函数 - contains
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  返回的值为类型 xs: boolean，该值指示是否的值*美元 arg1*包含由指定的字符串值*美元 arg2*。  
  
## <a name="syntax"></a>语法  
  
```  
  
fn:contains ($arg1 as xs:string?, $arg2 as xs:string?) as xs:boolean?  
```  
  
## <a name="arguments"></a>参数  
 *$arg1*  
 要测试的字符串值。  
  
 *$arg2*  
 要查找的子字符串。  
  
## <a name="remarks"></a>备注  
 如果的值*美元 arg2*是零长度字符串，该函数将返回**True**。 如果的值*美元 arg1*是一个零长度字符串和的值*美元 arg2*不是零长度字符串，该函数将返回**False**。  
  
 如果的值*美元 arg1*或*美元 arg2*是空序列，该参数被视为零长度字符串。  
  
 contains() 函数使用 XQuery 默认的 Unicode 码位排序规则来进行字符串比较。  
  
 为指定的子字符串值*美元 arg2*必须小于或等于 4000 个字符。 如果指定的值大于 4000 个字符，出现动态错误情况和 contains （） 函数返回空序列而不是布尔值 **，则返回 True**或**False**。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 不会对 XQuery 表达式生成动态错误。  
  
 若要获取不区分大小写的比较[大写](../xquery/functions-on-string-values-upper-case.md)或 lower-case 函数可用。  
  
## <a name="supplementary-characters-surrogate-pairs"></a>补充字符（代理项对）  
 XQuery 函数中代理对的行为依赖于数据库兼容级别，并且在某些情况下，还依赖于函数的默认命名空间 URI。 有关详细信息，请参阅主题中的"XQuery 函数可识别代理"部分[SQL Server 2016 中数据库引擎功能的重大更改](../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md)。 另请参阅[ALTER DATABASE 兼容性级别&#40;TRANSACT-SQL&#41; ](../t-sql/statements/alter-database-transact-sql-compatibility-level.md)并[排序规则和 Unicode 支持](../relational-databases/collations/collation-and-unicode-support.md)。  
  
## <a name="examples"></a>示例  
 本主题提供了对存储在 AdventureWorks 数据库中的各种 xml 类型列中的 XML 实例的 XQuery 示例。  
  
### <a name="a-using-the-contains-xquery-function-to-search-for-a-specific-character-string"></a>A. 使用 contains() XQuery 函数搜索特定的字符串  
 以下查询将查找概要说明中包含单词 Aerodynamic 的产品。 此查询将返回这些产品的 ProductID 和 <`Summary`> 元素。  
  
```  
--The product model description document uses  
--namespaces. The WHERE clause uses the exit()  
--method of the xml data type. Inside the exit method,  
--the XQuery contains()function is used to  
--determine whether the <Summary> text contains the word  
--Aerodynamic.   
  
USE AdventureWorks  
GO  
WITH XMLNAMESPACES ('https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd)  
SELECT ProductModelID, CatalogDescription.query('  
      <Prod>  
         { /pd:ProductDescription/@ProductModelID }  
         { /pd:ProductDescription/pd:Summary }  
      </Prod>  
 ') as Result  
FROM Production.ProductModel  
where CatalogDescription.exist('  
   /pd:ProductDescription/pd:Summary//text()  
    [contains(., "Aerodynamic")]') = 1  
```  
  
 结果  
  
 `ProductModelID Result`  
  
 `-------------- ---------`  
  
 `28     <Prod ProductModelID="28">`  
  
 `<pd:Summary xmlns:pd=`  
  
 `"https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">`  
  
 `<p1:p xmlns:p1="https://www.w3.org/1999/xhtml">`  
  
 `A TRUE multi-sport bike that offers streamlined riding and`  
  
 `a revolutionary design. Aerodynamic design lets you ride with`  
  
 `the pros, and the gearing will conquer hilly roads.</p1:p>`  
  
 `</pd:Summary>`  
  
 `</Prod>`  
  
## <a name="see-also"></a>请参阅  
 [针对 xml 数据类型的 XQuery 函数](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
