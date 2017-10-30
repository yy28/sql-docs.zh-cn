---
title: "字符串函数 (XQuery) |Microsoft 文档"
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
- string function
- fn:string function
ms.assetid: 7baa2959-9340-429b-ad53-3df03d8e13fc
caps.latest.revision: 27
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 426d16c1f943d72d6a599cf36b427ff4e19b4817
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="data-accessor-functions---string-xquery"></a>数据访问器函数的字符串 (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  返回的值*$arg*表示为字符串。  
  
## <a name="syntax"></a>语法  
  
```  
  
fn:string() as xs:string  
fn:string($arg as item()?) as xs:string  
```  
  
## <a name="arguments"></a>参数  
 *$arg*  
 一个节点或原子值。  
  
## <a name="remarks"></a>注释  
  
-   如果*$arg*空序列，则返回零长度字符串。  
  
-   如果*$arg*是一个节点，该函数返回通过使用字符串值访问器获取节点的字符串值。 W3C XQuery 1.0 和 XPath 2.0 数据模型规范中对此进行了定义。  
  
-   如果*$arg*是原子值，该函数返回由强制转换为表达式返回的相同字符串**xs: string**， *$arg*，除非另外说明。  
  
-   如果的一种*$arg*是**xs: anyuri**，而无需转义特殊字符将 URI 转换为字符串。  
  
-   在此实现中， **fn:string()**没有仅可以依赖于上下文的谓词的上下文中使用的参数。 特别要指出的是，它只能在方括号 ([ ]) 内使用。  
  
## <a name="examples"></a>示例  
 本主题提供对存储在各种的 XML 实例的 XQuery 示例**xml** AdventureWorks 数据库中的类型列。  
  
### <a name="a-using-the-string-function"></a>A. 使用 string 函数  
 下面的查询检索 <`ProductDescription`> 元素的 <`Features`> 子元素节点。  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
 /PD:ProductDescription/PD:Features  
')  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 下面是部分结果：  
  
```  
<PD:Features xmlns:PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">  
   These are the product highlights.   
   <p1:Warranty xmlns:p1="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
    <p1:WarrantyPeriod>3 years</p1:WarrantyPeriod>  
    <p1:Description>parts and labor</p1:Description>  
   </p1:Warranty>  
       ...  
</PD:Features>  
```  
  
 如果指定**string （)**函数，你收到指定的节点的字符串值。  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
 string(/PD:ProductDescription[1]/PD:Features[1])  
')  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 下面是部分结果：  
  
```  
These are the product highlights.   
3 yearsparts and labor...    
```  
  
### <a name="b-using-the-string-function-on-various-nodes"></a>B. 对各种节点使用 string 函数  
 在下面的示例中，一个 XML 实例被分配给一个 xml 类型变量。 查询指定用于说明应用的结果**string （)**到各种节点。  
  
```  
declare @x xml  
set @x = '<?xml version="1.0" encoding="UTF-8" ?>  
<!--  This is a comment -->  
<root>  
  <a>10</a>  
just text  
  <b attr="x">20</b>  
</root>  
'  
```  
  
 下面的查询检索文档节点的字符串值。 此值是通过串联所有后代文本节点的字符串值形成的。  
  
```  
select @x.query('string(/)')  
```  
  
 结果如下：  
  
```  
This is a comment 10  
just text  
 20  
```  
  
 下面的查询尝试检索处理指令节点的字符串值。 结果是一个空序列，因为它不包含文本节点。  
  
```  
select @x.query('string(/processing-instruction()[1])')  
```  
  
 下面的查询检索注释节点的字符串值并返回文本节点。  
  
```  
select @x.query('string(/comment()[1])')  
```  
  
 结果如下：  
  
```  
This is a comment   
```  
  
## <a name="see-also"></a>另请参阅  
 [针对 xml 数据类型的 XQuery 函数](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  

