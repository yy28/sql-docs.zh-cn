---
title: 命名空间 uri 函数 (XQuery) |Microsoft Docs
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
- fn:namespace-uri function
- namespace-uri function
ms.assetid: 9b48d216-26c8-431d-9ab4-20ab187917f4
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: a21c38506d44c687d639b13ca452e155a97adcef
ms.sourcegitcommit: bfa10c54e871700de285d7f819095d51ef70d997
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/14/2019
ms.locfileid: "54255102"
---
# <a name="functions-on-nodes---namespace-uri"></a>基于节点的函数 - namespace-uri
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回的命名空间 URI 中指定的 QName *$arg*为 xs: string。  
  
## <a name="syntax"></a>语法  
  
```  
fn:namespace-uri() as xs:string  
fn:namespace-uri($arg as node()?) as xs:string  
```  
  
## <a name="arguments"></a>参数  
 *$arg*  
 将检索其命名空间 URI 部分的节点名称。  
  
## <a name="remarks"></a>备注  
  
-   如果省略该参数，则默认值为上下文节点。  
  
-   在 SQL Server 中， **fn:namespace-uri()** 没有仅可以使用上下文相关的谓词的上下文中的参数。 特别要指出的是，它只能在方括号 ([ ]) 内使用。  
  
-   如果 *$arg*是空序列，则返回零长度字符串。  
  
-   如果 *$arg*是一个元素或属性节点的展开的 QName 不在命名空间，该函数返回长度为零的字符串  
  
## <a name="examples"></a>示例  
 本主题提供了一些针对 XML 实例存储在各种 XQuery 示例**xml**类型列中的 AdventureWorks 数据库。  
  
### <a name="a-retrieve-namespace-uri-of-a-specific-node"></a>A. 检索特定节点的命名空间 URI  
 下面的查询是针对非类型化的 XML 实例指定的。 查询表达式 (`namespace-uri(/ROOT[1])`) 将检索指定节点的命名空间 URI 部分。  
  
```  
set @x='<ROOT><a>111</a></ROOT>'  
SELECT @x.query('namespace-uri(/ROOT[1])')  
```  
  
 由于指定的 QName 没有命名空间 URI 部分而只有本地名称部分，因此结果是长度为零的字符串。  
  
 下面的查询指定类型的 instructions **xml**列。 表达式 (`namespace-uri(/AWMI:root[1]/AWMI:Location[1])`) 将返回 <`root`> 元素的第一个 <`Location`> 子元素的命名空间 URI。  
  
```  
SELECT Instructions.query('  
declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions" ;  
     namespace-uri(/AWMI:root[1]/AWMI:Location[1])') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 下面是结果：  
  
```  
https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions  
```  
  
### <a name="b-using-namespace-uri-without-argument-in-a-predicate"></a>B. 在谓词中使用没有参数的 namespace-uri()  
 对类型为 xml 的 CatalogDescription 列指定了以下查询。 表达式将返回其命名空间 URI 为 `https://www.adventure-works.com/schemas/OtherFeatures` 的所有元素节点。 命名空间-**uri （)** 函数指定不带参数，并使用上下文节点。  
  
```  
SELECT CatalogDescription.query('  
declare namespace p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
   /p1:ProductDescription//*[namespace-uri() = "https://www.adventure-works.com/schemas/OtherFeatures"]  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 以下是部分结果：  
  
```  
<p1:wheel xmlns:p1="https://www.adventure-works.com/schemas/OtherFeatures">High performance wheels.</p1:wheel>  
<p2:saddle xmlns:p2="https://www.adventure-works.com/schemas/OtherFeatures">  
  <p3:i xmlns:p3="http://www.w3.org/1999/xhtml">Anatomic design</p3:i> and made from durable leather for a full-day of riding in comfort.</p2:saddle>  
...  
```  
  
 可以将以前查询中的命名空间 URI 更改为 `https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain`。 然后，检索其展开的 QName 的命名空间 URI 部分为 `https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain` 的 <`ProductDescription`> 元素的所有子元素节点。  
  
### <a name="implementation-limitations"></a>实现限制  
 限制如下：  
  
-   **Namespace-uri （)** 函数返回类型 xs: string，而不是 xs: anyuri 的实例。  
  
## <a name="see-also"></a>请参阅  
 [基于节点的函数](https://msdn.microsoft.com/library/09a8affa-3341-4f50-aebc-fdf529e00c08)   
 [local-name 函数&#40;XQuery&#41;](../xquery/functions-on-nodes-local-name.md)  
  
  
