---
title: 包含函数 (XQuery) |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
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
- contains function (XQuery)
- fn:contains function
ms.assetid: 2c88c015-04fc-429b-84b2-835596a28b65
caps.latest.revision: 42
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: fceddcf918a99667e8c92fadc7aeddca59bb21a8
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "33076904"
---
# <a name="functions-on-string-values---contains"></a>函数对字符串值-包含
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  返回一个值的类型 xs: boolean，该值指示是否的值 *$arg1*包含由指定的字符串值 *$arg2*。  
  
## <a name="syntax"></a>语法  
  
```  
  
fn:contains ($arg1 as xs:string?, $arg2 as xs:string?) as xs:boolean?  
```  
  
## <a name="arguments"></a>参数  
 *$arg1*  
 要测试的字符串值。  
  
 *$arg2*  
 要查找的子字符串。  
  
## <a name="remarks"></a>注释  
 如果值 *$arg2*是零长度字符串，该函数将返回**True**。 如果值 *$arg1*是零长度字符串和的值 *$arg2*不是零长度字符串，该函数将返回**False**。  
  
 如果值 *$arg1*或 *$arg2*空序列，该参数将被视为零长度字符串。  
  
 contains() 函数使用 XQuery 默认的 Unicode 码位排序规则来进行字符串比较。  
  
 为指定的子字符串值 *$arg2*必须是小于或等于 4000 个字符。 如果指定的值大于 4000 个字符，就发生了动态错误条件并 contains （） 函数返回而不是布尔值的空序列**True**或**False**。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 不会对 XQuery 表达式生成动态错误。  
  
 若要获取不区分大小写比较，[大写](../xquery/functions-on-string-values-upper-case.md)或小写函数可用。  
  
## <a name="supplementary-characters-surrogate-pairs"></a>补充字符（代理项对）  
 XQuery 函数中代理对的行为依赖于数据库兼容级别，并且在某些情况下，还依赖于函数的默认命名空间 URI。 有关详细信息，请参阅主题中的"XQuery 函数是代理项感知"部分[中 SQL Server 2016 数据库引擎功能的重大更改](../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md)。 另请参阅[ALTER DATABASE 兼容级别&#40;TRANSACT-SQL&#41; ](../t-sql/statements/alter-database-transact-sql-compatibility-level.md)和[Collation and Unicode Support](../relational-databases/collations/collation-and-unicode-support.md)。  
  
## <a name="examples"></a>示例  
 本主题提供对 AdventureWorks 数据库中的各种 xml 类型列中存储的 XML 实例的 XQuery 示例。  
  
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
WITH XMLNAMESPACES ('http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd)  
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
  
 `"http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">`  
  
 `<p1:p xmlns:p1="http://www.w3.org/1999/xhtml">`  
  
 `A TRUE multi-sport bike that offers streamlined riding and`  
  
 `a revolutionary design. Aerodynamic design lets you ride with`  
  
 `the pros, and the gearing will conquer hilly roads.</p1:p>`  
  
 `</pd:Summary>`  
  
 `</Prod>`  
  
## <a name="see-also"></a>另请参阅  
 [针对 xml 数据类型的 XQuery 函数](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
